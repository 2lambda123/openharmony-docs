# 屏幕截图

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```
import screenshot from '@ohos.screenshot';
```

## ScreenshotOptions

设置截取图像的信息。

| 参数名     | 类型          | 必填 | 说明                                                         |
| ---------- | ------------- | ---- | ------------------------------------------------------------ |
| screenRect | [Rect](#Rect) | 否   | 表示截取图像的区域，不传值默认为全屏。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |
| imageSize  | [Size](#Size) | 否   | 表示截取图像的大小，不传值默认为全屏。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |
| rotation   | number        | 否   | 表示截取图像的旋转角度，取值可为0、90、180、270，默认值为0。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |


## Rect

表示截取图像的区域。

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| left   | number | 是   | 表示截取图像区域的左边界。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |
| top    | number | 是   | 表示截取图像区域的上边界。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |
| width  | number | 是   | 表示截取图像区域的宽度。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |
| height | number | 是   | 表示截取图像区域的高度。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |


## Size

表示截取图像的大小。

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| width  | number | 是   | 表示截取图像的宽度。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |
| height | number | 是   | 表示截取图像的高度。<br/>**系统能力**：SystemCapability.WindowManager.WindowManager.Core |

## screenshot.save

save(options?: ScreenshotOptions, callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取屏幕截图。

**系统能力**：SystemCapability.WindowManager.WindowManager.Core

**需要权限**：ohos.permission.CAPTURE_SCREEN

- 参数

  | 参数名   | 类型                                    | 必填 | 说明                                                         |
  | -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
  | options  | [ScreenshotOptions](#ScreenshotOptions) | 否   | 该类型的参数包含screenRect，imageSize，rotation三个参数，需要分别设置这三个参数。 |
  | callback | AsyncCallback&lt;image.PixelMap&gt;     | 是   | 回调返回一个PixelMap对象。                                   |

- 示例

  ```
  var ScreenshotOptions = {
  	"screenRect": {
  		"left": 200,
  		"top": 100,
  		"width": 200,
  		"height": 200},
  	"imageSize": {
  		"width": 300,
  		"height": 300},
  	"rotation": 0
  };
  screenshot.save(ScreenshotOptions, (err, data) => {
  	if (err) {
  		console.error('Failed to save the screenshot. Error: ' + JSON.stringify(err));
  		return;
  	}
  	console.info('Screenshot saved. Data: ' + JSON.stringify(data));
  });
  ```

## screenshot.save

save(options?: ScreenshotOptions): Promise&lt;image.PixelMap&gt;

获取屏幕截图。

**系统能力**：SystemCapability.WindowManager.WindowManager.Core

**需要权限**：ohos.permission.CAPTURE_SCREEN

- 参数

  | 参数名  | 类型                                    | 必填 | 说明                                                         |
  | ------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
  | options | [ScreenshotOptions](#ScreenshotOptions) | 否   | 该类型的参数包含screenRect，imageSize，rotation三个参数，需要分别设置这三个参数。 |

- 返回值

  | 类型                          | 说明                                            |
  | ----------------------------- | ----------------------------------------------- |
  | Promise&lt;image.PixelMap&gt; | 以Promise形式返回结果，返回image.PixelMap对象。 |

- 示例

  ```
  var ScreenshotOptions = {
  	"screenRect": {
  		"left": 200,
  		"top": 100,
  		"width": 200,
  		"height": 200},
  	"imageSize": {
  		"width": 300,
  		"height": 300},
  	"rotation": 0
  };
  let promise = screenshot.save(ScreenshotOptions);
  promise.then(() => {
      console.log('screenshot save success');
  }).catch((err) => {
      console.log('screenshot save fail: ' + JSON.stringify(err));
  });
  ```
