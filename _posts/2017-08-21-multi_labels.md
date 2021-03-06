---
layout: post
title: Multi-labels Classification
date: 2017-08-21
categories: blog
tags: [ML]
description: 多标签分类问题
---

### 多标签与多分类
1. 多分类是指在一个模式中将输入分成多个类，可做one-hot编码，用softmax处理。
2. 多标签是指在一个模型中有多个模态，一个输入可能有多个属于的模态。这是一个同时做多分类的问题。可以用sigmoid处理，loss使用交叉熵求和。

### 多标签增加了模型的复杂度
* 在一直多个模态相互独立的情况下，如果使用多个并行模型，类似于在系统中引入了已知信息，模型的复杂度会减小。
* 相反，端到端训练多标签意味着最后的特征层生成了所有模态信息的抽象，会增加模型复杂度，增加收敛难度。

### 多标签的loss
- 如果使用交叉熵求和，则多标签问题默认多个模态的分类同等重要，求的是整体的最优。如果这种整体的最优不存在，那收敛难度就很大。
- 如有24个标签，一种情况是前23种模态判断正确，最后一种判断错误；一种是第一种模态判断错误，后23种判断正确。对于求解最优loss的模型来说，这两种情况是一样的，但对于我们来说，意义可能并不一样。

### 多标签在实践中难以均衡样本
- 对于二分类问题，正例反例的数量需要进行一些均衡，通常用样本的权重来实现。而在多标签任务中，由于存在多个分类任务，每个任务的正反例比例不同，这样的均衡就很难通过样本权重来实现。
- 或许有其他的均衡方案。

### 但是有些情况下，标签直接关联度较高，就不能通过简单的拆分成多模型来做了。