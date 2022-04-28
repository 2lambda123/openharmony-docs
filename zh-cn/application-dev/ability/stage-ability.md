# Ability开发指导
## 场景介绍
Stage模型是基于API version 9的应用开发模型，对此模型的介绍详见[Stage模型综述](stage-brief.md)。基于Stage模型的Ability应用开发，主要涉及如下功能逻辑：
- 创建Page Ability应用，如视频播放、新闻资讯等，需要通过屏幕进行浏览的应用，以及支持人机交互。
- 获取Ability的配置信息，如ApplicationInfo、AbilityInfo及HapModuleInfo等。
- 启动/带参数启动/带返回结果启动/带AccountId启动其他Ability。
- 应用向用户申请授权。
- 系统环境变化通知给AbilityStage及Ability。
- 通用组件Call功能，详见[Call调用开发指导](stage-call.md)。
- 连接ServiceExtensionAbility，与ServiceExtensionAbility断开连接，详见[ServiceExtensionAbility开发指导](stage-serviceextension.md)。
- 应用迁移，详见[应用迁移开发指导](stage-ability-continuation.md)。

### 启动模式
ability支持单实例、多实例和指定实例3种启动模式。
在module.json中通过launchType配置项，可以配置具体的启动模式，其中：

| 启动模式     | 描述     |说明             |
| ----------- | -------  |---------------- |
| standard    | 多实例   | 每次startAbility都会启动一个新的实例 |
| singleton   | 单实例   | 系统中只存在唯一一个实例，startAbility时，如果已存在，则复用系统中的唯一一个实例 |
| specified   | 指定实例 | 运行时由ability内部业务决定是否创建多实例 |

缺省情况下是singleton模式。

## 接口说明
AbilityStage功能如下（AbilityStage类，拥有context属性，具体的API详见[接口文档](../reference/apis/js-apis-application-abilitystage.md)）：

**表1** AbilityStage API接口功能介绍
|接口名|描述|
|:------|:------|
|void onCreate()|AbilityStage初始化时被调用。|
|string onAcceptWant(want: Want)|启动指定Ability时被调用。|
|void onConfigurationUpdated(config: Configuration)|全局配置发生变更时被调用。|

Ability功能如下（Ability类，具体的API详见[接口文档](../reference/apis/js-apis-application-ability.md)）：

**表2** Ability API接口功能介绍
|接口名|描述|
|:------|:------|
|void onCreate(want: Want, param: AbilityConstant.LaunchParam)|Ability生命周期回调，Ability启动时被调用。|
|void onDestroy()|Ability生命周期回调，Ability销毁时被调用。|
|void onWindowStageCreate(windowStage: window.WindowStage)|Ability生命周期回调，创建window stage时被调用，应用开发者可通过window.WindowStage的接口执行页面加载等操作。|
|void onWindowStageDestroy()|Ability生命周期回调，销毁window stage时被调用。|
|void onForeground()|Ability生命周期回调，Ability切换至前台时被调用。|
|void onBackground()|Ability生命周期回调，Ability切换至后台时被调用。|
|void onNewWant(want: Want)|Ability回调，Ability的启动模式设置为单例时被调用。|
|void onConfigurationUpdated(config: Configuration)|Ability回调，Ability的系统配置更新时被调用。|

Ability类拥有context属性，context属性为AbilityContext类，AbilityContext类拥有abilityInfo、currentHapModuleInfo等属性，具体的API详见[接口文档](../reference/apis/js-apis-ability-context.md)。

**表3** AbilityContext API接口功能介绍
|接口名|描述|
|:------|:------|
|void startAbility(want: Want, callback: AsyncCallback<void>)|启动Ability。|
|void startAbility(want: Want, options: StartOptions, callback: AsyncCallback<void>)|启动Ability。|
|void startAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback<void>)|带AccountId启动Ability。|
|void startAbilityWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback<void>)|带AccountId启动Ability。|
|void startAbilityForResult(want: Want, callback: AsyncCallback<AbilityResult>)|带返回结果启动Ability。|
|void startAbilityForResult(want: Want, options: StartOptions, callback: AsyncCallback<AbilityResult>)|带返回结果启动Ability。|
|void startAbilityForResultWithAccount(want: Want, accountId: number, callback: AsyncCallback<AbilityResult>)|带返回结果及AccountId启动Ability。|
|void startAbilityForResultWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback<void>)|带返回结果及AccountId启动Ability。|
|void terminateSelf(callback: AsyncCallback<void>)|销毁当前的Page Ability。|
|void terminateSelfWithResult(parameter: AbilityResult, callback: AsyncCallback<void>)|带返回结果销毁当前的Page Ability。|

