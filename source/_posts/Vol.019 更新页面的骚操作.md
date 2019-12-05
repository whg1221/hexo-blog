---
title: 在nodejs下是用原生查询过滤无效
date: 2019-10-10 17:21:31
tags:
---
bug描述：在nodejs下使用.find({}, { _id: 0 })过滤无效
解决：nodejs的mongoDB插件使用的不是原生的查询语句，应该使用.find({}, { projection: { _id: 0 } })