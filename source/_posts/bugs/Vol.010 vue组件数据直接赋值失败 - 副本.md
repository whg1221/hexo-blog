---
title: vue组件数据直接赋值失败
date: 2017-11-08 19:25:31
categories:
  - bugs
tags:
  - vue
---
bug描述：vue cli中，先确定一个对象内部的数据结构，获取到真实数据后直接改变整个对象无效。但神奇的是debugger之后有效。

解决方案：先不确定对象内部的数据结构，在外面包一层对象，然后用extend方法进行赋值。