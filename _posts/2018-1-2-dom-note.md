---
layout: post
title:  "DOM 思维导图学习笔记"
categories: DOM
tags: DOM
author: jakchen
---
* content
{:toc}

[点击查看 DOM 思维导图学习笔记]({{ site.url }}/assets/DOM.png)

DOM (document object model)文档对象模型，是把整个HTML文档，看做是一个节点模型，它定义了访问 HTML 和 XML 文档的标准。




W3C DOM 标准被分为 3 个不同的部分：

- 核心 DOM - 针对任何结构化文档的标准模型
- XML DOM - 针对 XML 文档的标准模型
- HTML DOM - 针对 HTML 文档的标准模型

[点击查看 DOM 操作分类详细介绍]({{ site.url }}/2018/01/07/begin-use-jquery/#dom操作分类)

HTML DOM 定义了所有 HTML 元素的对象和属性，以及访问它们的方法。

换言之，HTML DOM 是关于如何获取、修改、添加或删除 HTML 元素的标准。

## D-document
![document]({{ site.url }}/assets/dom-d.png)

## O-object
![object]({{ site.url }}/assets/dom-o.png)

## O-model
![model]({{ site.url }}/assets/dom-m.png)

### 元素节点方法&属性
![model]({{ site.url }}/assets/elenode.png)

### 节点方法

```javascript
appendChild(node) //在末尾插入新的子节点（元素）
node.appendChild(newListItem);

removeChild(node) //删除子节点（元素）
node.removeChild(node) //node：你要移除的节点对象。
//例如：
var list=document.getElementById("myList"); list.removeChild(list.childNodes[0]);

replaceChild() //替换子节点。
node.replaceChild(newnode,oldnode) //新节点可以是文本中已存在的，或者是你新创建的。

insertBefore() //在指定的子节点前面插入新的子节点。
node.insertBefore(newnode,existingnode)
/*  newnode：要插入的节点对象
 *  existingnode：要添加新的节点前的子节点。
 */

createAttribute()  //创建属性节点。
document.createAttribute(attributename) // attributename：要创建的属性名称。

createElement()  //创建元素节点。
document.createElement(nodename) //nodename：创建元素的名称。

createTextNode()  //创建文本节点。
document.createTextNode(text)  //text：文本节点的文本。

getAttribute()  //返回指定的属性值。
element.getAttribute(attributename)  //attributename：想获取的属性值。

setAttribute() //把指定属性设置或修改为指定的值。
element.setAttribute(attributename,attributevalue)
/* attributename：要添加的属性名称。
 * attributevalue：要添加的属性值。
 */
```

![node-f]({{ site.url }}/assets/node-f.png)

### 节点属性


- **innerHTML**
- **nodeName**
- **nodeValue**
- **nodeType**
- **parentNode**
- **childNodes**
- **nextSibling**
- **previousSibling**
- **attributes**


![node-a]({{ site.url }}/assets/node-a.png)

## DOM 访问

1. getElementById()
2. getElementsByTagName()
3. getElementsByClassName()
4. getElementsByName()

getElementsByName() 方法可返回带有指定名称的对象的集合。

**语法：** `document.getElementsByName(name)`

name:必须。元素的名称。

```html
<input name="x" type="radio" value="猫">
<script>
var x=document.getElementsByName("x");
</script>
```
![dom-fw]({{ site.url }}/assets/dom-fw.png)

## DOM 修改

![dom-xg]({{ site.url }}/assets/dom-xg.png)

## HTML DOM

### 元素
![html-dom-ele]({{ site.url }}/assets/html-dom-ele.png)

### 事件
![html-dom-sj]({{ site.url }}/assets/html-dom-sj.png)

### 导航
![html-dom-dh]({{ site.url }}/assets/html-dom-dh.png)

<br><br><br>
本文参考链接：[HTML DOM 教程 - 菜鸟教程](http://www.runoob.com/htmldom/htmldom-tutorial.html)