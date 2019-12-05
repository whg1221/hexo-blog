---
title: vue不能监听数组变化的解决办法
date: 2017-08-28 15:23:31
tags:
---
由于 JavaScript 的限制， Vue 不能检测以下变动的数组：
当你利用索引直接设置一个项时，例如： vm.items[indexOfItem] = newValue
当你修改数组的长度时，例如： vm.items.length = newLength
为了解决第一类问题，以下两种方式都可以实现和 vm.items[indexOfItem] = newValue 相同的效果， 同时也将触发状态更新：
// Vue.setVue.set(example1.items, indexOfItem, newValue)
// Array.prototype.spliceexample1.items.splice(indexOfItem, 1, newValue)
为了解决第二类问题，你可以使用 splice：
example1.items.splice(newLength)
