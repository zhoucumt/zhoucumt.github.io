---
title: 'ES6学习笔记(一):let和const'
date: 2016-09-21 20:08:51
tags:
---
### 一、let
1.所声明的变量，只在let命令所在的代码块内有效。
2.for循环的计数器，就很合适使用let命令。

``` javascript

    var a = [];
	for (let i = 0; i < 10; i++) {
  		a[i] = function () {
    		console.log(i);
  		};
	}
	a[6](); // 6
	
```