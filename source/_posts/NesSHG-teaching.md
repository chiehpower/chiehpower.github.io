---
title: NewSHG流程教學
date: 2017-10-05 13:45:34
tags: [ NewSHG , CASTEP , M.S.]
categories: Linux
password: teaching-newshg
description: <center> 使用流程 與 注意事項。 </center>
photos:
- "https://lh3.googleusercontent.com/KKrLfHdHNMO5nxDe7x99MXMcqxU4SCqE_pvtw3ew11PX0ZEHP9ecG9D9iONCwKOI7uQbR_KOOFuX-p4pRVHKREtylexc-tQO-73yquDBUte3OBaJXShvB_CbRqBv-wvE2rXMQNhtI9F53ylXAFw6U7ivuyXZGF4rA5CmYHmF-UjVOn2RFUTN2wEEPUKbOgNXbG3f_YnZPxc5U4O13i7abXkzUVmrMxE7VO0wZc3br7NCfkhsmHgYVe1yt3Z3y8akIALeAUoxH3EVCYH1MOWqfLsGJvLPGxaQ7MyT6K4inj0DBECNJjbHRtg53Hx7_ClOd9VS7DSNTHlTLKoI7hHM2es5_NoyIFKBsOPFqxGmWjTePobR4HHZHXhJx-MJyUqmjxJVJCWV5tZyEoYeiAfzp6j8KauSqRVDWNO5w5bxlKnpWxcTN9_yuNS_GeHCZjqEEXNekR_y1mztSWs4M7NWhynIG7DwVlC8ksrXWudLt_mUqaDc8bf83-rl0vIosGN5vDRWcekWneTpHxwkUl72M6PFymwUT67NzLJeDqZHLAY2CuUdEgFEdyYBOmIYDqzNq1ZITgNCiMk-2GHFTXHsbA8kcUVrlyRtg4r1VijrF7VInEFFHukDcHkMs1JAjng89J7pBh5cQ7GTP1yhmdYqUgnQj0ppCVGzKIC3TF2aIYZiLwHZZRbhjH1k=w2044-h1532-no"
---

<!--more-->

*個人紀錄操作流程*
# NewSHG 使用流程教學

## 如何計算CHI2?
>影片教學如何操作NewSHG的整個操作流程。  

<iframe width="1280" height="720" src="https://www.youtube.com/embed/sJXKdD0PSy8" frameborder="0" allowfullscreen></iframe>

### 特別注意
>NewSHG支援舊版M.S.光學Optics.cst_ome檔
而較新的版本2016 2017計算出來的光學檔是 .ome_bin而非cst_ome
因此送入計算NewSHG會出現少檔案的錯誤
目前已知Version7.0是還可以正常算出cst_ome檔
-
可以看2016 2017版 光學.param檔案內是否為 spectral_task : Optics
採用spectral計算是較為精準一點 舊版是Optics
