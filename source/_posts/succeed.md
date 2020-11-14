---
title: Succeed & Record
date: 2017-10-04 14:12:54
tags: Mood
categories: Mood
photos:
- "https://lh3.googleusercontent.com/nCcX4V3SjBqV3rWyouxm-51A1Pq14rSvB0jrFlWRPsykYxo9CDVjdZe74KbwPOowMh4juk0_DTsYzxx5rPjbSsbCpTEovpthesX6wv730p2Z5U_VObKLndbwMStmktns_nKTieF3xyalT-sFg45Jl4dAPpmJd5Vsvg-AhuMrhX_12HFXPV_FvQO8uzdJuJy3hVRZxrUY6GQOYW91LrmDB-RL_XfVsRLv-q4P7uUL3-odhmHyWWCiX9tGFWo11HxK9p9oZTFMMu6oXmcmcGyLMxCIm6mGMolw7f5TBHyCE3sxjXU6CZLqcJ3r9itq5I58_ndsA131c3bzTFqu8F5NwGa_vUZiVcftiakXYOCuHdT3dfS7St9sG1C0aeaIe0jgQzcF8jzjX5bBjpqxTEM5_paOjG0eySxGAKtPe_5rjdhPBa9Kj5lHJ_MPEfi9rVbbgqN9TRleQ5LT0aj31S3yOnWExQ5NWuFei8rC7JkvaJg7F3ZO9iZQRSG_fNl4BNPxdcEkW47o4AUbwZ2xMSUBt3HUvyPXTUo-sR4cwyh1DAzAfWuS0FF0P-r6dycwkHv9RBz6VVRi7QPpHU6ycxm1pKUHSz_tiK9lc1t_z1_Yz9WN72ymB6qaslkrGNHgmJlIT_Vv1hg1wsrXev1YdQb_L0Bw9zhjnwZnrtPE6HJd1ZIzPGSPbbaAbMR-=w1561-h879-no"
---

# 2017年10月4日 成功架設Blog!

## Blog設立
非常開心終於...初步創立，
研究了一個禮拜...不斷的重複砍掉、重裝，
1. 其中有卡在站點配置裡的root(網上註解非常難理解阿!應該說定義不夠清楚!?)
  最後才發現原來是在hexo init時的地方錯誤，
  **應該是在git clone之後創一個新的blog資料夾目錄底下hexo init!!**
  真的是該死~~
  <!--more-->
2. 還卡過綁定的問題，因為要做一個連結，
  客戶端資料夾綁定於pages上，到底是處決於哪一個指令??
  ```
  git remote add origin (https://...)
  ```
  每次新增完一個資料，
  就得完成標配流程，
  ```
  git add .
  hexo clean
  hexo s                #查看一下
  hexo g
  hexo d
  git commit -m '(註解)' #自行找時機commit
  ```
3. 更換themes卡住!
  一開始landscape themes 是OK，
  一旦更換網站就壞了...改回去也沒用...
  這問題隨著改變了第一點遇到的問題之後就迎刃而解了!

---
## 可能遇到的問題
  1. 如果碰到一開始無法hexo d時，先安裝這個
  ```
  npm install hexo-deployer-git --save
  ```
  在重新hexo d就可以解決了!
  2. 假如你遇到port重複使用問題 可以使用指定port方式
  ```
  hexo s -p 5000(自行輸入)        
  ```
  換一個port，當然你關掉終端器，重開也就會恢復了啦~

---
## 貴人相助

最後，
**非常感謝 Lu大的協助** 沒有他熱心的幫忙，可能我還在自己閉門造車...
> <https://alumincan.github.io/>

