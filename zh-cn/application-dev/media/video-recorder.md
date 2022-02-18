# 视频录制开发指导

## 场景介绍

视频录制的主要工作是捕获音视频信号，完成音视频编码并保存到文件中，帮助开发者轻松实现音视频录制功能。它允许调用者指定录制的编码格式、封装格式、文件路径等参数。

图1 视频录制状态机

![zh-ch_image_video_recorder_state_machine](figures/zh-ch_image_video_recorder_state_machine.png)

## 视频录制零层图

**图2** 视频录制零层图

![zh-ch_image_video_recorder_zero](figures/zh-ch_image_video_recorder_zero.png)

## 视频录制开发步骤

详细API含义可参考：[js-apis-media.md](../reference/apis/js-apis-media.md)

### 全流程场景

包含流程：创建实例，设置录制参数，录制视频，暂停录制，恢复录制，停止录制，释放资源等流程。

```js
let videoProfile = {
    audioBitrate : 48000,
    audioChannels : 2,
    audioCodec : 'audio/mp4a-latm',
    audioSampleRate : 48000,
    fileFormat : 'mp4',
    videoBitrate : 48000,
    videoCodec : 'video/mp4v-es',
    videoFrameWidth : 640,
    videoFrameHeight : 480,
    videoFrameRate : 30
}

let videoConfig = {
    audioSourceType : 1,
    videoSourceType : 0,
    profile : videoProfile,
    url : 'file:///data/media/01.mp4',
    orientationHint : 0,
    location : { latitude : 30, longitude : 130 },
}
	
// 当发生错误上上报的错误回调接口
function failureCallback(error) {
    console.info('error happened, error name is ' + error.name);
    console.info('error happened, error code is ' + error.code);
    console.info('error happened, error message is ' + error.message);
}
	
// 当发生异常时，系统调用的错误回调接口
function catchCallback(error) {
    console.info('catch error happened, error name is ' + error.name);
    console.info('catch error happened, error code is ' + error.code);
    console.info('catch error happened, error message is ' + error.message);
}
	
let videoRecorder = null; // videoRecorder空对象在createVideoRecorder成功后赋值
let surfaceID = null; // 用于保存getInputSurface返回的surfaceID
// 创建videoRecorder对象
await media.createVideoRecorder().then((recorder) => {
    console.info('case createVideoRecorder called');
    if (typeof (recorder) != 'undefined') {
        videoRecorder = recorder;
        console.info('createVideoRecorder success');
    } else {
        console.info('createVideoRecorder failed');
    }
}, failureCallback).catch(catchCallback);

// 获取surfaceID并保存下来传递给camera相关接口
await videoRecorder.getInputSurface().then((surface) => {
    console.info('getInputSurface success');
    surfaceID = surface;
}, failureCallback).catch(catchCallback);
	
// 视频录制依赖相机相关接口，以下需要先调用相机起流接口后才能继续执行

// 视频录制启动接口
await videoRecorder.start().then(() => {
    console.info('start success');
}, failureCallback).catch(catchCallback);

// 调用pause接口时需要暂停camera出流
await videoRecorder.pause().then(() => {
    console.info('pause success');
}, failureCallback).catch(catchCallback);

// 调用resume接口时需要恢复camera出流
await videoRecorder.resume().then(() => {
    console.info('resume success');
}, failureCallback).catch(catchCallback);

// 停止camera出流后，停止视频录制
await videoRecorder.stop().then(() => {
    console.info('stop success');
}, failureCallback).catch(catchCallback);

// 重置录制相关配置
await videoRecorder.reset().then(() => {
    console.info('reset success');
}, failureCallback).catch(catchCallback);

// 释放视频录制相关资源并释放camera对象相关资源
await videoRecorder.release().then(() => {
    console.info('release success');
}, failureCallback).catch(catchCallback);

// 相关对象置null
videoRecorder = null;
surfaceID = null;
```

