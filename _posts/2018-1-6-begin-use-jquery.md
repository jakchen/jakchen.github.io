---
layout: post
title:  "开始使用 jQuery(3)-jQuery选择器"
categories: jQuery
tags: jQuery
author: jakchen
---
* content
{:toc}

选择器是jQuery 的根基，在jQuery中，对事件处理、遍历DOM、和Ajax操作都依赖于选择器。如果能熟练地使用选择器，不仅能简化代码而且可以达到事半功倍的效果。

jQuery的选择器完全继承了CSS的风格，只是CSS选择器是找到元素为其添加样式，而jQuery选择器是找到元素为其添加行为。另外，jQuery中涉及的操作CSS样式的部分比单纯的CSS功能更加强大。并且有跨浏览器的兼容性。




学会使用选择器是学习jQuery的基础，jQuery的行为规则都必须在获取到元素后才能生效。

PS：目前学到的除了(document)之外，所有的("body/#id/.class等")中都必须有引号。

### 例子

**行为和内容没有分离**
```html
<script>
  function demo(){
  alert('JavaScript demo.');
  }
</script>
<p onclick="demo();">点击我.</p>
```

**行为和内容分离**
```html
<p class="demo">jQuery Demo</p>
<script>
  $(".demo").click(function(){  // 给class为demo 的元素添加行为
     alert("jQuery demo!");
  })
</script>
```

**对CSS的写法和jQuery的写法进行比较**

- CSS 获取到元素的代码如下：
```css
.demo{   /*给class为demo的元素添加样式*/
  ...
}
```

- CSS 获取到元素的代码如下：
```javascript
$(".demo").click(function(){  // 给class为demo 的元素添加行为
  ...
  });
```

jQuery 选择器的写法与css选择器的写法十分相似，只不过两者的作用效果不同：**CSS 选择器找到元素后是添加样式，而jquery选择器找到元素后是添加行为。**jQuery 中涉及操作 CSS 样式的部分比单纯的 CSS 功能更为强大，并且拥有跨浏览器的兼容性。

## jQuery选择器的优势

### 简洁的写法

$()函数在jQuery中被作为一个选择器函数来使用。其中：

- $("#ID")用来代替 document.getElementById()函数，即通过ID获取元素；
- $("tagName")用来代替 document.getElementsByTagName()函数，即通过标签名来获取 HTML 元素。

