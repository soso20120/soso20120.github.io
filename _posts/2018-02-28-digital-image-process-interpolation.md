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

```
void NearestInsert(const Mat &src, Mat &dis, int factor) {

    unsigned char* src_data = (unsigned char*)src.data;
    unsigned char* dis_data = (unsigned char*)dis.data;

    double fac = (double)1 / (double)factor;
    int channel = src.channels();
    
    for (int x = 0; x < dis.rows; x++) {
        for (int y = 0; y < dis.cols; y++) {
            for (int k = 0; k < channel; k++) {
                dis_data[x * dis.step + y * channel + k] = src_data[(int)(fac * x) * src.step + (int)(fac * y)  * channel + k];
            }
        }
    }
}
```

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


```
void BilinearInsert(const Mat &src, Mat &dis, int factor) {

    unsigned char* src_data = (unsigned char*)src.data;
    unsigned char* dis_data = (unsigned char*)dis.data;

    double fac = (double)1 / (double)factor;
    int channel = src.channels();

    for (int x = 0; x < dis.rows; x++)
    {
        for (int y = 0; y < dis.cols; y++)
        {
            //对于目标图像(x, y),实际映射到原图的坐标为(fx * x, fy * y),但是若为小数，原图并不存在该点，因此近似为(i, j)  
            int i = (int)(fac * x);
            int j = (int)(fac * y);
            int out = (int)(x * dis.step + y * channel);
            //找到四个领域的下标  
            int ori1 =(int)(i * src.step + j * channel);
            int ori2 = (int)(i * src.step + (j + 1)  * channel);
            int ori3 = (int)((i + 1) * src.step + j * channel);
            int ori4 = (int)((i + 1) * src.step + (j + 1)  * channel);
            //f(i+u,j+v) = (1-u)(1-v)f(i,j) + (1-u)vf(i,j+1) + u(1-v)f(i+1,j) + uvf(i+1,j+1)    
            for (int k = 0; k <channel; k++)
            {
                float u = (float)(x * fac - i);
                float v = (float)(y * fac - j);
                dis_data[out + k] = src_data[ori1 + k] * (1 - u) * (1 - v) + src_data[ori2 + k] * (1 - u) * v 
                                    + src_data[ori3 + k] * u * (1 - v) + src_data[ori4 + k] * u * v;
            }
        }
    }
}
```

<br>
### 2 双三次插值法

&emsp;该方法利用三次多项式S(x)求逼近理论上最佳插值函数sin(x)/x, 其数学表达式为：

&emsp;三次曲线插值方法计算量较大，但插值后的图像效果最好。

![双三次插值公式](/assets/images/bicubic-formula.JPG)

![双三次插值公式](/assets/images/bicubic.JPG)

![双三次插值公式](/assets/images/bicubic-calculate.JPG)

```
float s_value(float x, float a) {
    x = fabs(x);
    if (x < 0) {
        return -1;
    }
    else if (x < 1) {
        return 1 - (a + 3) * x * x + (a + 2)*x * x * x;
    }
    else if (x < 2) {
        return -4 * a + 8 * a * x - 5 * a * x * x + a * x * x * x;
    }
    else {
        return 0;
    }
}

void BicubicInsert(const Mat &src, Mat &dis, int factor) {
    unsigned char* src_data = (unsigned char*)src.data;
    unsigned char* dis_data = (unsigned char*)dis.data;

    float fac = (float)1 / (float)factor;
    int channel = src.channels();
    float a = -0.05;

    for (int x = 0; x < dis.rows; x++) {
        for (int y = 0; y < dis.cols; y++) {
            //对于目标图像(x, y),实际映射到原图的坐标为(fac * x, fac * y),但是若为小数，原图并不存在该点，因此近似为(i, j)  
            int i = floor(fac * x);
            int j = floor(fac * y);
            //计算u、v
            float v = fac * x - i;
            float u = fac * y - j;
            //初始化A矩阵[s(1+v),s(v),s(1-v),s(2-v)]和C矩阵
            float A[4] = { s_value(1 + v,a),s_value(v,a),s_value(1 - v,a),s_value(2 - v,a) };
            float C[4] = { s_value(1 + u,a),s_value(u,a),s_value(1 - u,a),s_value(2 - u,a) };
            //由于需要16个点参与计算，所以对边界进行处理
            int i0 = max(0, i-1);
            int i2 = min(src.rows - 1, i + 1);
            int i3 = min(src.rows - 1, i + 2);
            int j0 = max(0, j-1);
            int j2 = min(src.cols - 1, j + 1);
            int j3 = min(src.cols - 1, j + 2);
            //对每一个通道进行计算
            for (int k = 0; k < channel; k++) {
                //初始化B矩阵
                float B[4][4] = { { src_data[i0*src.step + j0 * channel + k],src_data[i0*src.step + j * channel + k],src_data[i0*src.step + j2 * channel + k],src_data[i0*src.step + j3 * channel + k]},
                { src_data[i*src.step + j0 * channel + k],src_data[i*src.step + j * channel + k],src_data[i*src.step + j2 * channel + k],src_data[i*src.step + j3 * channel + k]},
                { src_data[i2*src.step + j0 * channel + k],src_data[i2*src.step + j * channel + k],src_data[i2*src.step + j2 * channel + k],src_data[i2*src.step + j3 * channel + k]},
                { src_data[i3*src.step + j0 * channel + k],src_data[i3*src.step + j * channel + k],src_data[i3*src.step + j2 * channel + k],src_data[i3*src.step + j3 * channel + k]}};
                //计算A*B*C
                float result = 0;
                for (int iA = 0; iA < 4; iA++) {
                    float sum = 0;
                    for (int iB = 0; iB < 4; iB++) {
                        sum += A[iB] * B[iB][iA];
                    }
                    result += sum * C[iA];
                }
                dis_data[x*dis.step + y * channel + k] = result;
            }
        }
    }
}
```
