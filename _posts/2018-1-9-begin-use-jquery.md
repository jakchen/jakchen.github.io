---
layout: post
title:  "开始使用 jQuery(6)-jQuery中的动画"
categories: jQuery
tags: jQuery
author: jakchen
---
* content
{:toc}

动画效果也是 jQuery 库吸引人的地方。通过 jQuery 的动画方法，能够轻松地为网页添加非常精彩的视觉效果，给用户一种全新的体验。




## 1.show()方法和hide()方法

### 1.show()方法和hide()方法

`show()` 方法和 `hide()` 方法是 jQuery 中最基本的动画方法。在 HTML 文档里，为一个元素调用 `hide()` 方法，会将该元素的 display 样式改为 “none”。

例如：使用如下代码隐藏 element 元素。
```javascript
$("element").hide();    //通过hide()方法将 element 元素隐藏
```

这段代码的功能与用 `css()` 方法设置 display 属性效果相同：
```javascript
$("element").css("display","none"); //通过css() 方法隐藏元素
```

当把元素隐藏后，可以使用 `show()` 方法将元素的 display 样式设置为先前的显示状态（“block”或“inline”或者其他除了“none”之外的值）。

jQuery 代码如下：
```javascript
$("element").show();
```

在前面的例子中，已经多次使用 `hide()` 方法和 `show()` 方法，通过这两种方法可以控制“内容”的显示和隐藏。

jQuery 代码如下：
```javascript
$(function(){
  $("#panel h5.head").toggle(function(){
    $(this).next().hide();
  },function(){
    $(this).next().show();
  })
})
```

注意 `hide()` 方法在将“内容”的 display 属性值设置为“none”之前，会记住原先的 display 属性。当调用 `show()` 方法时，会根据 `hide()` 方法记住 display 属性值来显示元素。

在本例中，“内容”的 display
属性的值是 “block”，当单击“标题”链接执行 `hide()` 方法的时候，`hide()` 方法会做两步动作，首先会记住“内容”的 display 属性的值“block”，然后吧 display 属性的值设置为“none”。

当执行 `show()` 方法的时候，“内容”的 display 属性的值就会被还原为调用 `hide()` 方法前的状态。

**注意：**用 jQuery 做动画效果要求要在标准模式下，否则可能会引起动画抖动。标准模式即要求文档头部包含如下的 DTD 定义：`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" " http://www.w3.org/TR/html4/loose.dtd">`

### 2.show()方法和hide()方法让元素动起来

`show()` 方法和 `hide()` 方法在不带任何参数的情况下，相当于 `css("display","none/block/inline")` ，作用是立即隐藏或显示匹配的元素，不会有任何动画。如果希望在调用 `show()` 方法时，元素慢慢地显示出来，可以为 `show()` 方法指定一个速度参数，例如，指定一个速度关键字 “slow” 。jQuery 代码如下：
```javascript
$("element").show("slow");
```

运行该代码后，元素将在600毫秒内慢慢地显示出来。其他的速度关键字还有 “normal” 和 “fast” （长度分别是400毫秒和200毫秒）。

不仅如此，还可以为显示速度指定一个数字，单位是毫秒。

例如，使用如下代码使元素在 1 秒钟（1000毫秒）内显示出来：
```javascript
$("element").show(1000);
```

类似的，以下代码将使元素在 1 秒钟（1000毫秒）内隐藏：
```javascript
$("element").hide(1000);
```

在前面的例子中，把其中的 `hide()` 方法改为 `hide(600)`，`show()` 方法改为 `show(600)`。

jQuery 代码如下：
```javascript
$(function(){
  $("#panel h5.head").toggle(function(){
    $(this).next().hide(600);
  },function(){
    $(this).next().show(600);
  });
})
```

运行该代码后，当单击“标题链接”时，“内容”已经产生动画了。效果如下图所示：

![显示隐藏元素][1]

