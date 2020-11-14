---
title: AIRSS
date: 2017-11-29 13:51:05
tags: [ AIRSS , CASTEP ]
categories: Linux
description:
photos:
  - "https://lh3.googleusercontent.com/Txg503nhDVQHVdmlP9NUYoJukPLFLgNuN_TC_sViAnQdJMKhWgnfeJ8WkljEBQL2WmXEygwL_UM_BmW7bt4nuzUsCHrQykE895C51RrtdZiel43gsl5tjVSQSgmbnH70TDoKoe-okSIpSIw_mjVp_2Po4WnqfiFvIxvFSUDk7Vs0w-IsOaK8ZQPzQ6voPMt8Dp53mu0P-o63ziPbkbasupBo-OYgAT65gn8Xxzudo0MMdcNK-EgTxsdPiygqK_GV0k-Hh9lLgBeK35k5PNHVgJpL7CrcCv4niQ80TH4Wo2cPrJbwwcfbq51A-LvgqSMgSpSEETdtEbdzj36LGELxFrBW8gs8wayMCMm3IfAng2GotfRHXKTkWIHBF62l9fnPW7kBLuwzYul88X_MGiVepOt4wK7EyfU-Yx8xoEcNq7LR4y6uxGATSyPCaRUYe8QtXWQctPsQcXGoAc0IhzuGC9GNOW2ukpsPQGV3hioVqy0yGUhlHtF1Qo2zEf-5r3sNQhU6R3CiLhxKiRaS8tjSiw56GUUAZ7_RiRal4bdIdQWLTD6PG20yt8QjYgyWXHfuNYG0fNB9dsacj0rjkSPUsmf60Gv6EWFIm73BYaC21olbORh9XN459R9ueyVdItHy2XIWfO6OeJ223sGTBOq60cIFtik-fHnL7oE1mNgE4lfy44CNlwabJF-maFwxtpPX8PywfJfhd33UYSmyzIE=w2168-h1220-no"
