---
layout: post
title:  "开始使用bootstrap(5)-轮播（Carousel）插件"
categories: bootstrap
tags: bootstrap
author: jakchen
---
* content
{:toc}

轮播（Carousel）插件是一种灵活的响应式的向站点添加滑块的方式。

 除此之外，内容也是足够灵活的，可以是图像、 内嵌框架、视频或者其他您想要放置的任何类型的内容。

 为了实现轮播，您只需要添加带有该标记的代码即可。不需要使用 data 属性，只需要简单的基于 class 的开发即可。



**下面是一个实例，代码如下：**

```html
<div id="myCarousel" class="carousel slide" data-ride="carousel">
    <!-- 轮播（Carousel）指标 -->
    <ol class="carousel-indicators">
        <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
        <li data-target="#myCarousel" data-slide-to="1"></li>
        <li data-target="#myCarousel" data-slide-to="2"></li>
    </ol>
    <!-- 轮播（Carousel）项目 -->
    <div class="carousel-inner">
        <div class="item active">
            <img src="images/img.jpg" alt="First slide">
            <div class="carousel-caption">标题 1</div>
        </div>
        <div class="item">
            <img src="images/img.jpg" alt="Second slide">
            <div class="carousel-caption">标题 2</div>
        </div>
        <div class="item">
            <img src="images/img.jpg" alt="Third slide">
            <div class="carousel-caption">标题 3</div>
        </div>
    </div>
    <!-- 轮播（Carousel）导航 -->
    <a class="carousel-control left" href="#myCarousel"
        data-slide="prev">
        <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control right" href="#myCarousel"
        data-slide="next">
        <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
    </a>
</div>
```

## 用法

### 通过 data 属性

使用 data 属性可以很容易控制轮播（Carousel）的位置。
1. 属性 `data-slide` 接受关键字 `prev` 或 `next`，用来改变幻灯片相对于当前位置的位置。
2. 使用 `data-slide-to` 来向轮播传递一个原始滑动索引，`data-slide-to="2"` 将把滑块移动到一个特定的索引，索引从 0 开始计数。
3. `data-ride="carousel"` 属性用于标记轮播在页面加载时就开始动画播放。

### 通过 JavaScript

1. 轮播（Carousel）可通过 JavaScript 手动调用：`$('.carousel').carousel()`

## 1.加载时播放动画

1. `data-ride="carousel"` 属性用于标记轮播在页面加载时就开始动画播放。