从代码执行过程中，可以发现，`hide(600)` 方法会同时减少“内容”的高度、宽度和不透明度，直至这 3 个属性的值都为 0，最后设置该元素的 CSS 规则为“display:none”。同理，`show(600)` 方法则会从上到下增大“内容”的高度，从左到右增大“内容”的宽度，同时增加“内容”的不透明度，直至新闻内容完全显示。

## 2.fadeIn()方法和fadeOut()方法

与 `show()` 方法不相同的是，`fadeIn()` 方法和 `fadeOut()` 方法只改变元素的不透明度。
- `fadeOut()` 方法会在指定的一段时间内降低元素的不透明度,直到元素完全消失("display:none")。
- fadeIn()方法则相反。

在上个例子中，如果只想改变“内容”的不透明度，就可以使用 `fadeOut()` 方法。

jQuery 代码如下：
```javascript
$(function(){
    $("#panel h5.head").toggle(function(){
    $(this).next().fadeOut();
  },function(){
    $(this).next().fadeIn();
  })
})
```

当第 1 次点击“标题”链接后，“内容”慢慢地消失了（淡出），当再次单击“标题”链接后，“内容”又慢慢地显示了（淡入），效果如下图
![淡入淡出][2]

## 3.slideUp()方法和slideDown()方法

`slideUp()` 方法和 `slideDown()` 方法只会改变元素的高度，
- 如果一个元素的 display 属性值为 “none”，当调用 `slideDown()` 方法时，这个元素将由上至下延伸显示。
- `slideUp()` 方法正好相反，元素将由下到上缩短隐藏。

使用 `slideUp()` 方法和 `slideDown()` 方法再次对“内容”的显示和隐藏方式进行改变，代码如下：
```javascript
$(function(){
    $("#panel h5.head").toggle(function(){
    $(this).next().slideUp();
  },function(){
    $(this).next().slideDown();
  })
})
```

![通过改变高度显示隐藏][3]

**注意：**jQuery 中的任何动画效果，都可以指定 3 种速度参数，即“slow” 、“normal” 和 “fast” （时间长度分别是 0.6 秒、0.4 秒和 0.2 秒）。当使用速度关键字时要加引号，例如 `show("slow")` ，如果用数字作为时间参数时就不需要加引号，例如 `show(1000)`。

## 4.自定义动画方法animate()

前面已经讲了 3 种类型的动画。
- 其中 `show()` 方法和 `hide()` 方法会同时修改元素的多个样式属性，即高度、宽度和不透明度；
- `fadeOut()` 方法和 `fadeIn()` 方法只会修改元素的不透明度；
- `slideDown()` 方法和 `slideUp` 方法只会改变元素的高度。

很多情况下，这些方法无法满足用户的各种需求，那么就需要对动画有更多的控制，需要采取一些高级的自定义动画来解决这些问题。在 jQuery 中，可以使用 `animate()` 方法来自定义动画。其语法结构为：
```javascript
animate(params,speed,callback);
```

参数说明如下：
- params：一个包含样式属性及值的映射，比如`{property1:"value1",property2:"value2",··· }`。
- speed：速度参数，可选。
- callback：在动画完成时执行的函数，可选。

### 1.自定义简单动画

前面的几个例子，从不同的方面使元素动了起来，`animate()` 方法也可以使元素动起来，而且 `animate()` 方法更具有灵活性。通过 `animate()` 方法，能够实现更加精致新颖的动画效果。

首先来看一个简单例子，在一个空白的 HTML 文档，里面有一个 id="panel" 的 &lt;div&gt; 元素，当 &lt;div&gt; 元素被单击后，能在页面上横向飘动。

先给这个 &lt;div&gt; 元素添加CSS样式。
```css
#panel {
  position: relative;
  width: 100px;
  height:100px;
  border: 1px solid #0050D0;
  background: #96E555;
  cursor: pointer
}
```

