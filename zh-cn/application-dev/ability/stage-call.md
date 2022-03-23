# Call调用开发指导
## 场景介绍
Ability Call调用是Ability能力的扩展，它为Ability提供一种能够被外部调用的能力。使Ability既能被拉起到前台展示UI，也支持Ability在后台被创建并运行。应用开发者可通过Call调用，使用IPC通信实现不同Ability之间的数据共享。Call调用的场景主要包括：
- 创建Callee被调用端。
- 访问Callee被调用端。

本文中的Caller和Callee分别表示调用者和被调用者，Call调用流程示意图如下。

![stage-call](figures/stage-call.png)

## 接口说明
Caller及Callee功能如下：具体的API详见[接口文档](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis/js-apis-application-ability.md#caller)。

**表1** Call API接口功能介绍
|接口名|描述|
|:------|:------|
|Promise<Caller> startAbilityByCall(want: Want)|获取指定通用组件的Caller通信接口，拉起指定通用组件并将其切换到后台。|
|void on(method: string, callback: CaleeCallBack)|Callee.on，通用组件Callee注册method对应的callback方法。|
|void off(method: string)|Callee.off，通用组件Callee去注册method的callback方法。|
|Promise<void> call(method: string, data: rpc.Sequenceable)|Caller.call，向通用组件Callee发送约定序列化数据。|
|Promise<rpc.MessageParcel> callWithResult(method: string, data: rpc.Sequenceable)|Caller.callWithResult，向通用组件Callee发送约定序列化数据, 并将返回的约定序列化数据带回。|
|void release()|Caller.release，释放通用组件的Caller通信接口。|
|void onRelease(callback: OnReleaseCallBack)|Caller.onRelease，注册通用组件通信断开监听通知。|

## 开发步骤
### 创建Callee被调用端
Callee被调用端，需要实现指定方法的数据接收回调函数、数据的序列化及反序列化方法。在需要接收数据期间，通过on接口注册监听，无需接收数据时通过off接口解除监听。
1. 配置Ability的启动模式
配置module.json5，将Callee被调用端所在的Ability配置为单实例"singleton"。

|Json字段|字段说明|
|:------|:------|
|"launchType"|Ability的启动模式，设置为"singleton"类型 |

Ability配置标签示例如下：
```json
"abilities":[{
    "name": ".CalleeAbility",
    "srcEntrance": "./ets/CalleeAbility/CalleeAbility.ts",
    "launchType": "singleton",
    "description": "$string:CalleeAbility_desc",
    "icon": "$media:icon",
    "label": "$string:CalleeAbility_label",
    "visible": true
}]
```
2. 导入Ability模块
```
import Ability from '@ohos.application.Ability'
```
3. 定义约定的序列化数据
调用端及被调用端发送接收的数据格式需协商一致，如下示例约定数据由number和string组成。具体示例代码如下：
```ts
export class MySequenceable {
    num: number = 0
    str: String = ""

    constructor(num, string) {
        this.num = num
        this.str = string
    }

    marshalling(messageParcel) {
        messageParcel.writeInt(this.num)
        messageParcel.writeString(this.str)
        return true
    }

    unmarshalling(messageParcel) {
        this.num = messageParcel.readInt()
        this.str = messageParcel.readString()
        return true
    }
}
```
4. 实现Callee.on监听及Callee.off解除监听
被调用端Callee的监听函数注册时机, 取决于应用开发者。注册监听之前的数据不会被处理，取消监听之后的数据不会被处理。如下示例在Ability的onCreate注册'CalleeSortMethod'监听，在onDestroy取消监听，收到序列化数据后对字符串排序后返回，应用开发者根据实际需要做相应处理。具体示例代码如下：
```ts
let TAG = '[CalleeAbility] '
let method = 'CalleeSortMethod'

function CalleeSortFunc(data) {
    let receiveData = new MySequenceable(0, '')
    data.readSequenceable(receiveData)
    console.log(TAG + 'receiveData[' + receiveData.num + ',' + receiveData.str + ']')
    return new MySequenceable(receiveData.num + 1, Array.from(receiveData.str).sort().join(''))
}

export default class CalleeAbility extends Ability {
    onCreate(want, launchParam) {
        try {
            this.callee.on(method, CalleeSortFunc)
        } catch (error) {
            console.error(TAG + method + 'register failed with error: ' + JSON.stringify(error))
        }
    }

    onDestroy() {
        try {
            this.callee.off(method)
        } catch (error) {
            console.error(TAG + method + 'unregister failed with error: ' + JSON.stringify(error))
        }
    }
}
```

### 访问Callee被调用端
1. 导入Ability模块
```
import Ability from '@ohos.application.Ability'
```
2. 获取Caller通信接口
Ability的context属性实现了startAbilityByCall方法，用于获取指定通用组件的Caller通信接口。如下示例通过`this.context`获取Ability实例的context属性，使用startAbilityByCall拉起Callee被调用端并获取Caller通信接口，注册Caller的onRelease监听。应用开发者根据实际需要做相应处理。具体示例代码如下：
```ts
let TAG = '[MainAbility] '
var caller = undefined
let context = this.context

context.startAbilityByCall({
    bundleName: 'com.samples.CallApplication',
    abilityName: 'CalleeAbility'
}).then((data) => {
    if (data != null) {
        caller = data
        console.log(TAG + 'get caller success')
        // 注册caller的release监听
        caller.onRelease((msg) => {
            console.log(TAG + 'caller onRelease is called ' + msg)
        })
        console.log(TAG + 'caller register OnRelease succeed')
    }
}).catch((error) => {
    console.error(TAG + 'get caller failed with ' + error)
})
```
3. 发送约定序列化数据
向被调用端发送Sequenceable数据有两种方式，一种是不带返回值，一种是获取被调用端返回的数据，method以及序列化数据需要与被调用端协商一致。如下示例调用Call接口，向Calee被调用端发送数据。具体示例代码如下：
```ts
let method = 'CalleeSortMethod'
let msg = new MySequenceable(1, 'call_str')
caller.call(method, msg).then(() => {
        console.log(TAG + 'caller call succeed')
    }).catch((error) => {
    console.error(TAG + 'caller call failed with ' + error)
})
```

如下示例调用CallWithResult接口，向Calee被调用端发送待处理的数据，并将method方法处理完毕的数据赋值给callback。具体示例代码如下：
```ts
let method = 'CalleeSortMethod'
let msg = new MySequenceable(1, sortString)
caller.callWithResult(method, msg)
    .then((data) => {
        let resultMsg = new MySequenceable(0, '')
        data.readSequenceable(resultMsg)
        callback(resultMsg.str)
        console.log(TAG + 'caller result is [' + resultMsg.num + ',' + resultMsg.str + ']')
    }).catch((error) => {
    console.error(TAG + 'caller callWithResult failed with ' + error)
})
```
4. 释放Caller通信接口
Caller不再使用后，应用开发者可以通过release接口释放Caller。具体示例代码如下：
```ts
try {
    caller.release()
    caller = undefined
    console.log(TAG + 'caller release succeed')
} catch (error) {
    console.error(TAG + 'caller release failed with ' + error)
}
```

## 开发实例
针对Stage模型本地Call功能开发，有以下示例工程可供参考：

[eTSStageCallAbility]()

本示例eTSStageCallAbility中，在Application目录的AbilityStage.ts中实现AbilityStage的接口，在MainAbility目录实现Ability的接口并设置"pages/index"为应用的界面，在CaleeAbility目录实现Callee被调用端。MainAbility获取Caller通信接口后，支持用户输入字符串，做序列化处理后传递给CaleeAbility被调用端处理，Calee将字符串排序，返回序列化数据并将排序结果显示在页面上。