---
title: vue组件数据直接赋值失败
date: 2017-12-07 14:58:31
categories:
  - bugs
tags:
  - vue
  - ts
---
bug描述：TypeScript项目中跑webpack会出现变量未定义的报错情况。
原因：因为采用了2.7版本的TS，对于语法要求较高，public name: string;类似这种是不严格的写法，应当都改成public name!: string;
解决方案：在tsconfig.json文件中增加一行配置，"strictPropertyInitialization": false,把严格模式关掉。