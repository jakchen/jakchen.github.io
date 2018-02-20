---
layout: post
title:  "开始使用 jQuery(4)-jQuery中的DOM操作"
categories: jQuery
tags: jQuery
author: jakchen
---
* content
{:toc}

## DOM操作分类

一般来说，DOM操作分为3个方面，即：

- DOM Core(核心)
- HTML-DOM
- CSS-DOM




### 1.DOM Core

DOM Core 并不专属于 JavaScript，任何一种支持 DOM 的程序设计语言都可以使用它。它的用途并非仅限于处理网页，也可以用来处理任何一种使用标记语言编写出来的文档，如 XML。

例如：
- 使用 DOM Core 来获取表单对象的方法：
```javascript
document.getElementsByTagName("form")
```
- 使用 DOM Core 来获取某元素的 src 属性的方法：
```javascript
element.getAttribute("src")
```
此外还有：`getElementById()`、`setAttribute()`等

### 2.HTML-DOM

在使用 JacaScript 和 DOM 为 HTML 文件编写脚本时，有许多专属于 HTML-DOM 的属性。HTML-DOM 的出现甚至比 DOM Core 还要早，它提供了一些更简明的记号来描述各种 HTML 元素的属性。

例如：
- 使用 HTML-DOM 来获取表单对象的方法：
```javascript
document.form;
```
- 使用 HTML-DOM 来获取某元素的 src 属性的方法：
```javascript
element.src;
```

**可以发现：获取某些对象、属性既可以用 DOM Core 来实现，也可以使用 HTML-DOM 来实现。相比较而言 HTML-DOM 的代码通常比较简短，不过它只能用来处理 Web 文档。**

### 3.CSS-DOM

CSS-DOM 是针对 CSS 的操作。在 JacaScript 中，CSS-DOM 技术的主要作用是获取和设置 style 对象的各种属性。通过改变 style 对象的各种属性，可以使网页呈现出各种不同的效果。

例如：
- 设置某元素的 style 对象字体颜色的方法：
```javascript
element = document.getElementById("hehe");
element.style.color="red";     //css-dom
```
```javascript
$("hehe").css("color","red");  //jquery
```

## 1.查找节点

```html
<p title="选择你最喜欢的水果." >你最喜欢的水果是?</p>
<ul>
  <li title='苹果'>苹果</li>
  <li title='橘子'>橘子</li>
  <li title='菠萝'>菠萝</li>
</ul>
```

### 1.查找元素节点

- 获取元素节点并打印出它的文本内容，jQuery 代码如下：
```javascript
var $li = $("ul li:eq(1)");   // 获取<ul>里第2个<li>节点
var li_txt =  $li.text();     // 输出第2个<li>元素节点的文本内容
alert(li_txt);                //打印文本内容
```

### 2.查找属性节点

利用 jQuery 选择器查找到需要的元素之后，就可以使用 `attr()` 方法获取它的各种属性的值。`attr()` 方法的参数可以是一个，也可以是两个。当参数是一个时，则是要查询的属性的名字，例如：

- 获取属性节点并打印出它的文本内容，jQuery 代码如下：
```javascript
var $para = $("p");              // 获取<p>节点
var p_txt = $para.attr("title"); // 获取<p>元素节点属性title
alert(p_txt);                    ////打印title属性值
```

## 2.创建节点

在 DOM 操作中，常常需要动态创建 HTML 内容，使文档在浏览器里的呈现效果发生变化，并且产生各种各样的人机交互的目的。

### 创建元素节点

创建并插入节点完整代码如下：
```javascript
$(function(){
  var $li_1 = $("<li></li>");    //  创建第一个<li>元素
  var $li_2 = $("<li></li>");    //  创建第二个<li>元素

  var $parent = $("ul");   // 获取<ul>节点。<li>的父节点

  $parent.append($li_1);     // 添加到<ul>节点中，使之能在网页中显示
  $parent.append($li_2);     // 可以采取链式写法：$parent.append($li_1).append($li_2);
});
```

**下面是详细步骤的介绍：**
例如要创建两个 `<li>` 元素节点，并且要把它们作为 `<ul>` 元素节点的子节点添加到DOM节点树上。完成这个任务需要两个步骤。

1. 创建两个`<li>`新元素。
2. 将这两个新元素插入文档中。

第 (1) 个步骤可以使用 jQuery 的工厂函数 `$()` 来完成，格式如下：
```javascript
$(html);
```
`$(html)`方法会根据传入的 HTML 标记字符串，创建一个 DOM 对象，并将这个 DOM 对象包装成一个 jQuery 对象后返回。

首先创建两个<li>元素，jQuery代码如下：
```javascript
var $li_1 = $("<li></li>"); // 创建第一个<li>元素
var $li_2 = $("<li></li>"); // 创建第二个<li>元素
```

然后将这两个新元素插入文档中，可以使用jQuery中的 `append()` 等方法。

