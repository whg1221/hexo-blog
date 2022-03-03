---
title: CSS绘图
date: 2016-06-03 18:00:00
categories:
  - dig-in
tags:
  - css
---
# 一、CSS绘制圆、椭圆、圆柱

## 采用border-radius

### 圆：

```css
.test {
	background: #fb3;
	width: 200px;
	height: 200px;
	border-radius: 50%;
}
```

### 椭圆：

```css
.test {
	background: #fb3;
	width: 200px;
	height: 150px;
	border-radius: 50%;
}
```

### 圆柱：

```css
.test {
	background: #fb3;
	width: 200px;
	height: 300px;
	border-radius: 50%/20%;
}
```

# 二、CSS绘制半圆

## 详解border-radius

![border-radius](/images/dig-in/002/image1.png)

### 上半圆：

```css
.test {
	background: #fb3;
	width: 200px;
	height: 100px;
	border-radius: 50%/100% 100% 0 0; /* 50% 50% 50% 50%/100% 100% 0 0 */
}
```

### 左半圆：

```css
.test {
	background: #fb3;
	width: 100px;
	height: 200px;
	border-radius: 100% 0 0 100% / 50%; /* 100% 0 0 100%/50% 50% 50% 50% */
}
```

斜杠前为水平半径，后为垂直半径

# 三、CSS绘制三角形、梯形

## 采用border方法

### 最简单的三角形：

```css
.test {
	width: 0;
	height: 0;
	border-width: 100px 50px;
	border-style: solid;
	border-color: #f30 #f30 #fff #fff;
}
```

### 梯形：

```css
.circle {
	width: 100px;
	height: 100px;
	border: 100px solid;
	border-color: #f30 #fff #fff #fff;
}
```

通过调节width、height、border、border-color属性改变形状，总体思想是用border绘制

# 四、box-shadow的使用

## 可以在box-shadow后叠加box-shadow，从而创造图形

### 最简单的三角形：

```css
.test {
	width: 0;
	height: 0;
	border-width: 100px 50px;
	border-style: solid;
	border-color: #f30 #f30 #fff #fff;
}
```

### 梯形：

```css
.circle {
	width: 100px;
	height: 100px;
	border: 100px solid;
	border-color: #f30 #fff #fff #fff;
}
```

通过调节width、height、border、border-color属性改变形状，总体思想是用border绘制

# 五、复杂图形

## 铅笔：

```html
<style>
div {
  position: relative;
  left: 100px;
  width:250px;
  height:50px;
  background: #237449;
  background-image: radial-gradient(ellipse at top, rgba(0,0,0,.6) 50px, transparent 54px),
                    linear-gradient(to right, transparent 25px, rgba(0,0,0,.6) 25px, rgba(0,0,0,.6) 30px, transparent 30px, transparent 35px, rgba(0,0,0,.6) 35px, rgba(0,0,0,.6) 40px, transparent 40px, transparent 210px, rgba(0,0,0,.6) 210px, rgba(0,0,0,.6) 215px, transparent 215px, transparent 220px, rgba(0,0,0,.6) 220px, rgba(0,0,0,.6) 225px, transparent 225px),
                    linear-gradient(to right, transparent 12px, rgba(41,237,133,.6) 12px, rgba(41,237,133,.6) 235px, transparent 235px),
                    linear-gradient(to bottom, transparent 62%, rgba(0,0,0,.3) 100%);
  box-shadow: 2px 2px 3px rgba(0,0,0,.3);
}
div:before {
  content: "";
  position: relative;
  left:-48px;
  top:15px;
  height: 10px;
  border-right: 48px solid #237449;
  border-bottom: 13px solid transparent;
  border-top: 13px solid transparent;
}
div:after {
  content: 'green';
  font-family: Arial, sans-serif;
  font-size: 12px;
  font-weight: bold;
  color: rgba(255,255,255,.9);
  text-align: right;
  padding-top: 37px;
  padding-right: 47px;
  box-sizing: border-box;
  display: inline-block;
  position: relative;
  left: -48px;
  width: 298px;
  height: 50px;
  top: -27px;
  background-image: linear-gradient(to bottom, rgba(255,255,255,0) 22px, rgba(255,255,255,.2) 27px, rgba(255,255,255,.2) 29px, rgba(255,255,255,0) 34px);
}
</style>
<body>
  <div></div>
</body>
```

## 盾牌：

```html
<style>
/*旋转代码*/
@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(180deg); }
}

#circle:before {
  content:"";
  width:600px;
  height:600px;
  position:absolute;
  background-image: linear-gradient(to right,transparent 0, transparent 225px, rgba(0,0,0,.3) 300px, transparent 375px, transparent 600px),
                    linear-gradient(to top,transparent 0, transparent 225px, rgba(0,0,0,.3) 300px, transparent 375px, transparent 600px),
                    linear-gradient(45deg,transparent 0, transparent 350px, rgba(255,255,255,.5) 425px, transparent 500px, transparent 600px),
                    linear-gradient(-45deg,transparent 0, transparent 350px, rgba(255,255,255,.5) 425px, transparent 500px, transparent 600px);
  /*神奇的旋转*/
  animation-name: spin;
  animation-duration: 5000ms; /* 40 seconds */
  animation-iteration-count: infinite;
  animation-timing-function: cubic-bezier(.5, .5, 0, 1);
}

#circle {
  position: relative;
  width:600px;
  height:600px;
  border-radius:50%;
  background:#f00;
  background-image:radial-gradient(blue, blue 75px, transparent 75px, transparent 300px),
                   repeating-radial-gradient(silver, silver 75px, red 75px, red 150px);
}

#star-five{
  top:278px;
  left:253px;
  width: 0;
  height: 0;
  color: #fff;
  margin: 50px 0;
  position: relative;
  display: block;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 35px solid #fff;
  -moz-transfrom:rotate(35deg);
  -webkit-transform:rotate(35deg);
  -ms-transform:rotate(35deg);
  -o-transform:rotate(35deg);
}

#star-five:before{
  width: 0;
  height: 0;
  border-left: 15px solid transparent;
  border-right: 15px solid transparent;
  border-bottom: 40px solid #fff;
  position: absolute;
  top: -22.5px;
  left: -32.5px;
  color: white;
  display: block;
  content: "";
  -moz-transform:rotate(-35deg);
  -webkit-transform:rotate(-35deg);
  -ms-transform:rotate(-35deg);
  -o-transform:rotate(-35deg);
}
#star-five:after{
  width: 0;
  height: 0;
  display: block;
  position: absolute;
  color: #fff;
  top: 3px;
  left: -53px;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 35px solid #fff;
  content: "";
  -moz-transform:rotate(-70deg);
  -webkit-transform:rotate(-70deg);
  -ms-transform:rotate(-70deg);
  -o-transform:rotate(-70deg);
}
</style>
<body>
  <div id="circle">
    <div id="star-five"></div>
  </div>
</body>
```