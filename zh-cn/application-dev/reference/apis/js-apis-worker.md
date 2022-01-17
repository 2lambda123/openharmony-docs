# 启动一个worker

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import worker from '@ohos.worker';
```


## 权限

无


## 属性

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| parentPort | [DedicatedWorkerGlobalScope](#dedicatedworkerglobalscope) | 是 | 是 | worker线程用于与宿主线程通信的对象 |


## WorkerOptions

worker构造函数函数的选项信息，用于为worker添加其他信息。

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| type | "classic" | 是 | 是 | 按照指定方式执行脚本。 |
| name | string | 是 | 是 | worker的名称。 |


## Worker

使用以下方法前，均需先构造worker实例，Worker类继承[EventTarget](#eventtarget)。


### constructor

constructor(scriptURL: string, options?: WorkerOptions)

worker构造函数。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | scriptURL | string | 是 | worker执行脚本的url，路径规范：若DevEco新建工程在pages同级下没有workers目录，需要新建workers目录，将脚本文件放入workers目录。 |
  | options | [WorkerOptions](#workeroptions) | 否 | worker构造的选项。 |

- 返回值：
  | 参数名 | 说明 |
  | -------- | -------- |
  | worker | 执行Worker构造函数生成的Worker对象，失败则返回undefined。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js", {name:"first worker"});
  ```


### postMessage

postMessage(message: Object, options?: PostMessageOptions): void

