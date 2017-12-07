---
layout: post
title:  "CSS布局6-响应式设计～待完善"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

## 响应式Responsive设计
  媒体类型 all screen print
```html
<link type="text/css" rel="stylesheet" href="style.css" media="only screen and (max-width:640px)">
@media screen and (max-width: 600px) {}
------------------------------------------

@media (min-width: 768px) {}
@media (min-width: 992px) {}
@media (min-width: 1200px) {}
------------------------------------------

<meta name="viewport" content="width=device-width, initial-scale=1">

```
## 响应式图片？
```css
img{max-width:100%;}
```