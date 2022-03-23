# 非线性容器HashMap 

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import HashMap from '@ohos.util.HashMap'  
```

## 系统能力

SystemCapability.Utils.Lang

## HashMap


### 属性

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| length | number | 是 | 否 | HashMap的元素个数。 |


### constructor

constructor()

HashMap的构造函数。

**示例：**

```
let hashMap = new HashMap();
```


### isEmpty

isEmpty(): boolean

判断该HashMap是否为空。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 为空返回true，不为空返回false。 |

**示例：**

```
const hashMap = new HashMap();
let result = hashMap.isEmpty();
```


### hasKey

hasKey(key: K): boolean

判断此HashMap中是否含有该指定key。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 指定Key。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 包含指定Key返回true，否则返回false。 |

**示例：**

```
let hashMap = new HashMap();
let result = hashMap.hasKey("Ahfbrgrbgnutfodgorrogorgrogofdfdf");
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
let result1 = hashMap.hasKey("Ahfbrgrbgnutfodgorrogorgrogofdfdf");
```


### hasValue

hasValue(value: V): boolean

判断此HashMap中是否含有该指定value。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | V | 是 | 指定value。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 包含指定value返回true，否则返回false。 |

**示例：**

```
let hashMap = new HashMap();
let result = hashMap.hasValue(123);
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
let result1 = hashMap.hasValue(123);
```


### get

get(key: K): V

获取指定key所对应的value。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 查找的指定key。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| V | 返回key映射的value值。 |

**示例：**

```
let hashMap = new HashMap();
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
hashMap.set("sdfs", 356);
let result = hashMap.get("sdfs");
```


### setAll

setAll(map: HashMap<K, V>): void

将一个HashMap中的所有元素组添加到另一个hashMap中。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| map | HashMap<K, V> | 是 | 被添加元素的hashMap。 |

**示例：**

```
let hashMap = new HashMap();
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
hashMap.set("sdfs", 356);
let newHashMap = new HashMap();
hashMap.setAll(newHashMap);
```


### set

set(key: K, value: V): Object

向HashMap中添加一组数据。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 添加成员数据的键名。 |
| value | V | 是 | 添加成员数据的值。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Object | 返回添加后的hashMap。 |

**示例：**

```
let hashMap = new HashMap();
let result = hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
```


### remove

remove(key: K): V

删除指定key所对应元素。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 指定key。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| V | 返回删除元素的值。 |

**示例：**

```
let hashMap = new HashMap();
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
hashMap.set("sdfs", 356);
let result = hashMap.remove("sdfs");
```


### clear

clear(): void

清除HashMap中的所有元素,并把length置为0。

**示例：**

```
let hashMap = new HashMap();
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
hashMap.set("sdfs", 356);
hashMap.clear();
```


### keys

keys(): IterableIterator&lt;K&gt;

返回包含此映射中包含的键名的新迭代器对象。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| IterableIterator&lt;K&gt; | 返回一个迭代器。 |

**示例：**

```
let hashMap = new HashMap();
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
hashMap.set("sdfs", 356);
let iter = hashMap.keys();
let temp = iter.next().value;
while(temp != undefined) {
  console.log(temp);
  temp = iter.next().value;
}
```


### values

values(): IterableIterator&lt;V&gt;

返回包含此映射中包含的键值的新迭代器对象。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| IterableIterator&lt;V&gt; | 返回一个迭代器。 |

**示例：**

```
let hashMap = new HashMap();
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
hashMap.set("sdfs", 356);
let iter = hashMap.values();
let temp = iter.next().value;
while(temp != undefined) {
  console.log(temp);
  temp = iter.next().value;
}
```


### replace

replace(key: K, newValue: V): boolean

对HashMap中一组数据进行更新（替换）。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 依据key指定替换的元素。 |
| newValue | V | 是 | 替换成员数据的值。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 是否成功对已有数据进行替换 |

**示例：**

```
let hashMap = new HashMap();
hashMap.set("sdfs", 123);
let result = hashMap.replace("sdfs", 357);
```


### forEach

forEach(callbackfn: (value?: V, key?: K, map?: HashMap<K, V>) => void, thisArg?: Object): void

通过回调函数来遍历HashMap实例对象上的元素以及元素对应的下标。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callbackfn | function | 是 | 回调函数。 |
| thisArg | Object | 否 | callbackfn被调用时用作this值。 |

callbackfn的参数说明：
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | V | 否 | 当前遍历到的元素键值对的值。 |
| key | K | 否 | 当前遍历到的元素键值对的键。 |
| map | HashMap<K, V> | 否 | 当前调用forEach方法的实例对象。 |

**示例：**

```
let hashMap = new HashMap();
hashMap.set("sdfs", 123);
hashMap.set("dfsghsf", 357);
hashMap.forEach((value, key) => {
  console.log(value, key);
});
```


### entries

entries(): IterableIterator&lt;[K, V]&gt;

返回包含此映射中包含的键值对的新迭代器对象。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| IterableIterator&lt;[K, V]&gt; | 返回一个迭代器。 |

**示例：**

```
let hashMap = new HashMap();
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
hashMap.set("sdfs", 356);
let iter = hashMap.entries();
let temp = iter.next().value;
while(temp != undefined) {
  console.log(temp[0]);
  console.log(temp[1]);
  temp = iter.next().value;
}
```


### [Symbol.iterator]

[Symbol.iterator]\(): IterableIterator&lt;[K, V]&gt;

返回一个迭代器，迭代器的每一项都是一个 JavaScript 对象,并返回该对象。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| IterableIterator&lt;[K, V]&gt; | 返回一个迭代器。 |

**示例：**
```
let hashMap = new HashMap();
hashMap.set("Ahfbrgrbgnutfodgorrogorgrogofdfdf", 123);
hashMap.set("sdfs", 356);

// 使用方法一：
for (let item of hashMap) { 
  console.log("key: " + item[0]);
  console.log("value: " + item[1]);
}

// 使用方法二：
let iter = hashMap[Symbol.iterator]();
let temp = iter.next().value;
while(temp != undefined) {
  console.log(temp[0]);
  console.log(temp[1]);
  temp = iter.next().value;
}
```