---
title: Deep Learning 深度學習
description: <center> </center>
photos:
  - ''
date: 2019-05-18 13:02:15
tags:
categories:
password:
---



Log-loss is suitable for Classification, and cross-entropy loss is same.
because the classification will use the sigmoid, and the cross-entropy can increase the residual of sigmoid.
the MSE is suitable for regression.
softmax is suitable for mutli-classification. (becasue softmax is sum of all value and the sum of them is 1. (we could think it is probability))

btw sigmoid is easily to happen the gradient descent vanishing problem.
After we use the sigmoid and softmax which are activation function, we can use the log-loss (Cross_entropy loss function) to estimate the accuracy.

---
## Pooling
- Max Pooling
把取範圍內的最大值
- Average Pooling
曲範圍內的均值
- Min Pooling
取範圍內的最小值出來


## Padding
padding = ‘VALID’
padding = ‘SAME’
## strides
要移動的格數


Softmax 回歸是邏輯回歸 (Logistic Regression) 的推廣，邏輯回歸適用於二元分類的問題，而 Softmax 回歸適用於多分類的問題。
https://medium.com/%E6%89%8B%E5%AF%AB%E7%AD%86%E8%A8%98/%E4%BD%BF%E7%94%A8-tensorflow-%E5%AD%B8%E7%BF%92-softmax-%E5%9B%9E%E6%AD%B8-softmax-regression-41a12b619f04



---
1. If the smaller is regularizers.l2 value, the more convergent is result.
2. For the optimizers, the adam is more efficient than the RMSprop.
3. The more neurons may not necessarily be getting better results.
4. What value the dropout should be used? When should the dropout be used? How many times should the dropout be used?
5. Could I use the Relu, tank, sigmoid in the same breath?
6. Why do we use the RMSprop rather than use the Adam?  
7. How to choose among the Cross Entropy (categorical_crossentropy), sparse_categorical_crossentropy and binary_crossentropy?

------

## RL

### Q learning

#### 英文

