# Background Task Management Development

## When to Use

If a service needs to be continued when the application or service module is running in the background (not visible to users), the application or service module can request a transient task or continuous task for delayed suspension based on the service type.


## Available APIs

```js
import backgroundTaskManager from '@ohos.backgroundTaskManager';
```

## Transient Tasks

**Table 1** Main APIs for transient tasks

| API| Description|
| -------- | -------- |
| function&nbsp;requestSuspendDelay(reason:&nbsp;string,&nbsp;callback:&nbsp;Callback&lt;void&gt;):&nbsp;**DelaySuspendInfo**; | Requests delayed suspension after the application switches to the background.<br>The default duration of delayed suspension is 180000 when the battery level is higher than or equal to the broadcast low battery level and 60000 when the battery level is lower than the broadcast low battery level.|
| function&nbsp;getRemainingDelayTime(requestId:&nbsp;number,&nbsp;callback:&nbsp;AsyncCallback&lt;number&gt;):&nbsp;void;<br>function&nbsp;getRemainingDelayTime(requestId:&nbsp;number):&nbsp;Promise&lt;number&gt;; | Obtains the remaining duration before the application is suspended. (The value of **requestId** is obtained from the return value of **requestSuspendDelay**.)<br>Two asynchronous methods are provided: callback and promise.|
| function&nbsp;cancelSuspendDelay(requestId:&nbsp;number):&nbsp;void; | Cancels the suspension delay. (The value of **requestId** is obtained from the return value of **requestSuspendDelay**.)|

**Table 2** Parameters in DelaySuspendInfo

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| requestId | number | Yes| ID of the suspension delay request.|
| actualDelayTime | number | Yes| Actual suspension delay duration of the application, in milliseconds.|


## How to Develop


1. Request a suspension delay.

    ```js
    import backgroundTaskManager from '@ohos.backgroundTaskManager';

    let myReason = 'test requestSuspendDelay';
    let delayInfo = backgroundTaskManager.requestSuspendDelay(myReason, () => {
        console.info("Request suspension delay will time out.");
    });

    var id = delayInfo.requestId;console.info("requestId is: " + id);
    ```


2. Obtain the remaining duration before the application is suspended.

    ```js
    backgroundTaskManager.getRemainingDelayTime(id).then( res => {
        console.log('promise => Operation succeeded. Data: ' + JSON.stringify(res));
    }).catch( err => {
        console.log('promise => Operation failed. Cause: ' + err.data);
    });
    ```


3. Cancel the suspension delay.

    ```js
    backgroundTaskManager.cancelSuspendDelay(id);
    ```


## Development Examples

```js
import backgroundTaskManager from '@ohos.backgroundTaskManager';
let myReason = 'test requestSuspendDelay';

// Request a suspension delay.
let delayInfo = backgroundTaskManager.requestSuspendDelay(myReason, () => {
    console.info("Request suspension delay will time out.");
});

// Print the suspension delay information.
var id = delayInfo.requestId;
var time = delayInfo.actualDelayTime;
console.info("The requestId is: " + id);
console.info("The actualDelayTime is: " + time);

// Obtain the remaining duration before the application is suspended.
backgroundTaskManager.getRemainingDelayTime(id).then( res => {
    console.log('promise => Operation succeeded. Data: ' + JSON.stringify(res));
}).catch( err => {
    console.log('promise => Operation failed. Cause: ' + err.data);
});

// Cancel the suspension delay.
backgroundTaskManager.cancelSuspendDelay(id);
```

## Continuous Tasks

### Required Permissions

ohos.permission.KEEP_BACKGROUND_RUNNING

**Table 3** Main APIs for continuous tasks

| API| Description|
| -------- | -------- |
| function startBackgroundRunning(context: Context, bgMode: BackgroundMode, wantAgent: WantAgent, callback: AsyncCallback&lt;void&gt;): void;<br>function startBackgroundRunning(context: Context, bgMode: BackgroundMode, wantAgent: WantAgent): Promise&lt;void&gt;; | Requests a continuous task from the system so that the application keeps running in the background.|
| function stopBackgroundRunning(context: Context, callback: AsyncCallback&lt;void&gt;): void;<br>function stopBackgroundRunning(context: Context): Promise&lt;void&gt;; | Cancels the continuous task.|


