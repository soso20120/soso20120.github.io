---
layout: post 
title: "回到页面顶部 - JS"
date: 2017-07-31 14:41:31 +0800
categories: [Web]
excerpt: 对JS中如何实现回到页面顶部
tags:
  - Web
  - JS
  - 前端
---

### Content

* content
{:toc}

### 1.锚点

该实现主要在页面顶部放置一个指定名称的锚点链接，然后在页面下方放置一个返回到该锚点的链接，用户点击该链接即可返回到该锚点所在的顶部位置。

```html
<div id="topAnchor"></div>
<a href="#topAnchor" style="position:fixed;right:0;bottom:0">回到顶部</a>
```

### 2.scrollTop属性

scrollTop属性表示被隐藏在内容区域上方的像素数。

元素未滚动时，scrollTop的值为0，如果元素被垂直滚动了，scrollTop的值大于0，且表示元素上方不可见内容的像素宽度

```js
//test为button的id
test.onclick = function(){
	document.body.scrollTop = document.documentElement.scrollTop = 0;
}
```

### 3.scrollTo()

scrollTo(x,y)方法滚动当前window中显示的文档。

```js
//test为button的id
test.onclick = function(){
	scrollTo(0,0);
}
```

### 4.scrollBy()

scrollBy(x,y)方法滚动当前window中显示的文档，x和y指定滚动的相对量。

```js
//test为button的id
test.onclick = function(){
	var top = document.body.scrollTop || document.documentElement.scrollTop
	scrollBy(0,-top);
}
```

### 5.scrollIntoView()

Element.scrollIntoView方法滚动当前元素，进入浏览器的可见区域。

```html
<div id="target"></div>
<button id="test" style="position:fixed;right:0;bottom:0">回到顶部</button>
```
```js
test.onclick = function(){
	target.scrollIntoView();
}
```

### CSS样式设计 - 伪类的应用

```html
<!DOCTYPE HTML>
<HTML>
<HEAD>
<STYLE TYPE="text/CSS">
.box{
position:fixed;
right:10px;
bottom :10px;
height:30px;
width :50px; 
text-align:center;
padding-top:20px; 
background-color :lightblue;
border-radius :20%;
overflow :hidden;
}
.box:hover:before{
top:50%
}
.box:hover .box-in{
visibility hidden;
}
.box:before{
position :absolute;
top :-50%;
left: 50%;
transform :translate(-50%,-50%);
content:'回到顶部';
width :40px;
color:peru;
font-weight:bold;
} 
</STYLE>
<TITLE>TEST</TITLE>
</HEAD>
<body style=height2000px;>
<div id="box" class="box">

<div class="box-in"></div>
</div>
</body>
</HTML>
```
