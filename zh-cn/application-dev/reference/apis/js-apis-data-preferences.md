# 轻量级存储

轻量级存储为应用提供key-value键值型的文件数据处理能力，支持应用对数据进行轻量级存储及查询。数据存储形式为键值对，键的类型为字符串型，值的存储数据类型包括数字型、字符型、布尔型。


> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import data_Preferences from '@ohos.data.preferences'
```

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.DistributedDataManager.Preferences.Core

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| MAX_KEY_LENGTH | string | 是 | 否 | key的最大长度限制，大小为80字节。 |
| MAX_VALUE_LENGTH | string | 是 | 否 | string类型value的最大长度限制，大小为8192字节。 |


## data_Preferences.getPreferences

getPreferences(context: Context, name: string, callback: AsyncCallback&lt;Preferences&gt;): void

读取指定文件，将数据加载到Preferences实例，用于数据操作，使用callback形式返回结果。


**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | context | Context | 是 | 应用程序或功能的上下文 |
  | name | string | 是 | 应用程序内部数据存储名称。 |
  | callback | AsyncCallback&lt;[Preferences](#preferences)&gt; | 是 | 回调函数。 |

- 示例：
  ```
  import Ability from '@ohos.application.Ability'
  import data_Preferences from '@ohos.data.preferences'
  var path = this.context.getDataBaseDir()
  data_Preferences.getPreferences(this.context, 'mystore', function (err, preferences) {
      if (err) {
          console.info("Get the preferences failed, path: " + path + '/mystore')
          return;
      }
      preferences.putSync('startup', 'auto')
      preferences.flushSync()
  })
  ```


## data_Preferences.getPreferences

getPreferences(context: Context, name: string): Promise&lt;Preferences&gt;

读取指定文件，将数据加载到Preferences实例，用于数据操作，使用Promise方式作为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | context | Context | 是 | 应用程序或功能的上下文 |
  | name | string | 是 | 应用程序内部数据存储名称。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[Preferences](#preferences)&gt; | Promise实例，用于异步获取结果。 |

- 示例：
  ```
  import Ability from '@ohos.application.Ability'
  import data_Preferences from '@ohos.data.preferences'
  var path = this.context.getDataBaseDir()
  let promisePre = data_Preferences.getPreferences(this.context, 'mystore')
  promisePre.then((preferences) => {
      preferences.putSync('startup', 'auto')
      preferences.flushSync()
  }).catch((err) => {
      console.info("Get the preferences failed, path: " + path + '/mystore')
  })
  ```


## data_Preferences.deletePreferences

deletePreferences(context: Context, name: string, callback: AsyncCallback&lt;void&gt;): void

从内存中移除指定文件对应的Preferences单实例，并删除指定文件及其备份文件、损坏文件。删除指定文件时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题，使用callback方式作为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | context | Context | 是 | 应用程序或功能的上下文 |
  | name | string | 是 | 应用程序内部数据存储名称。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  import Ability from '@ohos.application.Ability'
  import data_Preferences from '@ohos.data.preferences'
  data_Preferences.deletePreferences(this.context, 'mystore', function (err) {
      if (err) {
          console.info("Deleted failed with err: " + err)
          return
      }
      console.info("Deleted successfully.")
  })
  ```


## data_Preferences.deletePreferences

deletePreferences(context: Context, name: string): Promise&lt;void&gt;

从内存中移除指定文件对应的Preferences单实例，并删除指定文件及其备份文件、损坏文件。删除指定文件时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题，使用promise方式作为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | context | Context | 是 | 应用程序或功能的上下文 |
  | name | string | 是 | 应用程序内部数据存储名称。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步获取结果。 |

- 示例：
  ```
  import Ability from '@ohos.application.Ability'
  import data_Preferences from '@ohos.data.preferences'
  let promisedelPre = data_Preferences.deletePreferences(this.context, 'mystore')
  promisedelPre.then(() => {
      console.info("Deleted successfully.")
  }).catch((err) => {
      console.info("Deleted failed with err: " + err)
  })
  ```


## data_Preferences.removePreferencesFromCache

