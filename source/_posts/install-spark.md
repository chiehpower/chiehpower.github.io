---
title: Install pyspark × Use on Jupyter notebook × Colab
description: <center> I recorded two installing methods. (i.e. the Mac and Windows) </center>
photos:
  - 'https://lh3.googleusercontent.com/BL2KrSPXi9jyhnmAJoCeWIYkTHiUDeymiv6w6Jw7ESPY_G9n2Kr8hncerzl97s6Q2m9fzYS8FGWALBv31z1rDI3KW1Nq8AVmieNtpmnJtO-MfxitS4ZFrkt62VAbyCPCM3myZm5cy1KIYoUS2bbHp6cw1hQ_BjrzC33uBSkSLVdQoX5_QT9Po9bTwEr-lBjLH2Wh11xj7A8bd9M9WUWJUDFcHEQlydsgYzQ83Aobxf5Y_HWbtDTfCwR0Y_8R7xwLtYmAxLS_d4FSsyGJ0HlNdupW0Yy87RCW0PfZC1nG921KSoQ2MbWAaRx_hysgsZnWV4NXN1GB0g-BdMoaeAGZebHRCll9pbxJkdvvLQtJD2OjxB7DR2__3BpsKVgOWlAlxfk6IJqDagy7bcyeNFD9ilbwAekcHs0wZjqB0WtK7vTKVth4gGM5MUKEJM75GfMyRveaX3VkvgIg4KHYPwB5cu-Dj0VgPl7p0hJ2U5PS3rCkd4VsfFacGoF1GiBCrZzGpX2gFvlK07q9uciiHPX57bQ2aNJ8EkGcrjy4eXWc_-Ggydu-yjYACcdEM6J4AbR8HLfrunCnlOpVYGaX7ZiRd44zxCsgj5jjmxhX_XpstpzO8g0PgZlwF8-G7wSpRNkess56jhf1jhplDbCMZk5Vbc7iixjPdrA4jRg6435-SAOL_2sM-AeTrTCp-dAynaJ6nWi3e1NyiX0aZjZtfaWVeNiHgg=w2160-h1216-no'
date: 2019-03-12 01:48:41
tags: [Jupyter notebook, Spark, Pyspark, Hadoop, Java, Colab, Notes, Program]
categories: Program
password:
---

# The Steps of Mac Installation

I also saw this link:
https://anaconda.org/anaconda-cluster/notebook-pyspark-language/notebook

## Install pyspark by conda

```
Last login: Tue Mar  5 16:20:24 on ttys001
(base) Chiehde-MacBook-Pro:~ chiehpower$ conda install -c conda-forge pyspark
Collecting package metadata: done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.6.1
  latest version: 4.6.7

Please update conda by running

    $ conda update -n base -c defaults conda



\## Package Plan ##

  environment location: /Users/chiehpower/anaconda3

  added / updated specs:
    - pyspark


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2018.11.29         |        py37_1000         145 KB  conda-forge
    conda-4.6.7                |           py37_0         875 KB  conda-forge
    openssl-1.1.1b             |       h1de35cc_0         3.5 MB  conda-forge
    py4j-0.10.8.1              |             py_0         178 KB  conda-forge
    pyspark-2.4.0              |        py37_1000       203.5 MB  conda-forge
    ------------------------------------------------------------
                                           Total:       208.1 MB

The following NEW packages will be INSTALLED:

  py4j               conda-forge/noarch::py4j-0.10.8.1-py_0
  pyspark            conda-forge/osx-64::pyspark-2.4.0-py37_1000

The following packages will be UPDATED:

  certifi              pkgs/main::certifi-2018.11.29-py37_0 --> conda-forge::certifi-2018.11.29-py37_1000
  conda                       pkgs/main::conda-4.6.1-py37_0 --> conda-forge::conda-4.6.7-py37_0
  openssl              pkgs/main::openssl-1.1.1a-h1de35cc_0 --> conda-forge::openssl-1.1.1b-h1de35cc_0

The following packages will be SUPERSEDED by a higher-priority channel:

  ca-certificates    pkgs/main::ca-certificates-2018.12.5-0 --> conda-forge::ca-certificates-2018.11.29-ha4d7672_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
certifi-2018.11.29   | 145 KB    | ##################################### | 100%
py4j-0.10.8.1        | 178 KB    | ##################################### | 100%
pyspark-2.4.0        | 203.5 MB  | ##################################### | 100%
conda-4.6.7          | 875 KB    | ##################################### | 100%
openssl-1.1.1b       | 3.5 MB    | ##################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(base) Chiehde-MacBook-Pro:~ chiehpower$ ls
Applications		Library			anaconda3
Desktop			Movies			blog
Documents		Music			blog_backup
Downloads		Pictures		node_modules
Google 雲端硬碟		Public			package-lock.json
(base) Chiehde-MacBook-Pro:~ chiehpower$ cd anaconda3/
(base) Chiehde-MacBook-Pro:anaconda3 chiehpower$ ls
Anaconda-Navigator.app			org.freedesktop.dbus-session.plist
Applications				phrasebooks
bin					pkgs
conda-meta				plugins
condabin				python.app
doc					qml
docs					resources
envs					sbin
etc					share
fonts					shell
include					ssl
lib					translations
libexec					var
man					vscode_inst.py.log
mkspecs
(base) Chiehde-MacBook-Pro:anaconda3 chiehpower$
```

