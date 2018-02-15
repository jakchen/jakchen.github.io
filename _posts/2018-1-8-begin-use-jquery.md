---
layout: post
title:  "开始使用 jQuery(5)-jQuery中的事件"
categories: jQuery
tags: jQuery
author: jakchen
---
* content
{:toc}

JavaScript 和 HTML 之间的交互是通过用户和浏览器操作页面时引发的事件来处理的。当文档或者它的某些元素发生某些变化或操作时，浏览器会自动生成一个事件。

例如当浏览器装载完一个文档后，会生成事件；当用户单击某个按钮时，也会生成事件。




虽然利用传统的 JavaScript 事件能完成这些交互，但 jQuery 增加并扩展了基本的事件处理机制。jQuery不仅提供了更加优雅的事件处理语法，而且极大地增强了事件处理能力。

## 1.加载DOM

以浏览器装载文档为例，在页面加载完毕后，浏览器会通过 JavaScript 为 DOM 元素添加事件。

- 在常规的 JavaScript 代码中，通常使用 `window.onload` 方法，
- 而在 jQuery 中，使用的是 `$(document).ready()` 方法。

`$(document).ready()` 方法是事件模块中最重要的一个函数，可以极大地提高 Web 应用程序的响应速度。

jQuery 就是用 `$(document).ready()` 方法来代替传统 JavaScript 的 `window.onload` 方法的。通过使用该方法，可以在 DOM 载入就绪时就对其进行操纵并调用执行它所绑定的函数。

在使用过程中，需要注意 `$(document).ready()` 方法和 `window.onload` 方法之间的细微区别：

### 1.执行时机

`$(document).ready()` 方法和 `window.onload` 方法有相似的功能，但是在执行时机方面是有区别的。

- `window.onload`方法是在网页中所有的元素（包括元素的所有关联文件）完全加载到浏览器后才执行，即 JavaScript 此时才可以访问网页中的任何元素。
- 而通过 jQuery 中的 `$(document).ready()` 方法注册的事件处理程序，在DOM完全就绪时就可以被调用。此时，网页的所有元素对jQuery而言都是可以访问的，但是，这并不意味着这些元素关联的文件都已经下载完毕。

*举一个例子，有一个大型的图库网站，为网页中所有图片添加某些行为，例如单击图片后让它隐藏或显示。如果使用 `window.onload` 方法来处理，那么用户必须等到每一幅图片都加载完毕后，才可以进行操作。如果使用jQuery中的 `$(document).ready()` 方法来进行设置，只要DOM就绪就可以操作了，不需要等待所有图片下载完毕。很显然，把网页解析为 DOM 树的速度比把页面中的所有关联文件加载完毕的速度快很多。*

另外，需要注意一点，由于在 `$(document).ready()` 方法内注册的事件，只要 DOM 就绪就会被执行，因此可能此时元素的关联文件末下载完。例如与图片有关的HTML下载完毕，并且已经解析为 DOM 树了，但很有可能图片还未加载完毕，所以例如图片的高度和宽度这样的属性此时不一定有效。要解决这个问题，可以使用 jQuery 中另一个关于页面加载的方法——`load()` 方法。`load()` 方法会在元素的 onload 事件中绑定一个处理函数。如果处理函数绑定给 window 对象，则会在所有内容（包括窗口、框架、对象和图像等）加载完毕后触发，如果处理函数绑定在元素上，则会在元素的内容加载完毕后触发。jQuery代码如下：
```javascript
$(window).load(function(){
  // 编写代码
})
```

等价于 JavaScript 中的以下代码：
```javascript
window.onload = function(){
  // 编写代码
})
```

### 2.多次使用

现在详细讲解下 `windows.onload` 方法和 `$(document).ready()` 方法的区别：

假设网页中有两个函数，JavaScript代码如下：
```javascript
function one(){ alert("one"); }
function two(){ alert("two"); }
```
当网页加载完毕后，通过如下 JavaScript 代码来分别调用 one 函数和 two 函数：
```javascript
window.onload = one;
window.onload = two;
```

然而当运行代码后，发现只弹出字符串“two”对话框。

字符串“one”对话框不能被弹出的原因是JavaScript的onload事件一次只能保存对一个函数的引用，它会自动用后面的函数覆盖前面的函数，因此不能在现有的行为上添加新的行为。

为了达到两个函数顺序触发的效果，只能再创建一个新的JavaScript方法来实现，Javascript代码如下：
```javascript
window.onload = function(){
  one();
  two();
}
```

