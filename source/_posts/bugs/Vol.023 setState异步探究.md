---
title: setState异步探究
date: 2019-10-14 16:48:31
categories:
  - bugs
tags:
  - react
---
bug描述：react同级代码，两个setState会忽略前一个。就算写在回调函数里，state改变了，并没有触发render
解决：发生在一个同步函数前后的情况，要解决，得放在异步函数的前后