removePreferencesFromCache(context: Context, name: string, callback: AsyncCallback&lt;void&gt;): void

从内存中移除指定文件对应的Preferences单实例。移除Preferences单实例时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | context | Context | 是 | 应用程序或功能的上下文 |
  | name | string | 是 | 应用程序内部数据存储名称。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  import Ability from '@ohos.application.Ability'
  import data_Preferences from '@ohos.data.preferences'
  data_Preferences.removePreferencesFromCache(this.context, 'mystore', function (err) {
      if (err) {
          console.info("Removed preferences from cache failed with err: " + err)
          return
      }
      console.info("Removed preferences from cache successfully.")
  })
  ```


## data_Preferences.removePreferencesFromCache

removePreferencesFromCache(context: Context, name: string): Promise&lt;void&gt;

从内存中移除指定文件对应的Preferences单实例。移除Preferences单实例时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | context | Context | 是 | 应用程序或功能的上下文 |
  | name | string | 是 | 应用程序内部数据存储名称。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步获取结果。 |

- 示例：
  ```
  import Ability from '@ohos.application.Ability'
  import data_Preferences from '@ohos.data.preferences'
  let promiserevPre = data_Preferences.removePreferencesFromCache(this.context, 'mystore')
  promiserevPre.then(() => {
      console.info("Removed preferences from cache successfully.")
  }).catch((err) => {
      console.info("Removed preferences from cache failed with err: " + err)
  })
  ```


## Preferences

提供获取和修改存储数据的接口。


### get

get(key: string, defValue: ValueType, callback: AsyncCallback&lt;ValueType&gt;): void

获取键对应的值，如果值为null或者非默认值类型，返回默认数据。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称。它不能为空。 |
  | defValue | ValueType | 是 | 默认返回值。支持number、string、boolean。 |
  | callback | AsyncCallback&lt;ValueType&gt; | 是 | 回调函数。 |

- 示例：
  ```
  preferences.get('startup', 'default', function(err, value) {
      if (err) {
          console.info("Get the value of startup failed with err: " + err)
          return
      }
      console.info("The value of startup is " + value)
  })
  ```


### get

get(key: string, defValue: ValueType): Promise&lt;ValueType&gt;

获取键对应的值，如果值为null或者非默认值类型，返默认数据。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- **参数：**
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称。它不能为空。 |
  | defValue | ValueType | 是 | 默认返回值。支持number、string、boolean。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;ValueType&gt; | Promise实例，用于异步获取结果。 |

- 示例：
  ```
  let promiseget = preferences.get('startup', 'default')
  promiseget.then((value) => {
      console.info("The value of startup is " + value)
  }).catch((err) => {
      console.info("Get the value of startup failed with err: " + err)
  })
  ```


### put

put(key: string, value: ValueType, callback: AsyncCallback&lt;void&gt;): void

首先获取指定文件对应的Preferences实例，然后借助Preferences API将数据写入Preferences实例，通过flush或者flushSync将Preferences实例持久化。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要修改的存储的key。它不能为空。 |
  | value | ValueType | 是 | 存储的新值。支持number、string、boolean。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  preferences.put('startup', 'auto', function (err) {
      if (err) {
          console.info("Put the value of startup failed with err: " + err)
          return
      }
      console.info("Put the value of startup successfully.")
  })
  ```


### put

put(key: string, value: ValueType): Promise&lt;void&gt;

首先获取指定文件对应的Preferences实例，然后借助Preferences API将数据写入Preferences实例，通过flush或者flushSync将Preferences实例持久化。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要修改的存储的key。它不能为空。 |
  | value | ValueType | 是 | 存储的新值。支持number、string、boolean。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步处理。 |

- 示例：
  ```
  let promiseput = preferences.put('startup', 'auto')
  promiseput.then(() => {
      console.info("Put the value of startup successfully.")
  }).catch((err) => {
      console.info("Put the value of startup failed with err: " + err)
  })
  ```


### has

has(key: string, callback: AsyncCallback&lt;boolean&gt;): boolean

检查存储对象是否包含名为给定key的存储。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称，不能为空。 |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 回调函数。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | boolean | true表示存在，false表示不存在。 |

