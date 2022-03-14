# AbilityDelegator

> **说明**
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import { AbilityDelegator } from './application/abilityDelegator'
```



## AbilityDelegator

### addAbilityMonitor<sup>9+</sup>

addAbilityMonitor(monitor: AbilityMonitor, callback: AsyncCallback\<void>): void

添加AbilityMonitor实例（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                                                         | 必填说明 | 说明                                                         |
| -------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| monitor  | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor) | 是       | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor)实例 |
| callback | AsyncCallback\<void>                                         | 是       | 表示指定的回调方法                                           |

**示例：**

```js
var abilityDelegator;

function onAbilityCreateCallback() {
    console.info("onAbilityCreateCallback");
}

var monitor = {
    abilityName: "abilityname",
    onAbilityCreate: onAbilityCreateCallback
}

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.addAbilityMonitor(monitor, (err) => {
    console.info("addAbilityMonitor callback");
});
```



### addAbilityMonitor<sup>9+</sup>

addAbilityMonitor(monitor: AbilityMonitor): Promise\<void>

添加AbilityMonitor实例（promise形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名  | 类型                                                         | 必填 | 说明                                                         |
| ------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| monitor | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor) | 是   | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor)实例 |

**返回值：**

| 类型           | 说明                |
| -------------- | ------------------- |
| Promise\<void> | 以Promise形式返回。 |

**示例：**

```js
var abilityDelegator;

function onAbilityCreateCallback() {
    console.info("onAbilityCreateCallback");
}

var monitor = {
    abilityName: "abilityname",
    onAbilityCreate: onAbilityCreateCallback
}

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.addAbilityMonitor(monitor).then((void) => {
    console.info("addAbilityMonitor promise");
});
```



### removeAbilityMonitor<sup>9+</sup>

removeAbilityMonitor(monitor: AbilityMonitor, callback: AsyncCallback\<void>): void

删除已经添加的AbilityMonitor实例（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| monitor  | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor) | 是   | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor)实例 |
| callback | AsyncCallback\<void>                                         | 是   | 表示指定的回调方法                                           |

**示例：**

```js
var abilityDelegator;

function onAbilityCreateCallback() {
    console.info("onAbilityCreateCallback");
}

var monitor = {
    abilityName: "abilityname",
    onAbilityCreate: onAbilityCreateCallback
}

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.removeAbilityMonitor(monitor, (err) => {
    console.info("removeAbilityMonitor callback");
});
```



### removeAbilityMonitor<sup>9+</sup>

removeAbilityMonitor(monitor: AbilityMonitor): Promise\<void>

删除已经添加的AbilityMonitor实例（promise形式）

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 名称    | 类型                                                         | 必填 | 说明                                                         |
| ------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| monitor | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor) | 是   | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor)实例 |

**返回值：**

| 类型           | 说明                |
| -------------- | ------------------- |
| Promise\<void> | 以Promise形式返回。 |

- 示例

```js
var abilityDelegator;

function onAbilityCreateCallback() {
    console.info("onAbilityCreateCallback");
}

var monitor = {
    abilityName: "abilityname",
    onAbilityCreate: onAbilityCreateCallback
}

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.removeAbilityMonitor(monitor).then((void) => {
    console.info("removeAbilityMonitor promise");
});
```



### waitAbilityMonitor<sup>9+</sup>

waitAbilityMonitor(monitor: AbilityMonitor, callback: AsyncCallback\<Ability>): void

等待与AbilityMonitor实例匹配的ability到达OnCreate生命周期，并返回ability实例（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| monitor  | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor) | 是   | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor)实例 |
| callback | AsyncCallback\<Ability>                                      | 是   | 表示指定的回调方法                                           |

**示例：**

```js
var abilityDelegator;

function onAbilityCreateCallback() {
    console.info("onAbilityCreateCallback");
}

