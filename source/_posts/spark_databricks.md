---
title: Databricks 使用流程
description: <center> 介紹如何輕鬆在Databricks上操作Spark。 </center>
photos:
  - 'https://lh3.googleusercontent.com/R5LU72iR_Jldl9qecsMdy0W1cGQn-__taWMCuCiHCIiYSggrRmFD2uaWdBv06WdCH4OX-85IFzgN-JmfBtzaGqiBxrfhSJVWicxL_kEW95gQlDWhULtznDYVh0qpW-S-3fQvfFW1_Ncc5VDqontgbOWkkNE3vNs53t6zUFvNVPWkdA6r55-LqbhU5VR8qpS98b98MSAfI88b4sdFVjnxvtxJSVeBmUCfvaD0hni92fyEQT9QrKGUwYE006hE4mBSW4s4UwUJuIPGaqMY5KK7NKilQqk5Tqs6HtMMFMaVovMqYebjFb4VxCdE6NFhVqx5zPokSt81s2TWggQu2nNJCiA_jjBSU5pvcIrKyQo9MXrl1_mJsC3fVtp9oNE-ZEZ7MMnkUx6sT-sHhKPtZ6BnPKNz-DoaYIOF39QD6gswS2FsIml-raOvhZh2qaYAc9xyUSjymWt1IjIrTqEwQjG1RS4yOtUpYqmKS3x2870DoltgqHrGtTQF9TYPbBW3YpDGVGjFfeCXyH51O_2ua0E1G5C2p9-g4JIRBaKp6xhebXhdD5EvCkH-sm88mERT-sL6To57dpF5IYjVCBblcy_YHDHctV1kboxQeL6jdS3XlTUo7l6ghszlymUT3ACE801NjKQNKzdloZRmChn3Kk3CfB-251R90zQSqRa_ulRZSpvsbHhIE3IzJ5t3DNlD41k7GvvZU97uxvvzXgroLB1sr7MqaA=w2160-h1216-no'
date: 2019-03-12 13:04:23
tags: [Spark, Pyspark, Hadoop, Colab, Notes, Program, Databricks]
categories: Program
password:
---
使用Spark有一個不錯的平台『Databricks』，雖然後來已不使用ＸＤ 轉戰到Colab上操作。
因為Databricks免費使用有個缺點，容易時間一長就要重新創建Cluster。
當然使用這個好處是可以不用使用到本機的資源。

首先，如果要找登入帳號的頁面，在google首頁直接打上`databricks account login`，點選第一個`Login - Databricks Community Edition`

進入之後會看到這個畫面。
![databrick](/images/databricks_1.png)

我們可以看到旁邊有一些選項:
1. Home
2. Workspace：裡面會儲存所有的import檔案
3. Recents
4. Data
5. Clusters：每個檔案都需要有一個cluster來做支配。
6. Jobs
7. Search

我們會用到的是 `Workspace` ＆ `Clusters`部分。

{% cq %}總共有兩大Steps，首先第一步是要先創造一個Cluster。
再來是我們要把我們的file import 進去 Databricks。{% endcq %}

# Create Clusters 
點擊左側的Clusters，裡面列出所有的已創建或還未創建的群集。
剛登入的時候(或一般過了一段時間之後他會停止，需重創)，我們先創建一個。點擊上方的`✚ Create Cluster`之後會看到下方的畫面。
![databrick](/images/databricks_2.png)

可以隨意起個Cluster Name，我們選擇最新的Databricks Runtime Version版本吧！Python Version選擇3，然後其他可以不用動，最後就是Create Cluster。
一開始state是Pending，等個幾秒鐘讓他處理一下，當state變成Running時，這樣就創建成功囉！

# Create file
再來我們可以到Workspace area，如果是一開始使用是空的，我們可以選擇Create一個空白的file，或者要import file進去都可以。
按右鍵，或出現Create & Import。
![databrick](/images/databricks_3.png)
選擇Create file > Notebook，之後會跳出視窗填入file name、選擇使用的語言spark可以使用四種語言，個人使用Python，最後就是點選我們剛剛創建的cluster。完成之後就創建成功。
![databrick](/images/databricks_4.png)
我們直接type sc，shift+enter，可以看見`Out[1]: <SparkContext master=local[8] appName=Databricks Shell>`，完成。

如果是import file的人，記得在Detached點選我們剛創建的Cluster。
然後就可以運行我們的code了。
![databrick](/images/databricks_5.png)

不過一段時間就需要再重新操作一次cluster流程... lol
當然有另一個擇中辦法就是使用Colab，我覺得相對方便許多🤔

👉可以參考這篇[Install pyspark × Use on Jupyter notebook × Colab](https://chiehpower.com/2019/03/12/install-spark/)