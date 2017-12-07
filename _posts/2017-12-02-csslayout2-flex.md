---
layout: post
title:  "CSS布局2-伸缩布局盒模型flex"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

## 伸缩布局盒模型flex
  Flex布局的主要思想是让容器能使其子元素的宽高（或其他属性）能够以最好的方式去填充可用空间（主要是去适应不同的设备跟分辨率）。

  Flexbox布局常用于小的应用程序组件之中
  能动态修改子元素宽高，以满足在不同尺寸屏幕下的恰当布局




![image]({{ site.url }}/assets/flex2.jpg)


  设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。

- 弹性容器flex container
- 弹性元素flex item，弹性元素:在文档流中的子元素
- 主轴main axis
- 副轴cross axis


### 创建容器:display:flex;


###    一：有六个属性设置在box父容器上，来控制子元素的显示方式；
```css
flex-direction
flex-wrap
flex-flow
justify-content
align-items
align-content
```
特性
#### flex-direction
——弹性元素排列方向，决定主轴的对齐方向
```css
flex-direction:row|row-reverse|column| column-reverse
  /*
  row（默认值）:主轴为水平方向，起点在左端。
  row-reverse:主轴为水平方向，起点在右端。
  column:主轴为垂直方向，起点在上沿。
  column-reverse:主轴为垂直方向，起点在下沿。
  */
```

#### flex-wrap
——子元素超过一行，如何换行
```css
flex-wrap:nowrap|wrap|wrap-revers
  /*
  nowrap（默认值）：默认不换行。
  wrap：换行，第二行在第一行下面，从左到右
  wrap-reverse：换行，第二行在第一行上面，从左到右；
  */
```

#### flex-flow简写属性
——<flex-direction>|<flex-wrap>两个属性的简写
```css
flex-flow:<flex-direction>|<flex-wrap>
  /* 建议使用， 默认是 row  nowrap */
```

####  justify-content
——子元素在主轴对齐方式
```css
justify-content:flex-start;/*（默认值）：左对齐*/

  flex-start /*（默认值）：左对齐*/
  flex-end /*右对齐*/
  center /*居中*/
  space-between /*两端对齐，项目之间的间隔都相等。*/
  space-around /*每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。*/
```

#### align-items
——交叉轴如何对齐
```css
align-items:stretch

  flex-start /*交叉轴的起点对齐。*/
  flex-end /*交叉轴的终点对齐。*/
  center /*交叉轴的中点对齐。*/
  baseline /*项目的第一行文字的基线对齐。*/
  stretch /*（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。*/
```

#### align-content
——该属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。(设置cross-axis方向上 行 对齐方式)
```css
align-content:stretch;

  flex-start /*与交叉轴的起点对齐。*/
  flex-end /*与交叉轴的终点对齐。*/
  center /*与交叉轴的中点对齐。*/
  space-between /*与交叉轴两端对齐，轴线之间的间隔平均分布。*/
  space-around /*每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。*/
  stretch /*（默认值）：轴线占满整个交叉轴。*/
```

### 二   有六个属性设置在子元素项目上：
```css
order
flex-grow
flex-shrink
flex-basis
flex
align-self
```

#### order
——默认（0） 值越小越靠前，

#### flex-grow
——放大比例,默认是0,当有放大空间的时候，值越大，放大的比例越大

#### flex-shrink
——缩小比例  默认是1  值越大，缩小的时候比例越小；负值对该属性无效。

#### flex-basis
——设置flex item的初始宽/高

(定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。)
```css
flex-basis:main-size|<width>
```

#### flex简写属性
——该属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

#### align-self
——设置单个flex item在cross-axis方向上对齐方式
```css
align-self:auto|flex-start|flex-end|center|baseline|stretch
```