- Medium https://medium.freecodecamp.org/an-introduction-to-q-learning-reinforcement-learning-14ac0b4493cc
- [Reinforcement Learning with Q tables](https://itnext.io/reinforcement-learning-with-q-tables-5f11168862c8)
#### 中文

- Medium https://link.medium.com/YBSxkV55OV
- https://blog.csdn.net/itplus/article/details/9361915
- 莫煩 https://morvanzhou.github.io/tutorials/machine-learning/reinforcement-learning/4-2-DQN2/
  - [Morvan Github](https://github.com/MorvanZhou)

### RL

#### 英文

- [Reinforcement Learning Demystified: Markov Decision Processes (Part 2)](https://towardsdatascience.com/reinforcement-learning-demystified-markov-decision-processes-part-2-b209e8617c5a)
- [Deep Reinforcement Learning: Playing CartPole through Asynchronous Advantage Actor Critic (A3C) with tf.keras and eager execution](https://medium.com/tensorflow/deep-reinforcement-learning-playing-cartpole-through-asynchronous-advantage-actor-critic-a3c-7eab2eea5296)

#### 中文

- [ML Lecture 23-1: Deep Reinforcement Learning](https://www.youtube.com/watch?v=W8XF3ME8G2I) This is U2

(未整理)
>## RL
主要在介紹RL的value function and state-action function.
- [簡介 Markov Decision Process 與其應用](https://blog.techbridge.cc/2018/10/27/intro-to-mdp-and-app/)
(次推薦)
- [An introduction to Q-Learning: reinforcement learning](https://www.freecodecamp.org/news/an-introduction-to-q-learning-reinforcement-learning-14ac0b4493cc/)
- [Reinforcement Learning 健身房：OpenAI Gym](https://medium.com/pyladies-taiwan/reinforcement-learning-健身房-openai-gym-e2ad99311efc)
- [OpenAI gym 环境库](https://morvanzhou.github.io/tutorials/machine-learning/reinforcement-learning/4-4-gym/)
- [Reinforcement Learning 進階篇：Deep Q-Learning](https://medium.com/pyladies-taiwan/reinforcement-learning-進階篇-deep-q-learning-26b10935a745)
- [Reinforcement Learning Demystified: Markov Decision Processes (Part 2)](https://towardsdatascience.com/reinforcement-learning-demystified-markov-decision-processes-part-2-b209e8617c5a)
- [增强学习（二）----- 马尔可夫决策过程MDP](https://www.cnblogs.com/jinxulin/p/3517377.html)

------

### mnist_fashion

- How to use the mnist_fashion https://medium.com/tensorflow/hello-deep-learning-fashion-mnist-with-keras-50fcff8cd74a

------

### Practice Repository

https://github.com/Rowing0914/TF_RL/blob/master/agents/Q_learning_train.py
https://github.com/Rowing0914/TF_RL/blob/master/agents/DQN_eager.py~~

https://github.com/Rowing0914/TF_RL

------

QRN

------

### RNN

#### 英文

- [A tutorial on training recurrent neural networks](http://www.docin.com/p-704741266.html)
- [A Critical Review of Recurrent Neural Networks for Sequence Learning](https://arxiv.org/pdf/1506.00019.pdf)
- [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [LSTM implementation explained](https://apaszke.github.io/lstm-explained.html)
- [Deep Learning Lecture 12: Recurrent Neural Nets and LSTMs](https://www.youtube.com/watch?v=56TYLaQN4N8) This is U2
- [Recurrent Neural Network-RNN](https://medium.com/datadriveninvestor/recurrent-neural-network-rnn-52dd4f01b7e8)

#### 中文

- [遞歸神經網路（RNN）和長短期記憶模型（LSTM）的運作原理](https://brohrer.mcknote.com/zh-Hant/how_machine_learning_works/how_rnns_lstm_work.html)

------

多分類問題 activation=('softmax') loss='categorical_crossentropy' one-hot True labels

Softmax 函數通常會放在類神經網路的最後一層，將最後一層所有節點的輸出都通過指數函數 (exponential function)，並將結果相加作為分母，個別的輸出作為分子。



二分類問題 activation=('sigmoid')

------

Q: Why the MSE need to "square"?

A: Becasue  sometimes you have a lot of data which have positive and negative, so if you sum of loss, the loss will be small, but it is not correct.

# Reference
## Gradient descent
This website introduces many kinds of different gradient descent optimization algorithms. (Very higher quality)
- [An overview of gradient descent optimization algorithms](http://ruder.io/optimizing-gradient-descent/index.html#adam)

基本上是上面那篇的翻譯 XD
- [深度学习最全优化方法总结比较(SGD，Adagrad，Adadelta，Adam，Adamax，Nadam)](https://zhuanlan.zhihu.com/p/22252270)

## CNN
網路上許多
http://cs231n.github.io/convolutional-networks/#conv

## Youtube
最推薦的就是李宏毅教授的教學影片，真的非常非常推薦！
- [李宏毅教授](https://www.youtube.com/channel/UC2ggjtuuWvxrHHHiaDH1dlQ)
- 李宏毅教授的[教學網站](http://speech.ee.ntu.edu.tw/~tlkagk/courses.html)，有提供ppt

## 很不錯的文章

- [Tommy Huang](https://medium.com/@chih.sheng.huang821)

裡面有講述許多機器學習深度學習的原理
- [資料科學・機器・人](https://brohrer.mcknote.com/zh-Hant/)

## Kaggle
- [Kaggle](https://www.kaggle.com/learn/overview)

# 常見問題
梯度消失
梯度爆炸
怎麼樣的activation function才是好的function

# Fashion-MNIST with tf.Keras
- [Fashion-MNIST with tf.Keras](https://medium.com/tensorflow/hello-deep-learning-fashion-mnist-with-keras-50fcff8cd74a)
- [Fashion-MNIST：替代MNIST手写数字集的图像数据集](https://zhuanlan.zhihu.com/p/28847070)
