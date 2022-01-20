---
title: vue监听
date: 2017-08-25 16:31:31
categories:
  - bugs
tags:
  - vue
---
// $watch 是一个实例方法
vm.$watch('a', function (newVal, oldVal) {
  // 这个回调将在 `vm.a`  改变后调用
})