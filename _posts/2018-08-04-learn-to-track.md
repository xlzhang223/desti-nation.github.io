---
layout: post
title: Learn to Track - Deep Learning for Tractography
categories: [Paper]
description: Learn to Track
keywords: Track, DL
---

From MICCAI 2017

深度学习，尤其是 RNN , 在这样的纤维/血管等流线型数据的追踪方面大有可为。

---

## 题目
Learn to Track: Deep Learning for Tractography

## 主要内容
利用深度学习进行纤维束追踪。具体来说，建立了 FFNN 和 RNN 两个模型，其中 RNN 因为能够利用之前追踪的信息来预测未来的走向，因此 RNN 的模型 在Diffusion Signal上的追踪结果表现得更好。

![mark](http://pcxhsqn8a.bkt.clouddn.com/blog/180804/9dE87G90Jh.png?imageslim)

## 启示
深度学习，尤其是 RNN , 在这样的纤维/血管等流线型数据的追踪方面大有可为。

## 缺点
对于何时追踪终止这个问题没有给出解答，留待后需完善。

## 词语
核磁共振成像(MRI)
弥散加权成像（diffusion weighted imaging，DWI）


