---
title: 'vue学习笔记:条件渲染'
date: 2016-12-07 01:56:02
tags: vue v-for 列表渲染
---

### 1.文档地址：
http://vuejs.org/v2/guide/list.html

### 2.对比：vue1中和vue2中循环数组时的序号：

```
// vue1:在 v-for 块内我们能完全访问父组件作用域内的属性，另有一个特殊变量 
// $index，正如你猜到的，它是当前数组元素的索引：
<ul id="example-2">
  <li v-for="item in items">
    {{ parentMessage }} - {{ $index }} - {{ item.message }}
  </li>
</ul>
```

```
// vue2: (item, index) in items。注意item在前，index在后，
// 和js和jq的eacha循环中函数中的参数的顺序相反
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

### 3.key属性：

```
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```

### 4.v-show vs v-if
前者类似于dispaly:none,并且不适用与template标签，也不能和v-else连用


