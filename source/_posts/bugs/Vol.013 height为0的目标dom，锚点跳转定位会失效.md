---
title: height为0的目标dom，锚点跳转定位会失效
date: 2018-03-20 13:18:31
categories:
  - bugs
tags:
  - css
---
bug描述：height为0的目标dom，锚点跳转定位会失效
解决方案：写了1px的高度，再加上visibility:hidden是这个元素相对于浏览器存在