For details about **WantAgent**, see [WantAgent](../reference/apis/js-apis-notification.md#WantAgent).


**Table 4** Background modes
| Name| ID Value| Description|
| -------- | -------- | -------- |
| DATA_TRANSFER           | 1 | Data transfer.|
| AUDIO_PLAYBACK          | 2 | Audio playback.|
| AUDIO_RECORDING         | 3 | Audio recording.|
| LOCATION                | 4 | Positioning and navigation.|
| BLUETOOTH_INTERACTION   | 5 | Bluetooth-related task.|
| MULTI_DEVICE_CONNECTION | 6 | Multi-device connection.|
| WIFI_INTERACTION        | 7 | WLAN-related task (reserved).|
| VOIP                    | 8 | Voice and video call (reserved).|
| TASK_KEEPING            | 9 | Computing task (for PC only).|


## How to Develop

1. Declare the continuous task permission in the **config.json** file.

    ```json
    "module": {
        "package": "com.example.myapplication",
        ...,
        "reqPermissions": [
            {
            "name": "ohos.permission.KEEP_BACKGROUND_RUNNING"
            }
        ]
    }
    ```

2. Request a continuous task.

    ```js
    import backgroundTaskManager from '@ohos.backgroundTaskManager';
    import featureAbility from '@ohos.ability.featureAbility';
    import wantAgent from '@ohos.wantAgent';

    let wantAgentInfo = {
        wants: [
            {
                bundleName: "com.example.myapplication",
                abilityName: "com.example.myapplication.MainAbility"
            }
        ],
        operationType: wantAgent.OperationType.START_ABILITY,
        requestCode: 0,
        wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESET_FLAG]
    };

    // Obtain the WantAgent object by using the getWantAgent method of the wantAgent module.
    wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
        backgroundTaskManager.startBackgroundRunning(featureAbility.getContext(),
            backgroundTaskManager.BackgroundMode.DATA_TRANSFER, wantAgentObj).then(() => {
            console.info("Operation succeeded");
        }).catch((err) => {
            console.error("Operation failed Cause: " + err);
        });
    });
    ```

3. Cancel the continuous task.

    ```js
    import backgroundTaskManager from '@ohos.backgroundTaskManager';
    import featureAbility from '@ohos.ability.featureAbility';

    backgroundTaskManager.stopBackgroundRunning(featureAbility.getContext()).then(() => {
        console.info("Operation succeeded");
    }).catch((err) => {
        console.error("Operation failed Cause: " + err);
    });

    ```

## Development Examples

After a service is started, call the API for requesting a continuous task in the **onStart** callback of the Service ability to declare that the service needs to run in the background for a long time. In the **onStop** callback, call the API for canceling the continuous task.
In the **service.js** file:

```js
import backgroundTaskManager from '@ohos.backgroundTaskManager';
import featureAbility from '@ohos.ability.featureAbility';
import wantAgent from '@ohos.wantAgent';

function startBackgroundRunning() {
    let wantAgentInfo = {
        wants: [
            {
                bundleName: "com.example.myapplication",
                abilityName: "com.example.myapplication.MainAbility"
            }
        ],
        operationType: wantAgent.OperationType.START_ABILITY,
        requestCode: 0,
        wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESET_FLAG]
    };

    // Obtain the WantAgent object by using the getWantAgent method of the wantAgent module.
    wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
        backgroundTaskManager.startBackgroundRunning(featureAbility.getContext(),
            backgroundTaskManager.BackgroundMode.DATA_TRANSFER, wantAgentObj).then(() => {
            console.info("Operation succeeded");
        }).catch((err) => {
            console.error("Operation failed Cause: " + err);
        });
    });
}

function stopBackgroundRunning() {
    backgroundTaskManager.stopBackgroundRunning(featureAbility.getContext()).then(() => {
        console.info("Operation succeeded");
    }).catch((err) => {
        console.error("Operation failed Cause: " + err);
    });
}

export default {
    onStart(want) {
        console.info('ServiceAbility onStart');
        startBackgroundRunning();
    },
    onStop() {
        console.info('ServiceAbility onStop');
        stopBackgroundRunning();
    },
    onConnect(want) {
        console.info('ServiceAbility onConnect');
        return {};
    },
    onReconnect(want) {
        console.info('ServiceAbility onReconnect');
    },
    onDisconnect() {
        console.info('ServiceAbility onDisconnect');
    },
    onCommand(want, restart, startId) {
        console.info('ServiceAbility onCommand');
    }
};
```
