---
layout: post
title: Automated Object Tracing for Biomedical Image Segementation Using a Deep Convolution Neural Network
categories: [Paper]
description: Automated Object Tracing for Biomedical Image Segementation Using a Deep Convolution Neural Network
keywords: Tracing
---

From MICCAI 2018

---

## 1 题目
 Automated Object Tracing for Biomedical Image Segementation Using a Deep Convolution Neural Network

## 2 背景
当前分割技术可能导致分割结果不连续

## 3 主要工作
利用 CNN，通过追踪（细胞）边界来达到（细胞）分割的效果。

## 4 模型

![mark](http://pcxhsqn8a.bkt.clouddn.com/blog/180921/C24hg3F7fk.png?imageslim)

## 算法流程
![mark](http://pcxhsqn8a.bkt.clouddn.com/blog/180921/g576f3i12H.png?imageslim)

## 创新点
将分割问题重新定义为了边界追踪问题。

## 启示
追踪的时候可以`手工` or `利用其他网络的结果 ` 来给与初始追踪方向，前者人机结合的方法也可以称为`human-in-the-loop`。

## 缺点
对于何时追踪终止这个问题没有给出解答，留待后需完善。

## 词汇
`methodology` 方法学，方法论

`pathology` 病理学

`contour` 轮廓

`adequate` 充足的，适当的

`orders of magnitude` 数量级

`leverage` 利用

`auxiliary` 辅助物，辅助的