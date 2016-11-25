---
title: 'js的多个三元操作符的用法'
date: 2016-11-25 16:06:43
tags:
---


### 关于js的三元操作符，我们常用的用法很简单，就行这样：
```
var value1 = 'a';
var value2 = 'b';
var name = value1
    ? 'value1 exist'
    : 'value1 not exist';

name // 'value1 exist'
```
还是简单解释一下：这种写法主要是为了避免if...else这种多行的写法。上述例子的三元操作符其实可以写一行就可以了，这里主要是为了说明多个三元操作符写在一起时，在视觉上便于理解，所以写成多行。

### 然而，今天看vue源码的时候，看到了关于三元操作符的这样一段代码：
```
strats.activate = function (parentVal, childVal) {
  return childVal
    ? parentVal
      ? parentVal.concat(childVal)
      : isArray(childVal)
        ? childVal
        : [childVal]
    : parentVal
}
```
说实话，最开始看到这样几个操作符写在一起，看着有点晕，以前没怎么注意这种用法。于是，试着捋了一下这种用法。下面举例说明。

```
// value1存在时，继续对value2进行判断,也就是说类似于&&的操作
var name = value1
    ? value2
        ? 'value2 exist'
        : 'value2 not exist'
    : 'value1 not exist';
name //因此，此时，显示'value2 exist'
```

```
// 如果此时将value2的值修改为false，那么，由于value1仍然为true，所以依然会对value2进行判断，但是此时value2为false，所以显示'value2 not exist'
var value2 = false;
var name = value1
    ? value2
        ? 'value2 exist'
        : 'value2 not exist'
    : 'value1 not exist';
name //'value2 not exist'
```

```
// 如果把value1的值修改为false，那么就不会再对value2进行判断了，直接显示'value1 not exist'
// 就好像退出了一个条件分支，进入else里面了
var value1 = false;
var name = value1
    ? value2
        ? 'value2 exist'
        : 'value2 not exist'
    : 'value1 not exist';
name //'value1 not exist'
```