---
title: decision_tree
description: <center> </center>
photos:
  - ''
date: 2018-11-26 10:33:41
tags:
categories:
password:
---

Q1
how to write the split the code of node.

Q2
continous value?

Q3
categorical feature vs binary feature

Q4
 decision boundary:
 The border between two neighboring regions of different classes is known as a decision boundary.
 決策邊界

Q5
What is the difference between gradient boosting and Adaboost?

# Note
1. 如何选择feature？  选择能使错误率到最低的feature。
2. The goal is to find boxes R1,..., RJ that minimize (to some degree) the residual sum of squares (RSS).
3. R 裡面 dim()是看X有多少 Y有多少
4. bagging是减少variance，而boosting是减少bias
5.
# 流程
AdaBoost算法(R语言)

Boost算法是根据Valiant提出的PAC学习模型衍生得到，是一种可以自适应的改变训练样本的分布，
从而使得基分类器聚焦在特殊样本的迭代方法。从基本的Boost算法原理，
发展了很多不同的提升算法，如AdaBoost，Gradient Boosting等，
本文着重介绍AdaBoost算法。

AdaBoost算法与Bagging算法(R语言)不同的是，AdaBoost给每一个训练样本赋予一个权值，并且可以在每次提升后，自动调整权值。
在从原始数据集抽取自助样本集时，权值可以影响抽样分布。并且此算法对每个基分类器进行加权，而不是使用投票的方式得到最终结果。

算法流程

step1    N=原数据集大小;k=提升轮数; w={所有样本初始权值1/N};
step2    for i=1 to k{   
          根据w生成大小为N的自助样本集D[i];   
          D[i]上训练一个基分类器C[i];   
          C[i]对所有原始样本进行分类;   
          增加错误分类样本权值，减小争取分    类样本权值，得到新的w;}
step3    根据权重聚合每轮得到的C[i]，得到最终组合分类器;
