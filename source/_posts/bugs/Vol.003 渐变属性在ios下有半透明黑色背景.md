---
title: 渐变属性在ios下有半透明黑色背景
date: 2017-08-09 17:38:31
categories:
  - bugs
tags:
  - css
---
bug描述：使用background:linear-gradient(transparent, #fff)属性在chrome下正常从透明到白色渐变，在ios下渐变叠加半透明黑色背景。
解决方案：使用background-image: -webkit-linear-gradient(top, rgba(255,255,255,0.001) 0%, #fff 100%);