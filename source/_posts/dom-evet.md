---
title: dom 事件对象的碎知识
date: 2017-10-16 22:12:31
tags:
---
### 一些关于 DOM 的知识，之前有些很常用，但专业术语却不知道的

<!-- more -->

1. 1、DOM 事件级别：
    由于 web标准不断的更新，DOM 事件由原来的只能在HTML 元素上绑定click到现在能自定义事件，其中经历了
    1. DOM 0 在html 上 onclick="fn()" 或者 element.onclick=function() {}; 
    2. DOM 2 增加了 element.addEventListener('click', function(){}, false);
    3. DOM 3 增加了 element.addEventListener('keyup', function(){}, false); 类似的还有鼠标事件 mousedown 等
    ** 这里少了 DOM 1 ，并不是因为没有 DOM1 对应标准，而是该标准没有涉及DOM 操作相关的更新。
    ** 而addEventListener 里面的第三个参数 true 表示事件在捕获阶段执行， false 表示在冒泡阶段执行

2. 2、DOM 事件模型： 捕获向下，冒泡往上; DOM 事件流： 捕获阶段 --> 目标阶段 --> 冒泡阶段;
3. 3、DOM 捕获的具体阶段： window --> document --> html(document.documentElemnt) --> body(document.body) -->元素;
***
4. 4、Event 对象的常用 API： 
 
> event.preventDefault();

     这个方法神奇了，原本是用来阻止元素的默认行为，如 a 标签的链接转跳。
     在移动端 ！注意移动端！！它可以在 touchstart 事件里使用，从而阻止了 touchstart 后面的 touchmove 和 touchend 事件的触发，click也会被忽略。
     这个功能像 textarea 标签在readonly 属性为true时候，ios 的Safari 里点击是会触发一个缺少键盘的底部弹框，这个时候只要在touchstart 里加上这个方法就可以避免这个情况了。
     还有 touchmove 里调用这个方法也可以阻止浏览器的默认滚动事件

> event.stopPropagation();

    防止冒泡了，不解释

> event.stopImmediatePropagation();
    
    元素里面如果同时注册了两个click 事件，那么在 A 方法里调用这个方法可以阻止 B 方法的执行;

> event.currentTarget;

    当前触发事件的元素，适用场景： 事件委托中，即需要有for 循环中给每个子元素绑定事件
    通过冒泡基础，给父元素绑定一次事件就能获取到所有子元素的事件触发 event.target.
    此时 event.currentTarget 就是父级元素了
 
5. 5、 自定义事件：

* Event 类
```javascript
var eve = new Event('custome');
ele.addEventListener('custome', function(){});
ele.dispatchEvent(eve);
```
* CustomEvent 类
```javascript
var myEvent = new CustomEvent("userLogin", {
    detail: {
        username: "davidwalsh"
    },
    bubbles: true,  // 事件是否冒泡
    cancelable: false  // 是否可以取消事件的默认行为
});
element.addEventListener("userLogin", function(e) {
    console.info("Event is: ", e);
    console.info("Custom data is: ", e.detail);
});
element.dispatchEvent(myEvent);
```
    两个类区别在于 CustomEvent 在自定义事件时候可以传值，能指定是否冒泡和 能否取消默认行为;