向worker线程发送消息，数据的传输采用结构化克隆算法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | message | Object | 是 | 发送至worker的数据。 |
  | options | [PostMessageOptions](#postmessageoptions) | 否 | 可转移对象是&nbsp;ArrayBuffer&nbsp;的实例对象。transferList数组中不可传入null。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js");
  worker.postMessage("hello world");
  
  const worker = new worker.Worker("workers/worker.js");
  var buffer = new ArrayBuffer(8);
  worker.postMessage(buffer, [buffer]);
  ```


### on

on(type: string, listener: EventListener): void

向worker添加一个事件监听。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 监听事件的type。 |
  | listener | [EventListener](#eventlistener) | 是 | 回调的事件。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.on("alert", (e)=>{
      console.log("alert listener callback");
  })
  ```


### once

once(type: string, listener: EventListener): void

向worker添加一个事件监听，事件监听只执行一次便自动删除。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 监听事件的type。 |
  | listener | [EventListener](#eventlistener) | 是 | 回调的事件。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js");
  worker.once("alert", (e)=>{
      console.log("alert listener callback");
  })
  ```


### off

off(type: string, listener?: EventListener): void

删除worker的事件监听。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 需要删除事件的type。 |
  | listener | [EventListener](#eventlistener) | 否 | 需要删除的回调的事件。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js");
  worker.off("alert");
  ```


### terminate

terminate(): void

关闭worker线程，终止worker接收消息。

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.terminate()
  ```


### onexit

onexit?: (code: number) =&gt; void

Worker对象的onexit属性表示worker退出时被调用的事件处理程序，处理程序在宿主线程中执行。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | code | number | 否 | worker退出的code。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.onexit = function(e) {
      console.log("onexit")
  }
  ```


### onerror

onerror?: (err: ErrorEvent) =&gt; void

Worker对象的onerror属性表示worker在执行过程中发生异常被调用的事件处理程序，处理程序在宿主线程中执行。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | err | [ErrorEvent](#errorevent) | 否 | 异常数据。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.onerror = function(e) {
      console.log("onerror")
  }
  ```


### onmessage

onmessage?: (event: MessageEvent) =&gt; void

Worker对象的onmessage属性表示宿主线程接收到来自其创建的worker通过parentPort.postMessage接口发送的消息时被调用的事件处理程序，处理程序在宿主线程中执行。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | event | [MessageEvent](#messageevent) | 否 | 收到的worker消息数据。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.onmessage = function(e) {
      console.log("onerror")
  }
  ```


### onmessageerror

onmessageerror?: (event: MessageEvent) =&gt; void

Worker对象的onmessageerror属性表示当 Worker 对象接收到一条无法被序列化的消息时被调用的事件处理程序，处理程序在宿主线程中执行。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | event | [MessageEvent](#messageevent) | 否 | 异常数据。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.onmessageerror= function(e) {
      console.log("onmessageerror")
  }
  ```


## EventTarget


### addEventListener

addEventListener(type: string, listener: EventListener): void

向worker添加一个事件监听。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 监听事件的type。 |
  | listener | [EventListener](#eventlistener) | 是 | 回调的事件。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.addEventListener("alert", (e)=>{
      console.log("alert listener callback");
  })
  ```


### removeEventListener

removeEventListener(type: string, callback?: EventListener): void

删除worker的事件监听。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 需要删除事件的type。 |
  | callback | [EventListener](#eventlistener) | 否 | 需要删除的回调的事件。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.removeEventListener("alert")
  ```


### dispatchEvent

dispatchEvent(event: Event): boolean

分发定义在worker的事件。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | event | [Event](#event) | 是 | 需要分发的事件。 |

- 返回值：
  | 参数名 | 说明 |
  | -------- | -------- |
  | boolean | 分发的结果，false表示分发失败。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.dispatchEvent({type:"alert"})
  ```


### removeAllListener

removeAllListener(): void

删除worker的所有事件监听。

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.removeAllListener({type:"alert"})
  ```


## DedicatedWorkerGlobalScope

worker线程用于与宿主线程通信的类，通过postMessage接口发送消息给宿主线程、close接口关闭worker线程，DedicatedWorkerGlobalScope类继承[WorkerGlobalScope](#workerglobalscope)。


### postMessage

postMessage(message: Object, options?: PostMessageOptions): void

worker向宿主线程发送消息。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | message | Object | 是 | 发送至worker的数据。 |
  | options | [PostMessageOptions](#postmessageoptions) | 否 | 可转移对象是ArrayBuffer的实例对象。transferList数组中不可传入null。 |

- 示例：
  ```
  // main.js
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.postMessage("hello world")
  worker.onmessage = function(e) {
      console.log("receive data from worker.js")
  }
  
  // worker.js
  import worker from "@ohos.worker";
  const parentPort = worker.parentPort;
  parentPort.onmessage = function(e){
      parentPort.postMessage("receive data from main.js")
  }
  ```


### close

close(): void

关闭worker线程，终止worker接收消息。

- 示例：
  ```
  // main.js
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  
  // worker.js
  import worker from "@ohos.worker";
  const parentPort = worker.parentPort;
  parentPort.onmessage = function(e) {
      parentPort.close()
  }
  ```


### onmessage

onmessage?: (event: MessageEvent) =&gt; void

DedicatedWorkerGlobalScope的onmessage属性表示worker线程收到来自其宿主线程通过worker.postMessage接口发送的消息时被调用的事件处理程序，处理程序在worker线程中执行。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | event | [MessageEvent](#messageevent) | 否 | 收到的worker消息数据。 |

- 示例：
  ```
  // main.js
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  worker.postMessage("hello world")
  
  // worker.js
  import worker from "@ohos.worker";
  const parentPort = worker.parentPort;
  parentPort.onmessage = function(e) {
      console.log("receive main.js message")
  }
  ```


### onmessageerror

onmessageerror?: (event: MessageEvent) =&gt; void

DedicatedWorkerGlobalScope的onmessageerror属性表示当 Worker 对象接收到一条无法被反序列化的消息时被调用的事件处理程序，处理程序在worker线程中执行。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | event | [MessageEvent](#messageevent) | 否 | 异常数据。 |

- 示例：
  ```
  // main.js
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  
  // worker.js
  import worker from "@ohos.worker";
  const parentPort = worker.parentPort;
  parentPort.onmessageerror= function(e) {
      console.log("worker.js onmessageerror")
  }
  ```


## PostMessageOptions

明确数据传递过程中需要转移所有权对象的类，传递所有权的对象必须是ArrayBuffer。

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| transfer | Object[] | 是 | 是 | ArrayBuffer数组，用于传递所有权。 |


## Event

事件类。

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| type | string | 是 | 否 | 指定事件的type。 |
| timeStamp | number | 是 | 否 | 事件创建时的时间戳（精度为毫秒）。 |


## EventListener

事件监听类。


### (evt: Event): void | Promise&lt;void&gt;

执行的回调函数。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | evt | [Event](#event) | 是 | 回调的事件类。 |

- 返回值
  | 参数名 | 说明 |
  | -------- | -------- |
  | void&nbsp;\|&nbsp;Promise&lt;void&gt; | 无返回值或者以Promise形式返回。 |

- 示例：
  ```
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js");
  worker.addEventListener("alert", (e)=>{
      console.log("alert listener callback");
  })
  ```


## ErrorEvent

错误事件类，用于表示worker执行过程中出现异常的详细信息，ErrorEvent类继承[Event](#event)。

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| message | string | 是 | 否 | 异常发生的错误信息。 |
| filename | string | 是 | 否 | 出现异常所在的文件。 |
| lineno | number | 是 | 否 | 异常所在的行数。 |
| colno | number | 是 | 否 | 异常所在的列数。 |
| error | Object | 是 | 否 | 异常类型。 |


## MessageEvent

消息类，持有worker线程间传递的数据。

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| data | T | 是 | 否 | 线程间传递的数据。 |


## WorkerGlobalScope

worker线程自身的运行环境，WorkerGlobalScope类继承[EventTarget](#eventtarget)。


### 属性

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| name | string | 是 | 否 | worker的名字，有new&nbsp;Worker时指定。 |
| self | [WorkerGlobalScope](#workerglobalscope)&nbsp;&amp;&nbsp;typeof&nbsp;globalThis | 是 | 否 | WorkerGlobalScope本身。 |


### onerror

onerror?: (ev: ErrorEvent) =&gt; void

WorkerGlobalScope的onerror属性表示worker在执行过程中发生异常被调用的事件处理程序，处理程序在worker线程中执行。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | ev | [ErrorEvent](#errorevent) | 否 | 异常数据。 |

- 示例：
  ```
  // main.js
  import worker from '@ohos.worker';
  const worker = new worker.Worker("workers/worker.js")
  
  // worker.js
  import worker from "@ohos.worker";
  const parentPort = worker.parentPort
  parentPort.onerror = function(e){
      console.log("worker.js onerror")
  }
  ```
