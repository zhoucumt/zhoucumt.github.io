---
title: 'vue-router学习笔记1:基本用法'
date: 2016-12-15 17:12:29
tags: vue-router
---

### 1.文档地址：
http://router.vuejs.org/en/essentials/getting-started.html

### 2.完整代码
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>webpack+vue-router-demo</title>
    <style type="text/css">
        .router-link-active {
            color: red;
        }
    </style>

    <script src="https://unpkg.com/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
</head>
<body>
    <div id="app">
        <h1>Hello App!</h1>
        <p>
            <!-- use router-link component for navigation. -->
            <!-- specify the link by passing the `to` prop. -->
            <!-- <router-link> will be rendered as an `<a>` tag by default -->
            <router-link to="/foo">Go to Foo</router-link>
            <router-link to="/bar">Go to Bar</router-link>
        </p>

        <!-- route outlet -->
        <!-- component matched by the route will render here -->
        <router-view></router-view>
    </div>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
    <script type="text/babel">
        /**
         * 0. If using a module system (e.g. via vue-cli), import Vue and VueRouter and 
         * then call Vue.use(VueRouter).

         * 1. Define route components.
         * These can be imported from other files
         */
        const Foo = { template: '<div>foo</div>' }
        const Bar = { template: '<div>bar</div>' }

        /** 2. Define some routes
         * Each route should map to a component. The "component" can
         * either be an actual component constructor created via
         * Vue.extend(), or just a component options object.
         * We'll talk about nested routes later.
         */
        const routes = [
          { path: '/foo', component: Foo },
          { path: '/bar', component: Bar }
        ]

        /** 3. Create the router instance and pass the `routes` option
        * You can pass in additional options here, but let's
        * keep it simple for now.
        */
        const router = new VueRouter({
          routes // short for routes: routes
        })

        /** 4. Create and mount the root instance.
         * Make sure to inject the router with the router option to make the
         * whole app router-aware.
         */
        const app = new Vue({
          router
        }).$mount('#app')

        // Now the app has started!
    </script>
</body>
</html>
```

### 3.注意：
<meta charset="utf-8">必不可少，不然浏览器会报错

### 4.步骤
1).创建跳转链接标签：

```
<router-link to="/bar">Go to Bar</router-link>
```
创建视图标签：

```
<router-view></router-view>
```

2).定义路由组件:

```
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }
```

3).定义路由路径：

```
const routes = [
    { path: '/foo', component: Foo },
    { path: '/bar', component: Bar }
]
```

4).创建路由实例：

```
const router = new VueRouter({
      routes // short for routes: routes
})
```

5). 创建vue实例：

```
const app = new Vue({
      router
}).$mount('#app')
```

