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
[Deep Reinforcement Learning for Vessel Centerline Tracing in Multi-modality 3D Volumes](https://link.springer.com/chapter/10.1007/978-3-030-00937-3_86)

## 2 背景
前人做法：使用最短路径 / 构建损失评价指标

## 3 主要工作
使用`增强学习`构建了一个 end-to-end 的模型，来追踪3D多模态医学数据中的`血管中心线`。

## 4 方法
给 3D 图像 $I$ 以及血管中心线坐标 list $G = [g_{0}, g_{1}, ..., g_{n}]$, 期望 agent 学习到一个最优的轨迹 $P = [p_{0}, p_{1}, ..., p_{m}]$。将该问题视为序列决策问题，并建模为一个基于回报的马尔可夫决策过程 (MDP)。在时间步 $t$，agent 从状态空间 $S$ 接受状态 $s$，并依据策略 $\pi$，从动作空间 $A$ 中选择动作 $a$。

对于血管中心线追踪问题，我们允许 agent 在相邻的 voxels 中移动，所以其动作空间 $A$ = {上，下，左，右，前，后} 6个动作。

标量 reward 记为 $r_{t} = r_{s, a}^{s'}$，表示从状态 $s$ 采取动作 $a$ 到达 $s'$ 的回报。

从当前点 $p_{t}$ 到血管上最近的点记为 $g_{d}$。

接下来定义 point-to-curve 距离度量：

$$D(p_{t}, G) = \left \| \lambda (p_{t} - g_{d+k}) + (1-\lambda)(g_{d+k+1} - g_{d+k-1}) \right \| \tag{1}$$

前半部分让当前点尽可能靠近血管，后半部分是 momentum 使得点沿着曲线的方向走。其中 $k$ 是在均匀采样的曲线上的前进偏移量（默认 $k$ = 1）。

回报函数定义为：

![mark](http://pcxhsqn8a.bkt.clouddn.com/blog/180925/G8EFfLkGFf.png?imageslim)

$l$ 是凭借经验选择的阈值。接下来的操作和 Deep Q Learning 相同，用 $Q^{\pi}(s, a;\theta)$ 来逼近 $Q^{*}(s, a)$。


## 5 训练 Tricks
- 为了避免序列中的相关性造成的训练不稳定，几个 iterations 才会更新一次(训练中 10000 iterations 更新一次)。
- experience replay （大小 10, 0000）。
- $\epsilon$-greedy 策略：以 $\epsilon$ 概率选择 action，1 - $\epsilon$ 概率随机选择 action。
- 为了在开始阶段鼓励模型去探索，$\epsilon$ 开始为1，之后慢慢下降到0。
- 给 GroundTruth $G = [g_{0}, g_{1}, ..., g_{n}]$，初始点 $p_{0}^{'}$ 以 $\eta$ 概率选择 $g_{0}$，以 1 - $\eta$ 概率选择 $G$ 上的其他点。
- 终止：遇到 GroundTruth 的最后一个点或者达到了最大的 episode 长度。
- batch_size = 8 lr = 0.0005
- 前进偏移量 offset $k$ = 1
  
## 6 追踪 Tricks
- 为了进一步稳定追踪过程，对网络输出的 action-value 施加 momentum：$r_{t} = \alpha r_{t - 1} + (1- \alpha) r_{t}$
- 追踪停止：追踪移动出边界或者形成了一个环（追踪的点之前访问过）


## 7 模型
- Conv: 32 filters, size 4\*4\*4, stride 2 -> BN -> ReLU
- Conv: 46 filters, size 3\*3\*3, stride 2
- FC: 256
- FC: 128
- FC: 6

## 8 词汇
`vascular` 血管的

`navigation` 导航，航行，航海

`trajectory` 轨道，轨线

`optimal` 最优的，最佳的

## 9 参考资料
- [Understanding RL: The Bellman Equations](https://joshgreaves.com/reinforcement-learning/understanding-rl-the-bellman-equations/)
- [[笔记]Playing Atari with Deep Reinforcement Learning](https://junmo1215.github.io/paper/2017/11/03/Note-Playing-Atari-with-Deep-Reinforcement-Learning.html)
- [Markdown下LaTeX公式、编号、对齐](https://www.zybuluo.com/fyywy520/note/82980)