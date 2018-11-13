---
title: '[论文笔记] 抽取式自动文本摘要模型——SummaRuNNer'
date: 2018-11-13 11:31:13
categories: 
  - Paper Notes
  - Summarization
tags:
  - NLP
  - Summarization
  - Papers Notes
 
---

## 论文概述 ##
这篇文章提出了一个基于RNN的模型，来完成抽取式自动文本摘要任务。模型公式具有可解释性，并且可以利用已有的abstractive summary数据训练我们的extractive model。

<!-- more --> 
  

## SummaRuNNer模型 ##
作者把抽取式摘要（extractive summarization）问题转化为一个序列分类（sequence classification）问题：对文章的每句话都做一个二分类，被选中为摘要的一部分就标注为1，未被选中就标注为0。当然了，因为使用了RNN，每次做分类的时候，都会考虑之前句子的分类情况。 
### GRU ###
本模型使用的是RNN的变体——GRU。$u$被称作update gate，$r$被称作reset gate，$W$和$b$是模型需要训练的参数，$h$是真实值隐状态（ real-valued hidden-state）。GRU的计算公式如下：
\begin{aligned} \mathbf { u } _ { j } & = \sigma \left( \mathbf { W } _ { u x } \mathbf { x } _ { j } + \mathbf { W } _ { u h } \mathbf { h } _ { j - 1 } + \mathbf { b } _ { u } \right) \\ \mathbf { r } _ { j } & = \sigma \left( \mathbf { W } _ { r x } \mathbf { x } _ { j } + \mathbf { W } _ { r h } \mathbf { h } _ { j - 1 } + \mathbf { b } _ { r } \right) \\ \mathbf { h } _ { j } ^ { \prime } & = \tanh \left( \mathbf { W } _ { h x } \mathbf { x } _ { j } + \mathbf { W } _ { h h } \left( \mathbf { r } _ { j } \odot \mathbf { h } _ { j - 1 } \right) + \mathbf { b } _ { h } \right) \\ \mathbf { h } _ { j } & = \left( 1 - \mathbf { u } _ { j } \right) \odot \mathbf { h } _ { j } ^ { \prime } + \mathbf { u } _ { j } \odot \mathbf { h } _ { j - 1 } \end{aligned}

###文本表示###

























