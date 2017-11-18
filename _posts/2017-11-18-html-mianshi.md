---
layout: post
title:  "HTML 面试题"
categories: HTML
tags: HTML
author: jakchen
---
* content
{:toc}
### 1.HTML5的页面结构同HTML4或者更前的HTML有什么区别？

一个典型的WEB页面包含头部，脚部，导航，中心区域，侧边栏。现在如果我们想在在HTML4的HTML区域中呈现这些内容，我们可能要使用DIV标签。

但是在HTML5中通过为这些区域创建元素名称使他们更加清晰，也使得你的HTML更加可读。





![image]({{ site.url }}/assets/html5.jpg)

以下是形成页面结构的HTML5元素的更多细节：
```
<header>：代表HTML的头部数据
<footer>：页面的脚部区域
<nav>：页面导航元素
<article>：自包含的内容
<section>：使用内部article去定义区域或者把分组内容放到区域里
<aside>：代表页面的侧边栏内容
```
### 2.对WEB标准以及W3C的理解与认识
标签闭合、标签小写、不乱嵌套、提高搜索机器人搜索几率、使用外 链css和js脚本、结构行为表现的分离、文件下载与页面速度更快、内容能被更多的用户所访问、内容能被更广泛的设备所访问、更少的代码和组件，容易维 护、改版方便，不需要变动页面内容、提供打印版本而不需要复制内容、提高网站易用性；

### 3.xhtml和html有什么区别
HTML是一种基本的WEB网页设计语言，XHTML是一个基于XML的置标语言。

最主要的不同：

- XHTML 元素必须被正确地嵌套。
- XHTML 元素必须被关闭。
- 标签名必须用小写字母。
- XHTML 文档必须拥有根元素。

### 4.Doctype? 严格模式与混杂模式-如何触发这两种模式，区分它们有何意义?
用于声明文档使用那种规范（html/Xhtml）一般为 严格 过度 基于框架的html文档
加入XMl声明可触发，解析方式更改为IE5.5 拥有IE5.5的bug

### 5.行内元素有哪些?块级元素有哪些?
块级元素：div p h1 h2 h3 h4 form ul

行内元素：a b br i span input select

### 6.前端页面有哪三层构成，分别是什么?作用是什么?

结构层 Html 表示层 CSS 行为层 js;

### 7.你做的页面在哪些流览器测试过?这些浏览器的内核分别是什么?
Ie(Ie内核) 火狐（Gecko） 谷歌（webkit,Blink） opera(Presto),Safari(wbkit)

### 8 .什么是语义化的HTML?

直观的认识标签 对于搜索引擎的抓取有好处，用正确的标签做正确的事情！
html语义化就是让页面的内容结构化，便于对浏览器、搜索引擎解析；
在没有样式CCS情况下也以一种文档格式显示，并且是容易阅读的。搜索引擎的爬虫依赖于标记来确定上下文和各个关键字的权重，利于 SEO。
使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

### 9.HTML5 为什么只需要写 !DOCTYPE HTML？

HTML5 不基于 SGML，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）；而HTML4.01基于SGML,所以需要对DTD进行引用，才能告知浏览器文档所使用的文档类型。

### 10.Doctype作用？标准模式与兼容模式各有什么区别?

!DOCTYPE声明位于位于HTML文档中的第一行，处于html 标签之前。告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。
标准模式的排版 和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示,模拟老式浏览器的行为以防止站点无法工作。

### 11.html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？

HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
绘画 canvas
用于媒介回放的 video 和 audio 元素
本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；
sessionStorage 的数据在浏览器关闭后自动删除
语意化更好的内容元素，比如 article、footer、header、nav、section
表单控件，calendar、date、time、email、url、search
新的技术webworker, websockt, Geolocation
移除的元素
纯表现的元素：basefont，big，center，font, s，strike，tt，u；
对可用性产生负面影响的元素：frame，frameset，noframes；
支持HTML5新标签：
IE8/IE7/IE6支持通过document.createElement方法产生的标签，
可以利用这一特性让这些浏览器支持HTML5新标签，
浏览器支持新标签后，还需要添加标签默认的样式：

### 12.请描述一下 cookies，sessionStorage 和 localStorage 的区别？

cookie在浏览器和服务器间来回传递。 sessionStorage和localStorage不会
sessionStorage和localStorage的存储空间更大；
sessionStorage和localStorage有更多丰富易用的接口；
sessionStorage和localStorage各自独立的存储空间；

### 13.如何实现浏览器内多个标签页之间的通信?

调用localstorge、cookies等本地存储方式
