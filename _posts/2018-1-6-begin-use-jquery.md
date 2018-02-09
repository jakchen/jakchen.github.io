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

PS：目前学到的除了(document)之外，所有的(“body/#id/.class等”)中都必须有引号。

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

- `$(“div span”)`：选取&lt;div&gt;里的所有的&lt;span&gt;元素（后代元素）；
- `$(“div>span”)`：选取紧接在&lt;div&gt;元素下元素名是&lt;span&gt;的子元素；（注意：子元素和后代元素的区别）
- `$(‘.one+div’)`：选取class为one的下一个&lt;div&gt;同辈元素；或者`$(“.one”).next(“div”)`; (推荐使用)
- `$(‘#two~div’)`：选取id为two的元素后面的所有&lt;div&gt;兄弟元素。或者`$(“#prev”).nextAll(“div”)`;(推荐使用)

`$(“#prev”).siblings(“div”)：`：所有同辈元素（不管是id为#prev元素前面还是后面的同辈元素，都会被选取）

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
### 表单对象属性过滤


## 4.表单选择器。

