---
title: Lasso & Ridge Regression
description: <center> </center>
photos:
  - ''
date: 2018-11-18 19:11:32
tags: [Python, Lasso]
categories:
password:
---
Function Design:

Input:
1. iteration number
2. fitting object (i.e. X_train, y_train)
3. alpha value
4. weights

Normalized the data, if data need.
要注意是否有正規劃與中心化

beta/Weights n*1矩陣 且 n = features數目  也就是迴歸係數(吧!)

Q:
迴歸係數 Rergression coefficient is Beta/weights?
跌代圈數的地方 where does we implement iteration place?
取最小的COST 何意? RSS需要求導? If we need to get the min cost function, does the RSS need to take the derivative? And what's that meaning?
難道是用梯度下降來求(找)最小值? Surely we use the Gradient to find the minimun value?
So which one method do you use to calculate the RSS? Coordinate or Gradient?

1. 因為懲罰項是絕對值得原因所以圖形才會是直線在座標上才會是角狀(菱形)
2. 有梯度下降法也有座標下降法 (?)

Normalisation
or
Normalization

>English skill taught
chosen out
The primary key is chosen out of all candidate keys
從所有候選鑰匙中選擇主要鑰匙

We can't use the MinMaxScaler().
不可以用這個因為 性別 2 & 1都是有意義 但如果用了就會變成0 與 1 但這樣在計算上就不會有意思

Standardization, or mean removal and variance scaling


Data-snooping bias
数据透视偏差
>簡單來說就是：以為這兩個數據之間有一些關係或關聯，但其實兩者之間根本屁都沒關係。

是指在基于先前得到的实证经验后对历史数据进行分析后所得到的偏差。
数据窥视（ data-snooping ）是指从数据中发现统计上显著但实际并不存在的关系，是金融分析里面非常普遍和严重的一个问题。
```
<script src="http://code.jquery.com/jquery-2.0.0.js"></script>
{% asset_jupyter /Users/chiehpower/anaconda3/bin/python3.7 ../jupyter-demo/Lasso.ipynb %}
```




---
# 2019 05 14 理解。
# 為什麼我們需要做linear model Normalisation?
如果數據裡面有共線性問題，會造成數據的變異性高(Variance高)，因此我們可以透過model Normalisation來降低或去除。
如果是線性預測問題，一般來說常用的三種就是`Ridge Regression`,`Lasso`,`Elastic net`。
- RSS(residual sum of squares)+L2 norm 就是 Ridge Regression
- RSS(residual sum of squares)+L1 norm 就是 Lasso
Ridge Regression加了一個二階懲罰項，而Lasso加了一階懲罰項。

# 何時使用？
我們何時何種情況該使用Ridge regression 還是 Lasso?
一般來說，default是L2，他可以有效的將不相關的係數逼近0，而如果Lasso就會將不相干的係數為0，而這就得取決於你的需求。
不過，如果用Lasso有一缺點，因為他會將一些特徵係數變成0的因素，而降低了其正確性。


一般來說，當特徵變數量增加，我們常會遇到的三個主要問題：
1. Multicollinearity 多元共線性
2. Insufficient Solution 解決方案不充分
3. Interpretability 可解釋性

# 參考文章
[Regularized Regression | 正規化迴歸 – Ridge, Lasso, Elastic Net ](https://www.jamleecute.com/regularized-regression-ridge-lasso-elastic/)
