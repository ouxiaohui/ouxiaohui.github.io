---
title: 关于三栏布局（水平/垂直）各种方式及优缺点
date: 2018-01-21 10:53:42
tags:
---
## 今天来列举一下三栏布局
<!-- more -->
### 常见的三栏布局都是左右宽度固定、中间自适应的。
* 像这样：
    ![layout_hor](layout_hor.png)

### 然后我们先来假设最少高度是已知的
#### so 先写好通用样式，比如左边是骚黄，中间自适应，右边蓝色等等
```html
<style type="text/css">
        html *{
            margin: 0;
            padding: 0;
        }
        .layout{
            margin-top: 20px;
        }
        .layout .left, .layout .center, .layout .right{
            min-height: 100px;
        }
        .layout .left{
            background-color: yellow;
        }
        .layout .right{
            background-color: #4AA8D8;
        }
        .layout .center{
            background-color: #ff5722;
        }
    </style>
```
### 然后是 浮动的 方式来试一下
```html
<section class="layout float">
    <style media="screen">
        .layout.float{
            min-height: 100px;
        }
        .layout.float .left{
            float: left;
            width: 100px;
        }
        .layout.float .right{
            float: right;
            width: 100px;
        }
    </style>
    <div class="left"></div>
    <div class="right"></div>
    <article class="center">
        <h1>我是浮动的解决方案哟~~</h1>
        <div class="desc">
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
        </div>
    </article>
</section>
```
### 噢~ 浮动的不要太简单毕竟是老牌方法，优点就是兼容性好
### 缺点：需要清除浮动，否则对其他兄弟元素有影响、脱离文档流，当然还有一些惊悚的情况比如。。
  ![folat_spec](layout_float_sepc.png)
### 嗯嗯这就是大名鼎鼎的文本围绕效果。
如果要消除这个效果（或者说清除浮动带来的影响）就要创建BFC ，
什么？你说不知道BFC是啥？你说来我们谈谈。
#### BFC 英文是Block Formatting Context，中文直译为块级格式上下文。简单来讲就是一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。