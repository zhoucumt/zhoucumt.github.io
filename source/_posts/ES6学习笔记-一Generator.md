---
title: 'ES6学习笔记(八): Generator'
date: 2016-11-21 23:37:54
tags:
---


### 1.Generator函数是ES6提供的一种异步编程解决方案，语法行为与传统函数完全不同。从语法上，首先可以把它理解成，Generator函数是一个状态机，封装了多个内部状态。

### 2.执行Generator函数会返回一个遍历器对象，也就是说，Generator函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历Generator函数内部的每一个状态。

### 3.形式上，Generator函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield语句，定义不同的内部状态（yield语句在英语里的意思就是“产出”）。
```
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```
调用Generator函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象

### 4.yield语句就是暂停标志。yield语句不能用在普通函数中，否则会报错。

### 5.yield语句用作函数参数或赋值表达式的右边，可以不加括号。
```
foo(yield 'a', yield 'b'); // OK
let input = yield; // OK
```

### 5.由于Generator函数就是遍历器生成函数，因此可以把Generator赋值给对象的Symbol.iterator属性，从而使得该对象具有Iterator接口。
```
var myIterable = {};
myIterable[Symbol.iterator] = function* () {
  yield 1;
  yield 2;
  yield 3;
};

[...myIterable] // [1, 2, 3]
```

### 6.Generator函数执行后，返回一个遍历器对象。该对象本身也具有Symbol.iterator属性，执行后返回自身。
```
function* gen(){
  // some code
}

var g = gen();

g[Symbol.iterator]() === g
// true
```

### 7.for...of循环可以自动遍历Generator函数时生成的Iterator对象，且此时不再需要调用next方法。
```
function *foo() {
  yield 1;
  yield 2;
  yield 3;
  yield 4;
  yield 5;
  return 6;
}

for (let v of foo()) {
  console.log(v);
}
// 1 2 3 4 5
```
上面代码使用for...of循环，依次显示5个yield语句的值。这里需要注意，一旦next方法的返回对象的done属性为true，for...of循环就会中止，且不包含该返回对象，所以上面代码的return语句返回的6，不包括在for...of循环之中。