---
layout: post
title:  "CSS布局1-盒模型&定位"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

## 盒模型
### 盒子类型
```css
inline | block | inline-block | inline-table /*行内表格*/|list-item /*列表*/
```





### 盒子模型CSS属性
```css
margin
border
padding
content
width
height
```

#### 内边距
```css
padding
padding-bottom
padding-top
padding-left
padding-right
```

#### 外边距
```css
margin
margin-top
margin-bottom
margin-left
margin-right
```

**外边距合并**：外边距合并就是一个叠加的概念

### 指定针对元素的宽度和高度的计算方法
```css
 box-sizing:border-box/contnet-box
```

### 对盒子中容纳不下的内容的显示
```css
overflow:visible;
  hidden
  scroll
  auto
  visible/*(默认)*/
  no-diaplay
  no-content
  overflow-x
  overflow-y
```

### 自由缩放属性

  resize 用来改变元素尺寸大小 元素须使用

### overflow属性
```css
overflow:none;
  none
  both
  horizontal/*(仅改宽)*/
  vertical/*(仅改高)*/
  inheiit
```

### 轮廓

 突出元素作用,用于元素获取到焦点或被激活时
```css
outline:outline-color, outline-style, outline-width

outline-color
outline-style:double;
outline-width

outline-style:none | dotted | dashed | solid | double | groove | ridge | inset | outset | inherit

outline-width:thin | medium | thick | <length> | inherit
```

### 对盒子使用阴影
```css
box-shadow
```

## 布局：
```css
display:block|inline|inline-block|none

  block:/*默认宽度为父元素宽度，可设置宽高，换行显示*/
  inline:/*默认宽度为内容宽度，不可设置宽高，同行显示*/
  inline-block:/*默认宽度为内容宽度，可设置宽高，同行显示，整块换行*/
  none:/*设置元素不显示,不占据文档位置*/
visibility:hidden;/*仍占据文档位置*/
```

## 定位：
```css
position:top|right|bottom|left|z-index;
/*设置y元素边缘距离参照物边缘的距离，
z-index设置Z轴上的排序,大在前面；z-index栈*/

position:static|relative|absolute|fixed
/*
relative:相对定位,仍在文档流中，参照物为元素本身;使用场景：作为绝对定位元素的参照物
absolute：绝对定位，默认宽度为内容宽度，脱离文档流，参照物为第一个定位祖先/根元素;使用场景：轮播头图
fixed：固定定位，默认宽度为内容宽度，脱离文档流，参照物为视窗
*/

```
```css
float:left|right
/*
默认宽度为内容宽度，脱离文档流，向指定方向一直移动;float的元素在同一文档流;
float元素半脱离文档流：对元素，脱离文档流，对内容，在文档流
*/
clear:both|left|right
/*
应用于后续元素、块级元素。使用：
1. 加空白元素(clear:both;height: 0;overflow: hidden;visibility: hidden;)，
2. 父元素clearfix(.clearfix:after{content:'.';display: block;clear: both;height: 0;overflow: hidden;visibility: hidden;})
*/
```