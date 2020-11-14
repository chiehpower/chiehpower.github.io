---
title: Manjaro & 掛載硬碟流程
date: 2018-01-31 22:39:08
tags: [ Manjaro , Linux , Mount ]
categories: Linux
description: <center> Manjaro介紹，與掛載硬碟流程 </center>
password:
photos:
  - "https://lh3.googleusercontent.com/2bxqp4vHiAYRSrfHxzlKmfRNt2gQnXr5JuMvH2W0NdZXYA1m5EAkIKhb2OQJafKCpJwCy3RwDQxo4Brh7Zbq9-weqRHDbcllhaY5415ZcTxR8KHhJpjXfBRgM7MjxAsjBadadjXL1CFu34L1KjsfawjG7jQRhV7b0IGT8-BJbkPB6TWCfyIXgM6Olm0gYXndznr1uHmhY1Bg1P6CnUuwSPSBBVxuWmia2f2NuIfl6knOBfSL0lv0e2m8s-pB-bdXVboK-cRHygdmly-k_lod7uJ8qOKfSMk9eM17O1gG_AjSXbzfX9rjSlW7qM2Vu5Lsia_Fdn6rayRS8wSqTRa1NeXjDEStL-5TBVdZ2AlmJePZlsJhIiJqNIsEBoiqLhGbchHHf2fByKsGFiuHQj4BEeww3eHL0LbmQgbgo3fIezBvMZ_JhT0nptdW5nQshFXw4e_ZvbzMExLjlkK1rmoqgItfK75PH5qdipYdzPdljGsfGlVYUVXWX8h3vJMXuEvDRXJds-AJwPvYt9mrpl47hqb5w4OcS87w4l9d23E6uSzJ-ujr7nPjqKuA_ylTW5_EXhgQFaWAAIPmRSEjZXT4fnSZ1ohC13q40r4d9JJQalXZnhpothWwWtkOVwaSaeDypCni_NGgRK-iqb37UcdxRLPCYAqqszTaM1Bzz9qq3A1zA_pqaAsvY_6ECbFoMHKUAf3K9EuHKw-pCVAcOX8=w2160-h1216-no"
---
![Cinnamon (17.1.2)](/images/post_manjaro.jpg)
<!--more-->
這次介紹一個快速高自動化安裝是基於Arch Linux的發行版 - [Manjaro](https://manjaro.org/)
主要目標是為PC提供易於使用的自由的作業系統。
基本上就是自動裝好也不太需要做什麼額外設定。

# Cinnamon
我下載的版本是 Cinnamon
下載好後，在內部更新時會遇到說
```
lib32-glu: installing mhwd (0.6.0rc1-4) breaks dependency 'lib32-libgl'
```
請輸入以下指令做解決
```
sudo pacman -S mhwd mesa libglvnd lib32-mesa lib32-libglvnd --force
sudo pacman -Syu
```

* 如果要裝一些lib之類，找Arch的指令為主。

---
# 蜂鳴器
如果遇到蜂鳴器很吵，可以使用一個簡單的方式做解決 (非永久性)
```
rmmod pcspkr
```

---
# 硬碟掛載流程
由於我是使用VMware，硬碟上的使用常會遇到不足需要擴充，因此以下為掛載新硬碟的流程。
流程分成三步驟:
 ```
 1. 檢查 fdisk
 2. 格式化 mkfs
 3. 掛載 Mount
 ```

## 檢查
```
 1. ls /dev/[sh]d*
 2. fdisk -l /dev/___      #底線放你要掛載的硬碟 ex: /dev/sdb 之類
 3. fdisk /dev/___         # ex: fdisk /dev/sdb   
 ► n (分割區) ► p (分割數) ► w ► q
 4. fdisk -l /dev/___
 ```

## 格式化
```
- mkfs -t ext4 /dev/___  
- mkfs -t ext3 /dev/___    #看你是哪種，大部分是ext4
```

## 掛載
 1. sudo blkid             #查看UUID
 2. vi /etc/fstab 加入 UUID
 3. 掛載，看你要掛載在哪一個資料夾底下。我的操作流程是，在始目錄下創一個資料夾(ex: work)，然後輸入
 ```
 mount /dev/sdb /new/
 ```
 就會把sdb掛載在new資料夾上了。
 4. 最後就reboot 並用 df -h 檢查一下是否有新增成功。