虽然这样编写代码能解决某些问题，但还是不能满足某些需求，例如有多个 JavaScript 文件，每个文件都需要用到 `window.onload` 方法，这种情况下用上面提到的方法编写代码会非常麻烦。而 jQuery 的 `$(document).ready()` 方法能够很好地处理这些情况，每次调用 `$(document).ready()` 方法都会在现有的行为上追加新的行为，这些行为函数会根据注册的顺序依次执行。例如如下jQuery代码：
```javascript
function one(){ alert("one"); }
function two(){ alert("two"); }
$(document).ready(function(){ one(); })
$(document).ready(function(){ two(); });
```

运行代码后，会先弹出字符串“one”对话框，然后弹出字符串“two”对话框。

### 3.简写方式

上面我们 ready 函数写成这样：
```javascript
$(document).ready(function(){ // 编写代码 })
```

也可以简写成这样：
```javascript
$(function(){ // 编写代码 })
```

另外，  `$(document)` 也可以简写为 `$()`。当 `$()` 不带参数时，默认参数就是 “document”，因此可以简写为：
```javascript
$().ready(function(){ // 编写代码 })
```

3种方式都是一样的功能，可以根据自己的喜好，选择其中的一种。

## 2.事件绑定

在文档装载完成后，如果打算为元素绑定事件来完成某些操作，则可以使用 `bind()` 方法来对匹配元素进行特定事件的绑定，`bind()` 方法的调用格式为：
```javascript
bind( type [, data] , fn);
```

bind()方法有3个参数，说明如下。
- 第1个参数是事件类型，类型包括：`blur`、`focus`、`load`、`resize`、`scroll`、`unload`、`click`、`dblclick`、`mousedown`、`mouseup`、`mousemove`、`mouseover`、`mouseout`、`mouseenter`、`mouseleave`、`change`、`select`、`submit`、`keydown`、`keypress`、`keyup`和`error`等，当然也可以是自定义名称。
- 第2个参数为可选参数，作为 `event.data` 属性值传递给事件对象的额外数据对象。
- 第3个参数则是用来绑定的处理函数。

**注意：**可以发现，jQuery 中的事件绑定类型比普通的 JavaScript 事件绑定类型少了 “on”。例如鼠标单击事件在 jQuery 中对应的是 click 事件，而在 JavaScript 中对应的是 onclick() 函数。

### 1.实例-单击显示隐藏元素

假设网页中有一个 FAQ，单击“标题”链接将显示内容。

HTML 代码如下：
```html
<div id="panel">
  <h5 class="head">什么是jQuery?</h5>
  <div class="content">
    jQuery是继Prototype之后又一个优秀的JavaScript库，它是一个由 John Resig 创建于2006年1月的开源项目。jQuery凭借简洁的语法和跨平台的兼容性，极大地简化了JavaScript开发人员遍历HTML文档、操作DOM、处理事件、执行动画和开发Ajax。它独特而又优雅的代码风格改变了JavaScript程序员的设计思路和编写程序的方式。
  </div>
</div>
```

CSS 代码如下：
```css
*{margin:0;padding:0;}
body {
  font-size: 13px;
  line-height: 130%;
  padding: 60px }
#panel {
  width: 300px;
  border: 1px solid #0050D0; }
.head {
  height:24px;
  line-height:24px;
  text-indent:10px;
  background: #96E555;
  cursor: pointer;
  width:100%; }
.content { padding: 10px;
  text-indent:24px;
  border-top: 1px solid #0050D0;
  display:block;
  display:none; }
```

按照需求，需要完成以下几个步骤：
1. 等待 DOM 加载完毕。
2. 找到“标题”所在的元素，绑定 click 事件。
3. 找到“内容”元素，如果“内容”元素是显示的，则隐藏，如果“内容”元素是隐藏的，则显示。

jQuery 代码如下：
```javascript
$(function(){
    $("#panel h5.head").bind("click",function(){
      var $content = $(this).next();  //$(this).next()被多次引用，为它定义一个局部变量
      if($content.is(":visible")){  //如果“内容”显示  //is()方法：判断元素是否显示
      $content.hide();  //“内容”隐藏
    }else{
      $content.show();  //“内容”显示
    }
  })
})
```
运行代码，单击“标题”链接，“内容”就展开了。在这个例子中，为“标题”绑定了一个 click 事件，单击标题链接后，显示“内容”。

与 `ready()` 方法一样，`bind()` 方法也可以多次调用。

上面 jQuery 代码中有一个关键字 this ，与在 JavaScript 中的作用一样，this 引用的是携带相应行为的DOM元素。为了使该 DOM 元素能够使用 jQuery 中的方法，可以使用 `$(this)` 将其转换为 jQuery 对象。

