---
layout: post
title:  "开始使用bootstrap(2)-导航"
categories: bootstrap
tags: bootstrap
author: jakchen
---
* content
{:toc}


## 1.标签式导航

1. 以一个带有 class `.nav` 的无序列表 ul 开始。
2. 添加 class `.nav-tabs`。




代码如下：

```html
<ul class="nav nav-tabs">
  <li class="active"><a href="#">Home</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
</ul>
```

效果如下：
![标签式导航]({{ site.url }}/assets/tabsnav.png)

`.nav`类的CSS代码如下：
```css
.nav {
  padding-left: 0;
  margin-bottom: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eee;
}
```

`.nav-tabs`类及`.active`类的CSS代码如下：
```css
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 4px 4px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eee #eee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555;
  cursor: default;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
}
```

## 2.胶囊式导航

1. 以一个带有 class `.nav` 的无序列表 ul 开始。
2. 添加 class `.nav-pills`。

代码如下：

```html
<ul class="nav nav-pills">
  <li class="active"><a href="#">Home</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
</ul>
```

效果如下：
![胶囊式导航]({{ site.url }}/assets/pillsnav.png)

`.nav`类的CSS代码如下：
```css
.nav {
  padding-left: 0;
  margin-bottom: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eee;
}
```

`.nav-pills`类及`.active`类的CSS代码如下：
```css
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 4px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
```

## 导航两端对齐

可以在屏幕宽度大于 768px 时，通过在分别使用 `.nav`、`.nav-tabs` 或 `.nav`、`.nav-pills` 的同时使用 class `.nav-justified`，让标签式或胶囊式导航菜单与父元素等宽。
**在更小的屏幕上，导航链接会堆叠。**

代码如下：

```html
<ul class="nav nav-tabs nav-justified">
  <li class="active"><a href="#">Home</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
</ul>

<ul class="nav nav-pills nav-justified">
  <li class="active"><a href="#">Home</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
</ul>
```

效果如下：
![导航两端对齐]({{ site.url }}/assets/nav-justified.png)

`nav-justified`类的CSS代码如下：
```css
.nav-justified {
  width: 100%;
}

.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  margin-bottom: 5px;
  text-align: center;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}

@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 4px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}

@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 4px 4px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
```

## 禁用链接

对每个 .nav class里的li，如果添加了 `.disabled`class，则会创建一个灰色的链接，同时禁用了该链接的 :hover 状态。

代码如下：
```html
<h1>禁用链接</h1>
<ul class="nav nav-tabs">
  <li class="active"><a href="#">Home</a></li>
  <li class="disabled"><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
  <li><a href="#">导航</a></li>
</ul>
```

PS:该 class 只会改变 &lt;a&gt; 的外观，不会改变它的功能。
在这里，您需要使用自定义的 JavaScript 来禁用链接。

效果如下：
![导航禁用链接]({{ site.url }}/assets/nav-disabled.png)

`disabled`类的CSS代码如下：
```css
.nav > li.disabled > a {
  color: #777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777;
  text-decoration: none;
  cursor: not-allowed;
  background-color: transparent;
}
```

## 下拉菜单

### 标签导航下拉菜单

向标签添加下拉菜单的步骤如下：
1. 以一个带有 class `.nav` 的无序列表 `<ul>` 开始。
2. 添加 class `.nav-tabs`。
3. 再在`<ul>`里面添加带有 `.dropdown-menu` class 的无序列表`<ul>` 。

代码如下：

```html
<h1>下拉菜单</h1>
<ul class="nav nav-tabs">
  <li class="active"><a href="#">Home</a></li>
  <li role="presentation" class="dropdown">
      <a class="dropdown-toggle" data-toggle="dropdown" href="#" role="button" aria-haspopup="true" aria-expanded="false">
        Dropdown <span class="caret"></span>
      </a>
      <ul class="dropdown-menu">
        <li><a href="">导航</a></li>
        <li><a href="">导航</a></li>
        <li><a href="">导航</a></li>
      </ul>
    </li>
</ul>
```

效果如下：
![ 标签导航下拉菜单]({{ site.url }}/assets/nav-dropdown.png)

