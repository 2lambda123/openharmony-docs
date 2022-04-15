# Input Event Client


> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
>
> - The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> - The APIs of this module are system APIs and cannot be called by third-party applications.


## Modules to Import


```
import inputEventClient from '@ohos.multimodalInput.inputEventClient';
```


## inputEventClient.injectEvent

injectEvent({KeyEvent: KeyEvent}): void

Injects a key.

**System capability**: SystemCapability.MultimodalInput.Input.InputSimulator

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| KeyEvent | [KeyEvent](#keyevent) | Yes| Information about the key to inject.|

**Example**

```
let keyEvent = {
    isPressed: true,
    keyCode: 2,
    keyDownDuration: 0,
    isIntercepted: false
}
res = inputEventClient.injectEvent({KeyEvent: keyEvent});
```


## KeyEvent

Defines the information about the key to inject.

**System capability**: SystemCapability.MultimodalInput.Input.InputSimulator

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| isPressed | boolean | Yes| Whether the key is pressed.|
| keyCode | Number | Yes| Key code.|
| keyDownDuration | boolean | Yes| Duration for which the key is pressed.|
| isIntercepted | Number | Yes| Whether the key can be intercepted.|
