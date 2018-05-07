---
layout: post 
title: "SimpleDateFormat - JAVA"
date: 2017-08-07 14:56:54 +0800
categories: [Web]
excerpt: SimpleDateFormat中format方法实现转换
tags:
  - Web
  - 后台
  - JAVA
  - SpringMVC
---

### Content

* content
{:toc}

### 后台合并参数 

* **问题：**新增记录，年、月、日传不到后台数据库
* **原因：**字段类型未与数据库对应
* **解决：**把前台3个参数year，month，day在后台合并一个参数date

```java
//改runoffController里的gljl/add里的"daGljlBasic.setDate(newDaGljlBasicVo.getDate());"
String day=request.getParameter("day");
String month=request.getParameter("month");
String year=request.getParameter("year");
String ymd=year+"-"+month+"-"+day;
SimpleDateFormat dateFormat=new SimpleDateFormat("yyyy-MM-dd");
//重点，date为Date类型
Date date=null;
try {
	//parse方法可以把string型的字符串转换为特定格式的date类型
	date=dateFormat.parse(ymd);
	//System.out.println(date.toLocaleString().split(" ")[0]);
} catch (Exception e) {
	e.printStackTrace();
}
daGljlBasic.setDate(date);
```
	
### 前台显示date

* **问题：**date在前台显示乱码
* **原因：**Date类型经过转换导致
* **解决：**将Date类型改为String类型

```java
//改DaGljlBasicVo里date的getter和setter。
private String date;

public String getDate() {
	return date;
}

public void setDate(Date date) {
	SimpleDateFormat sf = new SimpleDateFormat("yyyy年MM月dd日hh时mm分ss秒");
    String format = sf.format(date);
	this.date = format;
}
```
