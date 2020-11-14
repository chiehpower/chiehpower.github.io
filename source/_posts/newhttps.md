---
title: Domain name & SSL Certification
date: 2018-04-02 12:57:59
tags: [ Domain name , SSL , Https , Cloudflare , Namecheap ]
categories: Website
description: <center>這篇主要講述購買替換新的Domain name以及用最低成本的方式取得SSL證書的流程與方法。</center>
password:
photos:
   - 'https://lh3.googleusercontent.com/fluLtrmNwhceUVlyAigxXLQMXGNFF15gsXaKGTXaE1Eav9sH4c5HjElebK5ULCxKPg_DTlx42ciFV4uaObxiOYSvwW2nJZn8xVIl4oVVU6Mwr2ILZl27dfhngqDGSbVE8EgLQhuG1sGFPYMoTYea68_obeyDhZVUqWM0DiXq9iMnDT9owL6lPi6fboHTglDHuu1gE-GYOjq2mygX-gW7PJCOmg8eLmI-IwxczWWi2oZWfhnYE_MxfhViNOgAF8i-Zxd8W5dh7Mh-0jcoiQ7wpyH8vyiIaqvPokEnXcrEz16tNhL9mNUuc24LSE5GxKyG6YUfq5aU4yUxQM-sC0jWflDR3GHqWLuSKYgEYP_z3m3lEv74n6Us298RH3Wh-T9brM_3nLes-sdXQkTjCsNMRGETA3VUtI94h3mAt-PBFqOMMTz51am3LcrcRWBCZJG3a9qZIELqZvSJUEJ_CZrR9DvJNu9Q2tId4FyI2vjRtFV6GsKVJw8GoVvTFO0p4-GGq_Pdhq1P8rdsmS1dtDKKf4PvlnyUtXWvJ1DcTvaNVDQBkh0R2LJ3uC9ySnyMnWS7Mrk36QaXUaeYKr97nDST00n4HqrP0dOqUJXdRP_D9nkMFG7RNaIx9TrxO3be_g3p7nkf2YOXcN7hUIBMGl9ZWiFBCrv9q0QOE_--qbq8VfQuRovIU5mAw_amUCUDO69ixt1Pa6JUWoGKjqjS7iM65zXPcE3ERg5VisQu=w972-h548-no'
---

<!--more-->
看了一下Domain name好像不貴，不過如果是挑選頂級域名價錢就會比較硬，最後我是挑選在Namecheap上買的，一年 NT300多還好，外加贈送WhoisGuard。
由於我是把hexo部署在Github Pages上，因此他的CNAME設定有固定的位置，可以參考這篇文章 [Github Pages 自訂域名 ](https://blog.dmoon.tw/github-pages-custom-domain/)。有了新的域名之後還要替他加上個綠色鎖頭(也就是SSL證書)，但是正式的證書其實很貴(看你的規模需要多大)，而且設定過程非常複雜，因此後來當然也有人為了解決這個問題就出現了一些折衷的方式，用很低成本的方式達到目的(?)，當然啦不免多說一下就是在安全上的效果還是會有差異的。
另外，現在各大搜尋引擎其實都會對於有SSL(https)在SEO上有加分，所以也是為什麼要裝R。

---
# 更換Domain name
## Namecheap上設定
```
進去Namecheap之後
Domain list ► Advanced DNS ► 增加 Type
A ► yoursite.com ► 192.30.252.153
A ► yoursite.com ► 192.30.252.154
CNAME ► www  ► yoursite.github.io
```
## Blog上設定
緊接著，到你的 \_config.yml 裡面的url更改新的 yoursite.com
以及到你的website Github Pages的倉庫裡setting裡面，有一區[GitHub Pages]設定你的新域名。
基本上這樣就完成了設定。
最後還要在yourname.github.io的根目錄下添加CNAME，在Hexo根目錄裡的source文件下創一個名為CNAME的文件，注意這個文件是沒有附檔名的(千萬不要設成.txt文本文件)，內容就輸入你的新域名 ex. chiehpower.com 這樣就可以儲存了。

但是 Blog 最好要加上 SSL證書(https) 比較好(不論是趨勢與安全)，想說在Namecheap上一起買服務，結果買了之後發現不能用...(這中間有點過程，還跟客服搞了一番)，但不得不說這家公司真的優，而且態度很好又高效率，主動詢問是否要退款。我很喜歡他們提供的服務，但他們回應 "Custom domains hosted within the Github Pages cannot use third-party certificates, according to their rules."，結論就是，github不接受第三方的證書，我最後只好退款他們建議我使用Cloudflare(網路上也大多都是建議用這種)，因此後來才轉戰CloudFlare的服務。

---
# SSL Certification
## Cloudflare
Cloudflare的原理網站上有許多介紹就不多講，可以參考這篇的文章[Github Pages 免費 ssl 設定](https://blog.dmoon.tw/github-pages-with-free-ssl/)
在CloudFlare上主要設定有三個地方吧
  1. DNS
  2. Crypto
  3. Page Rules

另外就是還要回去設定Namecheap上更改Nameservers設定，把Namecheap basic DNS 改成 Custom DNS，而這裡面是直接複製貼上CF上給的位置即可(更改之後要等待時間)。  
PS 要回去看一下你的website Github Pages的倉庫裡setting裡面，有一區[GitHub Pages]設定是否有跑掉(如果跑掉在設定回去即可)。

## 強制跳轉設定
設定完成Cloudflare之後，於自己的Blog內檔案中加入強制跳轉機制。
  第一步驟:
  ```
  _config.yml中加入:
    url: https://www.yoursite.com   # with the https protocol
    enforce_ssl: www.yoursite.com   # without any protocol
  ```
  [參考網址](https://sheharyar.me/blog/free-ssl-for-github-pages-with-custom-domains/)

  第二步驟:
  ```
  Themes ► Next ► layout ► _layout.swig ► <head>中加入
  <script type="text/javascript">
      var host = "yoursite.com";
      if ((host == window.location.host) && (window.location.protocol != "https:"))
          window.location.protocol = "https";
  </script>
  ```
  [參考網址](https://g2ex.github.io/2015/10/14/Hexo-with-SSL-Hosted-on-Github-Page/)

最後重新deploy一下就可以了。

>Referecnce: 圖片來自Google