为了使这个元素动起来，要更改元素的 “left” 样式属性。需要注意的是在使用 `animate()` 方法之前，必须先把样式的position样式设置为“relative”或者“absolute”。有了这个值，就可以调整样式的“left”属性，使元素动起来。

现在，添加如下 jQuery 代码：
```javascript
$(function(){
  $("#panel").click(function(){
    $(this).animate({left: "500px"}, 3000);
  })
})
```

在本段代码中，首先为 id 为  “panel” 的元素创建一个单击事件，然后对元素加入 `animate()` 方法，使元素在 3 秒（3000毫秒）内，向右移动 500 像素。运行效果如下图所示：
![自定义简单动画][4]

### 2.累加、累减动画

在之前的代码中，设置了{left:"500px"} 作为动画参数。如果在 500px 之前加上 “+=” 或者 “-=” 符号即表示在当前位置累加或者累减。代码如下：
```javascript
$(function(){
  $("#panel").click(function(){
    $(this).animate({left: "+=500px"}, 3000); //在当前位置累加 500px
  })
})
```

### 3.多重动画

- （1）同时执行多个动画

在上面的例子中，通过控制属性 left 的值实现了动画的效果，这是一个很单一的动画。如果需要同时执行多个动画，例如在元素向右滑动的同时，放大元素的高度。根据 `animate()` 方法的语法结构，可以写出如下的 jQuery 代码：

```javascript
$(function(){
  $("#panel").click(function(){
    $(this).animate({left:"500px",height:"200px"}, 3000);
  })
})
```

运行代码后，&lt;div&gt; 元素在向右滑动的同时，也会放大高度。如下图：
![同时执行多个动画][5]

-（2）按顺序执行多个动画

上例中，两个动画效果（left:"500px"和height:"200px"）是同时发生的，如果想要按顺序执行动画，例如让 &lt;div&gt; 元素先向右滑动，然后再放大它的高度，只需把代码拆开，然后按照顺序写就可以了，jQuery 代码如下：
```javascript
$(this).animate({left:"500px"},3000);
$(this).animate({height:"200px"},3000);
```

因为 `animate()` 方法都是对同一个 jQuery 对象进行操作，所有也可以写成链式的写法，代码如下：
```javascript
$(this).animate({left:"500px"},3000)
       .anmate({height:"200px"},3000);
```
这样一来，就满足上文提出的需求了。在“left”这个定位属性改变之前，“height”属性将不会被改变。像这样，动画效果执行具有先后顺序，称为**“动画队列”**。

### 4.综合动画

接下来将完成更复杂的动画。单击 &lt;div&gt; 元素后让它向右移动的同时增大它的高度，并将它的不透明度从 50% 变换到 100%，然后再让它从上到下移动，同时它的宽度变大，当完成这些效果后，让它以淡出的方式隐藏。

实现这些功能的jQuery 代码如下：

按照 `animate` 的规则则可以对元素进行各种动画操作，进行各种动画操作的组合：
```javascript
$(function(){
    $("#panel").css("opacity", "0.5");//设置不透明度
    $("#panel").click(function(){
      $(this).animate({left: "400px", height:"200px" ,opacity: "1"}, 3000)
             .animate({top: "200px" , width :"200px"}, 3000 )
             .fadeOut("slow");
    });
});
```

运行代码后，动画效果一步步执行完毕。通过这个例子可以看出，为同一元素应用多重效果时，可以通过链式方式对这些效果进行排队。

## 5.动画回调函数

在上例中，如果想在最后一步切换元素的 CSS 样式，而不是隐藏元素：
```javascript
css("border","5px solid blue");
```

如果只是按照常规的方式，将 `fadeOut("slow")` 改为 `css("border","5px solid blue")`

这样并不能得到预期。预期的效果是在动画的最后一步改变元素的样式，而实际的效果是，刚开始执行动画的时候，`css()` 方法就被执行了。

出现这个问题的原因是 `css()` 方法并不会加入到动画队列中，而是立即执行。可以使用回调函数(callback)对非动画方法实现排队。只要把 `css()` 方法写在最后一个动画的回调函数里即可。代码如下：