**注意：**当发现相同的选择器在你的代码里出现多次时，请把变量把它缓存起来，更多 jQuery 性能优化参考第 11 章。[jQuery性能优化的一篇文章](https://www.cnblogs.com/bigboyLin/p/4745175.html)

### 2.改变绑定事件类型

上面的例子中，给元素绑定的事件类型是 click，当用户单击的时候会触发绑定的事件，然后执行事件的函数代码。现在把事件类型换成 mouseover 和 mouseout，即当光标滑过的时候，就触发事件。需要进行以下几步操作：

1. 等待 DOM 加载完毕。
2. 找到“标题”所在的元素，绑定 mouseover 事件。
3. 找到“内容”元素，显示“内容”。
4. 找到“标题”所在的元素，绑定 mouseout 事件。
5. 找到“内容”元素，隐藏“内容”。

jQuery 代码如下：
```javascript
$(function(){
    $("#panel h5.head").bind("mouseover",function(){  //绑定鼠标悬停事件
       $(this).next().show(); //显示元素
  }).bind("mouseout",function(){  //绑定鼠标移出事件
       $(this).next().hide(); //隐藏元素
  })
})
```

代码运行后，当光标滑过“标题”链接后，相应的“内容”将被显示。当光标滑出“标题”链接后，相应的“内容”则被隐藏。

在上面几个例子中，分别用 `bind()` 方法给“标题”绑定了 click 事件、mouseover 事件和 mouseout 事件，绑定方法都一样。除此之外，bind0方法还能绑定其他所有的 JavaScript 事件。

### 3.简写绑定事件

像 click、mouseover 和 mouseout 这类事件，在程序中经常会使用到，jQuery 为此也提供了一套简写的方法。简写方法和 `bind()` 方法的使用类似，实现的效果也相同，惟一的区别是能够减少代码量。

例如把上面的例子改写成使用简写绑定事件的方式，代码如下：
```javascript
$(function(){
    $("#panel h5.head").mouseover(function(){
      $(this).next().show();
  }).mouseout(function(){
      $(this).next().hide();
  })
})
```

## 3.合成事件

jQuery 有两个合成事件——`hover()` 方法和 `toggle()` 方法，类似前面讲过的 `ready()` 方法，`hover()` 方法和 `toggle()` 方法都属于 jQuery 自定义的方法。

### 1.hover()方法

语法结构为：
```javascript
hover(enter,leave)。
```

- 用于模拟光标悬停事件。当光标移动到目标元素上时，会触发指定的第1个函数(enter);当光标移出这个元素时，会触发指定的第2个函数(leave)。

将上面的例子改写成 `hover()` 方法，jQuery 代码如下：
```javascript
$(function(){
    $("#panel h5.head").hover(function(){
      $(this).next().show();
  },function(){
      $(this).next().hide();
  })
})
```

代码运行后的效果与下面代码运行后的效果是一样的。当光标滑过“标题”链接时，相应的“内容”将被显示；当光标滑出“标题”链接后，相应的“内容”则被隐藏。
```javascript
$(function(){
    $("#panel h5.head").mouseover(function(){
            $(this).next("div.content").show();
    }).mouseover(function(){
            $(this).next("div.content").hide();
    })
});
```

**注意：**
1. CSS 中有伪类选择符，例如“:hover”，当光标悬停于元素上时，会改变元素的外观。伪类选择符可以用于任何元素。然而在IE 6浏览器中，伪类选择符仅可用于超链接元素。对于其他元素，可以使用 jQuery 的 `hover()` 方法。
2. `hover()` 方法准确来说是替代 jQuery 中的 `bind(“mouseenter”)` 和 `bind(“mouseleave”)`，而不是替代 `bind(“mouseover”)` 和 `bind(“mouseout”)`。因此当需要触发 `hover()` 方法的第2个函数时，需要用 `trigger(“mouseleave”)` 来触发，而不是 `trigger(“mouseout”)`。

### 2.toggle()方法

语法结构为：
```javascript
toggle(fnl, fn2, …fnN);
```

- 主要用于模拟鼠标连续单击事件。第1次单击元素，触发指定的第1个函数(fn1)；当再次单击同一元素时，则触发指定的第2个函数(fh2)；如果有更多函数，则依次触发，直到最后一个。随后的每次单击都重复对这几个函数的循环调用。

在前面的实例-单击显示隐藏元素的例子中，使用了以下jQuery代码：
```javascript
$(function(){
    $("#panel h5.head").bind("click",function(){
      var $content = $(this).next();
      if($content.is(":visible")){
      $content.hide();
    }else{
      $content.show();
    }
  })
})
```

虽然上面的代码能实现需要的效果，但是选择的方法并不是最适合的。如果需要连续单击“标题”链接，来达到使“内容”隐藏和显示的目的，那么很合适使用 `toggle()` 方法。原理如下：
```javascript
$(标题).toggle(function(){
    //内容显示
  },function(){
    //内容隐藏
});
```

使用 `toggle()` 方法来改写上面的例子，jQuery 代码如下：
```javascript
$(function(){
    $("#panel h5.head").toggle(function(){
      $(this).next().show();
  },function(){
      $(this).next().hide();
  })
})
```

- **通过使用 `toggle()` 方法不仅实现了相同效果，同时也简化了代码。**

- `toggle()` 方法在 jQuery 中还有另外一个作用：切换元素的可见状态。

如果元素是可见的，单击切换后则为隐藏；如果元素是隐藏的，单击切换后则为可见的。因此上面的代码还可以写成如下 jQuery 代码：
```javascript
$(function(){
  $("#panel h5.head").toggle(function(){
    $(this).next().toggle();
  },function(){
    $(this).next().toggle();
  })
})
```

### 单击显示隐藏元素并高亮标题
为了能有更好的用户体验，现在需要在用户单击“标题”链接后，不仅显示“内容”，而且高亮显示“标题”。

CSS 代码如下：
```css
.highlight{ background:#FF3300; }
```

需要完成以下几步步骤：

1. 等待 DOM 加载完毕。
2. 找到“标题”元素，添加 toggle() 方法，在 toggle() 方法里定义两个函数，分别代表显示和隐藏。
3. 在显示函数里，给“标题”添加高亮 class。
4. 在隐藏函数里，移除“标题”的高亮 class。

jQuery 代码为：
```javascript
$(function(){
    $("#panel h5.head").toggle(function(){
      $(this).addClass("highlight");
      $(this).next().show();
  },function(){
      $(this).removeClass("highlight");
      $(this).next().hide();
  });
})
```

运行代码后，如果“内容”是显示的，“标题”则会高亮显示；如果“内容”是隐藏的，则不会高亮显示“标题”。

## 4.事件冒泡

### 1.什么是冒泡

在页面上可以有多个事件，也可以多个元素响应同一个事件。

假设网页上有两个元素，其中一个元素嵌套在另一个元素里，并且都被绑定了 click 事件，同时 &lt;body&gt; 元素上也绑定了 click 事件，完整代码如下：

```html
<div id="content">
  外层div元素
  <span>内层span元素</span>
  外层div元素
</div>

<div id="msg"></div>
```

jQuery 代码如下：
```javascript
$(function(){
  // 为span元素绑定click事件
  $('span').bind("click",function(){
    var txt = $('#msg').html() + "<p>内层span元素被点击.<p/>";
    $('#msg').html(txt);
  });
  // 为div元素绑定click事件
  $('#content').bind("click",function(){
      var txt = $('#msg').html() + "<p>外层div元素被点击.<p/>";
    $('#msg').html(txt);
  });
  // 为body元素绑定click事件
  $("body").bind("click",function(){
    var txt = $('#msg').html() + "<p>body元素被点击.<p/>";
    $('#msg').html(txt);
  });
})
```
- 页面初始化效果如下图：<br>

![事件冒泡][1]

- 当单击内部 &lt;span&gt; 元素，即触发 &lt;span&gt; 元素的 click 事件时，会输出 3 条记录，如下图所示。这就是由事件冒泡引起的。<br>

![事件冒泡1][2]

在单击 &lt;span&gt; 元素的同时，也单击了包含 &lt;span&gt; 元素的元素 &lt;div&gt; 和包含 &lt;div&gt; 元素的元素 &lt;body&gt;，并且每一个元素都会按照特定的顺序响应 click。

元素的 click 事件会按照以下顺序“冒泡”。

1. &lt;span&gt;。
2. &lt;div&gt;。
3. &lt;body&gt;。

之所以称为冒泡，是因为事件会按照 DOM 的层次结构像水泡一样不断向上直至顶端，如下图所示：

![事件冒泡过程][3]

### 2.事件冒泡引发的问题

事件冒泡可能会引起预料之外的效果。上例中，本来只想触发 &lt;span&gt; 事件，然而 &lt;div&gt; 元素和 &lt;body&gt; 元素的 click 事件也同时被触发了。因此，有必要对事件的作用范围进行限制。

当单击 &lt;span&gt;  元素时，只触发 &lt;span&gt; 元素的 click 事件，而不触发 &lt;div&gt;  元素和 &lt;body&gt; 元素的 click 事件：当单击 &lt;div&gt; 元素时，只触发 &lt;div&gt; 元素的 click 事件，而不触发 &lt;body&gt; 元素的 click 事件。为了解决这些问题，介绍以下内容：

#### 事件对象

由于 IE-DOM 和标准 DOM 实现事件对象的方法各不相同，导致在不同浏览器中获取事件对象变得比较困难。针对这个问题，JQuery 进行了必要的扩展和封装，从而使得在任何浏览器中都能很轻松地获取事件对象以及事件对象的一些属性。

在程序中使用事件对象非常简单，只需要为函数添加一个参数，jQuery 代码如下：
```javascript
$("element").bind("click",function(event){  //event : 事件对象
  //...
});
```
这样，当单击 “element” 元素时，事件对象就被创建了。这个事件对象只有事件处理函数才能访问到。事件处理函数执行完毕后，事件对象就被销毁。

#### 停止事件冒泡

停止事件冒泡可以阻止事件中其他对象的事件处理函数被执行。在 jQuery 中提供了 `stopPropagation()` 方法来停止事件冒泡。
jQuery 代码如下：
```javascript
// 为span元素绑定click事件
$('span').bind("click",function(event){ //event:事件对象
  var txt = $('#msg').html() + "<p>内层span元素被点击.<p/>";
  $('#msg').html(txt);
  event.stopPropagation();    //  阻止事件冒泡
});
```

当单击 &lt;span&gt; 元素时，只会只会触发 &lt;span&gt; 元素上的 click 事件，而不会触发
&lt;div&gt; 元素和 &lt;body&gt; 元素的 click 事件。

可以用同样的方法解决 &lt;div&gt; 元素上的冒泡问题。
```javascript
// 为div元素绑定click事件
$('#content').bind("click",function(event){ //event:事件对象
    var txt = $('#msg').html() + "<p>外层div元素被点击.<p/>";
  $('#msg').html(txt);
  event.stopPropagation();    //  阻止事件冒泡
});
```
这样，当单击 &lt;span&gt; 元素或者 &lt;div&gt; 元素时，就只会输出相应的内容，而不会输出其他的内容，效果如下图所示：

![阻止事件冒泡][4]

#### 阻止默认行为

网页中的元素有自己默认的行为，例如，单击超链接后会跳转、单击“提交”按钮后表单会提交，有时需要阻止元素的默认行为。

在 jQuery 中，提供了 `preventDefault()` 方法来阻止元素的默认行为。

举一个例子，在项目中，经常需要验证表单，在单击“提交”按钮时，验证表单内容，例如某元素是否是必填字段，某元素长度是否够6位等，当表单不符合提交条件时，要阻止表单的提交（默认行为）。
HTML 代码如下：
```html
<form action="test.html">
用户名：<input type="text" id="username" />
<br/>
<input type="submit" value="提交" id="sub"/>
</form>

<div id="msg"></div>
```

jQuery 代码如下：
```javascript
$(function(){
   $("#sub").bind("click",function(event){
         var username = $("#username").val();  //获取元素的值
         if(username==""){     //判断值是否为空
         $("#msg").html("<p>文本框的值不能为空.</p>");  //提示信息
         event.preventDefault();  //阻止默认行为 ( 表单提交 )
     }
   })
})
```

当用户名为空时，单击“提交”按钮，会出现提示，并且表单不能提交。只有在用户名里输入内容后，才能提交表单。可见，preventDefault()方法能阻止表单的提交行为。

如果想同时对事件对象停止冒泡和默认行为，可以在事件处理函数中返回false。这是对在事件对象上同时调用 `stopPrapagation()` 方法和 `preventDefault()` 方法的一种简写方式。

在表单的例子中，可以把
```javascript
event.preventDefault(); //阻止默认行为
```

改写为：
```javascript
return false;
```

也可以把事件冒泡例子中的：
```javascript
event.stopPropaqation();  //停止事件冒泡
```

改写为：
```javascript
return false;
```

#### 事件捕获

事件捕获和事件冒泡是刚好相反的两个过程，事件捕获是从最顶端往下开始触发。

还是冒泡事件的例子，其中元素的click事件会按照以下顺序捕获。

1. &lt;body&gt;。
2. &lt;div&gt;。
3. &lt;span&gt;。

![事件捕获过程][5]

很显然，事件捕获是从最外层元素开始，然后再到最里层元素。因此绑定的 click 事件，首先会传递给 &lt;body&gt; 元素，然后传递给 &lt;div&gt; 元素，最后才传递给 &lt;span&gt; 元素。

遗憾的是，并非所有主流浏览器都支持事件捕获，并且这个缺陷无法通过 JavaScript 来修复。jQuery 不支持事件捕获，如果读者需要使用事件捕获，请直接使用原生的 JavaScript。

## 5.事件对象的属性

jQuery 在遵循 W3C 规范的情况下，对事件对象的常用属性进行了封装，使得事件处理在各大浏览器下都可以正常运行而不需要进行浏览器类型判断。

### 1.event.type

该方法作用是可以获取到事件的类型
```javascript
$(function(){
  $("a").click(function(event) {
    alert(event.type);//获取事件类型
    return false;//阻止链接跳转(阻止默认行为)
  });
})
```
以上代码运行后会返回"click"。

### 2.event.preventDefault()方法

[阻止默认行为方法介绍](#阻止默认行为) ，该方法的作用是阻止默认的事件行为。JavaScript 中符合 W3C 规范的 `preventDefault()` 方法在 IE 浏览器中却无效。jQuery 对其进行了封装，使之能兼容各种浏览器。

### 3.event.stopPropagation()方法

[停止事件冒泡方法介绍](#停止事件冒泡)，该方法的作用足阻止事件的冒泡。JavaScript 中符合 W3C 规范的 `stopPropagation()` 方法在 IE 浏览器中却无效。jQuery对其进行了封装，使之能兼容各种浏览器。

### 4.event.target

`event.target()` 方法的作用是获取到触发事件的元素。jQuery对 其封装后，避免了 W3C 、IE 和 safari 浏览器不同标准的差异。
```javascript
$(function(){
  $("a[href=http://www.nowamagic.net]").click(function(event) {
    var tg = event.target;  //获取事件对象
    alert(tg.href); //获取触发事件的<a>元素的href属性值
    return false; //阻止链接跳转
  });
})
```

以上代码运行后会返回"http://www.nowamagic.net"。

### 5.event.relatedTarget

方法在标准 DOM 中，mouseover 和 mouseout 所发生的元素可以通过 `event.target` 来访问，相关元素是通过 `event.relatedTarget` 来访问的。

`event.relatedTarget` 在 mouseover 中相当于 IE 浏览器的 `event.fromElement()` ，在 mouseout 中相当于 IE 浏览器的 `event.toElement` ，jQuery 对其进行了封装，使之能兼容各种浏览器。

### 6.event.pageX和event.pageY

该方法的作用是获取到光标相对于页面的x坐标和y班标。如果没有使用 jQuery 时，那么 IE 浏览器中是用 `event.x/event.y` ，而在 Firefox 浏览器中是用 `event.pageX/event.pageY` 。如果页面上有滚动条，则还要加上滚动条的宽度或高度。

在 IE 浏览器中还应该减去默认的2px的边框。

```javascript
$(function(){
  $("a").click(function(event) {
    alert("Current mouse position: " + event.pageX + ", " + event.pageY );  //获取鼠标当前相对于页面的坐标
    return false; //阻止链接跳转
  });
})
```

### 7.event.which

该方法的作用是在鼠标单击事件中获取到鼠标的左、中、右键；在键盘事件中获取键盘的按键。

- 比如，获取鼠标的左、中、右键：
```javascript
$("a").mousedown(function(e){
    alert(e.which)  // 1 = 鼠标左键 left; 2 = 鼠标中键; 3 = 鼠标右键
    return false;//阻止链接跳转
})
```
以上代码加载到页面后，用鼠标单击页面时，单击左、中、右键分别返回l、2、3。

- 比如，获取键盘的按键：
```javascript
$("input").keyup(function(){
  alert(e.which); //输出的是键码数字
  })
```

### 8.event.metaKey

针对不同浏览器对键盘中的 &lt;ctrl&gt; 按键解释不同，jQuery 也进行了封装，并规定 event.metaKey 为键盘事件中获取 &lt;ctrl&gt; 按键。

**注意：**更多的 event 的属性和方法可以访问：[更多事件对象-英文文档](http://docs.jquery.com/Events/jQuery.Event)，[更多事件对象-中文文档](http://www.css88.com/jqapi-1.9/category/events/event-object/)

### 9.event.originalEvent()方法

<del cite="《锋利的jQuery》里没有介绍这个event.originalEvent()方法">该方法的作用是指向原始的事件对象。</del>

## 6.移除事件

在绑定事件的过程中，不仅可以为同一个元素绑定多个事件，也可以为多个元素绑定同一个事件。假设网页上有一个 &lt;button&gt;元素，使用以下代码为该元素绑定多个相同的事件。
```html
<script>
$(function(){
 $('#btn').bind("click", function(){
       $('#test').append("<p>我的绑定函数1</p>");
    }).bind("click", function(){
       $('#test').append("<p>我的绑定函数2</p>");
    }).bind("click", function(){
       $('#test').append("<p>我的绑定函数3</p>");
    });
})
</script>
<button id="btn">点击我</button>
<div id="test"></div>
```

当单击按钮后，会出现下图的效果：

![移除事件][6]

### 1.移除按钮元素上以前注册的事件

首先在网页上添加一个移除事件的按钮。
```html
<button id="delAll">删除所有事件</button>
```

然后为按钮绑定一个事件，jQuery 代码如下：
```javascript
$('#delAll').click(function(){
  //处理函数
})
```

最后需要为该事件编写处理函数用于删除元素的所有 click 事件，jQuery 代码如下：
```javascript
$('#delAll').click(function(){
  $('#btn').unbind("click");
});
```

因为元素绑定的都是 click 事件，所以不写参数也可以达到同样的目的，jQuery 代码如下：
```javascript
$('#delAll').click(function(){
  $('#btn').unbind();
});
```

下面来看看 `unbind()` 方法的语法结构：
```javascript
unbind([type],[data]);
```

第 1 个参数是事件类型，第 2 个参数是将要移除的函数，具体说明如下：
1. 如果没有参数，则删除所有绑定的事件。
2. 如果提供了事件类型作为参数，则只删除该类型的绑定事件。
3. 如果把在绑定时传递的处理函数作为第 2 个参数，则只有这个特定的事件处理函数会被删除。

### 2.移除&lt;button&gt;元素的其中一个事件

首先需要为这些匿名处理函数指定一个变量。
例如下面的 jQuery 代码：
```javascript
$(function(){
 $('#btn').bind("click", myFun1 = function(){
       $('#test').append("<p>我的绑定函数1</p>");
    }).bind("click", myFun2 = function(){
       $('#test').append("<p>我的绑定函数2</p>");
    }).bind("click", myFun3 = function(){
         $('#test').append("<p>我的绑定函数3</p>");
      });
})
```

然后就可以单独删除某一个事件了，jQuery 代码如下：
```javascript
$('#delTwo').click(function(){
  $('#btn').unbind("click",myFun2); //删除“绑定函数2”
});
```

当单击“删除第二个事件”按钮后，再次单击“点击我”按钮，显示如下图的效果。
![移除特定事件][7]

另外，对于只需要触发一次，随后就要立即解除绑定的情况，jQuery 提供了一种简写方法——`one()` 方法。`one()` 方法可以为元素绑定处理函数。当处理函数触发一次后，立即被删除。即在每个对象上，事件处理函数只会被执行一次。

`one()` 方法的结构与 `bind()` 方法类似，使用方法也与 `bind()` 方法相同，其语法结构如下：
```javascript
one (type, [data], fn);
```

示例代码如下：
```javascript
$(function(){
 $('#btn').one("click", function(){
       $('#test').append("<p>我的绑定函数1</p>");
    }).one("click", function(){
       $('#test').append("<p>我的绑定函数2</p>");
    }).one("click", function(){
       $('#test').append("<p>我的绑定函数3</p>");
    });
})
```

使用 `one()` 方法为 &lt;button&gt; 元素绑定单击事件后，只在用户第 1 次单击按钮时，处理函数才执行，之后的单击就不会再起作用。

**注意：**jQuery 1.7新增了 `on()` ,`off()` ,`delegate()` 和`undelegate()` 事件绑定。具体介绍参考《锋利的jQuery(第2版)。

## 7.模拟操作

### 1.常用模拟

以上的例子都是用户必须通过单击按钮，才能触发 click 事件，但是有时，需要通过模拟用户操作，来达到单击的效果。例如在用户进入页面后，就触发 click 事件，而不需要用户去主动单击。

在 jQuery 中，可以使用 `trigger()` (trigger:触发)方法完成模拟操作。例如可以使用下面的代码来触发 id 为 btn 的按钮的 click 事件。
```javascript
$('#btn').trigger("click");
```

这样，当页面加载完毕后，就会立刻输出想要的效果。如图所示：

![移除事件][6]

也可以直接简写 `click()`，来达到同样的效果：
```javascript
$('#btn').click();
```

### 2.触发自定义事件

`trigger()` 方法不仅能触发浏览器支持的具有相同名称的事件，也可以触发自定义名称的事件。

例如为元素绑定一个 “myClick” 的事件，jQuery 代码如下：
```javascript
$(function(){
 $('#btn').bind("myClick", function(){
  $('#test').append("<p>我的自定义事件.</p>");
});
```

想要触发这个事件，可以使用以下代码来实现：
```javascript
$('#btn').trigger("myClick");
```

实现效果如下图所示：

![触发自定义事件][8]

### 3.传递数据

`trigger(type[，data])` 方法有两个参数，
1. 第 1 个参数是要触发的事件类型，
2. 第 2 个参数是要传递给事件处理函数的附加数据，以数组形式传递。

通常可以通过传递一个参数给回调函数来区别这次事件是代码触发的还是用户触发的。

下面是一个传递数据的例子。
```javascript
$(function(){
 $('#btn').bind("myClick", function(event, message1, message2){ //获取数据
  $('#test').append( "<p>"+message1 + message2 +"</p>");
});
 $('#btn').click(function(){
  $(this).trigger("myClick",["我的自定义","事件"]);
 }).trigger("myClick",["我的自定义","事件"]);
})
```

### 4.执行默认操作

trigger()方法触发事件后，会执行浏览器默认操作。例如：
```javascript
$("input").trigger("focus");
```

以上代码不仅会触发为 &lt;input&gt; 元素绑定的 focus 事件，也会使 &lt;input&gt; 元素本身得到焦点（这是浏览器的默认操作）。

如果只想触发绑定的 focus 事件，而不想执行浏览器默认操作，可以使用 jQuery 中另一个类似的方法——`triggerHandler()` 方法。
```javascript
$("input").triggerHandler("focus");
```

该方法会触发 &lt;input&gt; 元素上绑定的特定事件，同时取消浏览器对此事件的默认操作，即文本框只触发绑定的 focus 事件，不会得到焦点。

## 8.其他用法

前面已经对 `bind()` 方法进行了介绍，`bind()` 方法不仅能为以上绑定浏览器支持的具有相同名称的事件，也可以绑定自定义事件。不仅如此， `bind()` 方法还能做很多的事情。

### 1.绑定多个事件类型

例如可以为元素一次性绑定多个事件类型。jQuery 代码如下：
```javascript
$(function(){
 $("div").bind("mouseover mouseout", function(){
    $(this).toggleClass("over");
 });
})
```

当光标滑入 &lt;div&gt; 元素时，该元素的 class 切换为 “over” ；当光标滑出 &lt;div&gt; 元素时，class 切换为先前的值。这段代码等同于下面的代码：
```javascript
$(function(){
  $("div").bind("mouseover",function(){
    $(this).toggleClass("over");
  }).bind("mouseout",function(){
    $(this).toggleClass("over");
  });
});
```

很显然，第 1 种方式能减少代码量，这就是 jQuery 提倡的 “write less，do more”（写得更少，做得更多）理念。

### 2.添加事件命名空间，便于管理

例如可以把为元素绑定的多个事件类型用命名空间规范起来，jQuery 代码如下：

```javascript
$(function(){
  $("div").bind("click.plugin",function(){
    $("body").append("<p>click事件</p>");
  });
  $("div").bind("mouseover.plugin", function(){
    $("body").append("<p>mouseover事件</p>");
  });
  $("div").bind("dblclick", function(){
    $("body").append("<p>dblclick事件</p>");
  });
  $("button").click(function() {
    $("div").unbind(".plugin");
  });
})
```

在所绑定的事件类型后面添加命名空间，这样在删除事件时只需要指定命名空间即可。单击 &lt;button&gt; 元素后，“plugin” 的命名空间被删除，而不在 “plugin” 的命名空间的 “dblclick” 事件依然存在。

删除多个事件代码也可以写成以下链式代码，但显然上面的方式写得更少。
```javascript
$("div").unbind("click").unbind("mouseover");
```

### 3.相同事件名称，不同命名空间执行方法

例如可以为元素绑定相同的事件类型，然后以命名空间的不同按需调用，jQuery 代码如下：
```javascript
$(function(){
  $("div").bind("click",function(){
    $("body").append("<p>click事件</p>");
  });
  $("div").bind("click.plugin", function(){
    $("body").append("<p>click.plugin事件</p>");
  });
  $("button").click(function() {
    $("div").trigger("click!");    // 注意click后面的感叹号
  });
})
```

当单击 &lt;div&gt; 元素后，会同时触发 click 事件和 click.plugin 事件。如果只是单击 &lt;button&gt; 元素，则只触发 click 事件，而不触发 click.plugin 事件。注意，`trigger("click!")` 后面的感叹号的作用是匹配所有不包含在命名空间中的 click 方法。

如果需要两者都被触发，改为如下代码即可：
```javascript
$("div").trigger("click");  //去掉感叹号
```

到此，jQuery 中的事件已经介绍完了。

[1]:{{ site.url }}/assets/maopao.png '事件冒泡'
[2]:{{ site.url }}/assets/maopao1.png '事件冒泡1'
[3]:{{ site.url }}/assets/maopaogc.png '事件冒泡过程'
[4]:{{ site.url }}/assets/maopao2.png '阻止事件冒泡'
[5]:{{ site.url }}/assets/buhuogc.png '事件捕获过程'
[6]:{{ site.url }}/assets/yichusj.png '移除事件'
[7]:{{ site.url }}/assets/yichusj2.png '移除特定事件'
[8]:{{ site.url }}/assets/chufazdy.png '触发自定义事件'



