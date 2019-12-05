---
title: 无法显示svg
date: 2018-03-20 16:39:31
tags:
---
bug描述：引用带svg引用的css文件时，webpack起dev后会显示不出引用的svg图标，使用了svg-loader和svg-inline-loader都无效
解决方案：安装并配置使用svg-url-loader，配置如下
    {
      test: /\.svg/,
      use: {
        loader: 'svg-url-loader',
        options: {}
      }
    }