---
[AIRSS](https://www.mtg.msm.cam.ac.uk/Codes/AIRSS) 全名為 Ab initio Random Structure Searching
[檔案下載處 0.9版](https://www.mtg.msm.cam.ac.uk/files/airss-0.9.tgz)

**※特別注意 AIRSS目前是支援CASTEP 2017版本以上，在驅動CASTEP注意一下!**

初始在安裝時，Makefile前，請先export environment
```
export PATH=$PATH:/home/username/airss-0.9/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib64/
source ~/mpivars.sh
```

<!--more-->
於airss.pl腳本內，可以自行替換要驅動的CASTEP來源，甚至可以驅動MS的RunCASTEP腳本來做CASTEP計算。

# 一般基本計算指令與流程
- 計算結構搜尋
```
airss.pl -press (看要計算幾Gpa) -max (計算結構數量) -mpinp (核心數) -seed (檔名)
可另，外加上 -keep -step 0 等等指令。
```
- 分析
結構搜尋完之後用基本的分析指令
```
ca -r
```
- 由左到右的意思
  The above is a "ranking" of the results according to energy (strictly, enthalpy).
  The first column is the unique structure name, the second - pressure, the third - volume per formula unit (fu), the fourth - enthalpy/fu for the first, and then relative to that, the fifth - number of fu, the sixth - chemical formula, the seventh - symmetry, and the eighth - number of repeats.
  (參考Example 1.1部分有寫)
---

目前測試過的是，可以自行指定特定的potential(.cell file內指定)，在做搜尋的時候可於(.param)調整E-cut增加精確性的結構搜尋。
先前做了C_Si之間的結構搜尋，在分析時有注意到一件事情，AIRSS認定的space group與MS內的symmetry後找的space group上有幾個會有不同。
  舉例:
  AIRSS ► MS
  C2/m ► R-3M
  P63/mmc ► P1
  P1 or P-1 ► C2/m
  R-3M ► PM-3M
  C2/m ► I41/AMD
所以之後再做判斷時，可能要再多加確認，最嚴謹一點的方式是要在MS內做完幾何結構最佳化的計算再來看是最準確的。

由於AIRSS功能也可以做到讓其原子小幅度的震動，使其落到更低的亞穩態。(降低依些奇怪的結構出現)，而要做統計分析時要把計算的數量提高，才會比較精確(100甚至1000)。

---
# 資料提供
1. AIRSS內的關鍵字表(這些都可以從Cambridge上下載的到)
[AIRSS_cheat_sheet](https://drive.google.com/file/d/11EfzxEjXYz4pquAa2XzxERPkF1bAVEIt/view?usp=sharing)
2. AIRSS 0.9版 內提供的Example (我把他抓出來)
[AIRSS_Example](https://drive.google.com/file/d/1tqhWNFsX3ahki03RlCzgDEs_JYhEQUZU/view?usp=sharing)

# Code內容寫的關鍵字註釋
```
VARVOL ► Determine the variable target volume
OVERLAP ► What overlap to tolerate - using hard-sphere potentials
SLACK ► Fractional slack on the bonding
COMPACT ► Compact the final cell? Not if there is any symmetry, as the operators are not currently converted
Not if the cell is supposed to be fixed in any way, not if a cluster

NUM=2 為 兩個原子
POSAMP=3 代表最多可移動為 3 angstrom
MINSEP=0.75 ensured 原子分子 不會被 generated
```
---
# space group
https://en.wikipedia.org/wiki/Space_group

# cellsym
http://www.check2xsf.org.uk/cellsym.html

## Spglib
http://atztogo.github.io/spglib/

---
Less than 1% of crystals in most databases are P1

另一款預測結構程式
http://uspex-team.org/en/

Crystal structure prediction = CSP (?)
Potential energy surfaces = PEs (?)

http://doye.chem.ox.ac.uk/jon/structures/LJ/tables.150.html

---
# 討論與問題
1. 內文有錯字 if ► is (1.6)We start with a 55 atom icosahedral (point group Ih) cluster, centred on the origin. On generating the random structure this cluster if(應該是is) neither shifted (#POSAMP=0) nor rotated (#ANGAMP=0). The "# Ih" label is identical for all the 55 atoms of the cluster. The 56th atom is randomly located in a shell of outer radius 6 (#POSAMP=6) and inner radius 5 (#POSAMP=5). Structures in which any atoms are closer than 1.5 are rejected.
2. input file內制定的cluster是否與在command line時 下定的 -cluster 有何不同?
  host:1.6 cjp10$ airss.pl -pp3 -cluster -max 10 -seed Al
3. 另外，在input file內的cluster是否有順序之分?
  MINSEP=1.5
  CLUSTER
  POSAMP=0
  ANGAMP=0
  是否使用cluster之後 posamp angamp都會受cluster影響?
4. cluster 使用之後 無週期性邊界條件的問題
5. .pp程式說明檔在哪? 另外，特別注意 #Beta是甚麼意思?
6. 學習: In the above run the known ground state structure of LJ56 is located after 10 attempts.
7. (1.7)中， Q: 為什麼The shape of the unit cell is not optimised during the relaxation. 還需要 #FIX ?
  FIX_ALL_CELL : true A: 一個是在隨機搜尋時 固定 一個是在CASTEP計算時 固定
8. 1.7 HCP找出兩種結構 命中率 10個 只有一種結構(屬於能量最低) 使用MS做一個slab(小的) 然後做兩組 看淺的洞 還是 深的洞 能量高? (吸附位置) 最低能量的數量(命中率)問題 ► 波茲曼分布 ► 活化能 ► 導致在結構搜尋時，尋找能
量的谷底數
9. SUPERCELL n or a b c or ax ay az bx by bz cx cy cz the full matrix (9 numbers) 時 ax ay az bx by bz cx cy cz 任
給整數 保證一定是超晶包嗎?
---
