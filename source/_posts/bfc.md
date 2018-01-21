---
title: 块级格式化上下文 （BFC）
date: 2018-01-21 20:57:25
tags:
---
### 来认识一下 BFC 
BFC 英文是Block Formatting Context，中文直译为块级格式上下文

<!-- more -->
渲染规则 ：
* 1、在bfc 元素垂直方向的边距不会发生重叠。
* 2、bfc 的边距不会与浮动元素发生重叠（清除浮动原理）
* 3、bfc 在页面上是个独立的容器，外面和里面的元素互不影响
* 4、计算bfc 元素高度的时候，里面的浮动元素也会参与计算

创建bfc：
* 1、float 不为none
* 2、position 不为 static inherit
* 3、display属性为 table-cell 系列
* 4、overflow

通常有以下情况需要用到 BFC 来解决问题的：
* 1、垂直方向元素边距重叠了

效果如下：
![bfc_float](bfc_01.png)

兄弟元素之间的margin 重叠了然后取最大值，这个时候如果给其中一个变成BFC就可以阻止这各元素的重叠问题。

![bfc_float](bfc_02.png)

* 2、与float元素区域重叠了

![bfc_float](bfc_03.png)

这个时候给float 元素创建 BFC 就可以让float 元素的区域不会被其他元素影响了

![bfc_float](bfc_04.png)

* 3、就是需要计算float元素高度的 时候，给外层盒子创建BFC（清除浮动的原理~）