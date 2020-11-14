---
title: Linux
date: 2017-10-05 11:56:25
tags: [ Linux , Instruction ]
categories: Linux
photos:
- "https://lh3.googleusercontent.com/S04CeosUhKHc8I0G1YRT_ElQ_AS1CLQNLEhLxR76J7GCTCFX2V5DHxgpCXtka3jDgAac-FVr9smkj4yfpVleANxe2TVRe4idteadO0AkQWp0pMr5qDU4nhcqXrRCOaNaNnwY2osD9uZhZjTHg3vd-B-r6tETLpvnMF4SlYq7JCuVqJB5YtKPyS8x4tqfxi96q7PjwnfrOo3aWYMuczQGa3xIHMx5-zPvXtuL1O-PgZlFCFbHf8wjELg0p5FXjJI18Zram-HpqBwsyRKR_wXuQDVk_OL9Fb1n3U9ytNuunLan7yJcs8IvnB-fsJ3WhzZH_MmIi1eYEkHXVFobq6AK3NdNUAyT4i_KReZcCcVLUFOUtkIXCgOlpUh5kHCuXx2ldxyfR40nnvFnf6uQv6ICXPg9kVqphOTKUoEC1dqqVvy7bBSF6AP8I6I85f6xC85vNgz-uw343XUVBx2naF8-KfSeHYwAjOtNac7xCf_EDWIWF1qM8AOd60PSjRdls-nytfaNe8NR707bfeh5FfmLnHtG5toIMwBDHmj8fZ9Gw9sAw_nQmRH4lFQbH9Da7gpbWkPJVq2H3PuvqaDBIqwo_ppujlVy7mZKiCNrXDRQGrVe4d5ErquJqxH85B2P5zCN8aAuQ_lUWSOsu5yR4qOYgqlaZSPUwZdXhNG-3FVbJM3WBTyo0Nr03zHx=w1560-h878-no"
---
{% cq %}*In Linux ,
if you want to transmit files between server and server ,
you can use these instructions.*{% endcq %}
<!---more-->

1. # 傳送檔案(單個)
  從A伺服器傳檔案到B伺服器內
  於A伺服器內，
  請到你要傳送的目錄或檔案下
  接著用ftp方式登入B伺服器
  ```
  sftp user@(ip)
  ```
  登入B伺服器後，
  在B伺服器內，
  前往你想要傳送到的目的地檔案夾下 (Ex: /mnt/imdata1/Lee)
  ```
  put (檔名)
  ```
  ## 指定port
  BTW. 若是sftp要傳送的伺服器port是有特定的話指令改為		
  ```
  sftp -o port=(數字) (user)@(ip)
  ```

  ---

2. # 多個檔案或者檔案夾的伺服器之間傳送 (實用)
  >這個指令非常方便，只要你傳過的檔案他就不會再上傳一次，
  算是一種"更新的指令"，便於備份。

  使用時機，想要將A裡的資料備份到B伺服器，
  則於A伺服器內，
  到你要傳送的該目錄列下
  輸入
  ```
  rsync -alPvz (檔案) (user)@(ip):(目的)
  ```
  例句
  ```
  rsync -alPvz ./(file_name) dell@XXX.XXX.X.XX:/mnt/imdata1/Lee
  ```
  如果想要一次全部傳送檔案
  就使用米字符號代表全體(file_name改為星號)
  ./*

  1. ## 查硬碟容量
  ```
  df -h (-h 是換為kb)
  ```
  2. ## 查看該子目錄下檔案的大小		
  ```
  du -h --max-depth=1
  ```
  指令來源:
  <https://unix.stackexchange.com/questions/26934/using-sftp-to-transfer-a-directory>


  -
```
sftp 遠端主機  (可進行檔案傳輸)
put filename  (將檔案傳到遠端電腦)
get filename  (將檔案從遠端傳到本機)

ssh 遠端主機  (可進行指令操作)

tar -zcvf 壓縮後檔案名.壓縮格式 檔案名(將檔案壓縮)
tar -zxvf 檔案名   (將檔案解壓縮)
```

[註釋 原文網址](http://tnrc.ncku.edu.tw/course/93/fedora_core2/page7/p7.htm)
c   create一個tar ball
f   指定tar ball檔名
v   verbose，列出過程
z   使用gzip壓縮 tar ball
x   解出tar ball

---
# 查看電腦CPU資訊
```
cat /proc/cpuinfo
lscpu
```
---
Linux系統
Manjaro
