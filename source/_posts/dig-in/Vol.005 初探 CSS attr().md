---
title: 初探 CSS attr()
date: 2021-06-04 18:00:00
categories:
  - dig-in
tags:
  - css
---
# 一、什么是 CSS `attr()`

传统的`attr()`语法只能让HTML属性作为字符串使用，且只能使用在伪元素中，例如：

### 代码：

```html
<span class="example-1" data-title="提示">按钮</span>

<style>
  .example-1:hover::after {
    content: attr(data-title);
  }
</style>
```

### 效果：

<span class="example-1" data-title="提示">按钮</span>

<style>
  .example-1:hover::after {
		content: attr(data-title);
	}
</style>

全新的`attr()`语法可以让HTML属性值转换成任意的CSS数据类型。

### 代码：

```html
<button class="example-2" bgcolor="skyblue" radius="4">按钮</button>
<button class="example-2" bgcolor="#00000040" radius="1rem">按钮</button>
<button class="example-2" bgcolor="red" radius="50%">按钮</button>
<button class="example-2" bgcolor="orange" radius="100% / 50%" title="说明文字">按钮</button>

<style>
  .example-2 {
    background-color: attr(bgcolor color);
    border-radius: attr(radius px, 4px);
  }
</style>
```

### 效果：

理论上，上面的代码会有如下图所示的效果。

![image1](/images/dig-in/005/image1.png)

如果浏览器支持`attr()`语法，很多组件接口可以直接交给CSS完成，使得开发变得更加灵活。例如：

```css
[ml] { margin-left: attr(ml px, 0); }
[mt] { margin-top: attr(ml px, 0); }
[mr] { margin-right: attr(mr px, 0); }
[mb] { margin-bottom: attr(mb px, 0); }
[pl] { padding-left: attr(pl px, 0); }
[pt] { padding-top: attr(pt px, 0); }
[pr] { padding-right: attr(pr px, 0); }
[pb] { padding-bottom: attr(pb px, 0); }
```

开发人员要调整边距大小，可以直接写成：

```html
<div mt="10">上间距10px</div>
```

但是或许是出于安全/性能方面的考量，目前`attr()`函数的新语法没有任何浏览器支持。

![image2](/images/dig-in/005/image2.png)

# 二、Polyfill `attr()`新语法

CSS变量有一个特性，那就是CSS自定义属性值支持各种表达式和函数值，哪怕这个表达式是不知所云的东西。

例如随便自定义一个名叫`keyword()`的函数，然后使用如下所示的CSS调用：

```css
body {
	--keyword: keyword(red, 50%); 合法
	color: var(--keyword);
}
```

结果浏览器认为语法是合法的（比方说下图语句没有出现删除线，说明语句是合法的）：

![image3](/images/dig-in/005/image3.png)

于是我们就可以利用CSS变量的这个特性Polyfill `attr()`函数，原理如下。

## Polyfill实现原理

1. CSS自定义属性作为信使传递`attr()`函数，保证语法的合法性，例如：

```css
button {
	--attr-bg: attr(bgcolor color);
	background-color: var(--attr-bg);
}
```

2. 获取⻚⾯所有的包含`attr()`函数的⾃定义属性；
3. 遍历并观察所有DOM，如果设置了对应的⾃定义属性，将`attr()`语法转换成浏览器识别的常规自定义属性语法。

首先，我们要引入[css-attr.js](/js/dig-in/005/css-attr.js)文件

## Polyfill测试

### 代码：

```html
<button class="example-3" bgcolor="skyblue" radius="4">按钮</button>
<button class="example-3" bgcolor="white" radius="1rem">按钮</button>
<button class="example-3" bgcolor="red" radius="50%">按钮</button>
<button class="example-3">按钮</button>

<style>
  .example-3 {
    border: 0;
    padding: .5em 1em;
  }
  .example-3 {
    --attr-bg: attr(bgcolor color);
    background-color: var(--attr-bg);
    --attr-radius: attr(radius px, 4px);
    border-radius: var(--attr-radius);
  }
</style>
```

### 效果：

<button class="example-3" bgcolor="skyblue" radius="4">按钮</button>
<button class="example-3" bgcolor="white" radius="1rem">按钮</button>
<button class="example-3" bgcolor="red" radius="50%">按钮</button>
<button class="example-3">按钮</button>

<style>
   .example-3 {
   	border: 0;
   	padding: .5em 1em;
   }
   .example-3 {
   	--attr-bg: attr(bgcolor color);
   	background-color: var(--attr-bg);
   	--attr-radius: attr(radius px, 4px);
   	border-radius: var(--attr-radius);
   }
</style>

实际开发中，按钮元素往往需要一个默认的主样式，此时可以通过属性选择器进行区分，例如：

```html
<button class="example-4" bgcolor="skyblue" radius="4">按钮</button>
<button class="example-4" bgcolor="white" radius="1rem">按钮</button>
<button class="example-4" bgcolor="red" radius="50%">按钮</button>
<button class="example-4">按钮</button>

<style>
  .example-4 {
    border: 0;
    padding: .5em 1em;
  }
  .example-4[bgcolor] {
    --attr-bg: attr(bgcolor color);
    background-color: var(--attr-bg);
  }
  .example-4[radius] {
    --attr-radius: attr(radius px, 4px);
    border-radius: var(--attr-radius);
  }
</style>
```

这样自定义的HTML属性无论设置还是不设置都不会影响按钮的正常显示了。

<button class="example-4" bgcolor="skyblue" radius="4">按钮</button>
<button class="example-4" bgcolor="white" radius="1rem">按钮</button>
<button class="example-4" bgcolor="red" radius="50%">按钮</button>
<button class="example-4">按钮</button>

<style>
   .example-4 {
   	border: 0;
   	padding: .5em 1em;
   }
   .example-4[bgcolor] {
   	--attr-bg: attr(bgcolor color);
   	background-color: var(--attr-bg);
   }
   .example-4[radius] {
   	--attr-radius: attr(radius px, 4px);
   	border-radius: var(--attr-radius);
   }
</style>

## 意料之中的小彩蛋

还记得之前的margin代码么

```css
[ml] { margin-left: attr(ml px, 0); }
[mt] { margin-top: attr(ml px, 0); }
[mr] { margin-right: attr(mr px, 0); }
[mb] { margin-bottom: attr(mb px, 0); }
```

`attr()`同样支持复合的HTML属性值

```html
<div m="10px 20px 30px 40px">自定义四面margin</div>

<style>
  [m] {
    --m: attr(m);
    margin: var(--m);
  }
</style>
```

# 三、结束语

`attr()`同样存在很多缺点

比如自定义属性不能同名，定义的属性值过多不便于记忆&团队合作……

其实目前的css预处理器已经足够强大，团队合作更应注重css属性创建&调用规则的制定

`attr()`更多是一种对冷门领域的探索，可以在个人项目上试一下

<br />

参考资料: Polyfill吊炸天的CSS attr()新语法
[https://www.zhangxinxu.com/wordpress/2020/10/css-attr-polyfill/](https://www.zhangxinxu.com/wordpress/2020/10/css-attr-polyfill/)

<script type="text/javascript" src="/js/dig-in/005/css-attr.js"></script>