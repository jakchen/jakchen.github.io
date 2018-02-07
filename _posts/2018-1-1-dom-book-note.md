---
layout: post
title:  "《JavaScript DOM 编程艺术》笔记"
categories: DOM
tags: DOM
author: jakchen
---
* content
{:toc}

JS-DOM 编程艺术笔记



## DOM 提供的五个方法:

-  getElementByld
-  getElementsByTagName
-  getElementsByClassName
-  getAttribute
-  setAttribute

```javascript
  document.getElementByld("idName");
  document.getElementsByTagName("tagName");
  document.getElementsByClassName("className");
  object.getAttribute("attributeName");
  object. setAttribute("attributeName","value")
```

## DOM 提供的几个新属性:

事件处理函数：？···

- childNodes
- nodeType
- nodeValue
- firstChild
- lastChild

```javascript
  element.childNodes
  node.nodeType
  node.nodeValue
  node.firstChild; //等价于  node. childNodes[0];
  node.lastChild;//等价于node.childNodes[node.childNodes.length-l];
```

## 第五章
- 平稳退化:确保网页在没有 JavaScript的情况下也能正常工作。
- 分离JavaScript：把网页的结构和内容与JavaScript脚本的动作行为分开。
- 向后兼容性：确保老版本的浏览器不会因为你的脚本而死掉。
- 性能考虑：确定脚本执行的性能最优。
- 把事件添加到有着特定属性的一组元素上。getElementsByTagName和getAttribute
- 对象检测：if (!method) {return false;}

## 第六章

共享 onload 事件：

```javascript
function addLoadEvent(func) {
var oldonload = window.onload;
if (typeof window.onload != 'function') {
window.onload = func;
} else {
window.onload = function() {
oldonload();
func();
}
}
}
addLoadEvent(firstFunction);
addLoadEvent(secondFunction);
```

DOM Core 和 HTML-DOM:?···

## 第七章
动态创建标记：传统技术：`document.write`和`innerHTML`。DOM方法：`createElement`、`createTextNode`、`appendChild`、`insertBefore`

在现有元素后插入一个新元素
```javascript
insertAfter 函数
function insertAfter(newElement, targetElement) {
var parent = targetElement.parentNode;
if (parent.lastChild == targetElement) {
parent.appendChild(newElement);
} else {
parent.insertBefore(newElement, targetElement.nextSibling);}}
//nextSibling 属性：下一个兄弟元素。
```

Ajax:?···

## 第八章
- 充实文档内容：
- 得到隐藏在属性里的信息。
- 创建标记封装这些信息。
- 把这些标记插入到文档。

## 第九章
CSS-DOM:
style属性，获取和设置内嵌样式。
className 属性，
```javascript
function addClass(element,value) {
if (!element.className) {
element.className = value;
} else {
newClassName = element.className;
newClassName+= " ";
newClassName+= value;
element.className = newClassName;
}
}
```
调用：`addCIass(elementp,"intro")`;

## 第十章
js动画:`setTimeout()`，
`clearTimeout()`，