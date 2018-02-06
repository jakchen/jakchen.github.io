---
layout: post
title:  "开始使用bootstrap(4)-超大屏幕"
categories: bootstrap
tags: bootstrap
author: jakchen
---
* content
{:toc}

可以增加标题的大小，并为登陆页面内容添加更多的外边距（margin）。

使用超大屏幕（Jumbotron）的步骤如下：
1. 创建一个带有 class `.jumbotron` 的容器 <div>。
2. 除了更大的 <h1>，字体粗细 font-weight 被减为 200。




PS：为了获得占用全部宽度且不带圆角的超大屏幕，请在所有的 `.container` class 外使用 `.jumbotron` class

代码如下：
```html
<div class="container">
  <div class="jumbotron">
    <h1>欢迎登陆页面！</h1>
    <p>这是一个超大屏幕（Jumbotron）的实例。</p>
    <p><a class="btn btn-primary btn-lg" role="button">
    学习更多</a>
    </p>
  </div>
</div>
```

效果如下
![超大屏幕]({{ site.url }}/assets/jumbotron2.png)

`.jumbotron`类的CSS代码如下：
```css
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 21px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  padding-right: 15px;
  padding-left: 15px;
  border-radius: 6px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-right: 60px;
    padding-left: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 63px;
  }
}
```