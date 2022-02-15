# 性能打点

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 从API Version 8开始，该接口不再维护，推荐使用新接口[hiTraceMeter](js-apis-hitracemeter.md)。具体新接口在接口描述中说明。
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import bytrace from '@ohos.bytrace';
```


## 权限

无


## bytrace.startTrace

startTrace(name: string, taskId: number, expectedTime?: number): void

标记一个预追踪耗时任务的开始，expectedTime是可选参数，标识该任务的期望耗时。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | name | string | 是 | 要追踪的任务名称 |
  | taskId | number | 是 | 任务id |
  | expectedTime | number | 否 | 期望的耗时时间，单位：ms |

  > ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
  > 如果有多个相同name的任务需要追踪或者对同一个任务要追踪多次，并且这些会同时被执行，则每次调用startTrace的taskId必须不一致。如果具有相同name的任务是串行执行的，则taskId可以相同。在下面bytrace.finishTrace的示例中会举例说明。

- 示例：
  ```
  bytrace.startTrace("myTestFunc", 1);
  bytrace.startTrace("myTestFunc", 1, 5); //从startTrace到finishTrace流程的耗时期望为5ms
  ```


## bytrace.finishTrace

finishTrace(name: string, taskId: number): void

标记一个预追踪耗时任务的结束。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | name | string | 是 | 要追踪的任务名称 |
  | taskId | number | 是 | 任务id |

  > ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
  > finishTrace的name和taskId必须与流程开始的startTrace对应参数值一致。

- 示例：
  ```
  bytrace.finishTrace("myTestFunc", 1);
  ```

  ```
  //追踪并行执行的同名任务
  bytrace.startTrace("myTestFunc", 1);
  //业务流程...... 
  bytrace.startTrace("myTestFunc", 2);  //第二个追踪的任务开始，同时第一个追踪的同名任务还没结束，出现了并行执行，对应接口的taskId需要不同。
  //业务流程...... 
  bytrace.finishTrace("myTestFunc", 1);
  //业务流程...... 
  bytrace.finishTrace("myTestFunc", 2);
  ```

  ```
  //追踪串行执行的同名任务
  bytrace.startTrace("myTestFunc", 1);
  //业务流程...... 
  bytrace.finishTrace("myTestFunc", 1);  //第一个追踪的任务结束
  //业务流程...... 
  bytrace.startTrace("myTestFunc", 1);   //第二个追踪的同名任务开始，同名的待追踪任务串行执行。
  //业务流程...... 
  bytrace.finishTrace("myTestFunc", 1);
  ```


## bytrace.traceByValue

traceByValue(name: string, value: number): void

用来标记一个预追踪的数值变量，该变量的数值会不断变化。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | name | string | 是 | 要追踪的数值变量名称 |
  | value | number | 是 | 变量的值 |

- 示例：
  ```
  let traceCount = 3;
  bytrace.traceByValue("myTestCount", traceCount);
  traceCount = 4;
  bytrace.traceByValue("myTestCount", traceCount);
  //业务流程......
  ```
