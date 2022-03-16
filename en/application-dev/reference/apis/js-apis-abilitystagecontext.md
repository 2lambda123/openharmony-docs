# AbilityStageContext

> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.


Implements the context of an ability stage. This module is inherited from [Context](js-apis-application-context.md).


## Usage


The ability stage context is obtained through an **AbilityStage** instance.


  
```
import AbilityStage from '@ohos.application.AbilityStage';
class MyAbilityStage extends AbilityStage {
    onCreate() {
        let abilityStageContext = this.context;
    }
}
```


## Attributes

  | Name| Type| Readable| Writable| Description| 
| -------- | -------- | -------- | -------- | -------- |
| currentHapModuleInfo | HapModuleInfo | Yes| No| **ModuleInfo** object corresponding to the **AbilityStage**.| 
| config | [Configuration](js-apis-configuration.md) | Yes| No| Configuration for the environment where the application is running.| 