```javascript
$("#panel").click(function(){
$(this).animate({left: "400px", height:"200px" ,opacity: "1"}, 3000)
       .animate({top: "200px" , width :"200px"}, 3000 ,function(){
             $(this).css("border","5px solid blue");
         })
});
```

这样一来，`css()` 方法就加入到动画队列中了，从而满足了上文提出的需求。

**注意：**callback 回调函数适用于 jQuery 所有的动画效果方法，例如 `slideDown()` 方法的回调函数：
```javascript
$("#element").slideDown("normal",function(){
  //在效果完成后做其他的事情
});
```

这段代码表示 id="element" 的元素将在 0.4 秒内（正常速度）向下完全展开。当动画完成后，执行回调函数体内的代码。

## 6.停止动画和判断是否处于动画状态

### 1.停止元素的动画

很多时候需要停止匹配元素正在进行的动画，例如上例的动画，如果需要在某处停止动画，需要使用 `stop()` 方法。 `stop()` 方法的语法结构为：
```javascript
stop([clearQueue],[gotoEnd]);
```
参数 **clearQueue** 和 **gotoEnd** 都是可选的参数，为 Boolead 值（true或flase）。
- **clearQueue** 代表是否要清空未执行完的动画队列，
- **gotoEnd** 代表是否直接将正在执行的动画跳转到末状态。

- 如果直接使用 `stop()` 方法，则会立即停止当前正在进行的动画，如果接下来还有动画等待继续进行，则以当前状态开始接下来的动画。

经常会遇到这种情况，在为一个元素绑定 hover 事件之后，用户把光标移入元素时会触发动画效果，而当这个动画还没结束时，用户就将光标移出这个元素了，那么光标移出的动画效果将会被放进队列之中，等待光标移入的动画结束后再执行。因此如果光标移入移出得过快就会导致动画效果与光标的动作不一致。此时只要在光标的移入、移出动画之前加入 `stop()` 方法，就能解决这个问题。`stop()` 方法会结束当前正在进行的动画，并立即执行队列中的下一个动画。以下代码就可以解决刚才的问题。
```javascript
$("#panel").hover(function() {
  $(this).stop().animate({height : "150",width : "300"} , 200 );
},function() {
  $(this).stop().animate({height : "22",width : "60" } , 300 );
});
```

- 如果遇到组合动画，例如：

```javascript
$("#panel").hover(function() {
    $(this).stop()
           .animate({height : "150" } , 200 ) //如果在此时触发了光标移出的事件
                                              //将执行下面的动画
                                              //而非光标移出事件中的动画
           .animate({width : "300" } , 300 )
},function() {
    $(this).stop()
           .animate({height : "22" } , 200 )
           .animate({width : "60" } , 300 )
});
```

此时只用一个参数的 `stop()` 方法就显得力不从心了。因为 `stop()` 方法只会停止正在进行的动画，如果动画正执行在第 1 阶段（改变 height 的阶段），则触发光标移出事件后，只会停止当前的动画，并继续执行下面的 `animate({width:"300"},300)` 动画，而光标移出事件中的动画要等这个动画结束后才会继续执行，这显然不是预期的结果。这种情况下 `stop()` 方法的第 1 个参数就发挥作用了，可以把第 1个参数（clearQueue）设置为 true，此时程序会把当前元素接下来尚未执行完的动画队列都清空。把上面的代码改成如下代码，就能实现预期的效果。

```javascript
$("#panel").hover(function() {
    $(this).stop(true)
           .animate({height : "150" } , 200 ) //如果在此时触发了光标移出事件
                                              //直接跳过后面的动画队列
           .animate({width : "300" } , 300 )
  },function() {
    $(this).stop(true)
           .animate({height : "22" } , 200 )
           .animate({width : "60" } , 300 )
  });
```