- 示例：
  ```
  preferences.has('startup', function (err, isExist) {
      if (err) {
          console.info("Check the key of startup failed with err: " + err)
          return
      }
      if (isExist) {
          console.info("The key of startup is contained.")
      }
  })
  ```


### has

has(key: string): Promise&lt;boolean&gt;

检查存储对象是否包含名为给定key的存储。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称。它不能为空。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise实例，用于异步处理。 |

- 示例：
  ```
  let promisehas = preferences.has('startup')
  promisehas.then((isExist) => {
      if (isExist) {
          console.info("The key of startup is contained.")
      }
  }).catch((err) => {
      console.info("Check the key of startup failed with err: " + err)
  })
  ```


### delete

delete(key: string, callback: AsyncCallback&lt;void&gt;): void

从存储对象中删除名为给定key的存储。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称，不能为空。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  preferences.delete('startup', function (err) {
      if (err) {
          console.info("Delete startup key failed with err: " + err)
          return
      }
      console.info("Deleted startup key successfully.")
  })
  ```


### delete

delete(key: string): Promise&lt;void&gt;

从存储对象删除名为给定key的存储。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步处理。 |

- 示例：
  ```
  let promisedel = preferences.delete('startup')
  promisedel.then(() => {
      console.info("Deleted startup key successfully.")
  }).catch((err) => {
      console.info("Delete startup key failed with err: " + err)
  })
  ```


### flush

flush(callback: AsyncCallback&lt;void&gt;): void

将当前preferences对象中的修改保存到当前的preferences，并异步存储到文件中。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  preferences.flush(function (err) {
      if (err) {
          console.info("Flush to file failed with err: " + err)
          return
      }
      console.info("Flushed to file successfully.")
  })
  ```


### flush

flush(): Promise&lt;void&gt;

将当前preferences对象中的修改保存到当前的preferences，并异步存储到文件中。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步处理。 |

- 示例：
  ```
  let promiseflush = preferences.flush()
  promiseflush.then(() => {
      console.info("Flushed to file successfully.")
  }).catch((err) => {
      console.info("Flush to file failed with err: " + err)
  })
  ```


### clear

clear(callback: AsyncCallback&lt;void&gt;): void

清除此存储对象中的所有存储。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  preferences.clear(function (err) {
      if (err) {
          console.info("Clear to file failed with err: " + err)
          return
      }
      console.info("Cleared to file successfully.")
  })
  ```


### clear

clear(): Promise&lt;void&gt;

清除此存储对象中的所有存储。

此方法为异步方法。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步处理。 |

- 示例：
  ```
  let promiseclear = preferences.clear()
  promiseclear.then(() => {
      console.info("Cleared to file successfully.")
  }).catch((err) => {
      console.info("Clear to file failed with err: " + err)
  })
  ```


### on('change')

on(type: 'change', callback: Callback&lt;{ key : string }&gt;): void

订阅数据变更者类，订阅的key的值发生变更后，在执行flush方法后，callback方法会被回调。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 说明 |
  | -------- | -------- | -------- |
  | type | string | 事件类型，固定值'change'，表示数据变更。 |
  | callback | Callback&lt;{ key : string }&gt; | 回调对象实例。 |

- 示例：
  ```
  var observer = function (key) {
      console.info("The key of " + key + " changed.")
  }
  preferences.on('change', observer)
  preferences.put('startup', 'auto')
  preferences.flush()  // observer will be called.
  ```


### off('change')

off(type: 'change', callback: Callback&lt;{ key : string }&gt;): void

当不再进行订阅数据变更时，使用此接口取消订阅。

**系统能力**：SystemCapability.DistributedDataManager.Preferences.Core

- 参数：
  | 参数名 | 类型 | 说明 |
  | -------- | -------- | -------- |
  | type | string | 事件类型，固定值'change'，表示数据变更。 |
  | callback | Callback&lt;{ key : string }&gt; | 需要取消的回调对象实例。 |

- 示例：
  ```
  var observer = function (key) {
      console.info("The key of " + key + " changed.")
  }
  preferences.off('change', observer)
  ```