JQuery代码如下：
```javascript
var $parent = $(".nm_ul"); // 获取<ul>节点。<li>的父节点
$parent.append($li_1); // 添加到<ul>节点中，使之能在网页中显示
$parent.append($li_2); // 可以采取链式写法：$parent.append($li_1).append($li_2);
```

注意：
1. 动态创建的新元素节点不会被自动添加到文档中，而是需要使用其他方法将其插入文档中。
2. 当创建单个元素时，要注意闭合标签和使用标准的XHTML格式。<br>例如创建一个 `<p>`元素，可以用 `$("<p/>")` 或者 `$("<p></p>")` ，但不要使用 `$("<p>")` 或者大写的 `$("<P/>")`。

### 创建文本节点

如下面代码所示，创建文本节点就是在创建元素节点时直接把文本内容写出来，然后使用 `append()` 等方法将它们添加到文档中就可以了。

```javascript
var $li_1 = $("<li>新增节点：数据结构</li>"); // 创建第一个<li>元素
var $li_2 = $("<li>新增节点：设计模式</li>"); // 创建第二个<li>元素
var $parent = $("ul"); // 获取<ul>节点。<li>的父节点
$parent.append($li_1); // 添加到<ul>节点中，使之能在网页中显示
$parent.append($li_2); // 可以采取链式写法：$parent.append($li_1).append($li_2);
```

注意：
1. 无论 `$(html)`中的 HTML 代码多么复杂，都要使用相同的方式来创建。<br>例如 `$("<li><em>这是</em><b>一个</b><a href="#">复杂的组合</a></li>")`;

### 创建属性节点

创建属性节点与创建文本节点类似，也是直接在创建元素节点时一起创建。JQuery代码如下：

```javascript
$(function(){
  var $li_1 = $("<li title='香蕉'>香蕉</li>");  //创建一个<li>元素
                                                //包括元素节点,文本节点和属性节点
                                                //其中title='香蕉' 就是创建的属性节点
  var $li_2 = $("<li title='雪梨'>雪梨</li>");  //创建一个<li>元素
                                                //包括元素节点,文本节点和属性节点
                                                //其中title='雪梨' 就是创建的属性节点
   var $parent = $("ul");     // 获取<ul>节点。<li>的父节点
   $parent.append($li_1);     // 添加到<ul>节点中，使之能在网页中显示
   $parent.append($li_2);     // 等价于：$parent.append($li_1).append($li_2);
  });
```

## 3.插入节点

动态创建HTML元素并没有实际用处，还需要将新创建的元素插入文档中。将新创建的节点插入文档最简单的办法是，让它成为这个文档的某个节点的子节点。前面使用了一个插入节点的方法 `append()`，它会在元素内部追加新创建的内容。

**这些插入节点的方法不仅能将新创建的DOM元素插入到文档中，也能对原有的DOM元素进行移动。**

jQuery 提供的插入节点的方法：

<iframe src="{{ site.url }}/assets/html/jQuery-node-charu.html" frameborder="0" width="100%" height="690px;"></iframe>

## 4.删除节点

如果文档中某一个元素多余，那么应将其删除。jQuery 提供了三种删除节点的方法，即：

- remove()
- detach()
- empty()

### remove()

作用是从 DOM 中删除所有匹配的元素，传入的参数用于根据 jQuery 表达式来筛选元素。

例如：
```javascript
$("ul li:eq(1)").remove();  //获取第2个<li>元素节点后，将它从网页中删除
```

当某个节点用 `remove()` 方法删除后，该节点所包含的所有后代节点将同时被删除。这个方法的返回值是一个指向已被删除的节点的引用，因此可以在以后再使用这些元素。

下面的 jQuery 代码说明元素用 `remove()` 方法删除后，还是可以进行使用的。

```javascript
var $li = $("ul li:eq(1)").remove(); //获取第2个<li>元素节点后，将它从网页中删除
$li.appendTo("ul");                  //把刚才删除的节点又重新添加到<ul>元素里
```

`appendTo()` 方法也可以用来移动元素<br>
移动元素时首先从文档上删除此元素，然后将该元素插入得到文档中的指定节点

**另外** `remove()` 方法也可以通过传递参数来选择性地删除元素，
```javascript
$("ul li").remove("li[title]=菠萝");  //获取第2个<li>元素节点后，将它从网页中删除
```
### detach()

`detach()` 和 `remove()` 一样，也是从 DOM 中去除所有匹配的元素。

但需要注意的是，这个方法不会把匹配的元素从 jQuery 对象删除，因而可以在将来再使用这些匹配的元素。

与 `remove()` 不同的是，所有绑定的事件、附加的数据等都会保留修理。
```javascript
$(function(){
  $("ul li").click(function(){
  alert( $(this).html() );
  })
  var $li = $("ul li:eq(1)").detach(); // 获取第二个<li>元素节点后，将它从网页中删除。
  $li.appendTo("ul");   //重新追加此元素，发现它之前绑定的事件还在，如果使用remove()方法删除元素的话，那么它之前绑定的事件将失效。
});
```
### empty()

严格来说，`empty()` 方法并不是删除节点，而是清空节点，它能清空元素中的所有后代节点。jQuery 代码如下：

