# 线性容器Deque

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import Deque from '@ohos.util.Deque'  
```

## 系统能力

SystemCapability.Utils.Lang

## Deque

### 属性

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| length | number | 是 | 否 | Deque的元素个数。 |

### constructor

constructor()

Deque的构造函数。

**示例：**

```
let deque = new Deque();
```

### insertFront

insertFront(element: T): void

在deque头部插入元素。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| element | T | 是 | 插入的元素。 |

**示例：**

```
let deque = new Deque;
deque.insertFront("a");
deque.insertFront(1);
let b = [1, 2, 3];
deque.insertFront(b);
let c = {name : "lala", age : "13"};
deque.insertFront(false);
```

### insertEnd

insertEnd(element: T): void

在deque尾部插入元素。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| element | T | 是 | 插入的元素。 |

**示例：**

```
let deque = new Deque;
deque.insertEnd("a");
deque.insertEnd(1);
let b = [1, 2, 3];
deque.insertEnd(b);
let c = {name : "lala", age : "13"};
deque.insertEnd(false);
```

### has

has(element: T): boolean

判断此Deque中是否含有该指定元素。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| element | T | 是 | 指定的元素。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果包含指定元素返回true，否则返回false。 |

**示例：**

```
let deque = new Deque();
deque.has("Ahfbrgrbgnutfodgorrogorg");
deque.insertFront("Ahfbrgrbgnutfodgorrogorg");
deque.has("Ahfbrgrbgnutfodgorrogorg");
```

### popFirst

popFirst(): T

删除并返回双端队列的首元素。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| T | 返回被删除的元素。 |

**示例：**

```
let deque = new Deque();
deque.insertFront(2);
deque.insertFront(4);
deque.insertEnd(5);
deque.insertFront(2);
deque.insertFront(4);
deque.popFirst();
```

### popLast

popLast(): T

删除并返回双端队列的尾元素。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| T | 返回被删除的元素。 |

**示例：**

```
let deque = new Deque();
deque.insertFront(2);
deque.insertEnd(4);
deque.insertFront(5);
deque.insertFront(2);
deque.insertFront(4);
deque.popLast();
```

### forEach
forEach(callbackfn: (value: T, index?: number, deque?: Deque&lt;T&gt;) => void,
thisArg?: Object): void

通过回调函数来遍历Deque实例对象上的元素以及元素对应的下标。

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
| deque | Deque&lt;T&gt; | 否 | 当前调用forEach方法的实例对象。 |

**示例：**

```
let deque = new Deque();
deque.insertFront(2);
deque.insertEnd(4);
deque.insertFront(5);
deque.insertEnd(4);
deque.forEach((value, index) => {
  console.log(value, index);
});
```

### getFirst

getFirst(): T;
获取Deque实例中的头元素。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| T | 返回T型 |

**示例：**

```
let deque = new Deque();
deque.insertEnd(2);
deque.insertEnd(4);
deque.insertFront(5);
deque.insertFront(4);
deque.getFirst();
```

### getLast

getLast(): T
获取Deque实例中的尾元素。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| T | 返回T型 |

**示例：**

```
let deque = new Deque();
deque.insertFront(2);
deque.insertFront(4);
deque.insertFront(5);
deque.insertFront(4);
deque.getLast();
```

### [Symbol.iterator]

[Symbol.iterator]\(): IterableIterator&lt;T&gt;


返回一个迭代器，迭代器的每一项都是一个 JavaScript 对象,并返回该对象。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| IterableIterator&lt;T&gt; | 返回一个迭代器。 |

**示例：**
```
let deque = new Deque();
deque.insertFront(2);
deque.insertFront(4);
deque.insertFront(5);
deque.insertFront(4);

// 使用方法一：
for (let item of deque) { 
  console.log(item); 
}

// 使用方法二：
let iter = deque[Symbol.iterator]();
let temp = iter.next().value;
while(temp != undefined) {
  console.log(temp);
  temp = iter.next().value;
}
```