`.dropdown-menu`类、`.dropdown-menu > .active `类、`.dropdown-menu > .disabled`类的CSS代码如下：
```css
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  font-size: 14px;
  text-align: left;
  list-style: none;
  background-color: #fff;
  -webkit-background-clip: padding-box;
          background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, .15);
  border-radius: 4px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, .175);
          box-shadow: 0 6px 12px rgba(0, 0, 0, .175);
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  color: #262626;
  text-decoration: none;
  background-color: #f5f5f5;
}

.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  background-color: #337ab7;
  outline: 0;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  cursor: not-allowed;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
}
```

### 胶囊导航下拉菜单

步骤与创建带有下拉菜单的标签相同，只是需要把 `.nav-tabs` class 改为 `.nav-pills`。

代码如下：

```html
<h1>胶囊式导航-下拉菜单</h1>
<ul class="nav nav-pills">
  <li class="active"><a href="#">Home</a></li>
  <li role="presentation" class="dropdown">
      <a class="dropdown-toggle" data-toggle="dropdown" href="#" role="button" aria-haspopup="true" aria-expanded="false">
        Dropdown <span class="caret"></span>
      </a>
      <ul class="dropdown-menu">
        <li><a href="">导航</a></li>
        <li><a href="">导航</a></li>
        <li><a href="">导航</a></li>
      </ul>
    </li>
</ul>
```

效果如下：
![ 胶囊导航下拉菜单]({{ site.url }}/assets/nav2-dropdown.png)

## 动态标签

`.tab-content` 与 `.tab-pane` 和 `data-toggle="tab"` (data-toggle="pill" ) 一同使用, 设置标签页对应的内容随标签的切换而更改

效果如下：
![动态标签]({{ site.url }}/assets/nav3.gif)

代码如下
```html
<h1>动态标签</h1>
<p><strong>提示:</strong> .tab-content 与 .tab-pane 和 data-toggle="tab" (data-toggle="pill" ) 一同使用, 设置标签页对应的内容随标签的切换而更改。</p>
<ul class="nav nav-tabs">
  <li class="active"><a data-toggle="tab" href="#home">首页</a></li>
  <li><a data-toggle="tab" href="#menu1">菜单 1</a></li>
  <li><a data-toggle="tab" href="#menu2">菜单 2</a></li>
  <li><a data-toggle="tab" href="#menu3">菜单 3</a></li>
</ul>

<div class="tab-content">
  <div id="home" class="tab-pane fade in active">
    <h3>首页</h3>
    <p>菜鸟教程 —— 学的不仅是技术，更是梦想！！！</p>
  </div>
  <div id="menu1" class="tab-pane fade">
    <h3>菜单 1</h3>
    <p>这是菜单 1 显示的内容。这是菜单 1 显示的内容。这是菜单 1 显示的内容。</p>
  </div>
  <div id="menu2" class="tab-pane fade">
    <h3>菜单 2</h3>
    <p>这是菜单 2 显示的内容。这是菜单 2 显示的内容。这是菜单 2 显示的内容。</p>
  </div>
  <div id="menu3" class="tab-pane fade">
    <h3>菜单 3</h3>
    <p>这是菜单 3 显示的内容。这是菜单 3 显示的内容。这是菜单 3 显示的内容。</p>
  </div>
</div>
```

`.tab-content`类里的`.tab-pane`类的CSS代码如下：
```css
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
```

`data-toggle="tab"` (data-toggle="pill" )：通过 data 属性来调用标签页插件。

## 导航class总结

标签页与胶囊式标签页

- `.nav nav-tabs` 标签页
- `.nav nav-pills` 胶囊式标签页
- `.nav nav-pills nav-stacked` 胶囊式标签页以垂直方向堆叠排列的
- `.nav-justified` 两端对齐的标签页，在大于 768px 的屏幕上，通过 .nav-justified 类可以很容易的让标签页或胶囊式标签呈现出同等宽度。 在小屏幕上，导航链接呈现堆叠样式。
- `.disabled` 禁用的标签页
- `.dropdown-menu .nav-tabs` 标签添加下拉菜单
- `.dropdown-menu .nav-pills`带下拉菜单的胶囊式标签页
- `.tab-content` 与 .tab-pane 和 data-toggle="tab" (data-toggle="pill" ) 一同使用, 设置标签页对应的内容随标签的切换而更改
- `.tab-pane` 与 .tab-content 和 data-toggle="tab" (data-toggle="pill")一同使用, 设置标签页对应的内容随标签的切换而更改





