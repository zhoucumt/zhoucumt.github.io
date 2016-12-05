---
title: 'vue学习笔记:条件渲染'
date: 2016-12-06 00:23:20
tags: vue v-else 条件渲染
---

### 1.文档地址：
http://vuejs.org/v2/guide/conditional.html

### 2.新增语法:
v-else-if:

```
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
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


