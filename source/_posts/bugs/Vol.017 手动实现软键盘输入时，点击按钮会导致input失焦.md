---
title: 手动实现软键盘输入时，点击按钮会导致input失焦
date: 2018-08-20 11:26:31
categories:
  - bugs
tags:
  - js
---
非bug：手动实现软键盘输入时，点击按钮会导致input失焦
解决：按钮绑定mousedown事件，函数首行加入event.preventDefault();，可以阻止input的blur事件。