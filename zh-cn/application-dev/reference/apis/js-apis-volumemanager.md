# 卷管理

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
>
> - 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> - 此接口为系统接口，三方应用不支持调用。

## 导入模块

```js
import volumemanager from "@ohos.volumeManager";
```

## volumemanager.getAllVolumes

getAllVolumes(): Promise&lt;Array&lt;Volume&gt;&gt;

异步获取当前所有可获得的卷信息，以promise方式返回。

**系统能力**：SystemCapability.FileManagement.StorageService.Volume

- 返回值

  | 类型                               | 说明                       |
  | ---------------------------------- | -------------------------- |
  | Promise&lt;[Volume](#volume)[]&gt; | 返回当前所有可获得的卷信息 |

- 示例

  ```js
  volumemanager.getAllVolumes().then(function(volumes){
      // do something
  });
  ```

## volumemanager.getAllVolumes

getAllVolumes(callback: AsyncCallback&lt;Array&lt;Volume&gt;&gt;): void

异步获取当前所有可获得的卷信息，以callback方式返回。

**系统能力**：SystemCapability.FileManagement.StorageService.Volume

- 参数

  | 参数名   | 类型                                              | 必填 | 说明                                 |
  | -------- | ------------------------------------------------- | ---- | ------------------------------------ |
  | callback | callback:AsyncCallback&lt;[Volume](#volume)[]&gt; | 是   | 获取当前所有可获得的卷信息之后的回调 |
  
- 示例

  ```js
  let uuid = "";
  volumemanager.getAllVolumes(uuid, function(error, volumes){
      // do something
  });
  ```


## volumemanager.mount<sup>9+</sup>

mount(volumeId: string): Promise&lt;boolean&gt;

异步挂载指定卷，以promise方式返回。

**系统能力**：SystemCapability.FileManagement.StorageService.Volume

- 参数

  | 参数名   | 类型   | 必填 | 说明 |
  | -------- | ------ | ---- | ---- |
  | volumeId | string | 是   | 卷id |

- 返回值

  | 类型                   | 说明       |
  | ---------------------- | ---------- |
  | Promise&lt;boolean&gt; | 挂载指定卷 |

- 示例

  ```js
  let volumeId = "";
  volumemanager.mount(volumeId).then(function(flag){
      // do something
  });
  ```

## volumemanager.mount<sup>9+</sup>

mount(volumeId: string, callback:AsyncCallback&lt;boolean&gt;):void

异步获取指定卷的可用空间大小，以callback方式返回。

**系统能力**：SystemCapability.FileManagement.StorageService.Volume

- 参数

  | 参数名   | 类型                                  | 必填 | 说明                 |
  | -------- | ------------------------------------- | ---- | -------------------- |
  | volumeId | string                                | 是   | 卷id                 |
  | callback | callback:AsyncCallback&lt;boolean&gt; | 是   | 挂载指定卷之后的回调 |

- 示例

  ```js
  let volumeId = "";
  volumemanager.mount(volumeId, function(error, flag){
      // do something
  });
  ```

## volumemanager.unmount<sup>9+</sup>

unmount(volumeId: string): Promise&lt;boolean&gt;

异步卸载指定卷，以promise方式返回。

**系统能力**：SystemCapability.FileManagement.StorageService.Volume

- 参数

  | 参数名   | 类型   | 必填 | 说明 |
  | -------- | ------ | ---- | ---- |
  | volumeId | string | 是   | 卷id |

- 返回值

  | 类型                   | 说明       |
  | ---------------------- | ---------- |
  | Promise&lt;boolean&gt; | 卸载指定卷 |

- 示例

  ```js
  let volumeId = "";
  volumemanager.unmount(volumeId).then(function(flag){
      // do something
  });
  ```

## volumemanager.unmount<sup>9+</sup>

unmount(volumeId: string, callback:AsyncCallback&lt;boolean&gt;):void

异步卸载指定卷，以callback方式返回。

**系统能力**：SystemCapability.FileManagement.StorageService.Volume

- 参数

  | 参数名   | 类型                                  | 必填 | 说明                 |
  | -------- | ------------------------------------- | ---- | -------------------- |
  | volumeId | string                                | 是   | 卷id                 |
  | callback | callback:AsyncCallback&lt;boolean&gt; | 是   | 卸载指定卷之后的回调 |

- 示例

  ```js
  let volumeId = "";
  volumemanager.unmount(volumeId, function(error, flag){
      // do something
  });
  ```

## Volume<sup>9+</sup>

**系统能力**：以下各项对应的系统能力均为SystemCapability.FileManagement.StorageService.Volume。

### 属性

| 名称        | 类型    | 说明                 |
| ----------- | ------- | -------------------- |
| id<sup>9+</sup>          | number  | 卷id                 |
| uuid<sup>9+</sup>        | string  | 卷uuid               |
| description<sup>9+</sup> | string  | 卷相关描述           |
| removeAble<sup>9+</sup>  | boolean | 是否为可移动存储设备 |
| state<sup>9+</sup>       | int     | 当前卷状态           |
| path<sup>9+</sup>        | string  | 卷的挂载地址         |