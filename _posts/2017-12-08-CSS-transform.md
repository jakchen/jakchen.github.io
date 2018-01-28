---
layout: post
title:  "CSS变形1"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

## 变形
  transform:none|<transform-function> [,<transform-function>]
    可用于内联元素和块元素，多个变形函数，用空格分开
    例如：transform:translate(50%) rotate(45deg);





###  2d变形 translate() scale() rotate() skew()

    变形函数：5个
    translate(50px,20%) 偏移
      translateX():
      translateY():

    scale(<number>[,number]?) 缩放 scale(0.8,1.5)
      scaleX(<number>);
      scaleY(<number>);

    rotate(45deg) 旋转 正负值

    skew(<angle>[,<angle>]?) 倾斜 skew(30deg,30deg)
      skewX:(<angle>);
      skewY:(<angle>);

    matrix() 矩阵变形

    默认情况，变形的原点在元素的中心的。
    旋转、缩放、倾斜都可以重置原点

    设置坐标轴心transform-origin:[left|center|right|top|bottom|<%>|<length>]

      transform-origin:50% 50%;默认值
      transform-origin:0 0;  x0，y0
      transform-origin:20%;  x20%,y50%
      transform-origin:right 50px 20px;  x y50px,z20px,
      transform-origin:top right 20px;

###  3d变形 translate3d() scale3d() rotate3d()
        translateZ(length) 正负值
        scaleZ(<number>)
        rotaleX(<angle>)
        rotaleY(<angle>)
        rotaleZ(<angle>)

    perspective:none|<length> 透视
      取值越小，3D效果越明显 perspective属性都应用在父元素上
    perspective-origin：[left|center|right|top|<%>|<length>]
      透视位置 定义父元素 需要与perspective属性结合起来使用，该属性允许您改变 3D 元素的底部位置。
      perspective-origin:50% 50%;默认值
      perspective-origin:left bottom;
      perspective-origin:50% -800px;
      perspective-origin:right;

    translate3d(tx,ty,tz) 3d移动
      translateZ(length) 正负值

      例如：transform:translate3d(10px,20%,50px);

    scale3d(<number>,<number>,<number>);3d缩放
      scaleZ(<number>)

      transform:scale3d(1.2,1.2,1)

    rotate3d(<number>,<number>,<number>,<angle>);3d旋转
      rotaleX(<angle>)
      rotaleY(<angle>)
      rotaleZ(<angle>)

      transform:rotate3d(1,0,0,45deg)

###    旋转元素背面不可见backface-visibility:visible 可见| hidden
      定义当元素不面向屏幕时是否可见。

### 保留3d空间transform-style:flat|preserve-3d flat扁平化（默认值）|保留3d空间
    应用在3D变换的兄弟元素们的父元素