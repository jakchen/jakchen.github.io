---
layout: post
title:  "CSS字体2-文本属性"
categories: CSS
tags: CSS
author: jakchen
---
* content
{:toc}

使用文本属性，可以控制文本的颜色、字符间距，对齐文本，装饰文本，对文本进行缩进等。





## 缩进文本
```css
p{text-indent:3em;}
```
通过使用text-indent，可以将元素的第一行缩进一个指定长度，甚至是负值。一般的，可以将其应用到所有块级元素上，但不能应用到行内（inline）元素上，图像之类的替换元素也不行。不过，如果一个块级元素的首行中有一个图像，它也会跟着其余文本移动。
```css
p{
    padding:4em;
    text-indent:-4em;
}
```

上述代码可以实现段落的“悬挂缩进”，即第一行悬挂在余下元素的左边。设置内边距的原因是防止向左超出浏览器的边界。
text-indent可以使用所有长度单位（包括百分数）。
```css
div{width:400px;}
p{text-indent:10%;}
```

百分数要相对于缩进元素父元素的宽度。上例中，text-indent设为10%，所影响元素的第一行会缩进其父元素宽度的10%。

text-indent可以继承。

## 水平对齐

text-align，它会影响一个元素中文本行相互之间的对齐方式。它有4个关键字：left（左对齐），right（右对齐），center（中央对齐），justify（两端对齐）。只能应用于块级元素上。可以继承。text-align不会控制元素的对齐，只是影响其内部内容。

其中，center要通过设置元素的外边距来实现。justify中，文本行的左右两端都放在父元素的内边界上，然后，通过调整字母和单词之间的间隔实现每行的长度相等。要注意的是，实际上是由用户代理来决定两端对齐文本如何拉伸。

## 垂直对齐

### 行高

line-height是指文本行基线之间的距离，它确定了将各个元素框的高度增加或减少多少。实际上，line-height控制了行间距，line-height值和字体大小之差就是行间距。在应用到块级元素时，它定义了元素文本基线之间的最小距离。

### 工作文本行

文本行中的每个元素都会生成一个内容区，它的大小是由字体大小决定的，这个内容区会生成一个行内框（inline box）。如果不存在其他因素，这个行内框就等于生成区。将line-height的值减去font-size的值（可能是负值），再除以2，分别应用到内容区的顶部和底部，结果就是行内框。可以包含最高行内框的顶端和最低行内框的底端的最小框就是行框。

### 指定line-height值

如果使用normal，用户代理会自己计算，结果通常是字体大小的1.2倍。em、ex、百分数都相对于元素的font-size值计算。可以使用长度单位。

### 行高和继承

line-height从父元素继承时，要根据父元素计算，而不是根据子元素计算。
```css
body{font-size:10px;}
div{line-height:1em;}
p{font-size:18px;}
```
```html
<div>
<p>adasas<br>asasdas</p>
</div>
```
如上例，则文本间会发生重叠。因为line-height为10px，而font-size为18px，相减的结果为负值。解决方案如下：
```css
body{font-size:10px;}
div{line-height:1;}
p{font-size:18px;}
```

通过指定一个数来设置缩放因子，则各元素会根据自己的font-size计算line-height。

### 垂直对齐文本

vertical-align。只应用于行内元素和替换元素，不能继承。接受8个关键字：baseline（默认值）、sub、super、bottom、text-bottom、middle、top、text-top。
1. 基线对齐
baseline要求一个元素的基线与其父元素的基线对齐。如果一个垂直对齐元素没有基线，则其底端和其父元素的基线对齐。

2. 上标和下标
sub声明会使元素变成下标，即其基线或底端（替换元素）相对于父元素的基线降低。super恰好相反。需要注意的是，上标或下标的文本大小不会改变。

3. 底端对齐
bottom将元素行内框的底端与行框的底端对齐。text-bottom是指行内文本的底端，替换元素或其他任何非文本类型的元素都会忽略这个值。对于这些元素，将考虑一个“默认框”，其由父元素的font-size得到，要对齐的元素的行内框的底端再与这个默认框的底端对齐。

