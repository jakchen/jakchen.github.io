---
layout: post
title:  "CSS布局7-栅格布局gird"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

grid 的布局方式使响应式设计更加灵活了，它学习了平面装帧设计中的格线系统，将格线运用在屏幕上，让设计师能更好地理解响应式设计的布局动态变化，而不再是单一的静态页面。而对于前端开发者来说 grid 减轻了不少断点与计算缩放大小的工作。




因为 grid 布局方式不适用于 IE 10 以下，所以大型网站及门户为了顾及 progressive web design 仍然不敢采用 grid layout。响应式设计中经常会考虑到的不同屏幕布局对齐方式，而 box alignment 的出现则解决了这个问题。

2017.3.8
CSS Grid 在 Firefox 52 率先登陆，Chrome 也在三月底正式支持。

意义：Grid Layout 规范开创了 CSS 从一维布局到二维布局的新时代。


简评：CSS 网格模块是创建网站模型的绝佳工具。它是我尝试过的任何其他系统中最快让你体验布局的工具。

## 我们的网格

我们将从模仿一个经典网站的非常基本的网格开始：
![image]({{ site.url }}/assets/gird.jpg)

首先，我将解释我们需要的 HTML 和 CSS 代码，我将之分为 4 个部分。一旦你弄明白了，我们将继续布局试验。

## 1. 标记

首先我们需要一点点 HTML 代码。一个容器（我们把它变成网格的元素）和一些项目（标题，菜单，内容，页脚）。
```html
<div class="container">
  <div class="header">HEADER</div>
  <div class="menu">MENU</div>
  <div class="content">CONTENT</div>
  <div class="footer">FOOTER</div>
</div>
```

## 2. CSS 中的基础设置
然后我们需要设置我们的网格，并声明我们需要多少行和列。这是我们最初的 CSS：
```css
.container {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: 50px 350px 50px;
    grid-gap: 5px;
}
```
稍后我们会添加更多代码，但首先我想解释一下。

上面的代码意思是：创建一个有 12 列的网格，每列宽度为总宽度的十二分之一。创建三行，第一行高 50px，第二行高 350px，第三行高 50px，最后，网格中每个元素添加一个间隙。

## 3. 添加 grid-template-areas

让我们能轻松体验布局的功能叫模版区域。

把它添加到网格中，我们只需要简单地给 container 添加一个 grid-template-area 属性即可。语法可能有点怪，因为它不像任何其他的 CSS 语法。就像这样：

```css
.container {
    display: grid;
    grid-gap: 5px;
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: 50px 350px 50px;
    grid-template-areas:
        "h h h h h h h h h h h h"
        "m m c c c c c c c c c c"
        "f f f f f f f f f f f f";
}
```
grid-template-areas 属性背后的逻辑是你在代码中创建一个可视化的网格。你可以看到，它有 3 行、12 列。就像我们在定义 grid-template-columns 和 grid-template-rows 一样。

每一行代表一行，每一个字符（h，m，c，f）代表一个网格元素。

四个字符中的每一个都形成一个矩形：grid-area。

可能你已经猜到了，我选择的四个字符 h，m，c，f 分别代表了 header，menu，content，footer。我当然可以把它们换成我想要的任何字符，但使用它们描述的项目的第一个字符显然比较合理。

## 4. 把网格区域赋给项目

现在我们需要连接字符和网格中的项目。我们将使用 grid-area 属性：
```css
.header {
    grid-area: h;
}
.menu {
    grid-area: m;
}
.content {
    grid-area: c;
}
.footer {
   grid-area: f;
}
```
布局结果如下：
![image]({{ site.url }}/assets/gird2.jpg)

## 试验布局

现在终于到了我们体验这个功能的强大时候了，我们可以轻松地实验布局。只需要修改一下 grid-template-areas 中的字符即可。例如我们把上面的菜单移动到右边：
```css
grid-template-areas:
        "h h h h h h h h h h h h"
        "c c c c c c c c c c m m"
        "f f f f f f f f f f f f";
```
结果就会变成：
![image]({{ site.url }}/assets/gird3.jpg)

我们可以使用 . 来创建空白网格：
```css
grid-template-areas:
        ". h h h h h h h h h h ."
        "c c c c c c c c c c m m"
        ". f f f f f f f f f f .";
```
看起来是这样的：
![image]({{ site.url }}/assets/gird4.jpg)


## 添加响应能力

把这个和响应能力相结合简直就是一大杀器，以前这是不可能只用 HTML 和 CSS 就能达到这种效果的。假设当你用手机浏览时想让菜单放在标题旁边，你可以这样做：
```css
@media screen and (max-width: 640px) {
    .container {
        grid-template-areas:
            "m m m m m m h h h h h h"
            "c c c c c c c c c c c c"
            "f f f f f f f f f f f f";
    }
}
```
记住这些是用纯 CSS 代码完成的，不需要改动 HTML。无论 div 标签在标记中是如何放置的，我们都能随意转换。

这被称为源代码的独立性，这是 CSS 的一大进步。

它让 HTML 回归本职工作：标记内容。至于样式，那是 CSS 的工作。

[原文链接](https://zhuanlan.zhihu.com/p/31711806?utm_source=com.youdao.note&utm_medium=social)