其他选择器的写法参加 [更多的jQuery选择器](http:// '更多的jQuery选择器')

### 支持CSS1-CSS3选择器

jQuery 选择器支持 CSS 1 、CSS 2 、的全部和 CSS 3的部分选择器，同时它也有少量独有的选择器。

使用 CSS 选择器时，开发人员需要考虑主流浏览器是否支持某些选择器。而**在 jQuery 中，开发人员则可以放心地使用 jQuery 选择器而不需考虑浏览器是否支持这些选择器。**

### 完善的处理机制
- DOM 方法获取一个网页中不存在元素时，会报错。
- jQuery 方法获取一个网页中不存在的元素页时，不会报错。

在这里面有一个需要注意的地方就是当检查某个元素是否存在时不能使用true或者false,而应该使用length
```javascript
//错误写法 原因：$("#tt")获取的永远是对象，即使网页上没有此元素。
if($("#tt")){
      //do something
}

//正确写法1 原因：根据获取到元素的长度来判断。
if($("#tt").length > 0){
      //do something
}

//正确写法2 原因：转化成 DOM 对象判断。
if($("tt")[0]){
      //do something
}
```

## 1.基本选择器
基本选择器是jQuery中最常用的选择器，也是最简单的选择器，它通过id、class和标签名等来查找元素。

- `#id`：`$("test")`选取id为test的元素；
- `.class`：`$(".test")`选取所有class为test的元素；
- `elemtnt`：`$("p")`选取所有的&lt;p&gt;元素；
- `*`：`$("*")`选取所有的元素；
- `selector1，selector2，...，selectorN`：`$("div,span,p.myclass")`选取所有&lt;div&gt;，&lt;span&gt;和拥有class为myclass的&lt;p&gt;标签的一组元素。

## 2.层次选择器

通过DOM元素之间的层次关系来获取特定元素，例如
1. **后代元素**、
2. **子元素**、
3. **相邻元素**
4. **同辈元素**等。

- `$("div span")`：选取&lt;div&gt;里的所有的&lt;span&gt;元素（后代元素）；
- `$("div>span")`：选取紧接在&lt;div&gt;元素下元素名是&lt;span&gt;的子元素；（注意：子元素和后代元素的区别）
- `$('.one+div')`：选取class为one的下一个&lt;div&gt;同辈元素；或者`$(".one").next("div")`; (推荐使用)
- `$('#two~div')`：选取id为two的元素后面的所有&lt;div&gt;兄弟元素。或者`$("#prev").nextAll("div")`;(推荐使用)

`$("#prev").siblings("div")：`：所有同辈元素（不管是id为#prev元素前面还是后面的同辈元素，都会被选取）

## 3.过滤选择器

过滤选择器主要是通过特定的过滤规则来筛选出所需的DOM元素，过滤规则与CSS中的伪类选择器语法相同，即选择器**都以一个冒号(:)开头**。

按照不同的过滤规则，过滤选择器可以分为
1. 基本过滤
2. 内容过滤
3. 可见性过滤
4. 属性过滤
5. 子元素过滤
6. 表单对象属性过滤

### 基本过滤

<iframe src="{{ site.url }}/assets/html/jQuery-selector-jiben-guolv.html" frameborder="0" width="100%" height="770px;"></iframe>

### 内容过滤

<iframe src="{{ site.url }}/assets/html/jQuery-selector-neirong-guolv.html" frameborder="0" width="100%" height="295px;"></iframe>

**:empty** 和 **:parent** 这两个内容过滤选择器选取的元素相反。

### 可见性过滤

<iframe src="{{ site.url }}/assets/html/jQuery-selector-kejianxing-guolv.html" frameborder="0" width="100%" height="275px;"></iframe>

### 属性过滤

<iframe src="{{ site.url }}/assets/html/jQuery-selector-shuxing-guolv.html" frameborder="0" width="100%" height="710px;"></iframe>

### 子元素过滤

子元素过滤选择器的过滤规则相对于其他的选择器稍微有些复杂，不过只要将元素的父元素和子元素区分清楚，使用起来页非常简单。

另外还要注意它与普通的过滤选择器的区别。

<iframe src="{{ site.url }}/assets/html/jQuery-selector-ziyuansu-guolv.html" frameborder="0" width="100%" height="595px;"></iframe>

`:nth-child()`选择器是很常用的子元素过滤选择器，详细功能如下：

1. `:nth-child(even)`能选取每个父元素下的索引值是偶数(第2、4、6、8……个)的元素。
2. `:nth-child(odd)`能选取每个父元素下的索引值是奇数(第1、3、5、7……个)的元素。
3. `:nth-child(2)`能选取每个父元素下的索引值等于2的元素。
4. `:nth-child(3n)`能选取每个父元素下的索引值是3的倍数的元素。(n从1开始)
5. `:nth-child(3n+1)`能选取每个父元素下的索引值是(3n+1)的元素。(n从1开始)

### 表单对象属性过滤

此选择器注意是对所选择的表单元素进行过滤，例如选择被选中的下拉框，多选框等元素。

<iframe src="{{ site.url }}/assets/html/jQuery-selector-biaodanshuxing-guolv.html" frameborder="0" width="100%" height="295px;"></iframe>

## 4.表单选择器。

为了使用户能够更加灵活地操作表单，jQuery中专门加入了表单选择器。利用这个选择器，能够极其方便地获取到表单的某个或某类型的元素。

<iframe src="{{ site.url }}/assets/html/jQuery-selector-biaodan.html" frameborder="0" width="100%" height="690px;"></iframe>

## 选择器中的一些注意事项

### 选择器中含有特殊符号：

- 选择器中含有"."、"#"、"("或"]"等特殊字符。

根据W3C的规定，属性值中是不能含有这些特殊字符的。但在实际项目中偶尔会遇到表达式中含有"#"和"."等特殊字符。如果按照普通的方式去处理出来的话就会出错。解决此类错误的方法是使用转义符转义。

HTML代码如下：
```html
<div id="id#b">bb</div>
<div id="id[1]">cc</div>
```

如果按照普通的方式来获取，例如：
```javascript
$("#id#b");
$("#id[1]")
```

以上代码不能正确获取到元素，正确的写法如下：
```javascript
$("#id\\#b");      //转移特殊字符#
$("#id\\[1\\]")    //转移特殊字符[]
```

### 选择器中含有空格

- 选择器中含有空格的注意事项：

选择器中的空格也是不容忽视的，多一个空格或少一个空格也许会得到截然不同的结果。

**之所以会出现不同的结果，是因为后代选择器与过滤选择器的不同。**

例如：
```javascript
var $t_a=$('.test :hidden');    //带空格的jQuery选择器
```

以上代码是选取class为"test"的元素里面的隐藏元素

```javascript
var $t_b=$('.test:hidden');    //不带空格的jQuery选择器
```

以上代码是隐藏的class为"test"的元素

**一些方法：**
ps：例子省略。

- `show()`:显示隐藏的匹配元素
- `css(name,value)`:给元素设置样式
- `text(String)`:设置匹配元素的文本内容
- `filter(expr)`:筛选出与指定表达式匹配的元素集合，其中expr可以是多个选择器的组合，注意区分它和find()方法。find()会在元素内寻找匹配元素，而filter()则是筛选元素。一个是对他的·子集操作，一个是对自身集合元素进行筛选
- `addClass(class)`:未匹配的元素添加指定的类名

## 小结

选择器是行为与文档内容之间连接的纽带，选择器的最终目的就是能够轻松地找到文档中的元素。





