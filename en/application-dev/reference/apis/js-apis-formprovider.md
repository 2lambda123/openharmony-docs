# FormProvider

> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.

Provides APIs related to the form provider.

## Modules to Import

```
import formProvider from '@ohos.application.formProvider';
```

## Required Permissions

None.

## setFormNextRefreshTime

setFormNextRefreshTime(formId: string, minute: number, callback: AsyncCallback&lt;void&gt;): void;

Sets the next refresh time for a form. This API uses an asynchronous callback to return the result.

**System capability**

SystemCapability.Ability.Form

**Parameters**

  | Name| Type   | Mandatory| Description                                  |
  | ------ | ------ | ---- | ------------------------------------- |
  | formId | string | Yes  | Form ID.                              |
  | minute | number | Yes  | Refresh interval, in minutes. The value must be greater than or equal to 5.    |
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```js
  var formId = "12400633174999288";
  formProvider.setFormNextRefreshTime(formId, 5, (error, data) => {
      if (error) {
          console.log('formProvider setFormNextRefreshTime, error:' + error.code);
      }
  });
  ```

## setFormNextRefreshTime

setFormNextRefreshTime(formId: string, minute: number): Promise&lt;void&gt;;

Sets the next refresh time for a form. This API uses a promise to return the result.

**System capability**

SystemCapability.Ability.Form

**Parameters**

  | Name| Type   | Mandatory| Description                                  |
  | ------ | ------ | ---- | ------------------------------------- |
  | formId | string | Yes  | Form ID.                              |
  | minute | number | Yes  | Refresh interval, in minutes. The value must be greater than or equal to 5.    |

**Example**

  ```js
  var formId = "12400633174999288";
  formProvider.setFormNextRefreshTime(formId, 5).catch((error) => {
      console.log('formProvider setFormNextRefreshTime, error:' + JSON.stringify(error));
  });
  ```

## updateForm

updateForm(formId: string, formBindingData: FormBindingData, callback: AsyncCallback&lt;void&gt;): void;

Updates a form. This API uses an asynchronous callback to return the result.

**System capability**

SystemCapability.Ability.Form

**Parameters**

  | Name| Type                                                                   | Mandatory| Description            |
  | ------ | ---------------------------------------------------------------------- | ---- | ---------------- |
  | formId | string                                                                 | Yes  | ID of the form to update.|
  | formBindingData | [FormBindingData](js-apis-formbindingdata.md#formbindingdata) | Yes  | Data to be used for the update.   |
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```js
  import formBindingData from '@ohos.application.formBindingData';
  var formId = "12400633174999288";
  let obj = formBindingData.createFormBindingData({temperature:"22c", time:"22:00"});
  formProvider.updateForm(formId, obj, (error, data) => {
      if (error) {
          console.log('formProvider updateForm, error:' + error.code);
      }
  });
  ```

## updateForm

updateForm(formId: string, formBindingData: FormBindingData): Promise&lt;void&gt;;

Updates a form. This API uses a promise to return the result.

**System capability**

SystemCapability.Ability.Form

**Parameters**

  | Name| Type                                                                   | Mandatory| Description            |
  | ------ | ---------------------------------------------------------------------- | ---- | ---------------- |
  | formId | string                                                                 | Yes  | ID of the form to update.|
  | formBindingData | [FormBindingData](js-apis-formbindingdata.md#formbindingdata) | Yes  | Data to be used for the update.   |

**Example**

  ```js
  import formBindingData from '@ohos.application.formBindingData';
  var formId = "12400633174999288";
  let obj = formBindingData.createFormBindingData({temperature:"22c", time:"22:00"});
  formProvider.updateForm(formId, obj).catch((error) => {
      console.log('formProvider updateForm, error:' + JSON.stringify(error));
  });
  ```
