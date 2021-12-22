# 轻量级存储

轻量级存储为应用提供key-value键值型的文件数据处理能力，支持应用对数据进行轻量级存储及查询。数据存储形式为键值对，键的类型为字符串型，值的存储数据类型包括数字型、字符型、布尔型。


> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import dataStorage from '@ohos.data.storage'
```


## 权限

无


## 属性

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| MAX_KEY_LENGTH | string | 是 | 否 | key的最大长度限制，大小为80字节。 |
| MAX_VALUE_LENGTH | string | 是 | 否 | string类型value的最大长度限制，大小为8192字节。 |


## dataStorage.getStorageSync

getStorageSync(path: string): Storage

读取指定文件，将数据加载到Storage实例，用于数据操作，此方法为同步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [Storage](#storage) | 获取到要操作的Storage实例，用于进行数据存储操作。 |

- 示例：
  ```
  import dataStorage from '@ohos.data.storage'
  import featureAbility from '@ohos.ability.featureAbility'
  
  var context = featureAbility.getContext()
  var path = await context.getFilesDir()
  let storage = dataStorage.getStorageSync(path + '/mystore')
  storage.putSync('startup', 'auto')
  storage.flushSync()
  ```


## dataStorage.getStorage

getStorage(path: string, callback: AsyncCallback&lt;Storage&gt;): void

读取指定文件，将数据加载到Storage实例，用于数据操作，使用callback形式返回结果。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |
  | callback | AsyncCallback&lt;[Storage](#storage)&gt; | 是 | 回调函数。 |

- 示例：
  ```
  import dataStorage from '@ohos.data.storage'
  import featureAbility from '@ohos.ability.featureAbility'
  
  var context = featureAbility.getContext()
  var path = await context.getFilesDir()
  dataStorage.getStorage(path + '/mystore', function (err, storage) {
      if (err) {
          console.info("Get the storage failed, path: " + path + '/mystore')
          return;
      }
      storage.putSync('startup', 'auto')
      storage.flushSync()
  })
  ```


## dataStorage.getStorage

getStorage(path: string): Promise&lt;Storage&gt;

读取指定文件，将数据加载到Storage实例，用于数据操作，使用Promise方式作为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[Storage](#storage)&gt; | Promise实例，用于异步获取结果。 |

- 示例：
  ```
  import dataStorage from '@ohos.data.storage'
  import featureAbility from '@ohos.ability.featureAbility'
  
  var context = featureAbility.getContext()
  var path = await context.getFilesDir()
  let promise = dataStorage.getStorage(path + '/mystore')
  promise.then((storage) => {
      storage.putSync('startup', 'auto')
      storage.flushSync()
  }).catch((err) => {
      console.info("Get the storage failed, path: " + path + '/mystore')
  })
  ```


## dataStorage.deleteStorageSync

deleteStorageSync(path: string): void

从内存中移除指定文件对应的Storage单实例，并删除指定文件及其备份文件、损坏文件。删除指定文件时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题，此方法为同步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |

- 示例：
  ```
  dataStorage.deleteStorageSync(path + '/mystore')
  ```


## dataStorage.deleteStorage

deleteStorage(path: string, callback: AsyncCallback&lt;void&gt;)

从内存中移除指定文件对应的Storage单实例，并删除指定文件及其备份文件、损坏文件。删除指定文件时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题，使用callback方式作为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  dataStorage.deleteStorage(path + '/mystore', function (err) {
      if (err) {
          console.info("Deleted failed with err: " + err)
          return
      }
      console.info("Deleted successfully.")
  })
  ```


## dataStorage.deleteStorage

deleteStorage(path: string): Promise&lt;void&gt;

从内存中移除指定文件对应的Storage单实例，并删除指定文件及其备份文件、损坏文件。删除指定文件时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题，使用promise方式作为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步获取结果。 |

- 示例：
  ```
  let promise = dataStorage.deleteStorage(path + '/mystore')
  promise.then(() => {
      console.info("Deleted successfully.")
  }).catch((err) => {
      console.info("Deleted failed with err: " + err)
  })
  ```


## dataStorage.removeStorageFromCacheSync

removeStorageFromCacheSync(path: string): void

从内存中移除指定文件对应的Storage单实例。移除Storage单实例时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题。

此方法为同步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |

