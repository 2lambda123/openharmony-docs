# DataAbility 谓词

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import dataAbility from '@ohos.data.dataAbility'
```

## 系统能力
SystemCapability.DistributedDataManager.DataShare.Core



## dataAbility.createRdbPredicates


createRdbPredicates(name: string, dataAbilityPredicates: DataAbilityPredicates): rdb.RdbPredicates


从DataAabilityPredicates对象创建RdbPredicates对象。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | name | string | 是 | 数据库表中表名。 |
  | dataAbilityPredicates | [DataAbilityPredicates](#dataabilitypredicates) | 是 | dataAbility谓词。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | rdb.[RdbPredicates](js-apis-data-rdb.md#rdbpredicates) | 返回RdbPredicates对象。 |

- 示例：
  ```
  let dataAbilityPredicates = new dataAbility.DataAbilityPredicates()
  dataAbilityPredicates.equalTo("NAME", "Rose").between("AGE", 16, 30)
  let predicates = dataAbility.createRdbPredicates("EMPLOYEE", dataAbilityPredicates)
  ```


## DataAbilityPredicates

提供用于实现不同查询方法的谓词。


### equalTo


equalTo(field: string, value: ValueType): DataAbilityPredicates


配置谓词以匹配数据类型为ValueType且值等于指定值的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "lisi")
  ```


### notEqualTo


notEqualTo(field: string, value: ValueType): DataAbilityPredicates


配置谓词以匹配数据类型为ValueType且值不等于指定值的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.notEqualTo("NAME", "lisi")
  ```


### beginWrap


beginWrap(): DataAbilityPredicates


向谓词添加左括号。


- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回带有左括号的DataAbility谓词。 |

- 示例：
  ```
  let predicates = new dataAbilitylity.DataAbilityPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "lisi")
      .beginWrap()
      .equalTo("AGE", 18)
      .or()
      .equalTo("SALARY", 200.5)
      .endWrap()
  ```


### endWrap


endWrap(): DataAbilityPredicates


向谓词添加右括号。


- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回带有右括号的DataAbility谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "lisi")
      .beginWrap()
      .equalTo("AGE", 18)
      .or()
      .equalTo("SALARY", 200.5)
      .endWrap()
  ```


### or


or(): DataAbilityPredicates


将或条件添加到谓词中。


- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回带有或条件的DataAbility谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Lisa")
      .or()
      .equalTo("NAME", "Rose")
  ```


### and


and(): DataAbilityPredicates


向谓词添加和条件。


- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回带有和条件的DataAbility谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Lisa")
      .and()
      .equalTo("SALARY", 200.5)
  ```


### contains


contains(field: string, value: string): DataAbilityPredicates


配置谓词以匹配数据类型为String且value包含指定值的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.contains("NAME", "os")
  ```


### beginsWith


beginsWith(field: string, value: string): DataAbilityPredicates


配置谓词以匹配数据类型为String且值以指定字符串开头的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.beginsWith("NAME", "os")
  ```


### endsWith


endsWith(field: string, value: string): DataAbilityPredicates


配置谓词以匹配数据类型为String且值以指定字符串结尾的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.endsWith("NAME", "se")
  ```


### isNull


isNull(field: string): DataAbilityPredicates


配置谓词以匹配值为null的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.isNull("NAME")
  ```


### isNotNull


isNotNull(field: string): DataAbilityPredicates


配置谓词以匹配值不为null的指定字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.isNotNull("NAME")
  ```


### like


like(field: string, value: string): DataAbilityPredicates


配置谓词以匹配数据类型为string且值类似于指定字符串的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.like("NAME", "%os%")
  ```


### glob


glob(field: string, value: string): DataAbilityPredicates


配置谓词匹配数据类型为string的指定字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | string | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.glob("NAME", "?h*g")
  ```


### between


between(field: string, low: ValueType, high: ValueType): DataAbilityPredicates


将谓词配置为匹配数据类型为ValueType且value在指定范围内的指定字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | low | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示与谓词匹配的最小值。 |
  | high | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示与谓词匹配的最大值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.between("AGE", 10, 50)
  ```


### notBetween


notBetween(field: string, low: ValueType, high: ValueType): DataAbilityPredicates


