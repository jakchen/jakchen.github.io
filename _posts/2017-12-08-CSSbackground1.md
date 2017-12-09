---
layout: post
title:  "CSS背景1"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

## 前景色

一般来说，前景是元素的文本，还包括边框。最简单的方法是使用color属性改变文本颜色，同时还会影响边框的颜色。要覆盖的话，可以使用border-color。没什么好说的~~




## 背景

元素的背景区包括前景之下直到边框外边界的所有空间，因此，内容区和内边距都是背景的一部分，且边框画在背景之上。

## 背景色

关键字：background-color。可接受color、transparent（默认值），不能继承。

## 背景图像

关键字：background-image。接受url，没有继承性，可应用于所有元素。
可以和背景色结合使用，这样当背景图像无法加载时会显示背景色，或利用背景色填充未被背景图像覆盖的地方。

### 有方向的重复

关键字：background-repeat。可接受：
- repeat-x（水平方向平铺）、
- repeat-y（竖直方向平铺）、
- no-repeat（不重复）、
- repeat（水平竖直方向平铺）。

无继承性。初始值为repeat。

## 背景定位

关键字：background-position。可接受：
- left、
- right、
- center、
- bottom、
- top。

默认值为：0% 0%。

应用于块级元素和替换元素，无继承性。
最多接受两个值：一个对应水平方向，另一个对应竖直方向。
```css
p{
    background-iamge:url(xxx);
    background-repeat:no-repeat;
    background-position: top right;
 }
```

则在每个段落的右上角都会有一个图像。
也可以利用百分数描述位置。
```
top==top center==50% 0%
bottom==bottom center==50% 100%
left==left center==0% 50%
right==right center==100% 50%
center==center center==50% 50%
```
如果只设置了一个百分值，则视之为水平位置，竖直位置默认为50%。

还可以使用长度值。
```css
p{background-position:10px 20px;}
```
则图像从左上角向右偏移10px，向下偏移20px。
百分数和长度值可以结合使用：
```css
p{background-position:100% 23px;}
```
还可以使用负值,假设图像300像素高、300像素宽：
```css
p{background-repeat:no-repeat;}
p{background-position:-200px -200px;}
```

则会在左上角显示图像的右下1/3的部分。

利用图像位置（默认是在左上角）和图像重复（默认全铺）就可以在指定位置放置图像了。

## 关联

关键字：background-attachment。可接受：scroll（默认值）、fixed。无继承性。
通过使用fixed，可以声明图像相对于可视区是固定不动的（改变浏览器窗口的大小，可视区可能会改变，从而图像的位置可能会跟着改变。但是背景仍然是只在其包含元素中可见）。而scroll则声明图像会随着文档滚动。

## 简写

可以使用简写形式background。顺序不重要，不过要注意：如果background-position有两个值，必须一起出现，且若是长度或是百分数，必须水平在前竖直在后。缺少的属性为默认值（这可能会覆盖之前的规则，尽管创作人员并不想这么做）。