```javascript
$(function(){
  $("ul li:eq(1)").empty(); // 找到第二个<li>元素节点后，清空此元素里的内容,注意是元素里
});
```

## 5.复制节点

复制节点也是常用的DOM操作之一，例如很多购物网站的效果，用户不仅可以通过单击商品下方的“选择”按钮购买相应的产品，也可以通过鼠标拖动商品并将其放到购物车中。这个商品拖动功能就是用的复制节点，将用户选择的商品所处的节点元素复制一次，并将其跟随鼠标移动，从而达到购物效果。

### clone()

如果单击 `<li>` 元素后需要再复制一个 `<li>` 元素，可以使用 `clone()` 方法来完成。jQuery代码如下：
```javascript
$(function(){
 $("ul li").click(function(){
     $(this).clone().appendTo("ul"); // 复制当前点击的节点，并将它追加到<ul>元素
 })
});
```

复制节点后，被复制的新元素并不具有任何行为。如果需要新元素也具有复制功能（本例中是单击事件），可以使用如下JQuery代码：
```javascript
$("ul li").click(function(){
 $(this).clone(true).appendTo("ul"); // 注意参数true
 //可以复制自己，并且他的副本也有同样功能。
})
```
**原因：**在 `clone()` 方法中传递了一个参数 true ，它的含义是复制元素的同时复制元素中所绑定的事件。因此该元素的副本也具有复制功能（本例中是单击事件）。

## 6.替换节点
jQuery 提供的替换某个节点的方法：
- replaceWith()
- replaceAll()

### replaceWith()

`replaceWith()` 方法的作用是将所有匹配的元素都替换成指定的 HTML 或者 DOM 元素。
例如：将网页中“&lt;p title="你最喜欢的水果."&gt;你最喜欢的水果是？&lt;/p&gt;”替换成“&lt;strong&gt;你最不喜欢的水果是？&lt;/strong&gt;”，可以使用如下 jQuery 代码：

```javascript
$("p").replaceWith("<strong>你最不喜欢的水果是?</strong>");
   // 同样的实现： $("<strong>你最不喜欢的水果是?</strong>").replaceAll("p");
```

### replaceAll()

`replaceAll()` 方法与 `replaceWith()` 方法的作用相同，只是颠倒了 `replaceWith()` 操作。

**注意：**如果在替换之前，已经为元素绑定事件，替换后原先绑定的事件将会与被替换的元素一起消失，需要在新元素上重新绑定事件。

## 7.包裹节点

### wrap()
如果要将某个节点用其他标记包裹起来，jQuery 提供了相应的方法，即 `wrap()`，该方法对于需要在文档中插入额外的结构化标记非常有用，而且它不会破坏原始文档的语义。

jQuery 代码如下:
```javascript
$("strong").wrap("<b></b>"); //用<b>标签把<strong>元素包裹起来
```
得到的结果如下：
```html
<b>
  <strong title="选择你最喜欢的水果." >你最喜欢的水果是?</strong>
</b>
```

包裹节点操作还有其他两个方法，即：
- wrapAll()
- wrapInner()

### wrapAll()
该方法会将所有匹配的元素用一个元素来包裹。它不同于wrap()方法，`wrap()` 方法是将所有的元素进行单独的包裹。

HTML 代码如下：
```html
<strong title="选择你最喜欢的水果." >你最喜欢的水果是?</strong>
<strong title="选择你最喜欢的水果." >你最喜欢的水果是?</strong>
<ul>
  <li title='苹果'>苹果</li>
  <li title='橘子'>橘子</li>
  <li title='菠萝'>菠萝</li>
</ul>
```

- 如果使用 `wrap()` 方法包裹 &lt;strong&gt;元素，jQuery 代码如下：
```javascript
$("strong").wrap("<b></b>");
```
将会得到如下结果：
```html
<b><strong title="选择你最喜欢的水果.">你最喜欢的水果是?</strong></b>
<b><strong title="选择你最喜欢的水果.">你最喜欢的水果是?</strong></b>
```

- 使用 `wrapAll()` 方法包裹 &lt;strong&gt;元素，jQuery 代码如下：
```javascript
$("strong").wrapAll("<b></b>");
```
则会得到如下结果：
```html
<b>
  <strong title="选择你最喜欢的水果.">你最喜欢的水果是?</strong>
  <strong title="选择你最喜欢的水果.">你最喜欢的水果是?</strong>
</b>
```

**注意：**如果被包裹的多个元素间有其他元素，其他元素会被放到包裹元素之后。

### wrapInner()

该方法将每一个匹配的元素的子内容（包括文本节点）用其他结构化的标记包裹起来。

例如可以使用它来包裹 &lt;strong&gt; 标签的子内容，jQuery 代码如下：
```javascript
$("strong").wrapInner("<b></b>");
```

运行代码后，发现 &lt;strong&gt; 标签内的内容被一对 &lt;b&gt; 标签包裹了，结果如下：
```html
<strong title="选择你最喜欢的水果."><b>你最喜欢的水果是?</b></strong>
```

