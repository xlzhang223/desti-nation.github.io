---
layout: post
title: Machine Learning Yearning 笔记
categories: [Machine Learning]
description: Machine Learning Yearning 笔记
keywords: Machine Learning
---

吴恩达 ML Yearning 学习笔记

---

## 1 验证集和测试集

> 验证集和测试集的定义

- 将数据分为`训练集`、`验证集`和`测试集`，验证集和测试集用于检测算法性能。验证集和测试集最好能表示未来的没有见过的样本的情况，这样才能提高模型在实际情况中的泛化性能。

> 验证集和测试集应该服从同一分布

- 验证集和测试集应该服从同一分布。
- 如果一个系统在验证集上运行性能良好，却在测试集上效果不佳的现象，可能的原因有：
    
    1. 训练集和验证集服从同一分布：

        算法在验证集上过拟合了。

    2. 训练集和验证集不服从同一分布：
        
        2.1 算法在验证集上过拟合了。
        
        2.2 测试集比验证集更难预测

        2.3 测试集和验证集分布不同

