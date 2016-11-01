---
title: 'ES6学习笔记(五):Set数据结构'
date: 2016-11-01 00:57:51
tags:
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