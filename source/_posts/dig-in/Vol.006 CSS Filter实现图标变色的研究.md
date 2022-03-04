---
title: CSS Filter实现图标变色的研究
date: 2021-12-03 18:00:00
categories:
  - dig-in
tags:
  - css
---
# 一、起因

做售票机退订项目时，引用的公司框架中的InputNmuber组件，按钮的颜色与设计稿不一致，且为组件内部写死fill color值，无法外部配置修改。

（组件内按钮颜色为<span style="color: #0086F6">#0086F6</span>，设计稿按钮颜色为<span style="color: #1658DC">#1658DC</span>）

# 二、初步解决方案

参考[stackoverflow](https://stackoverflow.com/questions/29037023/how-to-calculate-required-hue-rotate-to-generate-specific-colour/29958459)讨论，采用CSS Filter方式转化色值。

以下是相关背景知识，太长不看的可以直接跳到转换步骤

> ### HSL色彩模式相关说明
>
> HSL和HSV都是一种将RGB色彩模型中的点在圆柱坐标系中的表示法。这两种表示法试图做到比基于笛卡尔坐标系的几何结构RGB更加直观。
>
> HSL即色相、饱和度、亮度（英语：Hue, Saturation, Lightness）。HSV即色相、饱和度、明度（英语：Hue, Saturation, Value），又称HSB，其中B即英语：Brightness。
>
> 色相（H）是色彩的基本属性，就是平常所说的颜色名称，如红色、黄色等。
>
> 饱和度（S）是指色彩的纯度，越高色彩越纯，低则逐渐变灰，取0-100%的数值。
>
> 明度（V），亮度（L），取0-100%。
>
> ![HSL色彩模式相关说明](/images/dig-in/006/image1.png)
>
> ### 从RGB到HSL的转换
>
> 设 (r, g, b)分别是一个颜色的红、绿和蓝坐标，它们的值是在0到1之间的实数。设max等价于r, g和b中的最大者。设min等于这些值中的最小者。要找到在HSL空间中的 (h, s, l)值，这里的h ∈ [0, 360）度是角度的色相角，而s, l ∈ [0,1]是饱和度和亮度，计算公式为：
>
> ![从RGB到HSL的转换](/images/dig-in/006/image2.png)

转换步骤如下：

1. 原色值、目标色值转化为HSL格式。（#0086F6 -> HSL(207deg,100%,48%)、#1658DC -> HSL(220deg,82%,47%)）

2. 计算两者差值

   H: 220 - 207        -> 13°

   S: 100 + (100 - 82) -> 118% (relative to base 100% = 18%)

   L: 100 + (47 - 48)  ->  99% (relative to base 100% = -1%)

3. 最终的CSS Filter为：

   filter: hue-rotate(13deg) saturate(118%) brightness(99%);

最终效果如下

原色值： ![原色值](/images/dig-in/006/image3.png)

转换后色值： ![转换后色值](/images/dig-in/006/image4.png)

目标色值：![目标色值](/images/dig-in/006/image5.png)

思考：可以看到计算出来的数据，颜色还有差距，数据微调之后仍然无法完美。

原因：[CSS的hue-rotate不是真正的色调旋转而是线性近似](https://stackoverflow.com/questions/19187905/why-doesnt-hue-rotation-by-180deg-and-180deg-yield-the-original-color/19325417)

![image6](/images/dig-in/006/image6.png)

![image7](/images/dig-in/006/image7.png)

# 三、略微深入研究

中文资料上参考张鑫旭的老文[《纯CSS实现任意格式图标变色的研究》](https://www.zhangxinxu.com/wordpress/2018/11/css-change-icon-color/)

1. 滤镜法：

   优点：支持svg定色图标的变色

   缺点：色差不可避免，只能接近，难以100%匹配

2. SVG背景叠加CSS遮罩法

   优点：能直接实现变色效果（无需计算）

   缺点：都引用SVG背景了，直接改个颜色不好么……

3. background-blend-mode混合模式

   优点同上

   缺点：图标需要黑色白底，其余缺点同上

# 四、继续深入研究

针对CSS Filter的大方向，[《How to transform black into any given color using only CSS filters》](https://stackoverflow.com/questions/42966641/how-to-transform-black-into-any-given-color-using-only-css-filters)的最高赞提出了一个复杂的算法，不同于其他答主的暴力计算比对误差值，时间复杂度上更优。

另外一条是走[SVG滤镜](https://www.w3.org/TR/filter-effects-1/)路线，采用feColorMatrix方法，通过矩阵计算能得到精确的色彩变换矩阵。但还是回到适用性，既然能直接控制SVG，也没有必要叠加如此复杂的滤镜了，直接改色就好了。

# 五、总结

- 适用场景

- 成本收益

- 后续探索

<br/>

参考：

1. 《How to calculate required hue-rotate to generate specific colour?》[https://stackoverflow.com/questions/29037023/how-to-calculate-required-hue-rotate-to-generate-specific-colour/29958459#29958459](https://stackoverflow.com/questions/29037023/how-to-calculate-required-hue-rotate-to-generate-specific-colour/29958459)
2. 《Why doesn't hue rotation by +180deg and -180deg yield the original color?》https://[stackoverflow.com/questions/19187905/why-doesnt-hue-rotation-by-180deg-and-180deg-yield-the-original-color/19325417#19325417](http://stackoverflow.com/questions/19187905/why-doesnt-hue-rotation-by-180deg-and-180deg-yield-the-original-color/19325417)
3. 《纯CSS实现任意格式图标变色的研究》[https](https://www.zhangxinxu.com/wordpress/2018/11/css-change-icon-color/)[://www.zhangxinxu.com/wordpress/2018/11/css-change-icon-color/](https://www.zhangxinxu.com/wordpress/2018/11/css-change-icon-color/)
4. 《How to transform black into any given color using only CSS filters》[https](https://stackoverflow.com/questions/42966641/how-to-transform-black-into-any-given-color-using-only-css-filters)[://stackoverflow.com/questions/42966641/how-to-transform-black-into-any-given-color-using-only-css-filters](https://stackoverflow.com/questions/42966641/how-to-transform-black-into-any-given-color-using-only-css-filters)
5. 《feColorMatrix》https://www.w3.org/TR/filter-effects-1/#feColorMatrixElement

