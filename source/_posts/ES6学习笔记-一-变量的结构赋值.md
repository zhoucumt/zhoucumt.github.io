---
title: 'ES6学习笔记(二):变量的解构赋值'
date: 2016-09-25 00:05:36
tags:
---
### 注意点
1.等号右边可以多余等号左边。

2.等号右边也可以少于等号左边。

3.等号右边的值一定要具有Iterator接口，比如数组

4.关于默认值，需要注意什么时候默认值不起作用

5.如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值。

6.对象也可以解构赋值

``` javascript

    var { foo, bar } = { foo: "aaa", bar: "bbb" };
    foo // "aaa"
    bar // "bbb"
    
```

7.注意括号的使用

``` javascript

    // 错误的写法
    var x;
    {x} = {x: 1};
    // SyntaxError: syntax error
    
    // 正确的写法
    ({x} = {x: 1});
````

8.字符串的解构赋值

``` javascript

    const [a, b, c, d, e] = 'hello';
	a // "h"
	b // "e"
	c // "l"
	d // "l"
	e // "o"
	
```

9.由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。

``` javascript

    let { prop: x } = undefined; // TypeError
	let { prop: y } = null; // TypeError
	
```

10.变量声明语句中，不能带有圆括号。

11.函数参数中，模式不能带有圆括号。

12.赋值语句中，不能将整个模式，或嵌套模式中的一层，放在圆括号之中。

    