- 示例：
  ```
  dataStorage.removeStorageFromCacheSync(path + '/mystore')
  ```


## dataStorage.removeStorageFromCache

removeStorageFromCache(path: string, callback: AsyncCallback&lt;Storage&gt;): void

从内存中移除指定文件对应的Storage单实例。移除Storage单实例时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题。

此方法为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |
  | callback | AsyncCallback&lt;[Storage](#storage)&gt; | 是 | 回调函数。 |

- 示例：
  ```
  dataStorage.removeStorageFromCache(path + '/mystore', function (err) {
      if (err) {
          console.info("Removed storage from cache failed with err: " + err)
          return
      }
      console.info("Removed storage from cache successfully.")
  })
  ```


## dataStorage.removeStorageFromCache

removeStorageFromCache(path: string): Promise&lt;void&gt;

从内存中移除指定文件对应的Storage单实例。移除Storage单实例时，应用不允许再使用该实例进行数据操作，否则会出现数据一致性问题。

此方法为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | path | string | 是 | 应用程序内部数据存储路径。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步获取结果。 |

- 示例：
  ```
  let promise = dataStorage.removeStorageFromCache(path + '/mystore')
  promise.then(() => {
      console.info("Removed storage from cache successfully.")
  }).catch((err) => {
      console.info("Removed storage from cache failed with err: " + err)
  })
  ```


## Storage

提供获取和修改存储数据的接口。


### getSync

getSync(key: string, defValue: ValueType): ValueType

获取键对应的值，如果值为null或者非默认值类型，返回默认数据。

此方法为同步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称。它不能为空。 |
  | defValue | ValueType | 是 | 给定key的存储不存在，则要返回的默认值。支持number、string、boolean。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | ValueType | 键对应的值，如果值为null或者非默认值类型，返回默认数据。 |

- 示例：
  ```
  let value = storage.getSync('startup', 'default')
  console.info("The value of startup is " + value)
  ```


### get

get(key: string, defValue: ValueType, callback: AsyncCallback&lt;ValueType&gt;): void

获取键对应的值，如果值为null或者非默认值类型，返回默认数据。

此方法为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称。它不能为空。 |
  | defValue | ValueType | 是 | 默认返回值。支持number、string、boolean。 |
  | callback | AsyncCallback&lt;ValueType&gt; | 是 | 回调函数。 |

- 示例：
  ```
  storage.get('startup', 'default', function(err, value) {
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
  let promise = storage.get('startup', 'default')
  promise.then((value) => {
      console.info("The value of startup is " + value)
  }).catch((err) => {
      console.info("Get the value of startup failed with err: " + err)
  })
  ```


### putSync

putSync(key: string, value: ValueType): void

首先获取指定文件对应的Storage实例，然后借助Storage API将数据写入Storage实例，通过flush或者flushSync将Storage实例持久化。

此方法为同步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要修改的存储的key。它不能为空。 |
  | value | ValueType | 是 | 存储的新值。支持number、string、boolean。 |

- 示例：
  ```
  storage.putSync('startup', 'auto')
  ```


### put

put(key: string, value: ValueType, callback: AsyncCallback&lt;void&gt;): void

首先获取指定文件对应的Storage实例，然后借助Storage API将数据写入Storage实例，通过flush或者flushSync将Storage实例持久化。

此方法为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要修改的存储的key。它不能为空。 |
  | value | ValueType | 是 | 存储的新值。支持number、string、boolean。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  storage.put('startup', 'auto', function (err) {
      if (err) {
          console.info("Put the value of startup failed with err: " + err)
          return
      }
      console.info("Put the value of startup successfully.")
  })
  ```


### put

put(key: string, value: ValueType): Promise&lt;void&gt;

首先获取指定文件对应的Storage实例，然后借助Storage API将数据写入Storage实例，通过flush或者flushSync将Storage实例持久化。

此方法为异步方法。

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
  let promise = storage.put('startup', 'auto')
  promise.then(() => {
      console.info("Put the value of startup successfully.")
  }).catch((err) => {
      console.info("Put the value of startup failed with err: " + err)
  })
  ```


### hasSync

hasSync(key: string): boolean

检查存储对象是否包含名为给定key的存储。

此方法为同步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称。它不能为空。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | boolean | true&nbsp;表示存在，false表示不存在。 |

- 示例：
  ```
  let isExist = storage.hasSync('startup')
  if (isExist) {
      console.info("The key of startup is contained.")
  }
  ```


### has

has(key: string, callback: AsyncCallback&lt;boolean&gt;): boolean

检查存储对象是否包含名为给定key的存储。

此方法为异步方法。

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
  storage.has('startup', function (err, isExist) {
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
  let promise = storage.has('startup')
  promise.then((isExist) => {
      if (isExist) {
          console.info("The key of startup is contained.")
      }
  }).catch((err) => {
      console.info("Check the key of startup failed with err: " + err)
  })
  ```


### deleteSync

deleteSync(key: string): void

从存储对象中删除名为给定key的存储。

此方法为同步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称。它不能为空。 |

- 示例：
  ```
  storage.deleteSync('startup')
  ```


### delete

delete(key: string, callback: AsyncCallback&lt;void&gt;): void

从存储对象中删除名为给定key的存储。

此方法为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | key | string | 是 | 要获取的存储key名称，不能为空。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  storage.delete('startup', function (err) {
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
  let promise = storage.delete('startup')
  promise.then(() => {
      console.info("Deleted startup key successfully.")
  }).catch((err) => {
      console.info("Delete startup key failed with err: " + err)
  })
  ```


### flushSync

flushSync(): void

将当前storage对象中的修改保存到当前的storage，并同步存储到文件中。

此方法为同步方法。

- 示例：
  ```
  storage.flushSync()
  ```


### flush

flush(callback: AsyncCallback&lt;void&gt;): void

将当前storage对象中的修改保存到当前的storage，并异步存储到文件中。

此方法为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  storage.flush(function (err) {
      if (err) {
          console.info("Flush to file failed with err: " + err)
          return
      }
      console.info("Flushed to file successfully.")
  })
  ```


### flush

flush(): Promise&lt;void&gt;

将当前storage对象中的修改保存到当前的storage，并异步存储到文件中。

此方法为异步方法。

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步处理。 |

- 示例：
  ```
  let promise = storage.flush()
  promise.then(() => {
      console.info("Flushed to file successfully.")
  }).catch((err) => {
      console.info("Flush to file failed with err: " + err)
  })
  ```


### clearSync

clearSync(): void

清除此存储对象中的所有存储。

此方法为同步方法。

- 示例：
  ```
  storage.clearSync()
  ```


### clear

clear(callback: AsyncCallback&lt;void&gt;): void

清除此存储对象中的所有存储。

此方法为异步方法。

- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

- 示例：
  ```
  storage.clear(function (err) {
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

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise实例，用于异步处理。 |

- 示例：
  ```
  let promise = storage.clear()
  promise.then(() => {
      console.info("Cleared to file successfully.")
  }).catch((err) => {
      console.info("Clear to file failed with err: " + err)
  })
  ```


### on('change')

on(type: 'change', callback: Callback&lt;StorageObserver&gt;): void

订阅数据变更者类需要实现StorageObserver接口，订阅的key的值发生变更后，在执行flush/flushSync方法后，callback方法会被回调。

- 参数：
  | 参数名 | 类型 | 说明 |
  | -------- | -------- | -------- |
  | type | string | 事件类型，固定值'change'，表示数据变更。 |
  | callback | Callback&lt;[StorageObserver](#storageobserver)&gt; | 回调对象实例。 |

- 示例：
  ```
  var observer = function (key) {
      console.info("The key of " + key + " changed.")
  }
  storage.on('change', observer)
  storage.putSync('startup', 'auto')
  storage.flushSync()  // observer will be called.
  ```


### off('change')

off(type: 'change', callback: Callback&lt;StorageObserver&gt;): void

当不再进行订阅数据变更时，使用此接口取消订阅。

- 参数：
  | 参数名 | 类型 | 说明 |
  | -------- | -------- | -------- |
  | type | string | 事件类型，固定值'change'，表示数据变更。 |
  | callback | Callback&lt;[StorageObserver](#storageobserver)&gt; | 需要取消的回调对象实例。 |

- 示例：
  ```
  var observer = function (key) {
      console.info("The key of " + key + " changed.")
  }
  storage.off('change', observer)
  ```


## StorageObserver

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | string | 否 | 变更的数据内容。 |