var monitor = {
    abilityName: "abilityname",
    onAbilityCreate: onAbilityCreateCallback
}

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.waitAbilityMonitor(monitor, (err, data) => {
    console.info("waitAbilityMonitor callback");
});
```



### waitAbilityMonitor<sup>9+</sup>

waitAbilityMonitor(monitor: AbilityMonitor, timeout: number, callback: AsyncCallback\<Ability>): void

设置等待时间，等待与AbilityMonitor实例匹配的ability到达OnCreate生命周期，并返回ability实例（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| monitor  | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor) | 是   | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor)实例 |
| timeout  | number                                                       | 是   | 最大等待时间，单位毫秒                                       |
| callback | AsyncCallback\<Ability>                                      | 是   | 表示指定的回调方法                                           |

**示例：**

```js
var abilityDelegator;
var timeout = 100;

function onAbilityCreateCallback() {
    console.info("onAbilityCreateCallback");
}

var monitor = {
    abilityName: "abilityname",
    onAbilityCreate: onAbilityCreateCallback
}

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.waitAbilityMonitor(monitor, timeout, (err, data) => {
    console.info("waitAbilityMonitor callback");
});
```



### waitAbilityMonitor<sup>9+</sup>

waitAbilityMonitor(monitor: AbilityMonitor, timeout?: number): Promise\<Ability>

等待与AbilityMonitor实例匹配的ability到达OnCreate生命周期，并返回ability实例（promise形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名  | 类型                                                         | 必填 | 说明                                                         |
| ------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| monitor | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor) | 是   | [AbilityMonitor](js-apis-application-abilityMonitor.md#AbilityMonitor)实例 |
| timeout | number                                                       | 否   | 最大等待时间，单位毫秒                                       |

**返回值：**

| 类型           | 说明                       |
| -------------- | -------------------------- |
| Promise\<void> | 以Promise形式返回Ability。 |

**示例：**

```js
var abilityDelegator;

function onAbilityCreateCallback() {
    console.info("onAbilityCreateCallback");
}

