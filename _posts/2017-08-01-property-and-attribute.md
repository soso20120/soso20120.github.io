---
layout: post 
title: "Property and Attribute"
date: 2017-08-01
categories: [Web]
excerpt: DOM和JS中Property(属性)和Attribute(特性)的区别
tags:
  - Web
  - JS
  - HTML
  - 前端
---

### Content

* content
{:toc}

### 1.Property

***property是DOM中的属性，是JavaScript里的对象***

DOM有其默认的基本属性property，无论如何，它们都会在初始化的时候再DOM对象上创建。

###### Boolean(true/false)

```JS
var a = Number(true);	//1
var b = Number(false);	//0
```

###### 数字

只是简单的传入和返回。

###### 特殊空值

```JS
var n = Number(null);		//0
var u = Number(undefined);	//NaN
var k = Number("");			//0
```

###### String

* 只有数字(整数和小数)，忽略前导0
* 空字符串见上面
* 只有十六进制格式，转换为对应的十进制
* 有其他格式，转换为NaN

### 2.Attribute

***attribute是HTML标签上的特性，它的值只能够是字符串***

HTML标签中定义的属性和值会保存该DOM对象的attributes属性里面。

### 3.赋值例子

```js
//在预先给input元素a赋值value="1"
a.value = 'new value of prop';
console.log(a.value);             // 'new value of prop'
console.log(a.attributes.value);  // 'value="1"'

a.attributes.value.value = 'new value of attr';
console.log(a.value);             // 'new value of attr'
console.log(a.attributes.value);  // 'new value of attr'
```

* 表明在给value赋值时，attribute并不会变，但是property变了。
* 而给attribute赋值时，则都发生了改变

### 4.总结

###### 创建

* DOM对象初始化时会在创建默认的基本property；
* 只有在HTML标签中定义的attribute才会被保存在property的attributes属性中；
* attribute会初始化property中的同名属性，但自定义的attribute不会出现在property中；
* attribute的值都是字符串。

###### 数据绑定
* attributes的数据会同步到property上，然而property的更改不会改变attribute；
* 对于`value`，`class`这样的属性/特性，数据绑定的方向是单向的，attribute->property；
* 对于`id`，数据绑定是`双向`的，attribute<=>property；
* 对于`disabled`，property上的disabled为false时，attribute上的disabled必定会并存在，此时数据绑定可以认为是`双向`的。

###### 使用
* 可以使用DOM的setAttribute方法来同时更改attribute；
* 直接访问attributes上的值会得到一个Attr对象，而通过getAttribute方法访问则会直接得到attribute的值；
* 大多数情况(除非有浏览器兼容性问题)，jQuery.attr是通过setAttribute实现，而jQuery.prop则会直接访问DOM对象的property。
