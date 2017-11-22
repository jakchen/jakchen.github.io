---
layout: post
title:  "问题待整理集合"
categories: 待整理
tags: 待整理
author: jakchen
---
* content
{:toc}
[emmet使用教程](http://docs.emmet.io/cheat-sheet/)
```
<html lang="zh-CN">
<meta charset="UTF-8" />
<!-- 这两个标签可以使用 -->
<base target="_blank" />
<!-- 在head标签里设置base，定义页面基准链接 -->
<link rel="shortcut icon" href="/favicon.ico" type="image/x-icon" />
<!-- 导入网站ico -->
```




```
<meta content="always" name="referrer">？？
```

[meta content="always"参考链接](http://blog.csdn.net/a3025056/article/details/71216097)
```
<meta name="referrer">
content 属性可取的值：
no-referrer 不要发送 HTTP Referer 首部。
origin 发送当前文档的 origin。 no-referrer-when-downgrade 当目的地是先验安全的(https->https)则发送 origin 作为 referrer ，但是当目的地是较不安全的 (https->http)时则不发送 referrer 。这个是默认的行为。
origin-when-crossorigin 在同源请求下，发送完整的URL (不含查询参数) ，其他情况下则仅发送当前文档的 origin。 unsafe-URL 在同源请求下，发送完整的URL (不含查询参数)。
```
```
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />？？
这是一个，文档兼容模式的定义。
Edge 模式告诉 IE 以最高级模式渲染文档，也就是任何 IE 版本都以当前版本所支持的最高级标准模式渲染，避免版本升级造成的影响。简单的说，就是什么版本 IE 就用什么版本的标准模式渲染
```

```
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```
使用以下代码强制 IE 使用 Chrome Frame 渲染
```
<meta http-equiv="X-UA-Compatible" content="chrome=1">
```
提示 IE 用户安装 Google Frame Google 官方提供了对 Google Frame 插件安装情况的检测，这里直接调用方法即可，如果检测到 IE 并未安装 Google Frame，则弹出对话框提示安装。
```
<script src="http://ajax.googleapis.com/ajax/libs/chrome-frame/1/CFInstall.min.js"></script><script>CFInstall.check();</script>
```
最佳的兼容模式方案，结合考虑以上两种：
```
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```
```
<link rel="dns-prefetch" href="//f.3.cn" />
<link rel="dns-prefetch" href="//d.jd.com" />
<link rel="dns-prefetch" href="//ai.jd.com" />
<link rel="dns-prefetch" href="//ch.jd.com" />？？
```
前端优化系列之一：DNS预获取 dns-prefetch 提升页面载入速度 [dns-prefetch 参考链接](https://www.cnblogs.com/lhm166/articles/6073787.html)
```
<meta name="renderer" content="webkit" />？？
```
[参考链接](http://blog.csdn.net/adc_god/article/details/51531263)
content的取值为webkit,ie-comp,ie-stand之一，区分大小写，分别代表用webkit内核，IE兼容内核，IE标准内核。

- 若页面需默认用极速核，增加标签：`<meta name="renderer" content="webkit">`
- 若页面需默认用ie兼容内核，增加标签：`<meta name="renderer" content="ie-comp"> `
- 若页面需默认用ie标准内核，增加标签：`<meta name="renderer" content="ie-stand">`

```
sublime3 htmlbeautify插件怎么用？
推荐使用HTML-CSS-JS Prettify，这个插件能格式化 HTML, CSS, JavaScript。这个插件需要配合node的安装路径，格式化代码的快捷键是crtl+shift+h 而htmlbeautify没用过，不知道是不是也是依赖node，快捷键是ctrl+alt+q
 ```
 Dreamweaver代码自动缩进对齐 一般情况下，我们用DW写的html或者css代码都计较混乱，难以阅读，即使刚开始很在意代码的可读性，但是等到所使用的标签越来越多，嵌套越来越深，这时我们已经很难去掌控html代码的格式问题了。废话不多说：
 1. 第一步：依次点击菜单栏的 “编辑” – “首选参数” – “代码格式” （注：Dreamweaver版本不同可能会有些许差异）
 2. 第二步：格式设置你可以参考我的，也可以根据个人喜好设置：
 3. 第三步：依次点击菜单栏的 “命令” -“应用源格式”。 如果查看其他人写好的源代码，需要缩进对齐的话，点击如图的按钮：


 [去除inline-block元素间间距的N种方法??](http://www.zhangxinxu.com/wordpress/2012/04/inline-block-space-remove-%E5%8E%BB%E9%99%A4%E9%97%B4%E8%B7%9D/)
