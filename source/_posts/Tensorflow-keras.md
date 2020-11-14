---
title:  Install Tensorflow & Keras
description: <center>安裝Tensorflow與Keras，並且能在Jupyter Notebook上使用。</center>
photos:
  - 'https://lh3.googleusercontent.com/gFXv2xgDGsRNIJ3TDjh77VMbrIetHpNPmP6kA-_3_RqJvORXcs2X9l06SbXYYgev0OYFDX2008IVWqnMv7WXNROYyG2mbudSxoXKfCVGkTM4RikGv844moH2ULT5JqSVTlfhtQcL3nZw1mWp-Q6Ah2VDezsPDjI3Tg0tAcjzlJhvuIbcIri_SLshKA5HMAkk6VYaP55q-SnuVfeQJFvVG0Xgc689p6rtFs2d8TX6LnVO87ihVC3o9IVqQh_CdC9Ck7Zqz9jOhy1idu8103JLl0wo8fon2CtUTNQ7CTCL8fVWESuhVZ3-fE4jyx-xKS20H_SxKdkawh0qFapeC5iEacxkPIkcSU9WUf5vEts7J7_7QxgkFQL5CPvJoJXcmIz0kIZN2g-FnU3UAMKkXwNBImRLObBAn1JoIflA1rexGGhBRDSx3mFgUS6jGHwQDb_veLJOIG8xHAIF1mPTBD_fN6KbRI_QYy7t6OLjQxPe7SY4IrFzBJn4CRlD2CI5v_rDLCTc6UqN6w3zV3fQ0e_lk6ZvVu7QX4L3J-RX9KvMU0d7DsBDR1q5a7Z0zRF_2zID4msYnVjMGKqBuaSFLcK5NXXrc2uqImB3nCTtHezNKOvt4EUGYzQS1Te1VrC3YD5gA4OBco7pfDakund79VRGlf6C4DtGOza71w1yIaNwlDptNDaROCgiLFwLu59KMaNSwOZun9VFdVIzRwzn8LA=w1707-h960-no'
date: 2019-01-31 13:25:12
tags: [Jupyter notebook, ipynb, Tensorflow, Keras, Python, Anaconda, Conda, Notes]
categories: Program
password:
---
深度學習的朋友應該都會需要接觸到這兩個鼎鼎有名的程式，這裡有幾點小地方需要注意一下。
如果碰到Anaconda軟體自己跳出來說要不要更新，先不要更新容易有問題發生。
另外一點在安裝的時候，一般來說有好幾種方式，常見方式一種是`pip`另一個是`conda`，這邊爬文之後建議用conda來安裝，效能比較好(?)
The friends of deep learning should need to use these two famous programs, there are a few small places to pay attention to.
If you encounter an Anaconda software which jumps out and says about update version thing, please don't update it because there are easily problems.
Another point is that there are several ways to install it. The common way is `pip` and the other is `conda`. After I searched some webistes, it recommended to use conda to install it. The performance is better (?)

> 設備與環境： (Device and Environment)
Anaconda version: 1.9.6
MAC bookpro OS: Mojave 10.14.3
Python 3.6

本人我也在windows 10上成功安裝，指令也是一樣的。
I also successfully installed on Windows 10, the commands are the same.

---
# Install TensorFlow
[OS我是選擇安裝無GPU版本]
[For OS, I chose the CPU version]

[Install tensorflow in Anaconda](https://www.anaconda.com/tensorflow-in-anaconda/)

## Create the virtual environment

Interested in trying out these TensorFlow packages? After installing Anaconda or Miniconda, create a new conda environment containing TensorFlow and activate it
```
conda create -n tensorflow tensorflow
conda activate tensorflow
```
Or for the GPU version
```
conda create -n tensorflow_gpuenv tensorflow-gpu
conda activate tensorflow_gpuenv
```

## Install TensorFlow packages
For Chinese
- 可以參考此篇 [TensorFlow 環境搭建](https://medium.com/@prairie5270/1-tensorflow-實戰深度學習框架-tensorflow-環境搭建-a779b24bd165)
- 還需要去anaconda裡面[安裝package](https://anaconda.org/search?q=tensorflow)

---
## Meet the error messages
```
2019-01-30 23:30:27.762541: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
```
解決方案：
Solution:
```
import os
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'
```

- 參考這篇[解決方案](https://blog.csdn.net/GeneralLi95/article/details/80463628)

---
## Solve the Jupyter and iPython problems
因為一般Jupyter是安裝在全域環境，而tensorflow是安裝在虛擬環境，因此做法是在tensorflow環境下安裝jupyter。
Because the general Jupyter is installed in a global environment and tensorflow is installed in a virtual environment, the solved method is to install jupyter in the tensorflow environment.
```
source activate tensorflow
conda install ipython
conda install jupyter
```
基本上應該就可以了
直接呼叫`jupyter notebook`出來輸入
Basically it should be fine.
Directly type the command `jupyter notebook`.
```
import tensorflow as tf
print ("TensorFlow version: " + tf.__version__)
```
有跑出來就是成功。
Running out is success.

# Install Keras

PS 需要先安裝好tensorflow。
在tensorflow的環境下執行安裝指令。
PS You need to install tensorflow first.
Execute the installing commands in the tensorflow environment...
```
conda install Keras
```
再次呼叫`jupyter notebook`出來試試看。
Type the `jupyter notebook` again and try it out.
```
from keras.models import Sequential
```
顯示 `Using TensorFlow backend.` 基本上應該就是成功了。
If it shows `Using TensorFlow backend.`, it is successful.

---
# Summary Steps [Lite]
1. 點開終端器，或者windows可以開啟Anaconda prompt。  
Open the terminal, or open the Anaconda prompt for Windows.
2. ```
  conda create -n tensorflow tensorflow
  conda activate tensorflow
  ```
3. ```
  conda install ipython
  conda install jupyter
  ```
4. ```
  conda install Keras
  ```

---
# Matplotlib's poblem
如果顯示
If it shows...
>ModuleNotFoundError: No module named 'matplotlib'

Steps:
1. 去Anaconda Navigator中選擇Environments再
Go to the Anaconda Navigator then selecting Environments.
2. 選擇tensorflow，在installed中查看是否安裝了matplotlib
Click the tensorflow and check in the `installed` whether the matplotlib is installed or not.
3. 如果沒有找到，就換到Not installed，將其安裝上，就可以解決了
If it is not found, change to `Not installed` and install it, you can solve it.

- [參考文章](https://blog.csdn.net/yangzijiang666/article/details/79695938)

---
# Source Environment
如果要啟動tensorflow一般就是在prompt裡面直接下指令 source環境，但如果要用按按鈕的方式其實也可以，點開Anaconda裡面，到環境(Environment)，選到Tensorflow右鍵，就會看到Open Terminal點開直接就可以了，如果你是要開jupyter notebook也可以直接選。
If you want to start jupyter notebook and activate the tensorflow environment, you can do this two ways.

One way is to open the Anaconda Navigator program, switch to the Tensorflow environment by clicking on `Environments` and selecting Tensorflow and then launch Jupyter notework directly.

The other way is to do this but through the Anaconda command prompt following the instructions above in my blog. (typing `source activate tensorflow`)

![activate_tensorflow](/images/activate_tensorflow.png)
