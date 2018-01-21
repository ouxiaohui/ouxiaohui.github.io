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

### 然后我们先来假设最小高度是已知的
#### so 先写好通用样式，比如左边是骚黄，中间自适应，右边蓝色等等
```css
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
        };
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
噢~ 浮动的不要太简单毕竟是老牌方法，优点就是兼容性好
缺点：需要清除浮动，否则对其他兄弟元素有影响、脱离文档流，当然还有一些惊悚的情况比如。。
  ![folat_spec](layout_float_sepc.png)
嗯嗯这就是大名鼎鼎的文本围绕效果。
如果要消除这个效果（或者说清除浮动带来的影响）就要创建BFC ，
什么？你说不知道BFC是啥？你说来我们谈谈。
#### BFC 英文是Block Formatting Context，中文直译为块级格式上下文。
简单来讲就是一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。

### 然后是定位的
```html
<section class="layout position">
    <style media="screen">
        .layout.position{
            position: relative;
            min-height: 120px;
        }
        .layout.position .left{
            position: absolute;
            left: 0;
            width: 100px;
        }
        .layout.position .right{
            position: absolute;
            right: 0;
            width: 100px;
        }
        .layout.position .center{
            position: absolute;
            left: 100px;
            right: 100px;
        }
    </style>
    <div class="left"></div>
    <div class="right"></div>
    <article class="center">
        <h1>我是定位的解决方案哟~~</h1>
        <div class="desc">
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
        </div>
    </article>
</section>
```
可以看出来定位的方法挺好用的，兼容性好还很灵活，想在哪就在哪，配合js还可以写动效啥的。
bug~ 缺点也很明显，一旦用了定位，下面所有的子元素都要用定位才能做了。

### 然后是flexbox
```html
<section class="layout flex">
    <style media="screen">
        .layout.flex{
            display: flex;
        }
        .layout.flex .left{
            width: 100px;
        }
        .layout.flex .right{
            width: 100px;
        }
        .layout.flex .center{
            flex: 1;
        }
    </style>
    <div class="left"></div>
    <article class="center">
        <h1>我是flexbox的解决方案哟~~</h1>
        <div class="desc">
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
        </div>
    </article>
    <div class="right"></div>
</section>
```
suguoyi~ flex 方法的代码量简直完爆上面两种，不存在对其他兄弟元素的影响不需要每个子元素都特别设置
毕竟flex 布局就是为了解决以上两种方法带来问题而生的，so兼容性是他的shortcoming

### 要不用table试一下吧？
```html
<section class="layout table">
    <style media="screen">
        .layout.table{
            display: table;
            width:100%;
            min-height: 100px;
        }
        .layout.table .left, .layout.table .right{
            width: 100px;
            display: table-cell;
        }
        .layout.table .center{
            display: table-cell;
        }
    </style>
    <div class="left"></div>
    <article class="center">
        <h1>我是table的解决方案哟~~</h1>
        <div class="desc">
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
        </div>
    </article>
    <div class="right"></div>
</section>
```
放下你对table 的偏见，其实table 布局并不是一无是处的，比如这个三栏布局比起浮动简直不要方便太多
1、兼容性好，无副作用
2、同高而且高度自适应的横排布局、类表格布局都能轻松实现

### 再来个 grid 的
```html
<section class="layout grid">
    <style media="screen">
        .layout.grid{
            display:grid;
            grid-template-columns: 100px auto 100px;
        }
    </style>
    <div class="left"></div>
    <article class="center">
        <h1>我是 grid 的解决方案哟~~</h1>
        <div class="desc">
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
            <p>内容内容内容内容</p>
        </div>
    </article>
    <div class="right"></div>
</section>
```
这。。grid 真的是让你的 css 在布局上，为所欲为！！
简单粗暴: 设置父元素为 grid ，然后制定子元素块 或者 以网格线来自定义宽或高
缺点嘛，当然是支不支持的问题了，IE10 都不支持啊。。

### 其他的想到在写了

### 最后，还有个已知最小高度的情况。
如果我们把内容增加，而不手动改其他代码看会是啥情况咯。

![end](layout_end.png)

阔以看到，最小高度的情况下 ，如果把内容增加，依然能用不鬼畜的有 flexbox 和 table 布局
恭喜两位获奖者，我们的工作人员将会在下辈子之前通知你来领取奖品~~~~~~~
end 
