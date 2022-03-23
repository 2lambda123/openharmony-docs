# 关系型数据库

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。



## 导入模块

```
import data_rdb from '@ohos.data.rdb'
```


## data_rdb.getRdbStore

getRdbStore(context?: Context, config: StoreConfig, version: number, callback: AsyncCallback&lt;RdbStore&gt;): void

获得一个相关的RdbStore，操作关系型数据库，用户可以根据自己的需求配置RdbStore的参数，然后通过RdbStore调用相关接口可以执行相关的数据操作，结果以callback形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| context<sup>8+</sup> | Context | 否 | 应用程序或功能的上下文 |
| config | [StoreConfig](#storeconfig) | 是 | 与此RDB存储相关的数据库配置。 |
| version | number | 是 | 数据库版本。 |
| callback | AsyncCallback&lt;[RdbStore](#rdbstore)&gt; | 是 | 指定callback回调函数。返回一个RdbStore。 |

**示例**：

```
import data_rdb from '@ohos.data.rdb'
const STORE_CONFIG = { name: "RdbTest.db"}
const SQL_CREATE_TABLE = "CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER, SALARY REAL, CODES BLOB)"
data_rdb.getRdbStore(STORE_CONFIG, 1, function (err, rdbStore) {
    rdbStore.executeSql(SQL_CREATE_TABLE)
    console.info('create table done.')
})
```

API9的示例请参考如下代码：

```
import Ability from '@ohos.application.Ability'
import data_rdb from '@ohos.data.rdb'
export default class MainAbility extends Ability {
    const STORE_CONFIG = { name: "RdbTest.db"}
    const SQL_CREATE_TABLE = "CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER, SALARY REAL, CODES BLOB)"
    data_rdb.getRdbStore(this.context, STORE_CONFIG, 1, function (err, rdbStore) {
        rdbStore.executeSql(SQL_CREATE_TABLE)
        console.info('create table done.')
    })
}
```

## data_rdb.getRdbStore

getRdbStore(context?: Context, config: StoreConfig, version: number): Promise&lt;RdbStore&gt;

获得一个相关的RdbStore，操作关系型数据库，用户可以根据自己的需求配置RdbStore的参数，然后通过RdbStore调用相关接口可以执行相关的数据操作，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| context<sup>8+</sup> | Context | 否 | 应用程序或功能的上下文 |
| config | [StoreConfig](#storeconfig) | 是 | 与此RDB存储相关的数据库配置。 |
| version | number | 是 | 数据库版本。 |

**返回值**：

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[RdbStore](#rdbstore)&gt; | 指定Promise回调函数。返回一个RdbStore。 |

**示例**：

```
import data_rdb from '@ohos.data.rdb'
const STORE_CONFIG = { name: "RdbTest.db" }
const SQL_CREATE_TABLE = "CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER, SALARY REAL, CODES BLOB)"
let promisegetRdb = data_rdb.getRdbStore(STORE_CONFIG, 1);
promisegetRdb.then(async (rdbStore) => {
    let promiseExecSql = rdbStore.executeSql(SQL_CREATE_TABLE, null)
    promiseExecSql.then(() => {
        console.info('executeSql creat done.')
    }).catch((err) => {
        console.log("executeSql creat err.")
    })
}).catch((err) => {
    console.log("getRdbStore err.")
})
```

API9的示例请参考如下代码：

```
import Ability from '@ohos.application.Ability'
import data_rdb from '@ohos.data.rdb'
export default class MainAbility extends Ability {
    const STORE_CONFIG = { name: "RdbTest.db" }
    const SQL_CREATE_TABLE = "CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER, SALARY REAL, CODES BLOB)"
    let promisegetRdb = data_rdb.getRdbStore(this.context, STORE_CONFIG, 1);
    promisegetRdb.then(async (rdbStore) => {
        let promiseExecSql = rdbStore.executeSql(SQL_CREATE_TABLE, null)
        promiseExecSql.then(() => {
            console.info('executeSql creat done.')
        }).catch((err) => {
            console.log("executeSql creat err.")
        })
    }).catch((err) => {
        console.log("getRdbStore err.")
    })
}
```

## data_rdb.deleteRdbStore

deleteRdbStore(context?: Context, name: string, callback: AsyncCallback&lt;void&gt;): void

删除数据库，结果以callback形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | context<sup>8+</sup> | Context | 否 | 应用程序或功能的上下文 |
  | name | string | 是 | 数据库名称。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 指定callback回调函数。如果数据库已删除，则为true；否则返回false。 |

**示例**：
  ```
  import data_rdb from '@ohos.data.rdb'
  data_rdb.deleteRdbStore("RdbTest.db", function (err, rdbStore) {
      console.info('delete store done.')
  })
  ```

API9的示例请参考如下代码：

```
import Ability from '@ohos.application.Ability'
import data_rdb from '@ohos.data.rdb'
export default class MainAbility extends Ability {
    data_rdb.deleteRdbStore(this.context, "RdbTest.db", function (err, rdbStore) {
        console.info('delete store done.')
    })
}
```

## data_rdb.deleteRdbStore

deleteRdbStore(context?: Context, name: string): Promise&lt;void&gt;

使用指定的数据库文件配置删除数据库，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | context<sup>8+</sup> | Context | 否 | 应用程序或功能的上下文 |
  | name | string | 是 | 数据库名称。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 指定Promise回调函数。如果数据库已删除，则为true；否则返回false。 |

**示例**：
  ```
  import data_rdb from '@ohos.data.rdb'
  let promisedeleteRdb = data_rdb.deleteRdbStore("RdbTest.db")
  promisedeleteRdb.then(()=>{
      console.info('delete store done.')
  }).catch((err) => {
      console.log("deleteRdbStore err.")
  })
  ```

API9的示例请参考如下代码：

```
import Ability from '@ohos.application.Ability'
import data_rdb from '@ohos.data.rdb'
export default class MainAbility extends Ability {
    let promisedeleteRdb = data_rdb.deleteRdbStore(this.context, "RdbTest.db")
    promisedeleteRdb.then(()=>{
        console.info('delete store done.')
    }).catch((err) => {
        console.log("deleteRdbStore err.")
    })
}
```

## RdbPredicates

表示关系型数据库（RDB）的谓词。该类确定RDB中条件表达式的值是true还是false。


### constructor

constructor(name: string)


构造函数。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | name | string | 是 | 数据库表名。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  ```

### inDevices

inDevices(devices: Array&lt;string&gt;): RdbPredicates


同步分布式数据库时指定组网内的远程设备。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | devices | Array&lt;string&gt; | 是 | 指定的组网内的远程设备ID。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicate.inDevices(['12345678abcde'])
  ```

### inAllDevices<sup>8+</sup>

inAllDevices(): RdbPredicates


同步分布式数据库时连接到组网内的所有远程设备。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.inAllDevices()
  ```

### equalTo

equalTo(field: string, value: ValueType): RdbPredicates


配置谓词以匹配数据字段为ValueType且值等于指定值的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](#valuetype) | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "lisi")
  ```


### notEqualTo

notEqualTo(field: string, value: ValueType): RdbPredicates


配置谓词以匹配数据字段为ValueType且值不等于指定值的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](#valuetype) | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.notEqualTo("NAME", "lisi")
  ```


### beginWrap

beginWrap(): RdbPredicates


向谓词添加左括号。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回带有左括号的Rdb谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "lisi")
      .beginWrap()
      .equalTo("AGE", 18)
      .or()
      .equalTo("SALARY", 200.5)
      .endWrap()
  ```


### endWrap

endWrap(): RdbPredicates


向谓词添加右括号。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回带有右括号的Rdb谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "lisi")
      .beginWrap()
      .equalTo("AGE", 18)
      .or()
      .equalTo("SALARY", 200.5)
      .endWrap()
  ```


### or

or(): RdbPredicates


将或条件添加到谓词中。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回带有或条件的Rdb谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Lisa")
      .or()
      .equalTo("NAME", "Rose")
  ```


### and

and(): RdbPredicates


向谓词添加和条件。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回带有和条件的Rdb谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Lisa")
      .and()
      .equalTo("SALARY", 200.5)
  ```


### contains

contains(field: string, value: string): RdbPredicates

配置谓词以匹配数据字段为String且value包含指定值的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.contains("NAME", "os")
  ```


### beginsWith

beginsWith(field: string, value: string): RdbPredicates


配置谓词以匹配数据字段为String且值以指定字符串开头的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.beginsWith("NAME", "os")
  ```


### endsWith

endsWith(field: string, value: string): RdbPredicates


配置谓词以匹配数据字段为String且值以指定字符串结尾的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.endsWith("NAME", "se")
  ```


### isNull

isNull(field: string): RdbPredicates


配置谓词以匹配值为null的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

- 示例
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.isNull("NAME")
  ```


### isNotNull

isNotNull(field: string): RdbPredicates


配置谓词以匹配值不为null的指定字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.isNotNull("NAME")
  ```


### like

like(field: string, value: string): RdbPredicates


配置谓词以匹配数据字段为String且值类似于指定字符串的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.like("NAME", "%os%")
  ```


### glob

glob(field: string, value: string): RdbPredicates


配置RdbPredicates匹配数据字段为String的指定字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。<br>支持通配符，*表示0个、1个或多个数字或字符，?表示1个数字或字符。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.glob("NAME", "?h*g")
  ```


### between

between(field: string, low: ValueType, high: ValueType): RdbPredicates


将谓词配置为匹配数据字段为ValueType且value在给定范围内的指定字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | low | [ValueType](#valuetype) | 是 | 指示与谓词匹配的最小值。 |
  | high | [ValueType](#valuetype) | 是 | 指示要与谓词匹配的最大值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.between("AGE", 10, 50)
  ```


### notBetween

notBetween(field: string, low: ValueType, high: ValueType): RdbPredicates


配置RdbPredicates以匹配数据字段为ValueType且value超出给定范围的指定字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | low | [ValueType](#valuetype) | 是 | 指示与谓词匹配的最小值。 |
  | high | [ValueType](#valuetype) | 是 | 指示要与谓词匹配的最大值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.notBetween("AGE", 10, 50)
  ```


### greaterThan

greaterThan(field: string, value: ValueType): RdbPredicates

配置谓词以匹配数据字段为ValueType且值大于指定值的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](#valuetype) | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.greaterThan("AGE", 18)
  ```


### lessThan

lessThan(field: string, value: ValueType): RdbPredicates


配置谓词以匹配数据字段为valueType且value小于指定值的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](#valuetype) | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.lessThan("AGE", 20)
  ```


### greaterThanOrEqualTo


greaterThanOrEqualTo(field: string, value: ValueType): RdbPredicates


配置谓词以匹配数据字段为ValueType且value大于或等于指定值的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](#valuetype) | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.greaterThanOrEqualTo("AGE", 18)
  ```


### lessThanOrEqualTo


lessThanOrEqualTo(field: string, value: ValueType): RdbPredicates


配置谓词以匹配数据字段为ValueType且value小于或等于指定值的字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](#valuetype) | 是 | 指示要与谓词匹配的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.lessThanOrEqualTo("AGE", 20)
  ```


### orderByAsc


orderByAsc(field: string): RdbPredicates


配置谓词以匹配其值按升序排序的列。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.orderByAsc("NAME")
  ```


### orderByDesc


orderByDesc(field: string): RdbPredicates


配置谓词以匹配其值按降序排序的列。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.orderByDesc("AGE")
  ```


### distinct

distinct(): RdbPredicates


配置谓词以过滤重复记录并仅保留其中一个。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回可用于过滤重复记录的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Rose").distinct("NAME")
  let promisequery = rdbStore.query(predicates, ["NAME"])
  promisequery.then((resultSet) => {
      console.log("resultSet column names:" + resultSet.columnNames)
      console.log("resultSet column count:" + resultSet.columnCount)
  }).catch((err) => {
      console.log("query err.")
  })
  ```


### limitAs

limitAs(value: number): RdbPredicates


设置最大数据记录数的谓词。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | value | number | 是 | 最大数据记录数。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回可用于设置最大数据记录数的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Rose").limitAs(3)
  ```


### offsetAs

offsetAs(rowOffset: number): RdbPredicates


配置RdbPredicates以指定返回结果的起始位置。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | rowOffset | number | 是 | 返回结果的起始位置，取值为正整数。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回具有指定返回结果起始位置的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Rose").offsetAs(3)
  ```


### groupBy

groupBy(fields: Array&lt;string&gt;): RdbPredicates


配置RdbPredicates按指定列分组查询结果。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | fields | Array&lt;string&gt; | 是 | 指定分组依赖的列名。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回分组查询列的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.groupBy(["AGE", "NAME"])
  ```


### indexedBy

indexedBy(indexName: string): RdbPredicates

配置RdbPredicates以指定索引列。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | indexName | string | 是 | 索引列的名称。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回具有指定索引列的RdbPredicates。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.indexedBy("SALARY_INDEX")
  ```


### in

in(field: string, value: Array&lt;ValueType&gt;): RdbPredicates


配置RdbPredicates以匹配数据字段为ValueType数组且值在给定范围内的指定字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | Array&lt;[ValueType](#valuetype)&gt; | 是 | 以ValueType型数组形式指定的要匹配的值。 |


**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.in("AGE", [18, 20])
  ```


### notIn

notIn(field: string, value: Array&lt;ValueType&gt;): RdbPredicates


将RdbPredicates配置为匹配数据字段为ValueType且值超出给定范围的指定字段。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | Array&lt;[ValueType](#valuetype)&gt; | 是 | 以ValueType数组形式指定的要匹配的值。 |


**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.notIn("NAME", ["Lisa", "Rose"])
  ```


## RdbStore

提供管理关系数据库(RDB)方法的接口。


### insert

insert(name: string, values: ValuesBucket, callback: AsyncCallback&lt;number&gt;):void

向目标表中插入一行数据，结果以callback形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | name | string | 是 | 指定的目标表名。 |
  | values | [ValuesBucket](#valuesbucket) | 是 | 表示要插入到表中的数据行。 |
  | callback | AsyncCallback&lt;number&gt; | 是 | 指定callback回调函数。如果操作成功，返回行ID；否则返回-1。 |

**示例**：
  ```
  const valueBucket = {
      "NAME": "Lisa",
      "AGE": 18,
      "SALARY": 100.5,
      "CODES": new Uint8Array([1, 2, 3, 4, 5]),
  }
  rdbStore.insert("EMPLOYEE", valueBucket, function (err, ret) {
      console.log("insert first done: " + ret)
  })
  ```


### insert

insert(name: string, values: ValuesBucket):Promise&lt;number&gt;

向目标表中插入一行数据，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | name | string | 是 | 指定的目标表名。 |
  | values | [ValuesBucket](#valuesbucket) | 是 | 表示要插入到表中的数据行。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 指定Promise回调函数。如果操作成功，返回行ID；否则返回-1。 |

**示例**：
  ```
  const valueBucket = {
      "NAME": "Lisa",
      "AGE": 18,
      "SALARY": 100.5,
      "CODES": new Uint8Array([1, 2, 3, 4, 5]),
  }
  let promiseinsert = rdbStore.insert("EMPLOYEE", valueBucket)
  promiseinsert.then(async (ret) => {
      console.log("insert first done: " + ret)
  }).catch((err) => {
      console.log("insert err.")
  })
  ```


### update

update(values: ValuesBucket, rdbPredicates: RdbPredicates, callback: AsyncCallback&lt;number&gt;):void

根据RdbPredicates的指定实例对象更新数据库中的数据，结果以callback形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | values | [ValuesBucket](#valuesbucket) | 是 | value指示数据库中要更新的数据行。键值对与数据库表的列名相关联 |
  | rdbPredicates | [RdbPredicates](#rdbpredicates) | 是 | 表示要插入到表中的数据行。 |
  | callback | AsyncCallback&lt;number&gt; | 是 | 指定的callback回调方法。返回受影响的行数。 |

**示例**：
  ```
  const valueBucket = {
      "NAME": "Rose",
      "AGE": 22,
      "SALARY": 200.5,
      "CODES": new Uint8Array([1, 2, 3, 4, 5]),
  }
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Lisa")
  rdbStore.update(valueBucket, predicates, function (err, ret) {
      console.log("updated row count: " + changedRows)})
  ```


### update

update(values: ValuesBucket, rdbPredicates: RdbPredicates):Promise&lt;number&gt;

根据RdbPredicates的指定实例对象更新数据库中的数据，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | values | [ValuesBucket](#valuesbucket) | 是 | value指示数据库中要更新的数据行。键值对与数据库表的列名相关联 |
  | rdbPredicates | [RdbPredicates](#rdbpredicates) | 是 | 表示要插入到表中的数据行。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 指定的Promise回调方法。返回受影响的行数。 |

**示例**：
  ```
  const valueBucket = {
      "NAME": "Rose",
      "AGE": 22,
      "SALARY": 200.5,
      "CODES": new Uint8Array([1, 2, 3, 4, 5]),
  }
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Lisa")
  let promiseupdate = rdbStore.update(valueBucket, predicates)
  promiseupdate.then(async (ret) => {
       console.log("updated row count: " + changedRows)
  }).catch((err) => {
      console.log("update err.")
  })
  ```


### delete

delete(rdbPredicates: RdbPredicates, callback: AsyncCallback&lt;number&gt;):void


根据rdbPredicates的指定实例对象从数据库中删除数据，结果以callback形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | rdbPredicates | [RdbPredicates](#rdbpredicates) | 是 | RdbPredicates的实例对象指定的删除条件。 |
  | callback | AsyncCallback&lt;number&gt; | 是 | 指定callback回调函数。返回受影响的行数。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Lisa")
  rdbStore.delete(predicates, function (err, rows) {
      console.log("delete rows: " + rows)
  })
  ```


### delete

delete(rdbPredicates: RdbPredicates):Promise&lt;number&gt;

根据rdbPredicates的指定实例对象从数据库中删除数据，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | rdbPredicates | [RdbPredicates](#rdbpredicates) | 是 | RdbPredicates的实例对象指定的删除条件。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 指定Promise回调函数。返回受影响的行数。 |

**示例**：
  ```
  let predicatesdelete = new data_rdb.RdbPredicates("EMPLOYEE")
  predicatesdelete.equalTo("NAME", "Lisa")
  let promisedelete = rdbStore.delete(predicates)
  promisedelete.then((rows) => {
      console.log("delete rows: " + rows)
  }).catch((err) => {
      console.log("delete err.")
  })
  ```


### query

query(rdbPredicates: RdbPredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;ResultSet&gt;):void

根据指定条件查询数据库中的数据，结果以callback形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | rdbPredicates | [RdbPredicates](#rdbpredicates) | 是 | 表示rdbPredicates的实例对象指定的查询条件。 |
  | columns | Array&lt;string&gt; | 是 | 表示要查询的列。如果值为空，则查询应用于所有列。 |
  | callback | AsyncCallback&lt;[ResultSet](js-apis-data-resultset.md)&gt; | 是 | 指定callback回调函数。如果操作成功，则返回ResultSet对象。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Rose")
  rdbStore.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"], function (err, resultSet) {
      console.log("resultSet column names:" + resultSet.columnNames)
      console.log("resultSet column count:" + resultSet.columnCount)
  })
  ```


### query

query(rdbPredicates: RdbPredicates, columns?: Array&lt;string&gt;):Promise&lt;ResultSet&gt;

根据指定条件查询数据库中的数据，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | rdbPredicates | [RdbPredicates](#rdbpredicates) | 是 | 表示rdbPredicates的实例对象指定的查询条件。 |
  | columns | Array&lt;string&gt; | 否 | 表示要查询的列。如果值为空，则查询应用于所有列。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[ResultSet](../apis/js-apis-data-resultset.md)&gt; | 指定Promise回调函数。如果操作成功，则返回ResultSet对象。 |

**示例**：
  ```
  let predicates = new data_rdb.RdbPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Rose")
  let promisequery = rdbStore.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"])
  promisequery.then((resultSet) => {
      console.log("resultSet column names:" + resultSet.columnNames)
      console.log("resultSet column count:" + resultSet.columnCount)
  }).catch((err) => {
      console.log("query err.")
  })
  ```


### querySql<sup>8+</sup>

querySql(sql: string, bindArgs: Array&lt;ValueType&gt;, callback: AsyncCallback&lt;ResultSet&gt;):void

根据指定SQL语句查询数据库中的数据，结果以callback形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | sql | string | 是 | 指定要执行的SQL语句。 |
  | bindArgs | Array&lt;[ValueType](#valuetype)&gt; | 是 | SQL语句中参数的值。 |
  | callback | AsyncCallback&lt;[ResultSet](js-apis-data-resultset.md)&gt; | 是 | 指定callback回调函数。如果操作成功，则返回ResultSet对象。 |

**示例**：
  ```
  rdbStore.querySql("SELECT * FROM EMPLOYEE CROSS JOIN BOOK WHERE BOOK.NAME = ?", ['sanguo'], function (err, resultSet) {
      console.log("resultSet column names:" + resultSet.columnNames)
      console.log("resultSet column count:" + resultSet.columnCount)
  })
  ```


### querySql<sup>8+</sup>

querySql(sql: string, bindArgs?: Array&lt;ValueType&gt;):Promise&lt;ResultSet&gt;

根据指定SQL语句查询数据库中的数据，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | sql | string | 是 | 指定要执行的SQL语句。 |
  | bindArgs | Array&lt;[ValueType](#valuetype)&gt; | 否 | SQL语句中参数的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;[ResultSet](../apis/js-apis-data-resultset.md)&gt; | 指定Promise回调函数。如果操作成功，则返回ResultSet对象。 |

**示例**：
  ```
  let promisequerySql = rdbStore.querySql("SELECT * FROM EMPLOYEE CROSS JOIN BOOK WHERE BOOK.NAME = ?", ['sanguo'])
  promisequerySql.then((resultSet) => {
      console.log("resultSet column names:" + resultSet.columnNames)
      console.log("resultSet column count:" + resultSet.columnCount)
  }).catch((err) => {
      console.log("querySql err.")
  })
  ```


### executeSql

executeSql(sql: string, bindArgs: Array&lt;ValueType&gt;, callback: AsyncCallback&lt;void&gt;):void

执行包含指定参数但不返回值的SQL语句，结果以callbck形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | sql | string | 是 | 指定要执行的SQL语句。 |
  | bindArgs | Array&lt;[ValueType](#valuetype)&gt; | 是 | SQL语句中参数的值。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 指定callback回调函数。 |

**示例**：
  ```
  rdbStore.executeSql("DELETE FROM EMPLOYEE", null, function () {
      console.info('delete done.')
  })
  ```


### executeSql

executeSql(sql: string, bindArgs?: Array&lt;ValueType&gt;):Promise&lt;void&gt;

执行包含指定参数但不返回值的SQL语句，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | sql | string | 是 | 指定要执行的SQL语句。 |
  | bindArgs | Array&lt;[ValueType](#valuetype)&gt; | 否 | SQL语句中参数的值。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 指定Promise回调函数。 |

**示例**：
  ```
  let promiseexecuteSql = rdbStore.executeSql("DELETE FROM EMPLOYEE")
  promiseexecuteSql.then(() => {
      console.info('delete done.')
  }).catch((err) => {
      console.log("executeSql err.")
  })
  ```

### beginTransaction<sup>8+</sup>

beginTransaction():void

在开始执行SQL语句之前，开始事务。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**示例**：
```
  rdbStore.beginTransaction()
  const valueBucket = {
      "name": "lisi",
      "age": 18,
      "salary": 100.5,
      "blobType": new Uint8Array([1, 2, 3]),
  }
  rdbStore.insert("test", valueBucket, function (err, ret) {
      console.log("insert done: " + ret)
  })
  rdbStore.commit()
```


### commit<sup>8+</sup>

commit():void

提交已执行的SQL语句。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**示例**：
```
  rdbStore.beginTransaction()
  const valueBucket = {
      "name": "lisi",
      "age": 18,
      "salary": 100.5,
      "blobType": new Uint8Array([1, 2, 3]),
  }

  rdbStore.insert("test", valueBucket, function (err, ret) {
      console.log("insert done: " + ret)
  })
  rdbStore.commit()
```


### rollBack<sup>8+</sup>

rollBack():void;

回滚已经执行的SQL语句。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**示例**：
```
  try {
      rdbStore.beginTransaction()
      const valueBucket = {
          "id": 1,
          "name": "lisi",
          "age": 18,
          "salary": 100.5,
          "blobType": new Uint8Array([1, 2, 3]),
      }
      rdbStore.insert("test", valueBucket, function (err, ret) {
          console.log("insert done: " + ret)
      })
      rdbStore.commit()
  } catch (e) {
      rdbStore.rollBack()
  }
```


### setDistributedTables

setDistributedTables(tables: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void

设置分布式列表，结果以callbck形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | tables | Array&lt;string&gt; | 是 | 要设置的分布式列表表名 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 指定callback回调函数。 |

**示例**：
  ```
  rdbStore.setDistributedTables(["EMPLOYEE"], function (err) {
      if (err) {
          console.info('setDistributedTables failed.')
          return
      }
      console.info('setDistributedTables success.')
  })
  ```


### setDistributedTables

 setDistributedTables(tables: Array&lt;string&gt;): Promise&lt;void&gt;

设置分布式列表，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | tables | Array&lt;string&gt; | 是 | 要设置的分布式列表表名。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 指定Promise回调函数。 |

**示例**：
  ```
  let promiseset = rdbStore.setDistributedTables(["EMPLOYEE"])
  promiseset.then(() => {
      console.info("setDistributedTables success.")
  }).catch((err) => {
      console.info("setDistributedTables failed.")
  })
  ```

### obtainDistributedTableName

obtainDistributedTableName(device: string, table: string, callback: AsyncCallback&lt;string&gt;): void

根据本地表名获取指定远程设备的分布式表名。在查询远程设备数据库时，需要使用分布式表名, 结果以callbck形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | device | string | 是 | 远程设备 。|
  | table | string | 是 | 本地表名。 |
  | callback | AsyncCallback&lt;string&gt; | 是 | 指定的callback回调函数。如果操作成功，返回远程设备的分布式表名。 |

**示例**：
  ```
  rdbStore.obtainDistributedTableName(deviceId, "EMPLOYEE", function (err, tableName) {
      if (err) {
          console.info('obtainDistributedTableName failed.')
          return
      }
      console.info('obtainDistributedTableName success, tableName=.' + tableName)
   })
  ```


### obtainDistributedTableName

 obtainDistributedTableName(device: string, table: string): Promise&lt;string&gt;

根据本地表名获取指定远程设备的分布式表名。在查询远程设备数据库时，需要使用分布式表名，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | device | string | 是 | 远程设备。 |
  | table | string | 是 | 本地表名。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;string&gt; | 指定Promise回调函数。如果操作成功，返回远程设备的分布式表名。 |

**示例**：
  ```
  let promiseDistr = rdbStore.obtainDistributedTableName(deviceId, "EMPLOYEE")
  promiseDistr.then((tableName) => {
      console.info('obtainDistributedTableName success, tableName=' + tableName)
  }).catch((err) => {
      console.info('obtainDistributedTableName failed.')
  })
  ```

### sync<sup>8+</sup>

sync(mode: SyncMode, predicates: RdbPredicates, callback: AsyncCallback&lt;Array&lt;[string, number]&gt;&gt;): void

在设备之间同步数据, 结果以callbck形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | mode | SyncMode | 是 | 指同步模式。该值可以是推、拉。 |
  | predicates | RdbPredicates | 是 | 约束同步数据和设备。 |
  | callback | AsyncCallback&lt;Array&lt;[string, number]&gt;&gt; | 是 | 指定的callback回调函数，用于向调用者发送同步结果。string：设备ID；number：每个设备同步状态，0表示成功，其他值表示失败。|

**示例**：
  ```
  let predicate = new rdb.RdbPredicates('EMPLOYEE')
  predicate.inDevices(['12345678abcde'])
  rdbStore.sync(rdb.SyncMode.SYNC_MODE_PUSH, predicate, function (err, result) {
      if (err) {
          console.log('sync failed')
          return
       }
      console.log('sync done.')
      for (let i = 0; i < result.length; i++) {
          console.log('device=' + result[i][0] + ' status=' + result[i][1])
       }
  })
  ```


### sync<sup>8+</sup>

 sync(mode: SyncMode, predicates: RdbPredicates): Promise&lt;Array&lt;[string, number]&gt;&gt;

在设备之间同步数据，结果以Promise形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | mode | SyncMode | 是 | 指同步模式。该值可以是推、拉。 |
  | predicates | RdbPredicates | 是 | 约束同步数据和设备。 |

**返回值**：
  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;Array&lt;[string, number]&gt;&gt; | 指定Promise回调函数，用于向调用者发送同步结果。string：设备ID；number：每个设备同步状态，0表示成功，其他值表示失败。 |

**示例**：
  ```
  let predicatesync = new data_rdb.RdbPredicates('EMPLOYEE')
  predicatesync.inDevices(['12345678abcde'])
  let promisesync = rdbStore.sync(data_rdb.SyncMode.SYNC_MODE_PUSH, predicatesync)
  promisesync.then((result) =>{
      console.log('sync done.')
      for (let i = 0; i < result.length; i++) {
          console.log('device=' + result[i][0] + ' status=' + result[i][1])
      }
  }).catch((err) => {
      console.log('sync failed')
  })
  ```

### on

on(event: 'dataChange', type: SubscribeType, observer: Callback&lt;Array&lt;string&gt;&gt;): void

注册数据库的观察者。当分布式数据库中的数据发生更改时，将调用回调。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | SubscribeType | 是 | 指在{@code SubscribeType}中定义的订阅类型。 |
  | observer | Callback&lt;Array&lt;string&gt;&gt; | 是 | 指分布式数据库中数据更改事件的观察者。 |

**示例**：
  ```
  function storeObserver(devices) {
      for (let i = 0; i < devices.length; i++) {
          console.log('device=' + device[i] + ' data changed')
      }
  }
  try {
      rdbStore.on('dataChange', data_rdb.SubscribeType.SUBSCRIBE_TYPE_REMOTE, storeObserver)
  } catch (err) {
      console.log('register observer failed')
  }
  ```

### off

off(event:'dataChange', type: SubscribeType, observer: Callback&lt;Array&lt;string&gt;&gt;): void

从数据库中删除指定类型的指定观察者, 结果以callbck形式返回。

**系统能力**：SystemCapability.DistributedDataManager.RelationalStore.Core。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | SubscribeType | 是 | 指在{@code SubscribeType}中定义的订阅类型。 |
  | observer | Callback&lt;Array&lt;string&gt;&gt; | 是 | 指已注册的数据更改观察者。|

**示例**：
  ```
  function storeObserver(devices) {
      for (let i = 0; i < devices.length; i++) {
          console.log('device=' + device[i] + ' data changed')
      }
  }
  try {
      rdbStore.off('dataChange', data_rdb.SubscribeType.SUBSCRIBE_TYPE_REMOTE, storeObserver)
  } catch (err) {
      console.log('unregister observer failed')
  }
  ```


## StoreConfig

管理关系数据库配置。

**系统能力**：以下各项对应的系统能力均为SystemCapability.DistributedDataManager.RelationalStore.Core。

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| name | string | 是 | 数据库文件名。 |


## ValueType

用于表示允许的数据字段类型。

**系统能力**：以下各项对应的系统能力均为SystemCapability.DistributedDataManager.RelationalStore.Core。

| 名称 | 说明 |
| -------- | -------- |
| number | 表示值类型为数字。 |
| string | 表示值类型为字符。 |
| boolean | 表示值类型为布尔值。|


## ValuesBucket

用于存储键值对。

**系统能力**：以下各项对应的系统能力均为SystemCapability.DistributedDataManager.RelationalStore.Core。

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| [key:&nbsp;string] | [ValueType](#valuetype)\|&nbsp;Uint8Array&nbsp;\|&nbsp;null | 是 | 用于存储键值对。 |


## SyncMode<sup>8+</sup>

指数据库同步模式。

**系统能力**：以下各项对应的系统能力均为SystemCapability.DistributedDataManager.RelationalStore.Core。

| 名称       | 默认值 | 说明 |
| --------  | ----- |----- |
| SYNC_MODE_PUSH | 0 | 表示数据从本地设备推送到远程设备。 |
| SYNC_MODE_PULL | 1 | 表示数据从远程设备拉至本地设备。 |

## SubscribeType<sup>8+</sup>

描述订阅类型。

**系统能力**：以下各项对应的系统能力均为SystemCapability.DistributedDataManager.RelationalStore.Core。

| 名称      | 默认值 | 说明 |
| -------- | ----- |---- |
| SUBSCRIBE_TYPE_REMOTE | 0 | 订阅远程数据更改。 |
