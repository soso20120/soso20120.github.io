---
layout: post 
title: "字符串转换数字 - JS"
date: 2017-07-24 08:24:25 +0800
categories: [Web]
excerpt: 对JS中Number()、parseInt()和parseFloat()的总结
tags:
  - Web
  - JS
  - 前端
---

### Content

* content
{:toc}

### 1.Number()

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

### 2.parseInt()

* 将字符串转换为数字，第二个参数可以指定二进制等
* 如果第一个字符不是数字或者负号，返回NaN
* 转换空字符串也会返回NaN

### 3.parseFloat()

* 从第一个字符开始解析，直到字符串末尾，或者到一个无效的浮点数字字符为止。
* 只能解析十进制，没有第二个参数

