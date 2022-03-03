---
title: Gulp构建前端开发一体化
date: 2016-03-31 18:00:00
categories:
  - dig-in
tags:
  - gulp
---
# 一、gulp安装

## 介绍：

gulp是基于任务的设计模式的自动化工具，通过插件的配合解决全套前端解决方案。

## 功能：

静态页面压缩、图片压缩、JS合并、SASS同步编译并压缩CSS、服务器控制客户端同步刷新等。

## 安装步骤：

1. 安装Node.js和npm

   https://nodejs.org/en/

   http://xiaoyaojones.blog.163.com/blog/static/28370125201351501113581/

2. 安装gulp

   ```shell
   $ npm install -g gulp
   ```

3. 安装gulp组件

   ```shell
   $ npm install ${gulp-component-name} –save-dev
   ```

# 二、gulp组件

## 官方组件库：

[http://gulpjs.com/plugins/](http://gulpjs.com/plugins/)

## 避免使用黑名单组件：

[https://github.com/gulpjs/plugins/blob/master/src/blackList.json](https://github.com/gulpjs/plugins/blob/master/src/blackList.json)

## 常用组件：

```js
imagemin = require('gulp-imagemin'), // 图片压缩
sass = require('gulp-ruby-sass'), // sass
minifycss = require('gulp-minify-css'), // css压缩
jshint = require('gulp-jshint'), // js检查
stylish = require('jshint-stylish'), // jshint报告
uglify = require('gulp-uglify'), // js压缩
rename = require('gulp-rename'), // 重命名
concat = require('gulp-concat'), // 合并文件
clean = require('gulp-clean'), // 清空文件夹
htmlmin = require('gulp-htmlmin'), // html压缩
replace = require('gulp-replace'), // 替换变量
px2rem = require('gulp-px2rem'), // 像素转rem
useref = require('gulp-useref'), // 引用的多个css和js合并
rev = require('gulp-rev-append'), // 引用资源增加时间戳
livereload = require('gulp-livereload'); // 服务器控制客户端同步刷新（需配合chrome插件LiveReload及tiny-lr）
```

# 三、gulp语法

src、dest、task、run、watch...

```js
var gulp = require('gulp')
		uglify = require('gulp-uglify');

gulp.task('minify', function() {
  gulp.src('js/app.js')
			.pipe(uglify())
			.pipe(gulp.dest('build'))
});
```

dest: 输出

task: 任务

run: 执行

watch: 监控

# 四、地面营销实践

## 项目目录结构：

```
project(项目名称)
	|–- node_modules 组件目录
	|–- dest 发布环境
		|–- css
		|–- images
		|–- js
		|–- index.html
	|–- src 开发环境
		|–- css
		|–- images
		|–- js
		|–- index.html
	|–- .jshintrc jshint配置文件
	|–- gulpfile.js gulp任务文件
```

# 五、其他

## 参考文档:

Gulp中文网：[http://www.gulpjs.com.cn/](http://www.gulpjs.com.cn/)

Gulp使用指南：[http://www.techug.com/gulp](http://www.techug.com/gulp)

使用Gulp构建本地开发Web服务器：[http://www.tuicool.com/articles/qUvyEj](http://www.tuicool.com/articles/qUvyEj)