- 第 2 个参数（gotoEnd）可以用于让正在执行的动画直接到达结束时刻的状态，通常用于后一个动画需要基于前一个动画的末状态的情况，可以通过 `stop(false,true)` 这种方式来让当前动画直接到达末状态。

当然也可以两者结合起来使用 `stop(true,true)` 即停止当前动画并直接到达当前动画的末状态，并清空动画队列。

注意，jQuery 只能设置正在执行的动画的最终状态，而没有提供直接到达未执行动画队列最终状态的方法。例如有一组动画：
```javascript
$("div.content")
  .animate({width : "300" } , 200 )
  .animate({height : "150" } , 300 )
  .animate({opacity : "0.2" } ,2000);
```

无论怎么设置 `stop()` 方法，均无法在改变 “width” 或者 “height” 时，将此 &lt;div&gt; 元素的末状态变成 300 x 150 的大小，并且设置透明度为 0.2。

### 2.判断元素是否处于动画状态

在使用 `animate()` 方法的时候，要避免动画积累而导致的动画与用户的行为不一致。当用户快速在某个元素上执行 `animate()` 动画时，就会出现动画积累。解决方法是判断元素是否处于动画状态，如果元素不处于动画状态，才为元素添加新的动画，否则不添加。代码如下：

当执行animate（）动画时，判断是否处于动画可以：
```javascript
if(!$(element).is(":animated")){  //判断元素是否正处于动画状态
  //如果当前没有进行动画，则添加新动画或者执行其他操作
}
```

这个判断方法在 `animate()` 动画中经常被用到，需要特别注意。

### 3.延迟动画

在动画执行的过程中，如果想对动画进行延迟操作，那么可以使用 `delay()` 方法，使用方式如下：

```javascript
$(this).animate({left: "400px", height:"200px" ,opacity: "1"}, 3000)
       .delay(1000)
       .animate({top: "200px" , width :"200px"}, 3000 )
       .delay(2000)
       .fadeOut("slow");
```

`delay()` 方法允许我们将队列中的函数延时执行。它既可以推迟动画队列中函数的执行，也可以用于自定义队列。

## 7.其他动画效果

除了上面提到的动画方法，jQuery 中还有 4 个专门用于交互的动画方法。

- `toggle(speed,[callback])`
- `slideToggle(speed,[callback])`
- `fadeTo(speed,opacity,[callback])`
- `fadeToggle(speed,[easing],[callback])`。

### 1.toggle()方法

`toggle()` 方法可以切换元素的可见状态。如果元素是可见的，则切换为隐藏；如果元素是隐藏的，则切换成可见的。

给“内容”添加 `toggle()` 事件，代码如下：
```javascript
$("#panel h5.head").click(function(){
    $(this).next().toggle();
})
```

当单击“标题”链接后，“内容”会在可见和隐藏两种状态之间切换。

相当于以下 jQuery 代码：
```javascript
$("#panel h5.head").toggle(function(){
  $(this).next().hide();
},function(){
  $(this).next().show();
});
```

### 2.slideToggle()方法

`slideToggle()` 方法通过高度的变化切换匹配元素的可见性。这个动画效果只调整元素的高度。

相当于 `slideUp()` 和 `slideDown` 方法不断的切换组合。

给“内容”添加 `slideToggle()` 事件，代码如下：
```javascript
$("#panel h5.head").click(function(){
    $(this).next().slideToggle();
})
```

当单击“标题”链接后，“内容”会在可见和隐藏两种状态之间切换，不过是通过改变元素的高度来实现的。

相当于以下 jQuery 代码：
```javascript
$("#panel h5.head").toggle(function(){
    $(this).next().slideUp();
},function(){
    $(this).next().slideDown();
});
```

### 3.fadeTo()方法

`fadeTo()` 方法可以把元素的不透明度以渐进的方式调整到指定的值。这个动画只调整元素的不透明度，即匹配的元素的高度和宽度不会发生变化。

