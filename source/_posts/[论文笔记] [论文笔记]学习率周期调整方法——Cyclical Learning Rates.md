---
title: '[论文笔记] 学习率周期调整方法——Cyclical Learning Rates'
date: 2018-11-27 22:12:50
categories: 
  - Paper Notes
  - Learning Rate
tags:
  - Deep Learning
  - Learning Rate
  - Papers Notes
 
---

## 论文概述 ## 
本文是论文《Cyclical Learning Rates for Training Neural Networks》的学习笔记。论文提出了学习率（learning rate）周期调整的方法：“Cyclical Learning Rates”，简称“CLS”，该方法在kaggle竞赛中被广泛应用。论文链接：https://arxiv.org/abs/1506.01186 。

<!-- more --> 
  

## Introduction ##
训练一个深度神经网络是一个很难的求解全局最优的问题。求解全局最优时，我们通常使用随机梯度下降法（stochastic gradient descent）来更新权重$\theta$，公式如下：
$$\theta ^ { t } = \theta ^ { t - 1 } - \epsilon _ { t } \frac { \partial L } { \partial \theta }$$
其中，$L$是损失函数（loss function），$\epsilon _ { t }$是学习率（learning rate）。太小的学习率会使收敛速度变得很慢，太大的学习率会导致模型无法收敛（diverge），因此选择一个合适的学习率显得尤为重要。  
传统观点认为，学习率应该是一个在训练过程中单调递减的值。本文论证了在训练过程中改变学习速率总体上是有益的，因此本文建议让全局学习速率在一定范围内循环变化，而不是将其设置为固定值。

## Cyclical Learning Rates ##
算法有三个参数，分别是：max_lr、base_lr、step_size，即上下边界和步长。下图即为学习率的变化情况：
![avatar](/images/2018-11-29-1.png)

那么这三个参数是如何选取的呢？
假设有5w个训练样本，batchsize=100，则每个epoch有500次迭代，实验结果表明step_size设置为2~8倍的迭代次数比较合适。  
使用 triangular 策略还给我们带来的一个好处是我们可以知道什么时候停止训练：我们可以采用周期性的lr进行训练3回，然后再继续训练4次甚至更多，能够达到很好的效果。  
那么怎么去选择 base_lr,max_lr两个参数呢？先将max_lr设置为step_size同样的值，base_lr为原架构的初始值，然后以此迭代5到10个epoch，画学习率与准确率之间的关系图，找最开始收敛的点和收敛后第一个下降的点，记录下来作为base_lr和max_lr的值。  

论文中介绍了三种CLR的方法：triangular、triangular2和exp range

 1. **triangular**  
首先计算当前迭代次数属于哪个 cycle，然后计算上图中每个点其具体的lr值是多少，建立坐标后，开始计算点(x,y)，我们知道了当前cycle，每个cycle的iter是 2*cycle*step_size，然后再用当前 iterations 减去这个值，y要区分是上升还是下降阶段。
![avatar](/images/2018-11-29-2.png)

```
    cycle = np.floor(1+iterations/(2*step_size)) 
    x = np.abs(iterations/step_size - 2*cycle + 1)
    lr = base_lr + (max_lr-base_lr)*np.maximum(0, (1-x))
 ```   

 
 2. **triangular2**  
 每个新的cycle，新的max_lr都减半
![avatar](/images/2018-11-29-3.png)
 3. **exp range**  
 每个新的cycle，新的max_lr指数下降
![avatar](/images/2018-11-29-4.png)
    