## 8.属性操作

在 jQuery 中，
- 用 `attr()` 方法来获取和设置元素属性，
- `removeAttr()` 方法来删除元素属性。

### 1.获取属性和设置属性

- 如果要获取 &lt;p&gt; 元素的属性 title，那么只需要给 `attr()` 方法传递一个参数，即属性名称。
jQuery 代码如下：
```javascript
var $para = $("p");               //获取<p>节点
var p_txt = $para.attr("title");  //获取<p>元素节点属性title
```

- 如果要设置 &lt;p&gt;元素的属性 title 的值，页可以使用同一个方法，不同的是，需要传递两个参数，即**属性名称**和**对应的值**。
jQuery 代码如下：
```javascript
$("p").attr("title","your title");  //设置单个的属性值
```

- 如果需要一次性为同一个元素设置多个属性，可以使用下面的代码来实现：
```javascript
$("p").attr({"title":"your title","name":"test"});  //将一个"名/值"形式的对象设置为匹配元素的属性
```

**注意：**jQuery 中很多方法都是同一个函数实现获取( getter )和( setter )的，例如上面的 `attr()` 方法，既能设置元素属性的值，也能获取元素属性的值。类似的还有 `html()` 、 `text()` 、 `height` 、 `width()` 、 `val()` 、 `css()`等方法。

### 2.删除属性

在某些情况下，需要删除文档中某个元素的特定属性，可以使用 `removeAttr()` 方法来完成该任务。

如果需要删除 &lt;p&gt; 元素的 title 属性，可以使用下面的代码实现：
```javascript
$("p").removeAttr("title");  //删除<p>元素的属性title
```

运行代码后 &lt;p&gt; 元素的 title 属性将被删除。
```html
<!-- 没有删除title属性前 -->
<p title="选择你最喜欢的水果." >你最喜欢的水果是?</p>

<!-- 删除title属性后 -->
<p>你最喜欢的水果是?</p>
```

**注意：**jQuery1.6 中新增了 `PROP()` 和 `removeProp()`，分别用来**获取在匹配的元素集中的第一个元素的属性值**和为**匹配的元素删除设置的属性。**

## 9.样式操作

### 1.获取样式和设置样式

HTML 代码如下：
```html
<p class="myClass" title="选择你最喜欢的水果." >你最喜欢的水果是?</p>
```

在上面的代码中，class 也是 &lt;p&gt; 元素的属性，因此获取 class 和设置 class 都可以使用 `attr()` 方法来完成。

- 例如使用 `attr()` 方法来获取 &lt;p&gt; 元素的 class ，jQuery 代码如下：
```javascript
var p_class = $("p").attr("class");  //获取<p>元素的class
```

- 也可以使用 `attr()` 方法来设置 &lt;p&gt; 元素的 class，jQuery 代码如下：
```javascript
$("p").attr("class","high");  //设置<p>元素的class为"high"
```

运行代码后，上面的 HTML 代码将变为如下结构：
```html
<p class="high" title="选择你最喜欢的水果." >你最喜欢的水果是?</p>
```

上面的代码是将原来的 class(myclass) 替换为新的 class(high)。如果需要的是“追加”效果，class 属性变为 "myclass high"，即 myclass 和 high 两种样式的叠加，那么可以使用 `addClass()` 方法。

### 2.追加样式

jQuery 提供了专门的 `addClass()` 方法来追加样式。

在 CSS 中有以下两条对的：
1. 如果给一个元素添加了多个 class 值，那么久相当于合并了它们的样式。
2. 如果有不同的 class 设定了同一样式属性，则后者覆盖前者。

`attr()` 和 `addClass()`的区别

<iframe src="{{ site.url }}/assets/html/jQuery-attr-addClass.html" frameborder="0" width="100%" height="315px;"></iframe>

### 3.移除样式

移除样式可以使用与 `addClass()` 方法相反的 `removeClass()` 方法来完成，它的作用是从匹配的元素中删除全部或者指定的 class。

- 例如可以使用如下的 jQuery 代码来删除&lt;p&gt;元素中值为 "high" 的class
```javascript
$('p').removeClass("high");  //移除<p>元素中值为"high"的class
```

输出结果为：
```html
<p class="another" title="选择你最喜欢的水果." >你最喜欢的水果是?</p>
```

- 如果要把&lt;p&gt;元素的两个class都删除，就用使用两次 `removeClass()` 方法，代码如下：
```javascript
$('p').removeClass("high").removeClass("another");
```
jQuery 提供了更简单的方法。可以以空格的方式删除多个 class 名，jQuery 代码如下：
```javascript
$('p').removeClass("high another");
```

- 另外，还可以利用 `removeClass()` 方法的一个特性来完成同样的效果。当它不带参数时，就会将 class 的值全部删除，jQuery 代码如下：
```javascript
$('p').removeClass();  //移除<p>元素的所有class
```

此时，&lt;p&gt;元素的 HTML 结构为：
```html
<p title="选择你最喜欢的水果." >你最喜欢的水果是?</p>
```