给“内容”添加 `fadeTo()` 事件，代码如下：
```javascript
$("#panel h5.head").click(function(){
    $(this).next().fadeTo(600, 0.2);
})
```

当“标题”链接被单击后，“内容”会渐渐地调整到指定的不透明度（20%）。


### 4.fadeToggle()方法

`fadeToggle()` 方法通过不透明度变化来切换匹配元素的可见性。这个动画效果只调整元素的不透明度。

给“内容”添加 `fadeToggle()` 事件，代码如下：
```javascript
$("#panel h5.head").click(function(){
    $(this).next().fadeToggle();
})
```

相当于以下 jQuery 代码：
```javascript
$("#panel h5.head").toggle(function(){
    $(this).next().fadeOut();
},function(){
    $(this).next().fadeIn();
});
```

## 8.动画方法概括

从基本动画方法 `hide()` 和 `show()` ，到 `fadeIn()` 和 `fadeOut()` ,然后到 `slideUp()` 和 `sildeDown()`，再到自定义动画方法 `animate()` ，最后到交互动画方法 `toggle()` 、 `slideToggle()` 、 `fadeTo()` 、和 `fadeToggle()` 。

### 1.改变样式属性

<iframe src="{{ site.url }}/assets/html/jQuery-animate.html" frameborder="0" width="100%" height="460px;"></iframe>

需要特别注意 `animate()` 方法，可以使用它来替代其他所有的动画方法。

- 用 `animate()` 方法代替 **show()** 方法
```javascript
$('p').animate({height:"show", width:"show", opacity:"show"}, 400);
```
等价于
```javascript
$("p").show(400);
```

- 用 `animate()` 方法代替 **fadeIn()** 方法
```javascript
$('p').animate({opacity:"show"}, 400);
```
等价于
```javascript
$("p").fadeIn(400);
```

- 用 `animate()` 方法代替 **slideDown()**方法
```javascript
$('p').animate({height:"show"}, 400);
```
等价于
```javascript
$("p").fadeDown(400);
```

- 用 `animate()` 方法代替 **fadeTo()** 方法
```javascript
$('p').animate({opacity:"0.6"}, 400);
```
等价于
```javascript
$("p").fadeTo(400,0.6);
```

- 用 `animate()` 方法代替 **hide()** 方法
```javascript
$('p').animate({height:"hiden", width:"hiden", opacity:"hiden"}, 400);
```

- 用 `animate()` 方法代替 **fadeOut()** 方法
```javascript
$('p').animate({opacity:"hiden"}, 400);
```

- 用 `animate()` 方法代替 **slideUp()** 方法
```javascript
$('p').animate({height:"hiden"}, 400);
```

事实上，这些动画就是 `animate()` 方法的一种内置了特定样式属性的简写形式。在 `animate()` 方法中，这些特定样式的属性值可以为“show”、“hide” 和 “toggle”，也可以是自定义数字（值）。

### 2.动画队列

1. 一组元素上的动画效果
- 当在一个 `animate()` 方法中应用多个属性时，动画是同时发生的。
- 当以链式的写法应用动画方法时，动画是按照顺序发生的（除非 queue 选项值为 false）。
2. 多组元素上的动画效果
- 默认情况下，动画都是同时发生的。
- 当以回调的形式应用动画方式时（包括动画的回调函数和 `queue()` 方法的回调函数），动画是按照回调顺序发生的。

另外，在动画方法中，要注意其他非动画方法会插队，例如 `css()` 方法要使非动画方法也按照顺序执行，需要把这些方法写在动画方法的回调函数中或者 `queue` 方法中。

[1]:{{ site.url }}/assets/hide.gif '显示隐藏元素'
[2]:{{ site.url }}/assets/fade.gif '淡入淡出'
[3]:{{ site.url }}/assets/slide.gif '通过改变高度显示隐藏'
[4]:{{ site.url }}/assets/animate.gif '自定义简单动画'
[5]:{{ site.url }}/assets/animate2.gif '同时执行多个动画'