---
## Java 版本過低問題

遇到JAVA版本過低問題 （非本人的錯誤訊息，但類似）
```
Exception in thread "main" java.lang.UnsupportedClassVersionError: org/apache/spark/network/util/ByteUnit : Unsupported major.minor version 52.0
    at java.lang.ClassLoader.defineClass1(Native Method)
    at java.lang.ClassLoader.defineClass(ClassLoader.java:803)
    at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:142)
    at java.net.URLClassLoader.defineClass(URLClassLoader.java:442)
    at java.net.URLClassLoader.access$100(URLClassLoader.java:64)
    at java.net.URLClassLoader$1.run(URLClassLoader.java:354)
    at java.net.URLClassLoader$1.run(URLClassLoader.java:348)
    at java.security.AccessController.doPrivileged(Native Method)
    at java.net.URLClassLoader.findClass(URLClassLoader.java:347)
    at java.lang.ClassLoader.loadClass(ClassLoader.java:425)
    at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:308)
    at java.lang.ClassLoader.loadClass(ClassLoader.java:358)
    at org.apache.spark.internal.config.package$.<init>(package.scala:41)
    at org.apache.spark.internal.config.package$.<clinit>(package.scala)
    at org.apache.spark.deploy.yarn.ApplicationMaster.<init>(ApplicationMaster.scala:73)
    at org.apache.spark.deploy.yarn.ApplicationMaster$$anonfun$main$1.apply$mcV$sp(ApplicationMaster.scala:763)
    at org.apache.spark.deploy.SparkHadoopUtil$$anon$2.run(SparkHadoopUtil.scala:67)
    at org.apache.spark.deploy.SparkHadoopUtil$$anon$2.run(SparkHadoopUtil.scala:66)
    at java.security.AccessController.doPrivileged(Native Method)
    at javax.security.auth.Subject.doAs(Subject.java:415)
    at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1698)
    at org.apache.spark.deploy.SparkHadoopUtil.runAsSparkUser(SparkHadoopUtil.scala:66)
    at org.apache.spark.deploy.yarn.ApplicationMaster$.main(ApplicationMaster.scala:762)
    at org.apache.spark.deploy.yarn.ExecutorLauncher$.main(ApplicationMaster.scala:785)
    at org.apache.spark.deploy.yarn.ExecutorLauncher.main(ApplicationMaster.scala)
```
>但其實已經安裝了最新版的JAVA版本，不過顯示出來的卻是舊版本。
主要是路徑問題。

---
## Improve the Java env path

更新一下JAVA的環境路徑

```
export JAVA_HOME=/Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin/Contents/Home/
```
可以放在 `.bash_profile` 裡，新增至最後一行

參考這篇：https://www.jianshu.com/p/bdde3dd6918a

>持續遇到問題
Exception: Java gateway process exited before sending its port number

---
## Install findspark

```
conda install -c conda-forge findspark
```
結果依然 **無法解決問題**。
```
(base) Chiehde-MacBook-Pro:~ chiehpower$ conda install -c conda-forge findspark
Collecting package metadata: done
Solving environment: done

\## Package Plan ##


  environment location: /Users/chiehpower/anaconda3

  added / updated specs:
    - findspark


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    conda-4.6.8                |           py37_0         877 KB  conda-forge
    findspark-1.3.0            |             py_1           6 KB  conda-forge
    ------------------------------------------------------------
                                           Total:         882 KB

The following NEW packages will be INSTALLED:

  findspark          conda-forge/noarch::findspark-1.3.0-py_1

The following packages will be UPDATED:

  conda                                        4.6.7-py37_0 --> 4.6.8-py37_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
findspark-1.3.0      | 6 KB      | ####################################################################################### | 100%
conda-4.6.8          | 877 KB    | ####################################################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(base) Chiehde-MacBook-Pro:~ chiehpower$
```

