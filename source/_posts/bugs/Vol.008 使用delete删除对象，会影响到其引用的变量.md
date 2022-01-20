---
title: 使用delete删除对象，会影响到其引用的变量
date: 2017-10-16 17:22:31
categories:
  - bugs
tags:
  - js
---
bug描述：
var target = {
	eg:true
};

var temp = target;

delete temp.eg;

// temp === {};
// target === {};

解决方案：不用delete，建立空对象直接指定属性。