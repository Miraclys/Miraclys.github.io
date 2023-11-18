---
title: python 数学建模与实验
date: 2023-08-28 13:31:38
tags: Python
description: The key record of python and mathematical modeling.
mathjax: true
---
虽然列表 list 可以完成数组操作，但不是真正意义上的数组，当数据量很大时，其速度很慢，故提供了 NumPy 扩展库完成数组操作。很多高级扩展库也依赖于它，比如 Scipy, Pandas 和 Matplotlib 等。

数组创建的几种方式：
{%asset_img 数组创建.png%}

NumPy 中的数组 array 和 list 的区别是：列表中可以是数据类型不同的元素，而 array 数组只允许存储相同数据类型。

二维数组中的索引 list 为 a[i][j] 而 array 为 a[i, j]

一般索引：
感觉有的地方还是和 matlab 很相似的。
{%asset_img 一般索引.png%}

文本文件读取：
{%asset_img 文本读取.png%}
二进制文件读取：
{%asset_img 二进制文件读取.png%}
另外，如果我们使用 NumPy 专用的二进制存取函数 `load() save() savez()` 会自动处理元素的类型和形状等信息。

open 打开文件的时候，如果打开的文件不在当前的目录，需要指定完整路径。注意，此时文件路径中的 `\` 要改为 `\\`，例如 `e:\mypython\test.txt` 应该改为 `e:\\mypython\\test.txt`.
{%asset_img 文件操作方式.png%}

join 函数：
{%asset_img join函数.png%}

#### 数据处理工具 Pandas
Pandas(Panel data, 面板数据) 是在 NumPy 的基础上开发的，是 Python 最强大的数据分析和探索工具之一。

#### Matplotlib 
Matplotib 是 Python 强大的数据可视化工具，类似于 MATLAB 语言。

pie 绘制饼状图 bar 绘制柱状图 hist 绘制二维直方图 scatter 绘制散点图

{%asset_img 常见样式颜色.png%}

#### scipy 
scipy 包含各种专用于科学计算常见问题的工具箱。其中 scipy.stats 则是统计和随机数的专门的库。
NumPy 能生成一定概率分布的随机数，但是如果需要更具体的概率密度、分布函数等，就用到 scipy.stats 模块了。Python 做简单的统计分析也可以用 scipy.stats 模块。

### 