---
layout: post
title:  "CSS字体1-字体系列&大小&加粗&变形"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

设置字体属性是样式表的最常见用途之一。


CSS字体处理中最复杂的是字体系列（font-family）匹配和字体加粗（font-weight）匹配，其次是字体大小（font-size）计算。




## 字体系列

由于种种原因，相同的字体可能会有不同的称呼。CSS定义了5种通用字体系列：
```
serif
成比例，且有上下短线。成比例是指字体中的字符根据其不同的大小会有不同的宽度。上下短线是指字符笔划末端的装饰。serif字体的例子包括Times、Georgia、New Century Schoolbook。

Sans-serif
成比例，没有上下短线。例子包括Helvetica、Geneva、Verdana、Arial、Univers。

Monospace
不成比例，通常用来模拟打字机打出的文本。所有字符的宽度都相同，上下短线可有可无。例子包括Courier、Courier New、Andale Mono。

Cursive
模拟人的手写体。通常，它们主要由曲线和serif字体中没有的笔划装饰构成。例子包括Zapf Chancery、Author、Comic Sans。

Fantasy
这类字体无法用任何特征去定义，但我们也很难把它轻易划归到另外一种字体中。例子包括Western、Woodblock、Klingon。
```
### 使用通用字体系列
```css
body{font-family:serif;}
```
由于没有指明具体字体，因此用户代理会选择其中一种应用到body元素，同时由于继承性，body中的所有元素也会有这种应用，除非有更特殊的选择器将其覆盖。

### 指定字体系列
```css
h1{font-family:Georgia;}
```
如果用户代理上Georgia字体不可用，则其很可能会使用自己的默认字体，显示效果可能会和我们期望的相差甚远。
```css
h1{font-family:Georgia,serif;}
```
如果在最后面加上了serif的话，则用户代理在找不到Georgia的情况下会从serif中选择一种，虽然显示结果不一样，但看上去不会差很多。
```css
h1{font-family:Times,'New Century Schoolbook',Georgia,serif;}
```
用户代理会按照这个顺序查找第一个能用的字体。

### 关于引号

注意到上面的最后一个例子，有个字体名加上了单引号。CSS规范中指出：当一种字体名中有空格或是类似$、#的符号时，建议加上引号。否则，用户代理可能会选择忽略它。唯一必须加引号的是与所接受关键字匹配的字体名，如名为”cursive”的字体，就必须加引号。通用字体系列在表示一组字体时不需要加引号，否则会被视为一种与其匹配的特定的字体名。双引号或单引号都行。但是把font-family放在style中时，则需要使用该属性本身未曾使用的引号，例如用双引号把font-family括起来，则里面只能用单引号。

## 字体加粗
```css
p{font-weight:bold;}
```
上述声明指出p元素应当使用粗体来显示，然而事实上，是使用了字体的一种粗体变形来显示。例如p使用Times字体，则粗体部分实际上使用的是TimesBold字体。

加粗如何起作用

关键字100~900对应了9级加粗度。实际上，它们本身并没有固定的加粗度。CSS规范指出：每个数对应一种加粗度，至少与前一个数对应的加粗度相同。一般的，这些数被定义为与一些常用变形名等价，如400对应于normal，700对应于bold。如果给定的字体系列中定义的加粗度少于9种，则用户代理还需要做一些工作：

1. 如果未指定500的加粗度，则其加粗度与400相同；

2. 如果未指定300的加粗度，则为之选一种比400更细的字体，如果没有则等同于400。这种情况同样适用于200,100；

3. 如果未指定600的加粗度，则为之选一种比400更粗的字体，如果没有则等同于500。这种情况同样适用于700,800,900。

显然，font-weight是可以继承的。

## 让字体更粗

如果把一个元素的加粗设置为bolder，则用户代理首先要计算其继承的父元素的加粗度，然后选一个数，它对应于比继承值更粗的加粗字体，而且在满足这条件的所有数中，选一个最小的。如果没有可选的字体，则选下一个更大的数值作为加粗度，900不变。
例如（对于某种字体）：
```css
p{font-weight:normal;}
p em{font-weight:bolder;}/*700*/

p{font-weight:bold;}
p em{font-weight:bolder;}/*800*/

p{font-weight:100}
p em{font-weight:bolder;}/*400*/
```

## 让字体更细（lighter）是一样的。

## 字体大小

字体本身有一个em框，它指示没有额外行间距（line-height）设置字体时基线间的距离。因此，font-size的作用就是为给定字体的em框提供一个大小，而不能保证字符实际显示的就是这种大小。

