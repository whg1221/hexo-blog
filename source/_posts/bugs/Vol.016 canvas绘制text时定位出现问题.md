---
title: canvas绘制text时定位出现问题
date: 2018-08-07 17:00:31
categories:
  - bugs
tags:
  - canvas
---
bug：canvas绘制text时定位出现问题
bug描述：绘制文字的Y轴定位总是不对，改成0,0之后发现文字消失，说明x,y的定位并不基于左上角坐标而是基于左下角坐标，坑爹！
bug解决：Y轴定位加上了fontSize值做了修正