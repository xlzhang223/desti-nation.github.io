---
layout: post
title: Automated Object Tracing for Biomedical Image Segementation Using a Deep Convolution Neural Network
categories: [Paper]
description: Automated Object Tracing for Biomedical Image Segementation Using a Deep Convolution Neural Network
keywords: Tracing
---

From MICCAI 2018

---

## 题目
 Automated Object Tracing for Biomedical Image Segementation Using a Deep Convolution Neural Network

## 主要内容
利用 CNN，通过追踪边界来达到分割的效果。

- 原始图像结合了其他语义分割的网络的结果（U-net），作为图片的一个辅助通道。

- 初始方向：来自于一段很短的人的手工标注 or U-net 分割的边界的一段

- 输入：一个与之前 trace 好的点有重叠的 patch

- 输出：要追踪的下 m 个点

通过反复迭代，直到追踪的点和初始点相交，追踪结束。

- 结果：在该 challenge 中比常见的语义分割网络要好， 达到了 state-of-the-art


## 启示
追踪的时候可以`手工` or `利用其他网络的结果 ` 来给与初始追踪方向，前者人机结合的方法也可以称为`human-in-the-loop`。

## 缺点
对于何时追踪终止这个问题没有给出解答，留待后需完善。

# 词汇
`methodology` 方法学，方法论