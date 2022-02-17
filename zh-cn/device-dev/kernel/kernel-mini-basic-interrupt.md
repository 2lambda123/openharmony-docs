# 中断管理

- [基本概念](#基本概念)
- [接口说明](#接口说明)
- [开发流程](#开发流程)
- [编程实例](#编程实例)
- [结果验证](#结果验证)

## 基本概念

在程序运行过程中，出现需要由CPU立即处理的事务时，CPU暂时中止当前程序的执行转而处理这个事务，这个过程叫做中断。当硬件产生中断时，通过中断号查找到其对应的中断处理程序，执行中断处理程序完成中断处理。

通过中断机制，在外设不需要CPU介入时，CPU可以执行其它任务；当外设需要CPU时，CPU会中断当前任务来响应中断请求。这样可以使CPU避免把大量时间耗费在等待、查询外设状态的操作上，有效提高系统实时性及执行效率。

下面介绍下中断的相关概念：

- 中断号
  中断请求信号特定的标志，计算机能够根据中断号判断是哪个设备提出的中断请求。

- 中断请求
  “紧急事件”向CPU提出申请（发一个电脉冲信号），请求中断，需要CPU暂停当前执行的任务处理该“紧急事件”，这一过程称为中断请求。

- 中断优先级
  为使系统能够及时响应并处理所有中断，系统根据中断事件的重要性和紧迫程度，将中断源分为若干个级别，称作中断优先级。

- 中断处理程序
  当外设发出中断请求后，CPU暂停当前的任务，转而响应中断请求，即执行中断处理程序。产生中断的每个设备都有相应的中断处理程序。

- 中断触发
  中断源向中断控制器发送中断信号，中断控制器对中断进行仲裁，确定优先级，将中断信号发送给CPU。中断源产生中断信号的时候，会将中断触发器置“1”，表明该中断源产生了中断，要求CPU去响应该中断。

- 中断向量
  中断服务程序的入口地址。

- 中断向量表
  存储中断向量的存储区，中断向量与中断号对应，中断向量在中断向量表中按照中断号顺序存储。


## 接口说明

OpenHarmony LiteOS-M内核的中断模块提供下面几种功能，接口详细信息可以查看API参考。

**表1** 中断模块接口

| 功能分类 | 接口名 | 描述 | 
| -------- | -------- | -------- |
| 创建、删除中断 | HalHwiCreate | 中断创建，注册中断号、中断触发模式、中断优先级、中断处理程序。中断被触发时，会调用该中断处理程序。 | 
| HalHwiDelete | 根据指定的中断号，删除中断。 | 
| 打开、关闭中断 | LOS_IntUnLock | 开中断，使能当前处理器所有中断响应。 | 
| LOS_IntLock | 关中断，关闭当前处理器所有中断响应。 | 
| LOS_IntRestore | 恢复到使用LOS_IntLock、LOS_IntUnLock操作之前的中断状态。 | 


## 开发流程

1. 调用中断创建接口HalHwiCreate创建中断。

2. 调用TestHwiTrigger接口触发指定中断（该接口在测试套中定义，通过写中断控制器的相关寄存器模拟外部中断，一般的外设设备，不需要执行这一步）。

3. 调用HalHwiDelete接口删除指定中断，此接口根据实际情况使用，判断是否需要删除中断。


> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> - 根据具体硬件，配置支持的最大中断数及可设置的中断优先级个数。
> 
> - 中断处理程序耗时不能过长，否则会影响CPU对中断的及时响应。
> 
> - 中断响应过程中不能直接、间接执行引起调度的LOS_Schedule等函数。
> 
> - 中断恢复LOS_IntRestore()的入参必须是与之对应的LOS_IntLock()的返回值（即关中断之前的CPSR值）。Cortex-M系列处理器中0-15中断为内部使用，因此不建议用户去申请和创建。


## 编程实例

本实例实现如下功能：

1. 创建中断。

2. 触发中断。

3. 删除中断。

代码实现如下，演示如何创建中断和删除中断，当指定的中断号HWI_NUM_TEST产生中断时，会调用中断处理函数：

```
#include "los_interrupt.h"

/*创建中断*/
#define HWI_NUM_TEST 7

STATIC VOID HwiUsrIrq(VOID)
{
    printf("in the func HwiUsrIrq \n"); 
}

static UINT32 Example_Interrupt(VOID)
{
    UINT32 ret;
    HWI_PRIOR_T hwiPrio = 3;
    HWI_MODE_T mode = 0;
    HWI_ARG_T arg = 0;
  
    /*创建中断*/
    ret = HalHwiCreate(HWI_NUM_TEST, hwiPrio, mode, (HWI_PROC_FUNC)HwiUsrIrq, arg);
    if(ret == LOS_OK){
        printf("Hwi create success!\n");
    } else {
        printf("Hwi create failed!\n");
        return LOS_NOK;
    }

    /* 延时50个Ticks， 当有硬件中断发生时，会调用函数HwiUsrIrq*/
    LOS_TaskDelay(50);

    /*删除中断*/
    ret = HalHwiDelete(HWI_NUM_TEST);    
    if(ret == LOS_OK){
        printf("Hwi delete success!\n");
    } else {
        printf("Hwi delete failed!\n");
        return LOS_NOK;
    }
    return LOS_OK;
}
```


## 结果验证

编译运行得到的结果为：


```
Hwi create success!
Hwi delete success!
```
