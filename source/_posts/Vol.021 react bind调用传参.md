---
title: 在nodejs下是用原生查询过滤无效
date: 2019-07-26 17:44:31
tags:
---
调用方式：
xxx.bind(this,{lalala:true})

函数:
xxx   =  (args,e)  = >  {
console.log(args)
e.stopPropagation();
...
}