### 绝对大小

font-size有7个绝对大小值：`xx-small`、`x-small`、`small`、`medium`、`large`、
`x-large`、`xx-large`。它们并没有明确的定义，而是相对的定义。根据CSS1规范，两个相邻的绝对大小值的缩放因子是向上1.5，向下0.66。实际上未必，一方面是由于不同的用户代理，另一方面是由于CSS2中的缩放因子可能介于1.0~1.2。

### 相对大小

关键字smaller和larger。在计算其相对于父元素的字体大小时会使用计算绝对大小时的缩放因子，且相对大小值不必限制在绝对大小范围内。

百分数和大小

百分数值和相对大小关键字类似，也是根据从父元素继承来的值进行计算，只不过可以进行更加细致的控制。也可以使用em，1em等于当前的字体大小，1em=100%。

字体大小和继承

font-size继承的是计算值而不是百分数。在计算值是小数时，有的用户代理会对其取整，从而在多重继承（例如列表嵌套）时由于误差累积造成较大的误差。

使用长度单位

可以使用一些长度值来设置font-size。例如：
```css
p.one{font-size:36pt;}
p.two{font-size:3pc;}
p.three{font-size:0.5in;}
p.four{font-size:1.27cm;}
p.five{font-size:12.7mm;}
```

以上所有声明都是等价的。
还可以通过像素来设置font-size。特别是当一个web页面上既有文本又有图像时，理论上可以将文本设置为与图像等高。

## 字体的风格

font-style的关键字有normal,italic,oblique。要注意的是italic和oblique的区别：italic（斜体）是一种单独的字体，对每个字符的结构都有一些变化，以显示外观的变化；而oblique（倾斜）则是正常竖直文本的倾斜版本。事实上，并不是每种字体都有italic和oblique两种变形，就算有，浏览器也未必能够区分它们。这时，如果没有italic而有oblique，则在需要使用前者的地方会使用后者；反过来不同，根据规范，用户代理可能不会把后者变成前者，它可能只是计算一个倾斜版本来生成oblique。

## 字体变形

font-variant有两个关键字：normal、small-caps。small-caps要求使用小型大写字母，如下图所示，采用了不同大小的大写字母：
```css
h1{font-variant:small-caps;}
h1 code{font-variant:normal;}
```
<h1>The Uses Of <code>font variant</code> On The Web</h1>

可见，大写字母会显示成更大的大写字母，小写字母会显示成小型的大写字母。

有些字体没有small-caps，CSS规范提供了两种方法：第一，用户代理自己缩放大写字母来生成small-caps；第二，统一使用大写字母，且大小相同。

## 拉伸和调整字体

由于长期没有浏览器理睬它们，CSS2.1中已将其删除o(╯□╰)o

## font属性

可以使用一种简写形式。例如：
```css
p{font:italic normal bold 36px/1.2 Verdana,sans-serif;}
```
下面详细分析上例。前三个属性是font-style、font-variant、font-weight，这三个属性是可选的，且没有顺序要求，如果是normal可以不写。最后两个是font-size、font-family，这两个是必选的，且顺序不能变，如果少了其中某个属性，则整个规则都是无效的，可能会被用户代理完全忽略。例如：
```css
p{font:italic 30px sans-serif;}/*No problem*/
p{font:normal 16px serif;}/*No problem*/
p{font:small-caps 1.5em;}/*Invalid*/
p{font:sans-serif;}/*Invalid*/
```

跟在font-size后面的是line-height，它也是可选的，根据font-size计算行高。但是一旦添加了，它就必须跟在font-size后面，且用斜线隔开。

适当地使用简写
```css
h1,h2,h3{font:italic small-caps normal 250% serif;}
h2{font:200% sans-serif;}
h3{font-size:150%;}
```

显示结果表明，h2既不是斜体，也不是小型大写字母。这是正确的，因为在使用简写font属性时，所有忽略的值都会被重置为默认值。而h3因为不是简写font，因此只会影响font-size。

使用系统字体

如果希望web页面结合用户操作系统的设置，就可以使用系统字体。例如：
```
caption
用于有标题的控件，如按钮。

icon
用于对图标加标签

menu
用于菜单

message-box
用于对话框

small-caption
用于对小控件加标签

status-bar
用于窗口状态条
```
利用这些值，可以创建基于web的应用，使之看上去非常像用户操作系统自带的应用。
```css
button{font:caption;}
```
系统字体可能会整体设置，不过，一旦设置了系统字体，就可以单独设置其中的一个属性，如：
```css
button{
      font:caption;
      font-size:36px;
}
```