---
# 後續研究的項目
## MathJax
> [MathJax](https://www.mathjax.org/#features) 使用於數學公式非常的便利
這個列為之後研究的主題之一

## 網域
>是否能把網站搬到自己的linux伺服器空間上架設?
以及能夠不依賴pages?

---
# 如何於不同電腦上維護Blog?
>要先來嘮叨一下，許多網站(有台灣人也有大陸人)在的闡述上，其實容易因為名詞的定義沒有事先講清楚，當然也許是我自己的問題啦XD 就會造成在自學上的一些小困擾。舉例 在講述Branch教學時，常會看到什麼master分支，一開始我還想說master就是主要支線為什麼又是分支? OK 原來是再說這個建立兩個分支裡的其中一個分支:master，所以稱為master分支。(是沒有不好，但為什麼不直接說master就好!!); 還有就是在 git remote add origin (LINK) 指令中的origin其實只是一個代號，自己可以隨意取一個名子然後加上(LINK)，讓程式知道他是誰就好。這些都是許多website不會註明清楚的，也是偶然間找到才知道...(淚

我相信許多Bloger總有一天會遇到需要面對這個情況 ► *如何在不同電腦上寫文章?*
1. 這個問題其實有幾個方式可以解決，而最初我想到的方法其實是最簡單也是最好的方式，初始架設的Blog就在Driver資料夾裡(ex Google Driver 之類)，而每次更新了blog內的資料後，driver就會自動幫你上傳更新雲端上的資料，在不同的電腦使用前先更新一下雲端的東西，接著就可以直接使用不用擔心有資料新舊的問題，也不用擔心把資料backup在Github這種公開平台上會有不小心密碼外洩的問題。
2. 另外，在各個網站上可以查到許多Hexoer在分享自己的經驗都會用到在同個倉庫建立Branch利用這個的功能來達到備份，而少部分的人則會使用另個方式 ► 建立另一個倉庫來做備份。 (不過都要小心讓自己的ssh或其他的key外流的風險，畢竟使用免費的Github就是在平台上公開自己的文件)

## [流程概念]
Github上有兩個倉庫，一個是用來部屬(deploy)倉庫(也就是架設部落格放的倉庫)，一個是用來備份用的。
然後每次要寫文章之前或者做Blog上的更改修改，就先從Github的備份倉庫上pull下來，改完之後deploy到部屬倉庫，最後收工時，在push整個文件(記得要先刪去/themes/.git的資料夾)到Github備份用的倉庫。

以上就是整個操作概念。

## [重要的注意事項]
1. 要在非初始架設blog的電腦上運行維護，要做的前置作業環境一樣要架設好(Node.js、git、hexo)，也可以先安裝好會使用的軟體(Atom)
2. /themes/.git 的檔案夾刪除並且要add所有資料夾以及commit完後，才能push
3. 一樣要設定
```
$git remote add origin ~   
$git remote add (backup_name) ~
也要設定
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
4. 要先去設定出新電腦的ssh-key，去github setting設定
5. 切記不要在新電腦新環境下使用 hexo init 指令

大概就是這些! (若有想到新的再補充)

---
# 設定密碼

```
themes ► next ► layout ► \_partials ► head.swig
```
文章: (https://blog.paddings.cn/2016/12/01/blog/hexo-password/)
密碼: password

---
# [Facebook 分享按鈕](https://developers.facebook.com/docs/plugins/share-button)
步驟 (網站上的步驟內容)
1. 選擇網址或網頁 ► 挑選要分享的網站或 Facebook 粉絲專頁的網址。
2. 程式碼配置器 ► 將網址貼至程式碼配置器，然後調整「分享」按鈕的 layout（版面）。點擊 Get Code（取得程式碼）按鈕，產生您的「分享」按鈕程式碼。
3. 複製並貼上 HTML 程式碼片段 ► 複製該程式碼片段，然後貼至目標網站的 HTML。

---
# [增加版權聲明](http://www.crocutax.com/2017/05/20/Hexo%E6%8C%81%E7%BB%AD%E4%BC%98%E5%8C%96-%E5%9C%A8%E6%96%87%E7%AB%A0%E5%B0%BE%E9%83%A8%E6%B7%BB%E5%8A%A0%E7%89%88%E6%9D%83%E5%A3%B0%E6%98%8E%E4%BF%A1%E6%81%AF/)
如果不使用Next內建的版權聲明，那就可以使用這個方式。
這個方式使用前請不用開啟原主題所提供的功能(依舊保持:false)。
步驟(參考文章內的流程):
1. 到 themes\next\layout\_macro\post.swig 文件裡，找到 <footer class="post-footer">地方，在下方輸入
```
{# 版權聲明節點 #}
<div>
 {% if not is_index %}
 <ul class="post-copyright">
    <li class="post-copyright-link">
     <strong>本文作者：</strong>
     <a href="/" title="歡迎訪問 {{ theme.author }} 的個人博客">{{ theme.author }}</a>
   </li>

   <li class="post-copyright-link">
     <strong>本文標題：</strong>
     <a href="{{ url_for(post.permalink) }}" title="{{ post.title }}">{{ post.title }}</a>
   </li>

   <li class="post-copyright-link">
     <strong>本文鏈結：</strong>
     <a href="{{ url_for(post.permalink) }}" title="{{ post.title }}">{{ post.permalink }}</a>
   </li>

   <li class="post-copyright-date">
       <strong>發布時間：</strong>{{ post.date.format("YYYY年M月D日 - HH時MM分") }}
   </li>

   <li class="post-copyright-license">
     <strong>版權聲明： </strong>
     本文由 {{theme.author}} 原創，採用 <a href="https://creativecommons.org/licenses/by-nc-sa/3.0/" rel="license" target="_blank">保留署名-非商業性使用-禁止演繹</a> </br>轉載請保留以上聲明信息！
   </li>
 </ul>
{% endif %}
</div>
```
看要什麼訊息可自由決定是否留下
2. 到themes\next\source\css\_custom\custom.styl裡面貼上Css樣式，裡面的顏色(border-left與background-color)可自由更改!
```
.post-copyright {
    margin: 2em 0 0;
    padding: 0.5em 1em;
    border-left: 3px solid #6b92b2;
    background-color: #F9F9F9;
    list-style: none;
}
```

---
# 更改文章版面的寬度

```
~\themes\next\source\css\_common\components\post\post-expand.styl
@media (max-width: 767px) {
  改成
@media (max-width: 1060px) {
```
再去
```
~\themes\next\source\css\_variables\base.styl
// Layout sizes
$main-desktop                   = 960px
$main-desktop-large             = 1200px
$content-desktop                = 700px
  改成
$main-desktop                   = 1060px
$main-desktop-large             = 1200px
$content-desktop                = 800px
```
[參考文章](http://cxjiang.top/2017/04/07/Hexo-NexT/)

---
# Google AdSense

1. 新建 AdSense 模板
```
themes/next/layout/\_custom/google_adsense.ejs
```
在 next 主題下的 layout/\_custom 文件夾下創建一個 google_adsense.ejs 文件
然後將 Google AdSense 的代碼複製到 google_adsense.ejs

2. 編輯 \_layout.swig
```
<!-- Google AdSense start -->
{% include '_custom/google_adsense.ejs' %}
<!-- Google AdSense end -->
```
根據 Google AdSense 的要求將代碼放置在 <head> 和 </head> 標記之間
[原文章](https://darrenliuwei.com/hexo-next-blog.html)

*另外，我還有在 Google AdSense 下方再貼上關於 Website Tracking的code*
Global Site Tag (gtag.js)
```
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/~~專屬自己的編碼~~"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-~貼上你專屬~~~');
</script>
```

---
# 更新 cryptiles
在 package-lock.json 裡面先搜尋到cryptiles位置，並在下方貼上新版本的語法。
For example:
```
"dependencies": {
  "cryptiles": ">=4.1.2"
}
```
(在我的檔案裡位於 578行)

---
# 轉換不同的電腦

遇到問題：網域失效
記得把CNAME檔案補回去，檔案在 根目錄/source/裡面。

## 解決訪客數問題
由於busuanzi(不蒜子)的網址更新,導致了使用Hexo Next主題時統計瀏覽數失效.
不蒜子官網:http://ibruce.info/2015/04/04/busuanzi/
解決方法:
到hexo的themes文件夾下, 進入
```
\themes\next\layout_third-party\analytics
```
打開: busuanzi-counter.swig
將src=“https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js”
修改為src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"

若有問題請直接參考官網！！！