### 4.切换样式

- `toggle()` 方法的作用是交替执行代码(3)和代码(4)两个函数，如果元素原来是显示的，则隐藏它；如果元素原来是隐藏的，则显示它。此时，`toggle()` 方法主要是控制行为上的重复切换。jQuery 代码如下：
```javascript
$toggleBtn.toggle(function(){
    //显示元素    代码(3)
  },function(){
    //隐藏元素    代码(4)
})
```

- 另外jQuery还提供了一个 `toggleClass()` 方法控制样式上的重复切换。如果类名存在则删除它，如果类名不存在则添加它。

### 5.判断是否含有某个样式

- `hasClass()` 可以用来判断元素中是否含有某个 class，如果有，则返回 true，否则返回false。

例如可以使用下面的代码，来判断&lt;p&gt;元素中是否含有“another” 的class：
```javascript
$("p").hasClass("another");
```

**注意：**这个方法是为了增强代码可读性而产生的。在jQuery内部实际上是调用了 `is()` 方法来完成这个功能的。该方法等价于如下代码：
```javascript
$("p").is(".another");
```

## 10.设置和获取HTML、文本和值

### 1.html()方法

- 此方法类似于 JavaScript中 的 innerHTML 属性，可以用来读取或者设置某个元素中的HTML内容。

HTML代码如下：
```html
<p title="选择你最喜欢的水果." ><strong>你最喜欢的水果是?</strong></p>
```

然后用 `html()` 方法对 &lt;p&gt; 元素进行操作：
```javascript
var p_html = $("p").html(); //获取<p>元素的HTML代码
alert(p_html);              //打印输出为： <strong>你最喜欢的水果是?</strong>
```

- 如果需要设置某元素的 HTML 代码，那么也可以使用该方法，不过需要为它传递一个参数。

例如要设置 &lt;p&gt; 元素的 HTML 代码，可以使用如下代码：
```javascript
$("p").html("<strong>你最喜欢的水果是?</strong>")  //设置<p>元素的HTML代码
```

**注意：**`html()`方法可以拥有 XHTML 文档，但不能用于 XML 文档。

### 2.text()方法

- 此方法类似于 JavaScript中 的 innerText 属性，可以用来读取或者设置某个元素中的文本内容。

HTML代码如下：
```html
<p title="选择你最喜欢的水果." ><strong>你最喜欢的水果是?</strong></p>
```

用 `text()` 方法对 &lt;p&gt; 元素进行操作：
```javascript
var p_text = $("p").text();  //获取<p>元素的文本内容
alert(p_text);               //打印输出为：你最喜欢的水果是?
```

- 与 `html()` 方法一样，如果需要为某元素设置文本内容，那么页需要传递一个参数。

例如对 &lt;p&gt; 元素设置文本内容，代码如下：
```javascript
$("p").text("你最喜欢的水果是?");  //设置<p>元素的文本
```

**注意：**
1. JavaScript 中的 `innerText` 属性并不能在 Firefox 浏览器下运行，而 jQuery 的 `text()` 方法支持所有的浏览器。
2. `text()` 方法对HTML文档和XML文档都有效。

### 3.val()方法

- 此方法类似于 JavaScript中 的 value 属性，可以用来设置或获取元素的值。无论元素是文本框，下拉列表还是单选框，它都可以返回元素的值。如果元素是多选，则返回一个包含所有选择的值的数组。

例如：登录界面的默认状态下，输入框里有提示文字，当将鼠标聚焦到输入框时，输入框里的“提示文字”将被清空。HTML 代码如下

```html
<input type="text" id="address" value="请输入邮箱地址"/>   <br/><br/>
<input type="text" id="password" value="请输入邮箱密码"/>  <br/><br/>
<input type="button" value="登录"/>
```

jQuery 代码如下：
```javascript
$("#address").focus(function(){         // 地址框获得鼠标焦点
      var txt_value =  $(this).val();   // 得到当前文本框的值
      if(txt_value=="请输入邮箱地址"){
                $(this).val("");              // 如果符合条件，则清空文本框内容
      }
    });
    $("#address").blur(function(){      // 地址框失去鼠标焦点
          var txt_value =  $(this).val();   // 得到当前文本框的值
      if(txt_value==""){
                $(this).val("请输入邮箱地址");// 如果符合条件，则设置内容
      }
    })

    $("#password").focus(function(){
      var txt_value =  $(this).val();
      if(txt_value=="请输入邮箱密码"){
                $(this).val("");
      }
    });
    $("#password").blur(function(){
          var txt_value =  $(this).val();
      if(txt_value==""){
                $(this).val("请输入邮箱密码");
      }
    })
```
**注意：**
1. `focus()` 方法相当于 JavaScript 中的 `onfocus()` 方法，作用是处理获得焦点时的事件。
2. `blur()` 方法相当于 JavaScript 中的 `onblur()`  方法，作用是处理失去焦点时的事件。

