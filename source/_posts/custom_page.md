---
title: How to create customized pages？
description: <center> 針對Hexo的Next添加客製化分頁。非常實用！！ </center>
photos:
  - 'https://lh3.googleusercontent.com/o5ynXVceB9w95Tnd4GeSa0jOFxf4-61FpjCk_l3LpaYW7KmCmbBRdiDtTrZGPevU7i7I6LTxo1xmroJWyuXPaMKha2hQfGMuqyORamN90BWCbSS7F8jPkPsh8F_QwJEoplGQnb0Qmoxe6d6go4WteaLxZ4SAjAds9zcdRFpth3iYlZMSxYCaMVKclEXke7_40oh2m5Csqh-CqNCcJ2iDyw8ecIIwf71DrLI2cZxgBIPq0dnp3xX2maHm-A9f_D_oc1C_Lymuq5SFA6tywdmQWc0GzU8-ZBeA4HFa_ML6QJa24h94PuO9iGHiBiWIVCdQPDyikKtpw4Cr7ol_6FBpVVoY2q1fpOsM-NytiDAxbAx66Jm59Zw5cJC14BwrZqCyqlcvtkNDwZrO76R_MJr-HInuN1rZ_m8Qh2qk9RHS8XyuJdG_EMXZ1BZpkagNPsYdsdsSrtY_aN1koUUeQDCF5GZiLUemrjZga47RftEHQeHPzL1FwXRHHRld_Wg1GjQsJjaejib-fFgFu3KMPx2yu6IVES_frFT99VahOWxic7oCkFuyqdWsuEyu2xKbS_LbRlG68T3m-ryf3FeG5v4lYaZlVEWVBTW5PmjSlwPNaJvRzvq5lyKONsyPyZZvRoNwI0gebx3lRDiuKAmmX-O4KZNhSEbN5srPES_mKkrjog75w84JIF9r9vuI0yZPh5yZRnwcBefgcrEL__roCu57OoXrtoIBCLnxK3cKYbFSlgIOM0hPpw=w1262-h946-no'
date: 2019-12-19 19:59:08
tags: [Notes, customized pages, hexo, Share]
categories: Notes
password:
---
>封面圖是使用iPhone 11 Pro於信義101附近採0.5倍焦拍攝。

我個人認為此篇的內容，可謂是相當有價值，這方面的資訊在網路上有點少，花了一點時間才解決，當然需要的人可能不多。
因此也這坑走了很久，我也為此成功而非常興奮開心啊！

# 正題
如何在Hexo的Next主題上，放置自己的東西、文章、Html、子分頁。

這部分細分兩個部分：
1. 想要在主目錄上的文章裡面，放置子文章、子分頁。
2. 想要在主目錄上的文章裡面，放置Html、自己的檔案。

第一點和第二點的差別在於，是否使用原生主題的渲染來做文章，OK 給個情境。
首先，有時候想要在此篇文章裡面在連結到子文章，但是我不想要讓這子文章顯露到主頁上的文章列表上，一定要從這篇文章裡面連結過去。進去之後繼續寫，而這個版面樣式跟父文章是一樣的。

第二就是，例如你想要放一下自己的自製履歷啦，或者其他你已經有現成的pdf或網頁檔(.html)等等的，就非常需要。因為這類似說做一個本地連結過去而已。

---
# 第一部分

如果想要放自己的東西在子分頁裡面 直接建立空白html就可以。
<!-- [HTML file test](../custom_page/test.html)
[Md file test](../custom_page//2019/12/19/test_md.md) -->
這部分暫時留著，之後繼續完成。

---
# 第二部分
這部分我覺得比較重要，因為我的page裡面的presentation，有我想要放的html檔案，先前也有想要放過履歷，都需要這個功能。
所以這部分我先拿我presentation這區來做範例。

首先感謝[這篇](https://www.zhihu.com/question/56677837)給的靈感，我參考了這篇的方法。

首先，因為我是放在page，所以需要先`hexo new page <name>`，接著在`\source\`資料夾下創建一個新的資料夾，裡面放你要的文件，這部分我是放我的html就好。
緊接著，去`根目錄`(不是主題下的)`_config.yml`裡面找到`skip_render`這區，在後放加入你的檔案位置。
有一點要說一下就是當你的東西放到source裡面他都會部署到public，所以理論上都是會採用主題裡的渲染，我們因此要把他給屏蔽掉。

For example:
我的新資料夾名為`demo`。

```
skip_render:
  - 'demo/*.html'
```

最後，就是在page裡面或者你一般的文章裡面，建立連結。
For example:

```
- [TensorRT](../demo/slides-tensorrt.html)
```

這裡要特別注意路徑，由於我是在Page裡面做輸入，所以要先回到上一層，在進去demo裡面的該html檔案。
如果你是在_post裡面，那就要在依照你放置的檔案做`相對路徑`的調整。記得要是`相對路徑`！！


以上！