## 开发步骤
### 创建Page Ability应用
创建Stage模型的Page Ability应用，需实现AbilityStage接口及Ability生命周期接口，并使用窗口提供的方法设置页面。具体示例代码如下：
1. 导入AbilityStage模块。
   ```
   import AbilityStage from "@ohos.application.AbilityStage"
   ```
2. 实现AbilityStage接口。
   ```ts
   export default class MyAbilityStage extends AbilityStage {
    onCreate() {
        console.log("MyAbilityStage onCreate")
    }
   }
   ```
3. 导入Ability模块。
   ```js
   import Ability from '@ohos.application.Ability'
   ```
4. 实现Ability生命周期接口。

   在`onWindowStageCreate(windowStage)`中通过loadContent接口设置应用要加载的页面，window接口的使用详见[窗口开发指导](../windowmanager/window-guidelines.md)。
   ```ts
   export default class MainAbility extends Ability {
    onCreate(want, launchParam) {
        console.log("MainAbility onCreate")
    }

    onDestroy() {
        console.log("MainAbility onDestroy")
    }

    onWindowStageCreate(windowStage) {
        console.log("MainAbility onWindowStageCreate")

        windowStage.loadContent("pages/index").then((data) => {
            console.log("MainAbility load content succeed with data: " + JSON.stringify(data))
        }).catch((error) => {
            console.error("MainAbility load content failed with error: "+ JSON.stringify(error))
        })
    }

    onWindowStageDestroy() {
        console.log("MainAbility onWindowStageDestroy")
    }

    onForeground() {
        console.log("MainAbility onForeground")
    }

    onBackground() {
        console.log("MainAbility onBackground")
    }
   }
   ```
### 获取AbilityStage及Ability的配置信息
AbilityStage类及Ability类均拥有context属性，应用可以通过`this.context`获取Ability实例的上下文，进而获取详细的配置信息。如下示例展示了AbilityStage通过context属性获取包代码路径、hap包名、ability名以及系统语言的方法。具体示例代码如下：
```ts
import AbilityStage from "@ohos.application.AbilityStage"
export default class MyAbilityStage extends AbilityStage {
    onCreate() {
        console.log("MyAbilityStage onCreate")
        let context = this.context
        console.log("MyAbilityStage bundleCodeDir" + context.bundleCodeDir)

        let currentHapModuleInfo = context.currentHapModuleInfo
        console.log("MyAbilityStage hap module name" + currentHapModuleInfo.name)
        console.log("MyAbilityStage hap module mainAbilityName" + currentHapModuleInfo.mainAbilityName)

        let config = this.context.config
        console.log("MyAbilityStage config language" + config.language)
    }
}
```

如下示例展示了Ability通过context属性获取包代码路径、hap包名、ability名以及系统语言的方法。具体示例代码如下：
```ts
import Ability from '@ohos.application.Ability'
export default class MainAbility extends Ability {
    onCreate(want, launchParam) {
        console.log("MainAbility onCreate")
        let context = this.context
        console.log("MainAbility bundleCodeDir" + context.bundleCodeDir)

        let abilityInfo = this.context.abilityInfo;
        console.log("MainAbility ability bundleName" + abilityInfo.bundleName)
        console.log("MainAbility ability name" + abilityInfo.name)

        let config = this.context.config
        console.log("MyAbilityStage config language" + config.language)
    }
}
```

### 启动Ability
应用可以通过`this.context`获取Ability实例的上下文，进而使用AbilityContext中的StartAbility相关接口启动Ability。启动Ability可指定Want、StartOptions、accountId，通过callback形式或promise形式实现。具体示例代码如下：
```ts
let context = this.context
var want = {
    "deviceId": "",
    "bundleName": "com.example.MyApplication",
    "abilityName": "MainAbility"
};
var options = {
    windowMode: 0,
    displayId: 2
};
context.startAbility(want, options).then((data) => {
    console.log("Succeed to start ability with data: " + JSON.stringify(data))
}).catch((error) => {
    console.error("Failed to start ability with error: "+ JSON.stringify(error))
})
```

