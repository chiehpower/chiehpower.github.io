---
title: Jmol-操作介紹 [基礎篇]
date: 2017-11-08 21:21:13
tags: [ Jmol , M.S. , CASTEP ]
categories: Program
description: <center> Jmol聲子振動的簡易操作流程。 </center>
photos:
- "https://lh3.googleusercontent.com/HWK216K6J6e0fVN3EweQYUh_fOJE95Dpu-E1M3M6OHN5OAJlZNby-HkuizJXWBpu2CEiNlxzAO6yhyN_W7a_WufjUSO8Ab44PqoUnuMWK7rNhPuObv9__ilYF76byhtIV53a-GIMpV2Y3VMRAT61rWtlcFMlbPGChWHT-BoQEPWQ8SUUT_lJ-SmokOvUi8MqwKy1_eephoJjK5zrvGbowuIBZzA5_ePs8JckzuO4cwBl6CF0Tl_NnVVjtG1MRNBbn9fMy2yp4BC9rBYJyMPin6x-J1PKrCjGkP22G3pFzzGIfgIHpkAcnlforlFXQeeKLE6nOiYZf4TpfHhz7SqD7zhA09oR5gIiL-cPGudjwVTyGC9W0D2CidpC71dAU5j03kLXfGG0Elf8M98Atje4kp7JQTcyJKmvzZpFXYSCZeX94X3os5x026wtWXI78zIsdCCCJHhq12cFYOOECad0Lv8LBvmkrv5hCRloypsFpIrhpMLiqOICeqDkBXhL64DRaVhMsto8399dXTjUahvkKxowEC1aEcmOJJLfeYfhtygSRyVMlKwpVkmXqTzbmoWv3YJ3LDBpNQmFehIgCdRUEFxbAMsTly11maCbp9441ApQUW0iBXJDYcZaHRi9OmoHveYTtK2Z0bGpYCXruMNXCCHE-UB4h38vKXVXR75xTpv1DTwfXSYdWH_HNZeUAQgA0Uy-iAhelnNI812aIRTRUM2ObQ=w2160-h1216-no"
---
**聲明: 本流程是學習於 李明憲教授所著-計算材料 為個人紀錄方便日後複習所用。**

# 取得軟體包
請先到Jmol網站上下載軟體包(檔案不大)
[Jmol官方網站](http://jmol.sourceforge.net/)
(本人操作14.14.1版本)

---
# 語言切換
Jmol有中文化界面，可以選擇使用中文語言
操作流程:
於中心黑色3D介面區右鍵點開了，倒數第二個可以看到語言，點入後選擇 zh-TW (繁體中文)

---
# 準備input file
請先於Material Studio內做好聲子計算(Phonon dispersion)，請先確認是否有(.phonon檔)

---
# 簡易的操作流程視頻
<div style="position:relative;height:0;padding-bottom:56.25%"><iframe src="https://www.youtube.com/embed/6blbtIsCeXM?ecver=2" width="640" height="360" frameborder="0" gesture="media" style="position:absolute;width:100%;height:100%;left:0" allowfullscreen></iframe></div>

---
# 需要更改的參數內容
請於檔案路徑之後，";"分號之前，自行補上以下這句話
```
{2 2 2} SUPERCELL {2 2 1} filter "q=(0 0 0)"
```
>前面項是以超晶包為基礎的整數倍做為調整
中間項(超晶包)是調整晶包內的大小
最後項是調整要觀看的q點位置

最後補上整個段落的內容做為例子提供給各位參考
```
zap; load SYNC "E:/JMOL/JMOL/Jmol-14.14.1-binary/graphene CASTEP Energy/graphene_PhonDisp.phonon"{2 2 2} SUPERCELL {2 2 1} filter "q=(0 0 0)";if (true && _loadScript == '' && defaultLoadScript == '' && _filetype == 'Pdb') {if ({(protein or nucleic)&*/1.1} && {*/1.1}[1].groupindex != {*/1.1}[0].groupindex){select protein or nucleic;cartoons only;}if ({visible && cartoons > 0}){color structure}else{wireframe -0.1};if (!{visible}){spacefill 23%};select *}
```