- 在该例子中，也可以使用表单元素的 `defaultValue` 属性来实现同样的功能， `defaultValue` 属于含该表单元素的初始值。代码如下：
```javascript
$("#address").focus(function(){         // 地址框获得鼠标焦点
      var txt_value =  $(this).val();     // 得到当前文本框的值
      if(txt_value==this.defaultValue){   //使用defaultValue属性
                $(this).val("");          // 如果符合条件，则清空文本框内容
      }
    });
    $("#address").blur(function(){      // 地址框失去鼠标焦点
          var txt_value =  $(this).val();   // 得到当前文本框的值
      if(txt_value==""){
                $(this).val(this.defaultValue);// 如果符合条件，则设置内容
      }
    })
```

通过上面的例子客服发现 `val()` 方法不仅能设置元素的值，同时也能获取元素的值。

- 另外， `val()` 方法还有另外一个用处，就是它能使 select（下拉列表框）、checkbox（多选框）和radio（单选框）相应的选项被选中，在表单操作中会经常用到。

HTML 代码如下：
```html
<input type="button" value="设置单选下拉框选中"/>
  <input type="button" value="设置多选下拉框选中"/>
  <input type="button" value="设置单选框和多选框选中"/>

<br/><br/>

<select id="single">
  <option>选择1号</option>
  <option>选择2号</option>
  <option>选择3号</option>
</select>

<select id="multiple" multiple="multiple" style="height:120px;">
  <option selected="selected">选择1号</option>
  <option>选择2号</option>
  <option>选择3号</option>
  <option>选择4号</option>
  <option selected="selected">选择5号</option>
</select>

<br/><br/>


<input type="checkbox" value="check1"/> 多选1
<input type="checkbox" value="check2"/> 多选2
<input type="checkbox" value="check3"/> 多选3
<input type="checkbox" value="check4"/> 多选4

<br/>

<input type="radio" value="radio1"/> 单选1
<input type="radio" value="radio2"/> 单选2
<input type="radio" value="radio3"/> 单选3
```

该网页中有一些元素是默认选中的，可以通过 `val()` 方法来改变它们的选中项。如果要使第 1 个下拉框的第 2 项被选中，可以用以下 jQuery 代码实现：
```javascript
$("#single").val("选择2号");
```

如果要使下拉列表的第2项和第三项被选中，可以用以下 jQuery 代码实现：
```javascript
$("#multiple").val(["选择2号", "选择3号"]);  //以数组的形式赋值
```

按照上面类似的写法，下面的代码可以使多选框和单选框被选中，jQuery 代码如下：
```javascript
$(":checkbox").val(["check2","check3"]);
$(":radio").val(["radio2"]);
```

**注意：**在上面这个例子中，可以使用 `val()` 方法，也可以使用 `attr()` 方法来实现同样的功能：
1. `$("single option:eq(1)").attr("selected",true)`;
2. `$("[value=radio2]:radio")attr.("checked,true")`;

## 11.遍历节点

### 1.children()方法

该方法用于取得匹配元素的子元素集合。

HTML 代码如下：
```html
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>...</title>
  </head>
  <body>
    <p title="选择你最喜欢的水果." >你最喜欢的水果是?</p>
    <ul>
      <li title='苹果'>苹果</li>
      <li title='橘子'>橘子</li>
      <li title='菠萝'>菠萝</li>
    </ul>
  </body>
</html>
```

下面使用 `children()` 方法来获取匹配元素的所有子元素的个数。

jQuery 代码如下：
```javascript
var $body = $("body").children();
   var $p = $("p").children();
   var $ul = $("ul").children();
   alert( $body.length );  // <body>元素下有2个子元素
   alert( $p.length );     // <p>元素下有0个子元素
   alert( $ul.length );    // <ul>元素下有3个子元素
   for(var i=0;i< $ul.length;i++){
         alert( $ul[i].innerHTML );  //循环输出<li>元素的HTML内容
   }
```

**注意：** `children()` 方法只考虑子元素而不考虑其他后代元素。

### 2.next()方法

该方法用于取得匹配元素后面紧邻的同辈元素。

例如：获取 &lt;p&gt; 元素的下一个同辈节点 &lt;ul&gt;：
```javascript
var $p1 = $("p").next();  //  取得紧邻<p>元素后的同辈元素
```

得到的结果将是：
```html
<ul>
  <li title='苹果'>苹果</li>
  <li title='橘子'>橘子</li>
  <li title='菠萝'>菠萝</li>
</ul>
```

### 3.prev()方法

该方法用于取得匹配元素前面紧邻的同辈元素。

例如：获取 &lt;ul&gt; 元素的上一个同辈节点 &lt;p&gt;：
```javascript
var $ul = $("ul").prev();  //  取得紧邻<ul>元素前的同辈元素
```

得到的结果将是：
```html
<p title="选择你最喜欢的水果." >你最喜欢的水果是?</p>
```

### 4.siblings()方法

该方法用于取得匹配元素前后所有的同辈元素。