>遇到另一問題
ValueError: Couldn't find Spark, make sure SPARK_HOME env is set or Spark is in an expected location (e.g. from homebrew installation).

---
加上了
```
export IPYTHON=1
export PYSPARK_DRIVER_PYTHON=python3
export PYSPARK_DRIVER_PYTHON_OPTS="jupyter notebook"
export PYSPARK_PYTHON=/Users/chiehpower/anaconda3/bin/python3
```
>之後還是一樣回報同樣問題。
Exception: Java gateway process exited before sending its port number

---
找到pyspark檔案夾的位置。
```
/Users/chiehpower/anaconda3/lib/python3.7/site-packages/pyspark
```
---
```
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
```
測試sc是否能在jupyter內運行。
```
sc.stop()
from pyspark import SparkContext
sc = SparkContext(appName="PySparkShell")
```
在這個路徑下
```
/Users/chiehpower/anaconda3/bin
```
發布jupyter notebook
成功運行，但應該路徑未設定好，還是會有問題發生。

---
是否運行這個
```
export PYSPARK_SUBMIT_ARGS="--master local[2]"
```
需要再驗證。

---
2019/03/13 測試之後
重開機之後測試，現在又能順利正常啟動Ｏ＿Ｏ
實在很怪～～
總之，環境也無需特別設定什麼，echo $SPARK_HOME也是空的但卻能正常運行。
大概是因為用conda安裝所以環境也都一併設定好了，所以jupyter notebook直接呼叫之後，
也不需要多設定什麼。
有遇到任何問題會在即時更新。

---
# The Steps of Windows Installation


> 參考文章：
> https://blog.csdn.net/shiheyingzhe/article/details/80714301

## Windows install spark

```
pip install pyspark
```

## Install the Java Oracle

> 連結：
> https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html

`version: windows jdk-11.0.2_windows-x64_bin.exe`

### Set the environment path

>我的電腦(右鍵)->內容->進階系統設定(顯示系統內容)->進階->環境變數

User的使用者變數新增`JAVA_HOME` and `C:\Program Files\Java\jdk-11.0.2`
系統變數 找到`Path`按新增 輸入`%JAVA_HOME%\bin`

若在終端器裡輸入`JAVA -version`未找到
可以去確認一下path裡面是否有`C:\ProgramData\Oracle\Java\javapath`這個位置，若有則去這個地方把裡面的檔案(應該會有三個檔案`java`，`javaw`，`javaws`)清掉，以及刪除path裡面的這個`C:\ProgramData\Oracle\Java\javapath`路徑
再次輸入查看版本指令應該會成功顯示。

## Download the spark and Hadoop package
> 連結：
> http://spark.apache.org/downloads.html
> https://www.apache.org/dyn/closer.lua/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz

`Version: spark-2.4.0-bin-hadoop2.7`

### Set the environment path

於D disk 解壓縮之後同樣進入修改環境變數

>User的使用者變數新增`SPARK_HOME` and `D:\spark-2.4.0-bin-hadoop2.7`
系統變數 找到`Path`按新增 輸入`%SPARK_HOME%\bin` and `%SPARK_HOME%\sbin`

## Install hadoop

> 連結：
> http://hadoop.apache.org/releases.html
> https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.1.2/hadoop-3.1.2.tar.gz

下載hadoop相對應的包，本應下載2.7.7版本，但由於網址出問題改下載3.1.2。
Download `version: binary 3.1.2`

### Set the environment path

於D disk 解壓縮之後同樣進入修改環境變數

>User的使用者變數新增`HADOOP_HOME` and `D:\hadoop`
系統變數 找到`Path`按新增 輸入`%HADOOP_HOME%\bin` and `%HADOOP_HOME%\sbin`

另外，到下方網址下載兩個文件`winutils.exe` and `winutils.pdb` 複製到`D:\hadoop\bin`裡面

> 連結：
> https://github.com/srccodes/hadoop-common-2.2.0-bin/tree/master/bin


基本上這樣就完成了。
輸入`pyspark`是否能於終端器中顯示。
測試jupyter notebook中是否能夠運行：
```
from pyspark import SparkContext
sc = SparkContext()
```
or
```
sc
```

---
# Install pyspark in Colab

>參考文章：
https://medium.com/@chiayinchen/使用-google-colaboratory-跑-pyspark-625a07c75000

Just type it, and it will work.
```
!pip install -q pyspark
```

![colab_spark](/images/colab_spark.png)

---
# Monitor your jobs

![spark_job](/images/py_spark_job.png)
