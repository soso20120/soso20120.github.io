---
layout: post 
title: "Select相关操作 - JS"
date: 2017-08-08 08:08:08 +0800
categories: [Web]
excerpt: 利用纯JS对select及option的操作
tags:
  - Web
  - 前端
  - JS
---

### Content

* content
{:toc}

### 1.创建Select

```js
var a = document.createElement("select");
a.id = "mySelect";
document.body.appendChild(a);
```
	
### 2.创建Option

```js
var b = document.getElementById("mySelect");
b.options.add(new Option("选项文本", "value"));
```

### 3.获得Option

```js
var index = b.selectedIndex;
//获得value
var value = b.options[index].value;
//获得选项文本
var text = b.options[index].text;
```

### 4.修改Option

```js
b.options[index] = new Option("xxx", "xxx");
```

### 5.删除Select和Option

```js
//删除所有option
b.options.length = 0;
//删除select
b.parentNode.removeChild(b);
```
