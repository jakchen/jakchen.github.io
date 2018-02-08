---
layout: post
title:  "开始使用 jQuery(2)-jQuery对象和DOM对象"
categories: jQuery
tags: jQuery
author: jakchen
---
* content
{:toc}

## DOM对象

通过 getElementById 或 getElementsByTagName 获取得到的 DOM 元素就是 DOM 对象。

DOM 对象可以使用 JavaScript 中的方法。例如：
```javascript
var domObj = getElementById("id"); //获得DOM对象
var ObjHTML = domObj.innerHTML; //使用JS中的属性——innerHTML
```




## jQuery对象

jQuery 对象就是通过 jQuery 包装 DOM 对象后产生的对象。

jQuery 对象是 jQuery 独有的。如果一个对象是 jQuery 对象, 那么它就可以使用 jQuery 里的方法。例如:

```javascript
$("#foo").html();//获取id为foo的元素内的html代码。.html()是jQuery里的方法
```

这段代码等同于

```javascript
document.getElementById("foo").innerHTML;
```

jQuery 对象无法使用 DOM 对象的任何方法, 同样 DOM 对象也不能使用 jQuery 里的任何方法

* 例如：jQuery 对象 $("#id").innerHTML 和 $("id").checked之类的写法都是错误的。可以用$("#id").heml()和$("#id").attr("checked")之类的jQuery方法来代替。

* 例如：document.getElementById("id").html()也会报错，只能用
document.getElementById("id").innerHTML语句。

## 相互转换

如果获取的是 jQuery 对象, 那么要在变量前面加上$，例如： `var $variable = jQuery 对象`

如果获取的是 DOM 对象, 则定义为： `var variable = DOM 对象`

```javascript
var $variable = jQuery 对象
var variable = DOM 对象
```

### jQuery对象转换成DOM对象

jQuery 对象不能使用 DOM 中的方法, 但如果对 jQuery 对象所提供的方法不熟悉，或者 jQuery 没有封装想要的方法, 不得不使用 DOM方法的时候, 有如下两种处理方法:

- (1) jQuery 对象是一个数组对象, 可以通过 [index] 的方法得到对应的 DOM对象。代码如下：
```javascript
var $cr = $("#cr"); //jQuery对象
var cr = $cr[0];    //DOM对象
```

- (2) 使用 jQuery 中的 get(index) 方法得到相应的 DOM 对象。代码如下：
```javascript
var $cr = $("#cr");   //jQuery对象
var cr = $cr.get(0);  //DOM对象
```

### DOM 对象转成 jQuery 对象

对于一个 DOM 对象, 只需要用 $() 把 DOM 对象包装起来(jQuery 对象就是通过 jQuery 包装 DOM 对象后产生的对象), 就可以获得一个 jQuery 对象。例如：
```javascript
var cr = document.getElementById("cr"); //DOM对象
var $cr = $(cr);                        //jQuery对象
```
转换后就可以使用 jQuery 中的方法了。

平时用到的jQuery对象都是通过$()函数制造出来的，$()函数就是一个jQuery对象的制造工厂。