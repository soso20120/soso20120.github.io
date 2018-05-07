---
layout: post 
title: "openCV之Mat"
date: 2018-02-23 12:22:11
categories: [Tech]
excerpt: Mat是opencv中的核心。
tags:
  - openCV
---

### Content

* content
{:toc}


> **[官方文档](https://docs.opencv.org/3.4.1/index.html)**

### 1 Mat

* Mat不仅仅是一个图像容器类,同时也是一个通用的矩阵类.
* 不必再手动为其开辟空间,也不必在不需要的时候立即将他的空间释放
* Mat是一个类,由两个数据部分组成:
    * 矩阵头:矩阵尺寸,存储方法,存储地址等等所有相关信息(矩阵头的尺寸是常数值)
    * 指向存储所有像素值数据块的指针.
* 赋值运算符和复制构造函数只会复制信息头和指向数据块指针的值.但是不会完整的复制一个矩阵(为了性能和避免内存溢出考虑).所以有多个对象引用同一个值矩阵,改变其中一个对象有改变其他的对象的可能.
* 使用`clone()`或者`copyTo()`来深层复制一幅图像的矩阵.       
* 前面已经知道一个矩阵可以被多个Mat对象引用，那么最后一个使用这个矩阵的对象，负责清理矩阵。

<br>
### 2 向量模板类

```
Mat (int rows, int cols, int type, const Scalar &s)
    Rows:行数
    Cols:列数
    Type:类型 CV_[位数][带符号与否][类型前缀][通道数]
        例:CV_8UC3表示使用8位的unsighed char类型.每个像素由三个元素组成的三通道.
    类型汇总:
    CV_8U(uchar)  
    CV_8UC1 (uchar)  CV_8UC2 (Vec2b)  CV_8UC3 (Vec3b)  CV_8UC4(Vec4b) 

    CV_8S(char)   
    CV_8SC1 (1通道)  CV_8SC2 (2通道)   CV_8SC3 (3通道)  CV_8SC4 (4通道)   

    CV_16U  (ushort)
    CV_16UC1 (ushort)  CV_16UC2 (Vec2w)   CV_16UC3 (Vec3w)   CV_16UC4 (Vec4w)   

    CV_16S  (short)
    CV_16SC1(short)   CV_16SC2(Vec2s)   CV_16SC3(Vec3s)   CV_16SC4(Vec4s)   

    CV_32S (int)
    CV_32SC1(int)   CV_32SC2(Vec2i)    CV_32SC3(Vec3i)  CV_32SC4(Vec4i)   

    CV_32F (float)
    CV_32FC1(float)   CV_32FC2(Vec2f)  CV_32FC3(Vec3f)   CV_32FC4(Vec4f)  

    CV_64F(double)  
    CV_64FC1(double)   CV_64FC2(Vec2d)  CV_64FC3(Vec3d)  CV_64FC4(Vec4d) 

Mat (int ndims, const int *sizes, int type, const Scalar &s)
    Ndims:维数.
    *size:一个数组,表示相应维数下面的具体数量
    Type:和上面一样
    Scalar:和上面一样.
 ```
