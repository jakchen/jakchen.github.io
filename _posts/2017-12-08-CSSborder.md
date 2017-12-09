---
layout: post
title:  "CSS边框1"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

## 边框

border是围绕元素内容和内边距的一条或多条线，可以规定元素边框的样式、宽度和颜色。




### 边框与背景

CSS2.1规范指出：元素的背景是内容、内边距和边框区的背景。

### 边框的样式



可以定义多种样式：
```css
p{border-style: solid dotted dashed double;}
```
则为段落定义了四种边框样式：实线上边框、点线右边框、虚线下边框和一个双线左边框。依旧是top-right-bottom-left 的顺序。

### 定义单边样式
```
border-top-style、border-right-style、border-bottom-style、border-left-style
```
再举个栗子：
```css
p {border-style: solid solid solid none;}
p {border-style: solid; border-left-style: none;}
```

注意：如果要使用第二种方法，必须把单边属性放在简写属性之后。因为如果把单边属性放在 border-style 之前，简写属性的值就会覆盖单边值 none。

### 边框的宽度

border-width。可以指定长度值，或是关键字：thin、medium、thick。CSS并没有定义三个关键字的确定值，这取决于用户代理。
```css
p{border-width:10px;}
div{border-width:thick;}
```

当然可以定义单边宽度：
```
border-top-width、border-right-width、border-bottom-width、border-left-width
```
```css
p {border-style: none; border-width: 50px;}
```
上述情况下，不仅边框的样式没有了，其宽度也会变成 0。因为如果边框样式为 none，即边框根本不存在，那么边框就不可能有宽度，因此边框宽度自动设置为 0，而不论原先定义的是什么。
例如：
```css
h1 {border-width: 20px;}
```
由于 border-style 的默认值是 none，如果没有声明样式，就相当于 border-style: none。因此，所有 h1 元素都不会有任何边框。所以，如果希望边框出现，就必须声明一个边框样式。

### 边框的颜色

border-color，一次可以接受最多4个颜色值。
```css
p {border-color: blue rgb(25%,35%,45%) #909090 red;}
```
值复制规则仍会适用于此。

注意：默认的边框颜色是元素本身的前景色。如果没有为边框声明颜色，它将与元素的文本颜色相同。另一方面，如果元素没有任何文本，假设它是一个表格，其中只包含图像，那么该表的边框颜色就是其父元素的文本颜色（因为 color 可以继承）。

然后是定义单边颜色：
```
border-top-color、border-right-color、border-bottom-color、border-left-color
```
```css
h1 {border-color: black;border-right-color: red;}
```
### 透明边框

CSS2 引入了边框颜色值 transparent。这个值用于创建有宽度的不可见边框。
```css
a{border-color:transparent;}
```
从某种意义上说，利用 transparent，使用边框就像是额外的内边距一样；此外还有一个好处，就是能在你需要的时候使其可见。这种透明边框相当于内边距，因为元素的背景会延伸到边框区域（如果有可见背景的话）。