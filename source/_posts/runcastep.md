---
title: RunCASTEP
date: 2017-10-05 13:47:47
tags: [ CASTEP , linux , M.S. ]
categories: Linux
photos:
- "https://lh3.googleusercontent.com/kRVzkYjMDcKZuN1POOu9IZ_uefIg-xMyvysNoFoEu0PeAvL-Ukh4-SFsjzokAfq49lsdDgz7T9s2mCl761ZhpSQpBlYdwfoHQUwhYRzhMhFgOqOLBDtsFpQcGk2_ytKM79_KxeVUxcJWKbTiqcXvlED_NCv2IjlNBE_uq-XZOWWw9jmFAB88c2Z14nWGqLbp4JKxWiWNWE4ejafehAI4vVgAxX0mFHW6t4DO7755OblcDOGtkA0x2-ENovqRplJceJU7EKQA5noEvzTEhUHxpeZeQWdFTiQZdem0BQ042B91rUqeRBdzkCFWE8CdVU1mFzeC7cnJgMACyIiDw2gsaIitOYaFxdMa6TnVygTRAbc6xj5luAzubktugOgyYqqGEmmC6cWYmPOiSkL1Nyw95b7eRTPUy7XvLg9xnqAPnGusjI3L_rfcpCs6LvecK3mAVKoI4HH2N9lD38sAppde7bPpGQZpIzftnHW81OLqaGef52UhWFX5A9S9u1dzPcXBzC4VnCrOvyIR0Iru79GDoJWISqzO-8LFx7yBh-JI87le-KZLkbbUyAmW-1vRBCquen1yn9tcmmU1H9Hj26PEahbZyHR6qLdesHxy8GKRtoP_R-2A-B2wS2vVS15zUa64P_JjWSeU_Srz2utizjbm0UOElMUoqD-SDqigAuZca0tGrCQ2KY1whPT-=w2724-h1534-no"
---
# 文字模式計算CASTEP

*由於是紀錄操作流程，過程寫的路徑是本人電腦中的路徑，不保證每台電腦完全相同*

> <前提>
若要從伺服器上直接做CASTEP的運算的話，
請至以下路徑紀錄你的RunCASTEP.sh的檔案存放位置

```
/home/phy/Accelrys/MS55/MaterialsStudio55/etc/CASTEP/bin/RunCASTEP.sh -np [CPU數量] [SCF檔名] [光學檔名]
```

<!--more-->
---
# 這裡單純先寫下我的紀錄算urea單分子的做法
1. 先進入你的jobs檔案下
  真正在跑的時候需要 **四個檔案** ，所以先取出準備好
   1. *.cell* 檔
   2. *\_Optics.check* (若沒有要重算SCF，就只需要拿 *Optics.check* 檔案)
   3. *.param*
   4. *.recpot* (贗勢pseudopotential)
2. 接著進入光學的 **.cell** 檔內，啟動vi於cell檔內做修改光學的 **k-point** 動作
3. 然後找到 **%BLOCK OPTICS_KPOINT_LIST** 與 **%ENDBLOCK OPTICS_KPOINT_LIST**
  之間可以發現有 **三個0**
>前面三個代表abc方向向量，後面的1代表權種

4. 把前面三個0改成 0.25
5. 然後esc 在輸入:wq
> (w代表儲存 q代表離開 )

6. 輸入
```
/home/phy/Accelrys/MS55/MaterialsStudio55/etc/CASTEP/bin/RunCASTEP.sh -np 8 urea.....\_Optics
```
>(特此說明)因為我只要重算optics的部分，
因此前面檔名(SCF計算用的) 我就不放 但需要提供.check檔，不然無法跳越

**運算機制為前面SCF先算完後產生一個.check檔案提供給後面做光學運算**
而我採用8個cpu做運算。

*每個伺服器安裝地方所放的runcastep.sh檔位置可能不同，必須事先確認一下*
以上為一整個流程。
