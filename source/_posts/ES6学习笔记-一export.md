---
title: 'ES6学习笔记(十一):export'
date: 2016-11-28 19:06:26
tags: export 模块化
---


### 1.ES6模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS和AMD模块，都只能在运行时确定这些东西。比如，CommonJS模块就是对象，输入时必须查找对象属性。

### 2.ES6模块不是对象，而是通过export命令显式指定输出的代码，输入时也采用静态命令的形式。
```
// ES6模块
import { stat, exists, readFile } from 'fs';
```
上面代码的实质是从fs模块加载3个方法，其他方法不加载。这种加载称为“编译时加载”，即ES6可以在编译时就完成模块加载，效率要比CommonJS模块的加载方式高。当然，这也导致了没法引用ES6模块本身，因为它不是对象。

### 3.浏览器使用ES6模块的语法如下。
```
<script type="module" src="foo.js"></script>
```

### 4.模块的两种等价写法：
```
// profile.js
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;
```

```
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};
```

### 5.通常情况下，export输出的变量就是本来的名字，但是可以使用as关键字重命名。
```
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```

### 6.注意，import命令具有提升效果，会提升到整个模块的头部，首先执行。下面的代码不会报错，因为import的执行早于foo的调用。
```
foo();

import { foo } from 'my_module';
```

### 7.如果在一个模块之中，先输入后输出同一个模块，import语句可以与export语句写在一起。
```
export { es6 as default } from './someModule';

// 等同于
import { es6 } from './someModule';
export default es6;
```

### 8.为了给用户提供方便，让他们不用阅读文档就能加载模块，就要用到export default命令，为模块指定默认输出。
```
// export-default.js
export default function () {
  console.log('foo');
}
```
其他模块加载该模块时，import命令可以为该匿名函数指定任意名字。

```
// import-default.js
import customName from './export-default';
customName(); // 'foo'
```
需要注意的是，这时import命令后面，不使用大括号。

### 9.下面代码的两组写法，第一组是使用export default时，对应的import语句不需要使用大括号；第二组是不使用export default时，对应的import语句需要使用大括号。
```
// 输出
export default function crc32() {
  // ...
}
// 输入
import crc32 from 'crc32';

// 输出
export function crc32() {
  // ...
};
// 输入
import {crc32} from 'crc32';
```

### 10. 正是因为export default命令其实只是输出一个叫做default的变量，所以它后面不能跟变量声明语句。
```
// 正确
export var a = 1;

// 正确
var a = 1;
export default a;

// 错误
export default var a = 1;
```

### 11.模块之间也可以继承。假设有一个circleplus模块，继承了circle模块。
```
// circleplus.js

export * from 'circle';
export var e = 2.71828182846;
export default function(x) {
  return Math.exp(x);
}
```
上面代码中的export *，表示再输出circle模块的所有属性和方法。注意，export *命令会忽略circle模块的default方法。然后，上面代码又输出了自定义的e变量和默认方法。
