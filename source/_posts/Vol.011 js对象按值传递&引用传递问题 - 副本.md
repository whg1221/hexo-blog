---
title: vue组件数据直接赋值失败
date: 2017-12-07 14:58:31
tags:
---
 bug描述：
var startt = aaa,
ext = bbb;
ext = startt.setHours(0,0,0,0);
会导致startt变化！

就算设置var tempTime = startt; 然后修改tempTime，也会导致startt变化！！！

解决方案：只能定义var tempTime = aaa ;然后再改ext，才能避免修改的继承问题。。。

更好的解决方案：使用JSON.parse JSON.stringify深拷贝对象，可以避免对象的引用传递问题