以 DOM 树的结构为例，&lt;ul&gt; 元素和 &lt;p&gt; 元素互为同辈元素，&lt;ul&gt;元素下的3个 &lt;li&gt; 元素页互为同辈元素。如果要获取 &lt;p&gt; 元素的同辈元素，则可以使用如下代码：
```javascript
var $p2 = $("p").siblings();  //取得<p>元素的同辈元素
```
### 5.closest()方法

该方法用于取得最近的匹配元素。

首先检查当前元素是否匹配，如果匹配则直接返回元素本身。如果不匹配则向上查找父元素，逐级向上直到找到匹配选择器的元素。如果什么都没找到则返回一个空的jQuery 对象。

比如，给单击的目标元素的最近的 &lt;li&gt; 元素添加颜色，可以使用如下代码：
```javascript
$(document).bind("click", function (e) {
    $(e.target).closest("li").css("color","red");
  })
```

### 6.parent(),parents()与closest()的区别

`parent()` , `parents()` 与 `closest()`方法两两之间有类似又有不同，在此简短的区分一下这三个方法，如下所示。可以根据实际需求灵活地选中使用哪个方法。

<iframe src="{{ site.url }}/assets/html/jQuery-parent-parents-closest.html" frameborder="0" width="100%" height="445px;"></iframe>

