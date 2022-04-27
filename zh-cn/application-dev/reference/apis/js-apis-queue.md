# 线性容器Queue

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import Queue from '@ohos.util.Queue'  
```

## 系统能力

SystemCapability.Utils.Lang


## Queue


### 属性

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| length | number | 是 | 否 | Queue的元素个数。 |


### constructor

constructor()

Queue的构造函数。

**示例：**

```ts
let queue = new Queue();
```


### add

add(element: T): boolean

在队列尾部插入元素。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| element | T | 是 | 添加进去的元素。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 插入成功返回true，否则返回false。 |

**示例：**

```ts
let queue = new Queue();
let result = queue.add("a");
let result1 = queue.add(1);
queue.add(1);
let b = [1, 2, 3];
queue.add(b);
let c = {name : "lala", age : "13"};
let result3 = queue.add(c);
```

### pop

pop(): T

删除头元素并返回该删除元素。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| T | 返回删除的元素。 |

**示例：**

```ts
let queue = new Queue();
queue.add(2);
queue.add(4);
queue.add(5);
queue.add(2);
queue.add(4);
let result = queue.pop();
```

### getFirst

getFirst(): T

获取队列的头元素。

**参数：**

| 类型 | 说明 |
| -------- | -------- |
| T | 返回获取的元素。 |

**示例：**

```ts
let queue = new Queue();
queue.add(2);
queue.add(4);
queue.add(5);
queue.add(2);
let result = queue.getFirst();
```

### forEach

forEach(callbackfn: (value: T, index?: number, Queue?: Queue&lt;T&gt;) => void,
thisArg?: Object): void

通过回调函数来遍历Queue实例对象上的元素以及元素对应的下标。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| callbackfn | function | 是 | 回调函数。 |
| thisArg | Object | 否 | callbackfn被调用时用作this值。 |

callbackfn的参数说明：

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | T | 是 | 当前遍历到的元素。 |
| index | number | 否 | 当前遍历到的下标值。 |
| Queue | Queue&lt;T&gt; | 否 | 当前调用forEach方法的实例对象。 |

**示例：**

```ts
let queue = new Queue();
queue.add(2);
queue.add(4);
queue.add(5);
queue.add(4);
queue.forEach((value, index) => {
  console.log(value, index);
});

```

### [Symbol.iterator]

[Symbol.iterator]\(): IterableIterator&lt;T&gt;


返回一个迭代器，迭代器的每一项都是一个 JavaScript 对象,并返回该对象。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| IterableIterator&lt;T&gt; | 返回一个迭代器。 |

**示例：**
```ts
let queue = new Queue();
queue.add(2);
queue.add(4);
queue.add(5);
queue.add(4);

// 使用方法一：
for (let item of queue) { 
  console.log(item); 
}

// 使用方法二：
let iter = queue[Symbol.iterator]();
let temp = iter.next().value;
while(temp != undefined) {
  console.log(temp);
  temp = iter.next().value;
}
```