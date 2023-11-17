---
title: matlab记录
date: 2023-08-26 09:06:51
tags: matlab
description: The key record of matlab. 
mathjax: true
---
{% asset_img matlab点乘点除.png matlab %}

x:y:z 一般表示 x 初值 y 步长 z 终值

if - end 和 if - else - end

x(i) 访问 x 数组中下标为 i 的元素

meshgrid 函数是MATLAB中用于生成网格采样点数的函数，通常进行2D、3D图形的绘制。
{%asset_img meshgrid生成网格.png%}
```
x = -10:0.5:10;
y = -10:0.5:10;
[xx, yy] = meshgrid(x, y);
z = xx .^2 - yy .^2;
mesh(xx, yy, z);
```

https://blog.csdn.net/qq_54186956/article/details/127274462 sym syms 函数应用

{%asset_img subs函数.png%}

在命令行输入 `format rat` 后，输出为分数格式，不再约成小数。

在命令行输入 `doc xxx` 可以直接查看官方解释 `xxx` 函数的文档。

`num2str(xxx)` 其中 xxx 是一个数，转换一个行向量，每个字符代表向量的一个元素

`result = [s1, s2]` 进行字符串拼接

{%asset_img 矩阵操作.jpg%}

提取矩阵的行数：$length(A(:,1))$
提取矩阵的列数：$length(A(1,:))$

matlab 中读取图片和显示图片函数 `imread` 和 `imshow` https://blog.csdn.net/dp327264/article/details/105087849

`subplot` 函数是将多个图片画到一个画面上的工具 `subplot(m,n,p)` 表示 m 行 n 列从左到右 从上到下第 p 个

灰度图像二值化：图像二值化（ Image Binarization）就是将图像上的像素点的灰度值设置为0或255，也就是将整个图像呈现出明显的黑白效果的过程。
在数字图像处理中，二值图像占有非常重要的地位，图像的二值化使图像中数据量大为减少，从而能凸显出目标的轮廓。

matlab 中关于数字图像处理的工具箱是 IPT(Image Processing Toolbox) 

{%asset_img 灰度图.png%}
对于汉字处理的话，灰度图会引入误差，所我们转化为二值图。

`find(xx)` 函数可以返回满足 xx 条件的下标组成的行向量。
例如 `x=[1 2 3 4 5 6 7]; find(x >= 5)` 返回的就是：`5     6     7`

`max(A)` A 可以是矩阵或者向量，就是返回其中最大的元素

元组是matlab的数据类型之一，其元胞中可存储文本，数值，矩阵等等不同的数据类型，因此应用较为方便。因此，在采用matlab进行数据处理时，对元组的创建、读取、写入、转化函数的掌握尤为重要。
`cell(dim)` 是创建 dim$\times$dim维的空元组，下标必须是正整数，不能是 0.