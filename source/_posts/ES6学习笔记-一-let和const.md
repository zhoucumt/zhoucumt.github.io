---
title: 'ES6学习笔记(一):let和const'
date: 2016-09-21 20:08:51
tags:
---
### 一、let

1.所声明的变量，只在let命令所在的代码块内有效。

2.for循环的计数器，就很合适使用let命令。


```javascript

    var a = [];
    for (let i = 0; i < 10; i++) {
        a[i] = function () {
            console.log(i);
        };
    }
    a[6](); // 6
    
```


3.不存在变量提升。暂时性死区:TDZ(temporal dead zone)

4.不存在变量提升：只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

5.只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

6.let不允许在相同作用域内，重复声明同一个变量。（注意是相同作用域）。

7.ES6引入了块级作用域，明确允许在块级作用域之中声明函数


```javascript
    
    // 报错
    function () {
      let a = 10;
      var a = 1;
    }

    // 报错
    function () {
      let a = 10;
      let a = 1;
    }
```



### 二、const
1.同样地，只在块级作用域有效，不可提升，存在暂时性死区，只能声明之后再使用，也不可重复声明。

2.冻结对象：Object.freeze

``` javascript

    const foo = Object.freeze({});

    // 常规模式时，下面一行不起作用；
    // 严格模式时，该行会报错
    foo.prop = 123;
```