### 跨设备启动Ability（当前仅对系统应用开放）
>说明：由于DeviceManager的getTrustedDeviceListSync接口仅对系统应用开放，当前跨设备启动Ability仅支持系统应用
跨设备场景下，需指定对端设备deviceId，具体示例代码如下：
```ts
let context = this.context
var want = {
    "deviceId": getRemoteDeviceId(),
    "bundleName": "com.example.MyApplication",
    "abilityName": "MainAbility"
};
context.startAbility(want).then((data) => {
    console.log("Succeed to start remote ability with data: " + JSON.stringify(data))
}).catch((error) => {
    console.error("Failed to start remote ability with error: "+ JSON.stringify(error))
})
```
从DeviceManager获取指定设备的deviceId。具体示例代码如下：
```ts
import deviceManager from '@ohos.distributedHardware.deviceManager';
function getRemoteDeviceId() {
    if (typeof dmClass === 'object' && dmClass != null) {
        var list = dmClass.getTrustedDeviceListSync();
        if (typeof (list) == 'undefined' || typeof (list.length) == 'undefined') {
            console.log("MainAbility onButtonClick getRemoteDeviceId err: list is null");
            return;
        }
        console.log("MainAbility onButtonClick getRemoteDeviceId success:" + list[0].deviceId);
        return list[0].deviceId;
    } else {
        console.log("MainAbility onButtonClick getRemoteDeviceId err: dmClass is null");
    }
}
```

### 应用向用户申请授权
应用需要某些权限如存储、位置信息、访问日历时，需要向用户申请授权。明确需要申请的权限后，在`module.json`中添加待申请的权限，同时通过接口`requestPermissionsFromUser`以动态弹窗的方式向用户申请授权。以访问日历为例，具体示例代码如下：
module.json的修改：
```json
"requestPermissions": [
    {
    "name": "ohos.permission.READ_CALENDAR"
    }
]
```
通过动态弹窗向用户申请授权：
```ts
let context = this.context
let permissions: Array<string> = ['ohos.permission.READ_CALENDAR']
context.requestPermissionsFromUser(permissions).then((data) => {
    console.log("Succeed to request permission from user with data: "+ JSON.stringify(data))
}).catch((error) => {
    console.log("Failed to request permission from user with error: "+ JSON.stringify(error))
})
```
在跨设备场景下，需要向用户申请数据同步的权限。具体示例代码如下：
```ts
let context = this.context
let permissions: Array<string> = ['ohos.permission.DISTRIBUTED_DATASYNC']
context.requestPermissionsFromUser(permissions).then((data) => {
    console.log("Succeed to request permission from user with data: "+ JSON.stringify(data))
}).catch((error) => {
    console.log("Failed to request permission from user with error: "+ JSON.stringify(error))
})
```

### 系统环境变化通知给AbilityStage及Ability
全局配置，比如系统语言和颜色模式发生变化时，通过`onConfigurationUpdated`接口通知给AbilityStage和Ability。系统应用可以通过`updateConfiguration`接口更新系统语言和颜色模式。如下示例展示了AbilityStage的`onConfigurationUpdated`回调实现，系统语言和颜色模式发生变化时触发该回调。具体示例代码如下：
```ts
import Ability from '@ohos.application.Ability'
import ConfigurationConstant from '@ohos.application.ConfigurationConstant'
export default class MyAbilityStage extends AbilityStage {
    onConfigurationUpdated(config) {
        console.log("MyAbilityStage onConfigurationUpdated")
        console.log("MyAbilityStage config language" + config.language)
        console.log("MyAbilityStage config colorMode" + config.colorMode)
    }
}
```

如下示例展示了Ability的`onConfigurationUpdated`回调实现，系统语言、颜色模式以及Display相关的参数，比如方向、Density，发生变化时触发该回调。具体示例代码如下：
```ts
import Ability from '@ohos.application.Ability'
import ConfigurationConstant from '@ohos.application.ConfigurationConstant'
export default class MainAbility extends Ability { {
    onConfigurationUpdated(config) {
        console.log("MainAbility onConfigurationUpdated")
        console.log("MainAbility config language" + config.language)
        console.log("MainAbility config colorMode" + config.colorMode)
        console.log("MainAbility config direction" + config.direction)
        console.log("MainAbility config screenDensity" + config.screenDensity)
        console.log("MainAbility config displayId" + config.displayId)
    }
}
```

## 相关实例
针对Stage模型Ability开发，有以下相关示例可供参考：
- [`StageCallAbility`：StageAbility的创建与使用（eTS）（API9）](https://gitee.com/openharmony/app_samples/tree/master/ability/StageCallAbility)