配置谓词以匹配数据类型为ValueType且value超出给定范围的指定字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | low | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示与谓词匹配的最小值。 |
  | high | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示与谓词匹配的最大值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.notBetween("AGE", 10, 50)
  ```


### greaterThan


greaterThan(field: string, value: ValueType): DataAbilityPredicates


配置谓词以匹配数据类型为ValueType且值大于指定值的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.greaterThan("AGE", 18)
  ```


### lessThan


lessThan(field: string, value: ValueType): DataAbilityPredicates


配置谓词以匹配数据类型为valueType且value小于指定值的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.lessThan("AGE", 20)
  ```


### greaterThanOrEqualTo


greaterThanOrEqualTo(field: string, value: ValueType): DataAbilityPredicates


配置谓词以匹配数据类型为ValueType且value大于或等于指定值的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.greaterThanOrEqualTo("AGE", 18)
  ```


### lessThanOrEqualTo


lessThanOrEqualTo(field: string, value: ValueType): DataAbilityPredicates


配置谓词以匹配数据类型为ValueType且value小于或等于指定值的字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | [ValueType](js-apis-data-rdb.md#valuetype) | 是 | 指示要与谓词匹配的值。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.lessThanOrEqualTo("AGE", 20)
  ```


### orderByAsc


orderByAsc(field: string): DataAbilityPredicates


配置谓词以匹配其值按升序排序的列。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.orderByAsc("NAME")
  ```


### orderByDesc


orderByDesc(field: string): DataAbilityPredicates


配置谓词以匹配其值按降序排序的列。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.orderByDesc("AGE")
  ```


### distinct


distinct(): DataAbilityPredicates


配置谓词以过滤重复记录并仅保留其中一个。


- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回可用于过滤重复记录的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Rose").distinct("NAME")
  let resultSet = await rdbStore.query(predicates, ["NAME"])
  ```


### limitAs


limitAs(value: number): DataAbilityPredicates


设置最大数据记录数的谓词。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | value | number | 是 | 最大数据记录数。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回可用于设置最大数据记录数的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Rose").limitAs(3)
  ```


### offsetAs


offsetAs(rowOffset: number): DataAbilityPredicates


配置谓词以指定返回结果的起始位置。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | rowOffset | number | 是 | 返回结果的起始位置，取值为正整数。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回具有指定返回结果起始位置的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.equalTo("NAME", "Rose").offsetAs(3)
  ```


### groupBy


groupBy(fields: Array&lt;string&gt;): DataAbilityPredicates


配置谓词按指定列分组查询结果。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | fields | Array&lt;string&gt; | 是 | 指定分组依赖的列名。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回分组查询列的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.groupBy(["AGE", "NAME"])
  ```


### indexedBy


indexedBy(indexName: string): DataAbilityPredicates


配置谓词以指定索引列。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | indexName | string | 是 | 索引列的名称。 |

- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回具有指定索引列的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.indexedBy("SALARY_INDEX")
  ```


### in


in(field: string, value: Array&lt;ValueType&gt;): DataAbilityPredicates


配置谓词以匹配数据类型为ValueType数组且值在给定范围内的指定字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | Array&lt;[ValueType](js-apis-data-rdb.md#valuetype)&gt; | 是 | 以ValueType型数组形式指定的要匹配的值。 |


- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.in("AGE", [18, 20])
  ```


### notIn


notIn(field: string, value: Array&lt;ValueType&gt;): DataAbilityPredicates


配置谓词以匹配数据类型为ValueType数组且值不在给定范围内的指定字段。


- 参数：
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | field | string | 是 | 数据库表中的列名。 |
  | value | Array&lt;[ValueType](js-apis-data-rdb.md#valuetype)&gt; | 是 | 以ValueType型数组形式指定的要匹配的值。 |


- 返回值：
  | 类型 | 说明 |
  | -------- | -------- |
  | [DataAbilityPredicates](#dataabilitypredicates) | 返回与指定字段匹配的谓词。 |

- 示例：
  ```
  let predicates = new dataAbility.DataAbilityPredicates("EMPLOYEE")
  predicates.notIn("NAME", ["Lisa", "Rose"])
  ```

