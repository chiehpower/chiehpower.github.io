---
title: Tensorboard
description: <center> </center>
photos:
  - ''
date: 2019-06-17 12:59:35
tags:
categories:
password:
---


# 目標
1. [Tensorboard](https://github.com/tensorflow/tensorboard/blob/master/README.md)
2. [Jupyter with Tensorboard](https://github.com/lspvic/jupyter_tensorboard)
3. [JupyterLab with Tensorboard](https://github.com/chaoleili/jupyterlab_tensorboard)
2和3比較麻煩一點。暫且放著。希望未來能夠完成。


# 初始練習
首先，我們先使用現成的code測試一下是否能夠成功的在本機(local)運行。
如果成功之後，我們再來學習如何使用在自己的code上。

我使用[2017 IT 邦幫忙鐵人賽]的[第28天深度學習(2)TensorBoard](https://github.com/yaojenkuo/learn_python_for_a_r_user/blob/master/day28.md)內教學來做練習，並且一一測試確實能在tensorboard上跑出結果。
附上連結：https://github.com/yaojenkuo/learn_python_for_a_r_user

把Code直接貼到py檔內做運行即可。
每次跑完，並於終端器上輸入`tensorboard --logdir='TensorBoard/'`
(因為code裡面`tf.summary.FileWriter("TensorBoard/")`是寫`TensorBoard/`)
便會跳出一行網址，複製於瀏覽器上輸入就可以看到結果了。

按照裡面教學流程做應該沒問題。

>不過這個教學是使用tensorflow來做計算，不適用keras。
以下直接提供現成檔案，跟`第28天深度學習`內的是一樣的。
- [tensorboard_test.py](../Tensorboard/tensorboard_test.py)

# 嘗試Keras
接下來我們嘗試使用Keras套件包與Tensorboard的效果，
參考terrence大大寫的[用Keras跑tensorflow](http://terrence.logdown.com/posts/1321107-keras-run-tensorflow)
一樣我也附上copy網站上所操作的code的檔案，可直接下載練習。
於終端器輸入`tensorboard --logdir=/tmp/keras_log`即可看到結果。

>PS 其中我修正了`histogram_freq=0`部分，若按照網站上的code在我電腦上跑會有error。
- [tensorboard_keras_test.py](../Tensorboard/tensorboard_keras_test.py)
