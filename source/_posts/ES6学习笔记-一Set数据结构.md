---
title: 'ES6学习笔记(五):Set数据结构'
date: 2016-11-01 00:57:51
tags:set
---


#### 1.ES6提供了新的数据结构Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

#### 2.Set本身是一个构造函数，用来生成Set数据结构。
```javascript
var s = new Set();

[2, 3, 5, 4, 5, 2, 2].map(x => s.add(x));

for (let i of s) {
  console.log(i);
}
// 2 3 5 4
```

#### 3.Set函数可以接受一个数组（或类似数组的对象）作为参数，用来初始化。
```javascript
// 例一
var set = new Set([1, 2, 3, 4, 4]);
[...set]
// [1, 2, 3, 4]

// 例二
var items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size // 5

// 例三
function divs () {
  return [...document.querySelectorAll('div')];
}

var set = new Set(divs());
set.size // 56

// 类似于
divs().forEach(div => set.add(div));
set.size // 56
```

#### 4.利用Set实现最简单的数组去重方法
```javascript
// 去除数组的重复成员
[...new Set(array)]
```

##### 5.在Set内部，两个NaN是相等。
```javascript
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b);
set // Set {NaN}
```

##### 6.两个对象总是不相等的
``` javascript
let set = new Set();

set.add({});
set.size // 1

set.add({});
set.size // 2
```

#### 7.Array.from方法可以将Set结构转为数组
```javascript
var items = new Set([1, 2, 3, 4, 5]);
var array = Array.from(items);
```

#### 8.另外一种比较简单的数组去重方法
``` javascript
function dedupe(array) {
  return Array.from(new Set(array));
}

dedupe([1, 1, 2, 3]) // [1, 2, 3]
```

#### 9.Set结构的实例有四个遍历方法，可以用于遍历成员。
- keys()：返回键名的遍历器
- values()：返回键值的遍历器
- entries()：返回键值对的遍历器
- 使用回调函数遍历每个成员

#### 10.WeakSet:
- WeakSet的成员只能是对象，而不能是其他类型的值。
- WeakSet中的对象都是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于WeakSet之中。这个特点意味着，无法引用WeakSet的成员，因此WeakSet是不可遍历的。

```javascript
var ws = new WeakSet();
ws.add(1)
// TypeError: Invalid value used in weak set
ws.add(Symbol())
// TypeError: invalid value used in weak set

var a = [[1,2], [3,4]];
var ws = new WeakSet(a);
// WeakSet {[1, 2], [3, 4]}

var b = [3, 4];
var ws = new WeakSet(b);
// Uncaught TypeError: Invalid value used in weak set(…)
```

#### 11.WeakSet没有size属性，没有办法遍历它的成员。

#### 12.WeakSet的一个用处，是储存DOM节点，而不用担心这些节点从文档移除时，会引发内存泄漏。