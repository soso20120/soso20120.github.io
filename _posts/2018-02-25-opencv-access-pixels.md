---
layout: post 
title: "openCV之访问像素"
date: 2018-02-25 12:22:11
categories: [Tech]
excerpt: 可以通过直接访问、指针等方法
tags:
  - openCV
---

### Content

* content
{:toc}

### 1 at方法

at可以直接访问到某个位置的像素

>at <类型> (行,列) [通道(if通道)]

```
Mat pic1 = imread("1.jpg");
pic1.at<cv::Vec3b>(i, j)[0] = 0;
```

[类型参考该文章](http://)

<br>
### 2 ptr指针

OpcnCV提供的方法

> ptr (int  i0 = 0)  访问某行<br>
> ptr ( int  i0,int  i1 )  访问某点

```
float *data = pic2.ptr<float>(row);   //返回该行的地址
float a  = data[0];  		//访问该行第一个像素点
float b = data[col][2];  	//多通道的情况
```
