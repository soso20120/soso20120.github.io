---
layout: post 
title: "图像处理之插值方法"
date: 2018-02-28 18:32:11
categories: [Tech]
excerpt: 主要介绍了Nearest-neighbor、Bilinear和Bicubic interpolation。
tags:
  - openCV
---

### Content

* content
{:toc}


### 1 最近邻点插值法

&emsp;这是最简单的一种插值方法，不需要计算，在待求象素的四邻象素中，将距离待求象素最近的邻象素灰度赋给待求象素。设i+u, j+v(i,j为正整数，u,v为大于零小于1的小数，下同)为待求象素坐标，则待求象素灰度的值 f(i+u, j+v)。

&emsp;最近邻点插值法计算量较小，但可能会造成插值生成的图像灰度上的不连续，在灰度变化的地方可能出现明显的锯齿状。

![最近邻点插值法](/assets/images/Nearest-neighbor.JPG)

<br>
### 2 双线性插值法

&emsp;双线性内插法是利用待求象素四个邻象素的灰度在两个方向上作线性内插。

&emsp;双线性内插法的计算比最邻近点法复杂，计算量较大，但没有灰度不连续的缺点，结果基本令人满意。它具有低通滤波性质，使高频分量受损，图像轮廓可能会有一点模糊。

```
对于(i, j+v): f(i, j) 到 f(i, j+1) 的灰度变化为线性关系则有：
        f(i, j+v) = [f(i, j+1) - f(i, j)] * v + f(i, j)
同理对于(i+1, j+v)则有：
        f(i+1, j+v) = [f(i+1, j+1) - f(i+1, j)] * v + f(i+1, j)
从f(i, j+v) 到 f(i+1, j+v) 的灰度变化也为线性关系，由此可推导出待求象素灰度的计算式如下：
f(i+u, j+v) = (1-u) * (1-v) * f(i, j) + (1-u) * v * f(i, j+1) 
            + u * (1-v) * f(i+1, j) + u * v * f(i+1, j+1)
```

![双线性插值法](/assets/images/bilinear.JPG)

<br>
### 2 双三次插值法

&emsp;该方法利用三次多项式S(x)求逼近理论上最佳插值函数sin(x)/x, 其数学表达式为：

&emsp;三次曲线插值方法计算量较大，但插值后的图像效果最好。

![双三次插值公式](/assets/images/bicubic-formula.JPG)

![双三次插值公式](/assets/images/bicubic.JPG)

![双三次插值公式](/assets/images/bicubic-calculate.JPG)