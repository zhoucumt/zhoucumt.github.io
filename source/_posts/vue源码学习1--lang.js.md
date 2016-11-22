---
title: 'vue源码学习1--lang.js'
date: 2016-11-22 23:44:27
tags: vue 源码
---
### 说明：本笔记仅作为自己学习vue源码时的笔记，一边学习，一边记录疑惑，很可能许多疑惑就是很低级的疑惑，还请赐教。
### vue源码中src/util/lang.js中提供了许多工具方法。总结起来大概有对象操作、数组操作、类型转换、方法绑定、名称转换以及其他等方法 

#### 1.对象操作
##### 1.1 set
```
export function set (obj, key, val) {
  if (hasOwn(obj, key)) {
    obj[key] = val
    return
  }
  if (obj._isVue) {
    set(obj._data, key, val)
    return
  }
  var ob = obj.__ob__
  if (!ob) {
    obj[key] = val
    return
  }
  ob.convert(key, val)
  ob.dep.notify()
  if (ob.vms) {
    var i = ob.vms.length
    while (i--) {
      var vm = ob.vms[i]
      vm._proxy(key)
      vm._digest()
    }
  }
  return val
}
```
*疑惑：* ob.convert(key, val)和ob.dep.notify()这些方法是哪里定义的