var monitor = {
    abilityName: "abilityname",
    onAbilityCreate: onAbilityCreateCallback
}

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.waitAbilityMonitor(monitor).then((data) => {
    console.info("waitAbilityMonitor promise");
});
```



### getAppContext<sup>9+</sup>

getAppContext(): Context

获取应用Context

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型                                  | 说明                                        |
| ------------------------------------- | ------------------------------------------- |
| [Context](js-apis-Context.md#Context) | 应用[Context](js-apis-Context.md#Context)。 |

**示例：**

```js
var abilityDelegator;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
var context = abilityDelegator.getAppContext();
```



### getAbilityState<sup>9+</sup>

getAbilityState(ability: Ability): number

获取指定ability的生命周期状态

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明            |
| ------- | ------- | ---- | --------------- |
| ability | Ability | 是   | 指定Ability对象 |

**返回值：**

| 类型   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| number | 指定ability的生命周期状态。状态枚举值使用[AbilityLifecycleState](js-apis-abilityDelegatorRegistry.md#AbilityLifecycleState)。 |

**示例：**

```js
var abilityDelegator;
var ability;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.getCurrentTopAbility((err, data) => {
    console.info("getCurrentTopAbility callback");
    ability = data;
    var state = abilityDelegator.getAbilityState(ability);
    console.info("getAbilityState" + state);
});
```



### getCurrentTopAbility<sup>9+</sup>

getCurrentTopAbility(callback: AsyncCallback\<Ability>): void

获取当前应用顶部ability（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明               |
| -------- | ----------------------- | ---- | ------------------ |
| callback | AsyncCallback\<Ability> | 是   | 表示指定的回调方法 |

**示例：**

```js
var abilityDelegator;
var ability;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.getCurrentTopAbility((err, data) => {
    console.info("getCurrentTopAbility callback");
    ability = data;
});
```



### getCurrentTopAbility<sup>9+</sup>

getCurrentTopAbility(): Promise\<Ability>

获取当前应用顶部ability（promise形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型              | 说明                                   |
| ----------------- | -------------------------------------- |
| Promise\<Ability> | 以Promise形式返回当前应用顶部ability。 |

**示例：**

```js
var abilityDelegator;
var ability;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.getCurrentTopAbility().then((data) => {
    console.info("getCurrentTopAbility promise");
    ability = data;
});
```



### startAbility

startAbility(want: Want, callback: AsyncCallback\<void>): void

启动指定ability（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                                   | 必填 | 说明               |
| -------- | -------------------------------------- | ---- | ------------------ |
| want     | [Want](js-apis-featureAbility.md#Want) | 是   | 启动Ability参数    |
| callback | AsyncCallback\<void>                   | 是   | 表示指定的回调方法 |

**示例：**

```js
var abilityDelegator;
var want = {
    bundleName: "bundleName",
    abilityName: "abilityName"
};

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.startAbility(want, (err, data) => {
    console.info("startAbility callback");
});
```



### startAbility

startAbility(want: Want): Promise\<void>

启动指定ability（promise形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型                                   | 必填 | 说明            |
| ------ | -------------------------------------- | ---- | --------------- |
| want   | [Want](js-apis-featureAbility.md#Want) | 是   | 启动Ability参数 |

**返回值：**

| 类型           | 说明                |
| -------------- | ------------------- |
| Promise\<void> | 以Promise形式返回。 |

**示例：**

```js
var abilityDelegator;
var want = {
    bundleName: "bundleName",
    abilityName: "abilityName"
};

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.startAbility(want).then((data) => {
    console.info("startAbility promise");
});
```



### doAbilityForeground<sup>9+</sup>

doAbilityForeground(ability: Ability, callback: AsyncCallback\<boolean>): void

调度指定ability生命周期状态到Foreground状态（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                    |
| -------- | ----------------------- | ---- | ------------------------------------------------------- |
| ability  | Ability                 | 是   | 指定Ability对象                                         |
| callback | AsyncCallback\<boolean> | 是   | 表示指定的回调方法<br/>\- true：成功<br/>\- false：失败 |

**示例：**

```js
var abilityDelegator;
var ability;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.getCurrentTopAbility((err, data) => {
    console.info("getCurrentTopAbility callback");
    ability = data;
    abilityDelegator.doAbilityForeground(ability, (err, data) => {
        console.info("doAbilityForeground callback");
    });
});
```



### doAbilityForeground<sup>9+</sup>

doAbilityForeground(ability: Ability): Promise\<boolean>

调度指定ability生命周期状态到Foreground状态（promise形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明            |
| ------- | ------- | ---- | --------------- |
| ability | Ability | 是   | 指定Ability对象 |

**返回值：**

| 类型              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| Promise\<boolean> | 以Promise形式返回执行结果。<br/>\- true：成功<br/>\- false：失败 |

**示例：**

```js
var abilityDelegator;
var ability;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.getCurrentTopAbility((err, data) => {
    console.info("getCurrentTopAbility callback");
    ability = data;
    abilityDelegator.doAbilityForeground(ability).then((data) => {
        console.info("doAbilityForeground promise");
    });
});
```



### doAbilityBackground<sup>9+</sup>

doAbilityBackground(ability: Ability, callback: AsyncCallback\<boolean>): void

调度指定ability生命周期状态到Background状态（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                    | 必填 | 说明                                                    |
| -------- | ----------------------- | ---- | ------------------------------------------------------- |
| ability  | Ability                 | 是   | 指定Ability对象                                         |
| callback | AsyncCallback\<boolean> | 是   | 表示指定的回调方法<br/>\- true：成功<br/>\- false：失败 |

**示例：**

```js
var abilityDelegator;
var ability;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.getCurrentTopAbility((err, data) => {
    console.info("getCurrentTopAbility callback");
    ability = data;
    abilityDelegator.doAbilityBackground(ability, (err, data) => {
        console.info("doAbilityBackground callback");
    });
});
```



### doAbilityBackground<sup>9+</sup>

doAbilityBackground(ability: Ability): Promise\<boolean>

调度指定ability生命周期状态到Background状态（promise形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明            |
| ------- | ------- | ---- | --------------- |
| ability | Ability | 是   | 指定Ability对象 |

**返回值：**

| 类型              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| Promise\<boolean> | 以Promise形式返回执行结果。<br/>\- true：成功<br/>\- false：失败 |

**示例：**

```js
var abilityDelegator;
var ability;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.getCurrentTopAbility((err, data) => {
    console.info("getCurrentTopAbility callback");
    ability = data;
    abilityDelegator.doAbilityBackground(ability).then((data) => {
        console.info("doAbilityBackground promise");
    });
});
```



### print

print(msg: string, callback: AsyncCallback\<void>): void

打印日志信息到单元测试终端控制台（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                 | 必填 | 说明               |
| -------- | -------------------- | ---- | ------------------ |
| msg      | string               | 是   | 日志字符串         |
| callback | AsyncCallback\<void> | 是   | 表示指定的回调方法 |

**示例：**

```js
var abilityDelegator;
var msg = "msg";

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.print(msg, (err) => {
    console.info("print callback");
});
```



### print

print(msg: string): Promise\<void>

打印日志信息到单元测试终端控制台（promise形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明       |
| ------ | ------ | ---- | ---------- |
| msg    | string | 是   | 日志字符串 |

**返回值：**

| 类型           | 说明                |
| -------------- | ------------------- |
| Promise\<void> | 以Promise形式返回。 |

**示例：**

```js
var abilityDelegator;
var msg = "msg";

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.print(msg).then(() => {
    console.info("print promise");
});
```



### executeShellCommand

executeShellCommand(cmd: string, callback: AsyncCallback\<ShellCmdResult>): void

执行指定的shell命令（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明               |
| -------- | ------------------------------------------------------------ | ---- | ------------------ |
| cmd      | string                                                       | 是   | shell命令字符串    |
| callback | AsyncCallback\<[ShellCmdResult](js-apis-application-shellCmdResult.md#ShellCmdResult)> | 是   | 表示指定的回调方法 |

**示例：**

```js
var abilityDelegator;
var cmd = "cmd";

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.executeShellCommand(cmd, (err,data) => {
    console.info("executeShellCommand callback");
});
```



### executeShellCommand

executeShellCommand(cmd: string, timeoutSecs: number, callback: AsyncCallback\<ShellCmdResult>): void

执行指定的shell命令（callback形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名      | 类型                                                         | 必填 | 说明               |
| ----------- | ------------------------------------------------------------ | ---- | ------------------ |
| cmd         | string                                                       | 是   | shell命令字符串    |
| timeoutSecs | number                                                       | 是   | 设定时间，单位秒   |
| callback    | AsyncCallback\<[ShellCmdResult](js-apis-application-shellCmdResult.md#ShellCmdResult)> | 是   | 表示指定的回调方法 |

**示例：**

```js
var abilityDelegator;
var cmd = "cmd";
var timeout = 100;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.executeShellCommand(cmd, timeout, (err,data) => {
    console.info("executeShellCommand callback");
});
```



### executeShellCommand

executeShellCommand(cmd: string, timeoutSecs: number): Promise\<ShellCmdResult>

执行指定的shell命令（promise形式）

**系统能力：**SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名      | 类型   | 必填 | 说明             |
| ----------- | ------ | ---- | ---------------- |
| cmd         | string | 是   | shell命令字符串  |
| timeoutSecs | number | 否   | 设定时间，单位秒 |

**返回值：**

| 类型                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Promise\<[ShellCmdResult](js-apis-application-shellCmdResult.md#ShellCmdResult)> | 以Promise形式返回Shell命令执行结果[ShellCmdResult](js-apis-application-shellCmdResult.md#ShellCmdResult)对象。 |

**示例：**

```js
var abilityDelegator;
var cmd = "cmd";
var timeout = 100;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.executeShellCommand(cmd, timeout).then((data) => {
    console.info("executeShellCommand promise");
});
```