PS：It cannot be used in combination with (redundant and unnecessary)
explicit JavaScript initialization of the same carousel.
（它不能与相同的轮播结合(多余和不必要的）显式JavaScript初始化）

代码如下：
```html
<div id="myCarousel" class="carousel slide" data-ride="carousel">
  <!-- 轮播（Carousel）指标 -->
  ···
  <!-- 轮播（Carousel）项目 -->
  ···
  <!-- 轮播（Carousel）导航 -->
  ···
</div>
```

## 2.滑动索引

1. 使用 `data-slide-to` 来向轮播传递一个原始滑动索引，`data-slide-to="2"` 将把滑块移动到一个特定的索引，索引从 0 开始计数。

解释：滑动索引即轮播底部的小圆点，例如当小圆点属性 `data-slide-to="2"` 时，点击小圆点，将向指定索引滑动。

代码如下：
```html
<!-- 轮播（Carousel）指标 -->
<ol class="carousel-indicators">
    <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
    <li data-target="#myCarousel" data-slide-to="1"></li>
    <li data-target="#myCarousel" data-slide-to="2"></li>
</ol>
```

## 3.可选的标题

1. 可以通过 `.item`内的 `.carousel-caption` 元素向幻灯片添加标题。 只需要在该处放置任何可选的 HTML 即可，它会自动对齐并格式化。

代码如下：
```html
<!-- 轮播（Carousel）项目 -->
<div class="carousel-inner">
    <div class="item active">
        <img src="images/img.jpg" alt="First slide">
        <div class="carousel-caption">标题 1</div>
    </div>
    <div class="item">
        <img src="images/img.jpg" alt="Second slide">
        <div class="carousel-caption">标题 2</div>
    </div>
    <div class="item">
        <img src="images/img.jpg" alt="Third slide">
        <div class="carousel-caption">标题 3</div>
    </div>
</div>
```

效果如下：<br>
![可选的标题]({{ site.url }}/assets/carousel.gif)
![可选的标题](https://s1.ax1x.com/2018/02/06/9lIYTA.gif)

`.carousel-caption`类的CSS代码如下：
```css
.carousel-caption {
  position: absolute;
  right: 15%;
  bottom: 20px;
  left: 15%;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, .6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-caption {
    right: 20%;
    left: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
```
## 4.轮播导航

1. 属性 `data-slide` 接受关键字 `prev` 或 `next`

代码如下：
```html
<!-- 轮播（Carousel）导航 -->
<a class="carousel-control left" href="#myCarousel"
    data-slide="prev">
    <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
    <span class="sr-only">Previous</span>
</a>
<a class="carousel-control right" href="#myCarousel"
    data-slide="next">
    <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
    <span class="sr-only">Next</span>
</a>
```

效果如下：<br>
![轮播（Carousel）导航 ]({{ site.url }}/assets/carousel.gif)
![轮播（Carousel）导航 ](https://s1.ax1x.com/2018/02/06/9lIYTA.gif)

## 选项(data-*)

有一些选项是通过 data 属性或 JavaScript 来传递的。

  选项名称    | 类型/默认值            | Data 属性名称 |     描述      |
------------- | ---------------------- | ------------- | -------------
  interval    | number 默认值：5000    | data-interval | 自动循环每个项目之间延迟的时间量。如果为 false，轮播将不会自动循环。 |
   pause      | string 默认值："hover" | data-pause   | 鼠标进入时暂停轮播循环，鼠标离开时恢复轮播循环。|
wrap  | boolean 默认值：true | data-wrap | 轮播是否连续循环。|

### data-interval

自动循环每个项目之间延迟的时间量。如果为 false，轮播将不会自动循环。

```
number 默认值：5000
```

### data-pause

鼠标进入时暂停轮播循环，鼠标离开时恢复轮播循环。

```
string 默认值："hover"
```

### data-wrap

轮播是否连续循环。

```
boolean 默认值：true
```

## 方法
轮播（Carousel）插件中有用的方法：

  方法        | 描述                   | 实例          |
------------- | ---------------------- | ------------- |
.carousel(options)  | 初始化轮播为可选的 options 对象，并开始循环项目。  | $('#identifier').carousel({interval: 2000})|
.carousel('cycle')  | 从左到右循环轮播项目。 | $('#identifier').carousel('cycle') |
.carousel('pause')  |   停止轮播循环项目。 | $('#identifier').carousel('pause') |
.carousel(number)   | 循环轮播到某个特定的帧（从 0 开始计数，与数组类似）。 | $('#identifier').carousel(number)|
.carousel('prev')   | 循环轮播到上一个项目。 | $('#identifier').carousel('prev')|
.carousel('next')   | 循环轮播到下一个项目。 | $('#identifier').carousel('next')|


### .carousel(options)

初始化轮播为可选的 options 对象，并开始循环项目。
```javascript
$('#identifier').carousel({
    interval: 2000
})
```

### .carousel('cycle')

从左到右循环轮播项目。
```javascript
$('#identifier').carousel('cycle')
```

### .carousel('pause')

停止轮播循环项目。

```javascript
$('#identifier').carousel('pause')
```

### .carousel(number)

循环轮播到某个特定的帧（从 0 开始计数，与数组类似）。

```javascript
$('#identifier').carousel(number)
```

### .carousel('prev')

循环轮播到上一个项目。

```javascript
$('#identifier').carousel('prev')
```

### .carousel('next')

循环轮播到下一个项目。

```javascript
$('#identifier').carousel('next')
```

## 事件

轮播（Carousel）插件中要用到的事件。这些事件可在函数中当钩子使用。

  事件        | 描述    | 实例    |
------- | --------- | ------------- |
slide.bs.carousel | 当调用 slide 实例方法时立即触发该事件。 |$('#identifier').on('slide.bs.carousel', function () {    // 执行一些动作...}) |
slid.bs.carousel |  当轮播完成幻灯片过渡效果时触发该事件。 |$('#identifier').on('slid.bs.carousel', function () {    // 执行一些动作...}) |


### slide.bs.carousel

当调用 slide 实例方法时立即触发该事件。

```javascript
$('#identifier').on('slide.bs.carousel', function () {
    // 执行一些动作...
})
```

### slid.bs.carousel

当轮播完成幻灯片过渡效果时触发该事件。

```javascript
$('#identifier').on('slid.bs.carousel', function () {
    // 执行一些动作...
})
```