除此之外，在 jQuery 中还有很多遍历节点的方法，例如 `find()` 、 `filter()` 、 `nextAll` 和 `prevAll()` 等。可以查看《锋利的jQuery(第2版)》附录的 jQuery 速查表文档。[在线的jQuery 速查表文档](http://hemin.cn/jq/ '在线的jQuery 速查表文档')

## 12.CSS-DOM操作

CSS-DOM 技术简单来说就是读取和设置 style 对象的各种属性。

style 属性很有用，但最大不足是无法通过它来提取到通过外部CSS设置的样式信息，然而在 jQuery 中，这些都是非常的简单。

### css()
- 可以直接利用 `css()` 方法获取元素的样式属性，jQuery 代码如下：
```javascript
$("p").css("color");  //获取<p>元素的元素颜色
```

无论 color 属性是外部 CSS 导入，还是直接拼接在 HTML 元素里(内联)，`css()` 方法都可以获取到属性 style 里的其他属性的值。

- 也可以直接利用 `css()` 方法设置某个元素的单个样式，例如：
```javascript
$("p").css("color","red");  //设置<p>元素的样式颜色为红色
```

- 与 `attr()` 方法一样，`css()` 方法也可以同时设置多个样式属性，代码如下：
```javascript
$("p").css({"fontSize":"30px" ,"backgroundColor":"#888888"})  //同时设置字体大小和背景色
```

**注意：**
1. 如果值是数组，将会被自动转化为像素值。
2. 在 `css()` 方法中，如果属性中带有 “-” 符号，例如 font-size 和 background-color 属性，如果在设置这些属性的值的时候不带引号，那么就要用驼峰式写法，例如：`$("p").css({ fontSize:"30px,backgroundColor:"#888888" "})` 。如果带上了引号，既可以写成 “font-size”，也可以写成 “fontSize”。总之建议加上引号，养成良好的习惯。

- 对透明度的设置，可以直接使用 opacity 属性，jQuery 已经处理好了兼容性的问题，代码如下：
```javascript
$("p").css("opacity","0.5");
```

### height()
- 如果需要获取某个元素的 height 属性，则可以通过如下jQuery 代码实现：
```javascript
$(element).css("height");
```

在jQuery 中还有另外一种方法也可以获取元素的高度，即 height()。它的作用是取得匹配元素当前计算的高度值(px)。jQuery 代码如下：
```javascript
$("p").height();  //获取<p>元素的高度值
```

`height()`方法也能用来设置元素的高度，如果传递的值是一个数字，则默认单位为 `px`。如果要用其他单位（例如 em ），则必须传递一个字符串。jQuery 代码如下：
```javascript
$("p").height("100");   //设置<p>元素的高度值为100px
$("p").height("100px"); //设置<p>元素的高度值为100px
$("p").height("100em"); //设置<p>元素的高度值为100em
```

**注意：**
1. `height()` 方法可以用来获取 window 和 document 的高度。
2. 两者的区别是：`css()`方法获取的高度值与样式的设置有关，可能会得到 "auto" ，也可能得到 "10px" 之类的字符串；而 `height()` 方法获取的高度值则是样式在页面中的实际高度，与样式的设置无关，并且不带单位。

### width()
- 与 `height()` 方法对应的还有一个 `width()` 方法，它可以取得匹配样式的宽度值（px）。
```javascript
$("p").width();  //获取<p>元素的宽度
```

同样， `width()` 方法也能用来设置元素的宽度。
```javascript
 $("p").width("400px");  //设置<p>元素的宽度值为400px
```

此外，在 CSS-DOM 中，关于元素定位有以下几个经常使用的方法。

### 元素定位

#### 1. offset()方法

它的作用是获取元素在当前视窗的相对偏移，其中返回的对象包含两个属性，即 top 和 left，它只对可见元素有效。

例如用它获取 &lt;p&gt; 元素的偏移量，jQuery 代码如下：
```javascript
var offset = $("p").offset(); //获取<p>元素的offset()
var left = offset.left;       //获取左偏移
var top =  offset.top;        //获取上偏移
```

#### 2.position()方法

它的作用是获取元素相对于最近的一个 position 元素属性设置为 relative 或者 absolute 的祖父节点的相对偏移，与 `offset()` 一样，它返回的对象也包括两个属性，即 top 和 left 。jQuery 代码如下：
```javascript
var position = $("p").position(); //获取<p>元素的position()
var left = position.left;       //获取左偏移
var top =  position.top;        //获取上偏移
```

#### 3.scrollTop()和scrollLeft()方法

- 这两个方法的作用分别是获取元素的滚动条距顶端的距离和距左侧的距离。

例如使用下面的代码获取 &lt;p&gt; 元素的滚动条距离：
```javascript
var $p = $("p");
var scrollTop = $p.scrollTop();       //获取元素的滚动条距顶端的距离
var scrollLeft =  $p.scrollLeft();     //获取元素的滚动条距左侧的距离
```

- 另外，可以为这两个方法指定一个参数，控制元素的滚动条滚动到指定位置。

例如使用如下代码控制元素内的滚动条滚动到距顶端300和距左侧300的位置：
```javascript
$("textarea").scrollTop(300); //元素的垂直滚动条滚动到指定的位置
$("textarea").scrollLeft(300);  //元素的横向滚动条滚动到指定的位置
```

## 代码实例

巩固 jQuery 中的 DOM 操作。

- 超链接提示效果

HTML 代码如下：
```html
<p><a href="#" class="tooltip" title="这是我的超链接提示1.">提示1.</a></p>
<p><a href="#" class="tooltip" title="这是我的超链接提示2.">提示2.</a></p>
<p><a href="#" title="这是自带提示1.">自带提示1.</a></p>
<p><a href="#" title="这是自带提示2.">自带提示2.</a> </p>
```

JavaScript代码如下：
```javascript
$(function(){
  var x = 10; //防止自制的提示与鼠标的距离太近
  var y = 20;
  $("a.tooltip").mouseover(function(e){ //鼠标悬停事件
    this.myTitle = this.title;  //获取链接原有title
    this.title = "";  //清空链接原有title，阻止title默认样式显示
    var tooltip = "<div id='tooltip'>"+ this.myTitle +"<\/div>"; //创建 div 元素
    $("body").append(tooltip);  //把它追加到文档中
    $("#tooltip") //设置追加的div的CSS定位
      .css({
        "top": (e.pageY+y) + "px",  //pageY:显示鼠标指针的Y坐标位置
        "left": (e.pageX+x)  + "px"
      }).show("fast");    //设置x坐标和y坐标，并且显示
    }).mouseout(function(){ //鼠标移出事件
    this.title = this.myTitle;  //还原链接原有title
    $("#tooltip").remove();   //移除追加的div
    }).mousemove(function(e){ //鼠标悬停并移动事件，提示效果跟着鼠标一起移动
    $("#tooltip")
      .css({
        "top": (e.pageY+y) + "px",
        "left": (e.pageX+x)  + "px"
      });
  });
})
```

- 图片提示效果

稍微修改上面链接提示效果代码，就可以做出一个图片的提示效果。

HTML 代码如下：
```html
<ul>
  <li><a href="images/apple_1_bigger.jpg" class="tooltip" title="苹果 iPod"><img src="images/apple_1.jpg" alt="苹果 iPod" /></a></li>
  <li><a href="images/apple_2_bigger.jpg" class="tooltip" title="苹果 iPod nano"><img src="images/apple_2.jpg" alt="苹果 iPod nano"/></a></li>
  <li><a href="images/apple_3_bigger.jpg" class="tooltip" title="苹果 iPhone"><img src="images/apple_3.jpg" alt="苹果 iPhone"/></a></li>
  <li><a href="images/apple_4_bigger.jpg" class="tooltip" title="苹果 Mac"><img src="images/apple_4.jpg" alt="苹果 Mac"/></a></li>
</ul>
```

jQuery 代码如下：
```javascript
$(function(){
  var x = 10;
  var y = 20;
  $("a.tooltip").mouseover(function(e){
    this.myTitle = this.title;
    this.title = "";
    var imgTitle = this.myTitle? "<br/>" + this.myTitle : "";
    var tooltip = "<div id='tooltip'><img src='"+ this.href +"' alt='产品预览图'/>"+imgTitle+"<\/div>"; //创建 div 元素
    $("body").append(tooltip);  //把它追加到文档中
    $("#tooltip")
      .css({
        "top": (e.pageY+y) + "px",
        "left":  (e.pageX+x)  + "px"
      }).show("fast");    //设置x坐标和y坐标，并且显示
    }).mouseout(function(){
    this.title = this.myTitle;
    $("#tooltip").remove();  //移除
    }).mousemove(function(e){
    $("#tooltip")
      .css({
        "top": (e.pageY+y) + "px",
        "left":  (e.pageX+x)  + "px"
      });
  });
})
```






