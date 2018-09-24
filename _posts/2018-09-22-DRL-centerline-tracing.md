---
layout: post
title: Deep Reinforcement Learning for Vessel Centerline Tracing in Multi-modality 3D Volumes
categories: [Paper]
description: DRL
keywords: Reinforcement Learning
---

From MICCAI 2018

---


## 1 题目
Deep Reinforcement Learning for Vessel Centerline Tracing in Multi-modality 3D Volumes

## 2 背景
前人做法：使用最短路径 / 构建损失评价指标

## 3 主要工作
使用`增强学习`构建了一个 end-to-end 的模型，来追踪3D多模态医学数据中的`血管中心线`。

## 4 方法
给 3D 图像 $I$ 以及血管中心线坐标 list $G = [g_{0}, g_{1}, ..., g_{n}]$, 期望 agent 学习到一个最优的轨迹 $P = [p_{0}, p_{1}, ..., p_{m}]$。将该问题视为序列决策问题，并建模为一个基于回报的马尔可夫决策过程 (MDP)。


## 算法流程


## 创新点


## 启示



## 词汇
`vascular` 血管的

`navigation` 导航，航行，航海

`trajectory` 轨道，轨线

`optimal` 最优的，最佳的

## 参考资料
- 