---
title: Weighted den teaching
date: 2017-10-05 14:14:23
tags: [ Linux , Weighted_den ]
categories: Linux
photos:
- "https://lh3.googleusercontent.com/j_iBCIPw_Kd3koMGNNcFH5ET9KUxOyGkNpidd-BuoSL4W2f1uyV2DgfjK1q2fNWQkdWThY8RoKzk56JFB5Q_uZqh3Cn3ZXc4kti8bT1WJ7Op0HtLsUEvqk1Ilmpl5RU9E-tFFNWE0DLY-DO7SHBl7nbFfOBhlHeA2xEN8GuNeGCn9nGE9rwqLHmTBxX1QlGzzezN0eLe-cbjwqnsEi34Egv0PI-nt52-j-7vXx_Y08LO4dALlfdsvEGRCROAJXSwq_3OCTv5mACJgT-RMjn4mKSqvUFXn0MkU4fLGjwCxw4Cc8HAumiL2IjC_JLDRZw0m6fSA5dIXeoBZNi7DsKV82p0BzuCyEpT_pP6pjbpFk2m0GBH_Cdy3Leaeas69DLxZI8d3qik_Wm7V9XijqPNj_wXSOJ2m7nLUk0BENJU9z8En-IGIGci8C17NWdsV12tGJlNcR_FhtLnxeT2l_tX7oTVth23N6UCR-H4t-Dw4Qgf6AHheko4ZTF-3l2Ok7u79zpdTdOtAZB-CFkOwxQfeM5berorq0JvLnzYnDcSuncdYk3pJP0LNfJuyAeQbdX4SMpv2doB9JHxwM0X7bTt1pU-Jn5XSANUuk_1cwiKI22D3MINJOlnkne27N1dLYnllOkL62ULQh49QxPImDK6EKLL_SmeJ31zq-l_talsevb83hQePgWeWCh-UKVTue6Tx75pqBv_yFCfcneYLPAD-83PckyC0eIPBIpTYaVjdtZDEagtFw=w2160-h1216-no"
---
*Weighted_den 步驟操作紀錄&教學*

> **需搭配NEW_opt的操作**

 *NEW_opt是李明憲教授實驗室開發的程式*
<!--more-->

# Pseudopotential檔放在M.S.中的位置
```
C:\Program Files (x86)\Accelrys\Materials Studio 8.0 x64 Server\share\Resources\Quantum\Castep\Potentials
```

---
# 命令檔案更改權力
```
chmod +x 檔名
```

---
# Weighted_den 事前準備
目前，我先以 *[chiral_Pb6 CASTEP GeomOpt]* 這個材料包當作教學說明
計算完成NewSHG之後，會出現以下幾種副檔名
```
1. chiral_Pb6_Optics.shg_weight_veocc
2. chiral_Pb6_Optics.shg_weight_veunocc
3. chiral_Pb6_Optics.shg_weight_vhocc
4. chiral_Pb6_Optics.shg_weight_vhunocc
```

>VE     電子
>VH     電洞
>Occ    佔據
>Unocc 未佔據態

*註解其含意*
>VE 有一個佔據態 兩個未佔據態
>VH 有兩個佔據態 一個未佔據態

所以，一般看 VE_Occ 與 VH_Unocc

我們先創造出含有 *.wden_in* 這個附檔名(自行創立)

---
# 創立.wden_in [方法]
```
vi +檔名.wden_in
EX. vi chiral_Pb6_Optics.wden_in
```
把要執行的[檔名]複製起來 (看你是要做上那四種哪一個)
之後打開 *chiral_Pb6_Optics.wden_in* 這個檔案貼上

>[舉例]
就把chiral_Pb6_Optics.shg_weight_veocc 複製貼上於vi chiral_Pb6_Optics.wden_in之內


>於vi內操作時，鍵入 "i" 代表於vi內寫入 "esc"便可以停止這個操作
":w"代表存入 ":q"代表離開

接下來 執行weighted_den這個檔案產生 *.grd* 檔

---
# 執行Weighted_den程式指令
```
./weighted_den (file_name)_Optics
EX. ./weighted_den chiral_Pb6_Optics
```
便可產生這一個 *檔名_wden.grd* 的副檔名檔案
>[舉例]
chiral_Pb6_Optics_wden.grd

如果無法執行，有一個可能就是沒有把 **potential**　放入這個檔案內
就要去M.S.裡面拿取他所需要的檔案 (路徑在最上方有紀錄)
當然，你必須先看缺甚麼potential檔案

---
# 檢測材料所需的贋勢[方法]
```
vi 檔案名_Optics.cell
EX. vi Chiral-Pb6_metal_Optics.cell
```
拉到最下面，看 *[%BLOCK SPECIES_POT]*
會說你缺甚麼的檔案
然後去電腦c曹裡面取檔案
>[路徑]
C:\Program Files (x86)\Accelrys\Materials Studio 8.0\share\Resources\Quantum\Castep\Potentials

找到你需要的檔案，並且複製放入伺服器上，與該材料同目錄下即可。

---
#最後更改 *.grd* 檔名[工收]

產生完 *.grd* 檔之後，再來把這個檔案的名子改掉，
因為每次做完都會產生 **一樣的名子** 的檔案，因此要把它改掉。

[方法]
```
mv 原本檔名 後來的黨名
EX. mv chiral_Pb6_Optics_wden.grd chiral_Pb6_Optics_vhunocc.grd
```
如此就大功告成，完整的產生出一個我們需要的 *.grd* 檔案。
當然要幾個就要重複流程幾次。