4. 顶端对齐
top的作用和bottom相反，类似的，text-top的作用也和text-bottom相反。对齐的具体位置取决于行内有哪些元素，它们有多高，以及父元素font-size的大小。
5. 居中对齐
middle往往应用于图像。它把行内元素框的中点与父元素的基线上方0.5ex处的一个点对齐，这里的0.5ex是相对于父元素的font-size定义o(╯□╰)o（感觉没必要这么细致吧~~）

6. 百分数
使用百分数不能模仿图像的middle对齐。如果为vertical-align设置一个百分数，会把元素的基线或底端相对于父元素的基线升高或降低指定的量（指定的百分数要计算为该元素line-height的值，而不是相对于其父元素的line-height）。正百分数使元素升高，负百分数使元素降低。

7. 长度对齐
可以使用长度单位来升高或降低元素。

需要注意的是，所有垂直对齐的元素都会影响行高，这意味着不会发生串行或重叠现象。

## 字间隔和字母间隔

### 字间隔

word-spacing接受正值或负值，可用任意长度单位，用于改变字之间的间隔。关于字的定义，暂且简单地理解为“由非空白字符组成的串，并由某种空白符包围。”
```css
p{word-spacing:0.5em;}
```
### 字母间隔

letter-spacing与word-spacing类似，区别在于前者改变的是字母或字符之间的距离。可以用它来突出强调效果。
```css
h1{letter-spacing:0,25em;}
```

## 文本转换

text-transform，可接受的值有uppercase（将文本转换成全大写）、lowercase（全小写）、capitalize（只对每个单词的首字母大写）、none（不变）。有继承性。

## 文本装饰

text-decoration，可接受的值有：underline（下划线）、overline（上划线）、line-through（贯穿线）、blink（文本闪烁）、none（去掉所有文本装饰）。无继承性。
还可以设置划线颜色和样式：
text-decoration-color
text-decoration-style
例如，想去掉链接的下划线：
```css
a{text-decoration:none;}
```
可以在一个规则中结合多种装饰：
```css
a{text-decoration:underline overline;}
```
要注意的是，如果用两个不同的装饰与同一个元素相匹配，则胜出规则的值会完全替代另一个值：
```css
h2.try{text-decoration:line-through;}
h2{text-decoration:underline overline;}
```

则所有class值为try的h2只有贯穿线，而没有上划线和下划线。

关于文本装饰的继承性

规范指出，text-decoration没有继承性，但事实上子元素能够“继承”父元素的文本装饰：
```css
p{text-decoration:underline;}
```
```html
<p>xxxxxx<span>xxxx</span>xxx</p>
```

则会发现，span中的文本下也有下划线，即使加一条规则：
```css
span{text-decoration:none;}
```
你会发现，没有任何改变。

有些浏览器会违反规范，去掉子元素中的文本装饰，因为这是大多数创作人员所希望的。有一种方法可以“去掉”子元素中的文本装饰：在一个元素上使用文本装饰意味着整个元素都有相同的颜色装饰，即使子元素有不同的颜色，因此可以显式声明子元素的装饰,使其与元素匹配：
```css
p{text-decoration:underline;color:black;}
span{text-decoration:underline;color:gray;}
```

则span中的文本下会有灰色的下划线，“覆盖”了父元素黑色的下划线。

## 处理空白符

white-space会影响用户代理对文档中的空格、换行、tab字符的处理。无继承性。
```css
p{white-space:normal;}
```
这个规则告诉浏览器按平常的做法去做：丢掉多余的空白符，换行符会转换成空格，且一行中多个空格的序列也会转换成一个空格。
```css
p{white-space:pre;}
```
则空白符不会被忽略，包括回车。
```css
p{white-space:nowrap;}
```
该规则会防止元素中的文本换行，除非使用<*br>*元素。
```css
p{white-space:pre-warp;}
```
则文本中的空白符和换行符都会被保留。
```css
p{white-space:pre-line;}
```
则空白符序列会被合并，但换行符会被保留。


## 文本方向

direction，可接受的值有：ltr,rtl。例如：
```css
*:lang(ar),*:lang(he){direction:rtl;}
```