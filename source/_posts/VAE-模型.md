---
title: VAE 模型
date: 2024-04-24 23:45:30
tags:
---

### 概述

变分自编码器（Variational Auto-Encoders，VAE）作为深度生成模型的一种形式，是由 Kingma 等人于 2014 年提出的基于变分贝叶斯（Variational Bayes，VB）推断的生成式网络结构。与传统的自编码器通过数值的方式描述潜在空间不同，它以概率的方式描述对潜在空间的观察。

### 原理

传统的自编码器模型主要由两部分构成：编码器（encoder）和解码器（decoder）。

### 链接

1. https://zhuanlan.zhihu.com/p/64485020
2. https://www.bilibili.com/video/BV1A7411N7mD/?p=6&share_source=copy_web&vd_source=ca842ea19ddf18fb9427fb4d903d435a 对于变分法的讲解
3. https://www.zhangzhenhu.com/aigc/变分自编码器.html
4. https://zhuanlan.zhihu.com/p/650543717 VAE 的推导，好文章
5. https://blog.csdn.net/qq_41196612/article/details/109528221 VAE 推导
6. https://github.com/AntixK/PyTorch-VAE 不同 VAE 的实现