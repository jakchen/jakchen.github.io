---
layout: post
title:  "CSS布局4-居中布局解决方案"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

## 水平居中：

### 1.inline-block + text-align
```css
inline-block + text-align
  子元素：inline-lock
  父元素：text-align:center;
```

### 2.table + margin
```css
  子元素：display：table
  margin：0 auto;
```

### 3. absolute + transform
```css
 父元素：position:relative

 子元素：position:absolute
 left:50%;
 transform:translateX(-50%);
```

### 4. flex + justify-content
```css
  父元素：display:flex;  justify-content:center;
```

### 5. 父元素：display:flex;
```css
  父元素：display:flex;
  子元素：margin：0 auto;
```

## 垂直居中：
### 1. table-cell + vartical-align
```css
  父元素：display:table-cell;
  vertical-clign:middle;
```

### 2. absolute + transform
```css
  父元素：position:relative;

  子元素:position:absolue;
   top:50%;
    transform:translateY(-50%);
```

### 3. flex + align-items
```css
  父元素：display:flex;
  align-items:center;
```

## 水平垂直居中:
### 1. inline-block + text-align + table-cell + vartical-align
```css
先水平居中:
  子元素：inline-lock
  父元素：text-align:center

再垂直居中：
  父元素：display:table-cell;
  vartical-align:middle;
```

### 2. absolute + transform
```css
  父元素：position:relative;

  子元素：position:absolute;
   left:50%;
   top:50%;
   transform:translate(-50%,-50%);
```

### 3. flex + justify-content + align-items
```css
  父元素：display:flex;
   justify-content:cennter;
   align-items:center;
```
