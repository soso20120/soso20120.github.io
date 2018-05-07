---
layout: post 
title: "数字转换及取整 - JAVA"
date: 2017-07-29 09:55:25 +0800
categories: [Web]
excerpt: JAVA中，字符串与数字相互转换通过valueOf()方法，取整有ceil()，floor()，round()
tags:
  - Web
  - JAVA
  - 后台
---

### Content

* content
{:toc}

### 1.Sring转换为int

###### valueOf()

Integer类的静态方法，非合法的参数强转会抛出异常。

>返回的是Integer对象，可以使用对象方法

```JAVA
int a = Integer.valueOf("12");
```

###### parseInt()

Integer类的静态方法。

>返回的是int类型

```JAVA
int c = Integer.parseInt("12");
```

### 2.int转换为String

```JAVA
String b = String.valueOf(12);
```

### 3.取整Math.round()

* 参数的`小数点后第一位<5`，运算结果为参数`整数部分`。
* 参数的`小数点后第一位>5`，运算结果为参数`整数部分绝对值+1，符号（即正负）不变`。
* 参数的`小数点后第一位=5`，正数运算结果为`整数部分+1，负数运算结果为整数部分`。

>大于五全部加，等于五正数加，小于五全不加

### 4.向上取整ceil()

```JAVA
int d = Math.ceil(11.3);	//12
int g = Math.ceil(-11.3);	//-11
```

### 5.向下取整floor()

```JAVA
int e = Math.floor(11.3);	//11	
int f = Math.floor(-11.3);	//-12
```