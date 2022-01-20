---
title: v-show v-if 性能差异初体验
date: 2017-08-09 13:27:31
categories:
  - bugs
tags:
  - vue
---
bug描述：config-data数据过大时，data配置页面加载速度及编辑操作会非常卡顿，需做优化。
出现原因：使用v-show方式渲染导致大量display:none的dom。
解决方案：将vue的show渲染方式改为if，按需渲染，不占用大量dom资源。