---
title: Hexo with the Jupyter notebook
description: <center> 在Hexo上面展示Jupyter檔案內容。</center>
photos:
  - 'https://lh3.googleusercontent.com/o8VeTA51bEaOhG3q5fm5kqlV7Uuf8vKUXPff8vHousbCwngxzK1QsLDbHhcalSv9vJuGlkRGF-4GB-36gam7UGRkIyK5hsZlwJeq9U80B8RG4t6T5itb6jgUSC_X57mVnF2A8IktgVp_SsUJyK_G6g4sT3xVGzzPzrDm1ZDvhLsacqIjLc-fjOZlu0gn8cj232RpvwTMibHtkKm9pi25Y-C6_O95Q3NqTiUPH1ofsm-ds31eLi1PjQtn1qFF3DXc3lXX_tbY326I53XvH0BboaD_c_BrhpteKGwcSFwFVgHSCy4pXkab0s2GHU33rAUoDdhVAIHVbC6JM6pa1z68fQnP6cEt_ox5i6P7l2qIFf-uAKhp6kn1YnG-NAzW2K1UHw_0DzAD2GU5xoAldWunr4zA8f1_W6pcZq7Sz-oaCMZiU8h165qyj9yDR3CqSkZzK05u-Z6jiw05W_zO10V365XfhajG8qpyo4qm4opTB5LPbi1ffK-y48J3-huvpRSYje_VC3oyvOTtLPTydglt6FCs8p1pQZd0sCPK48_9mO4S1SvqooLJQYBn1_FSQ_FhBG5L5_WiY0fONEGH8PmreBz7CuwkHmJICpemKM5WDhQAXFhhTGXSbyuoWCX2YrguGMDLw3HPUwLrO5GzsLO3-UR_a1ZLOHzQnTdL4uez3ZDLUuVNpyQgo7YxZcfozWoE7v-dndi2l88Ej1PddVc=w2208-h1242-no'
date: 2019-01-20 13:19:10
tags: [Jupyter notebook, ipynb, hexo, Notes, Program]
categories: Program
password:
---
作為一個程序員，一定會用到Jupyter Notebook的，非常好用，但是之前已經想很久要把檔案放上來可以展示，與blog結合。
# Steps
主要步驟簡單：
## 第一步 安裝 hexo-jupyter-notebook
進入根目錄
```
npm install hexo-jupyter-notebook --save
```

## 第二步 安裝兩個 pandoc 和 nbconvert
不過如果有安裝Anaconda的話基本上都有

## 第三步 打開配置裡面的選項

根目錄下的 \_config.yml
把裡面的 post_asset_folder改為true

## 第四步 創建檔案夾，存放ipybn用的檔案夾
在_posts該目錄下創新的檔案夾 取名為jupyter-demo文件夾，專門放ipynb檔案的

## 第五步 插入語法
在需要展示的地方插入語法
```
<script src="http://code.jquery.com/jquery-2.0.0.js"></script>
{% asset_jupyter /Users/chiehpower/anaconda3/bin/python3.7 ../jupyter-demo/Lasso.ipynb %}
```
意義是
```
{% asset_jupyter python_path jupyter_file_name %}
```
注意：jupyter_file_name不可以用絕對路徑。

我因為有安裝過anaconda3所以直接使用裡面的python
路徑是
```
/Users/chiehpower/anaconda3/lib/python3.7
```
(chiehpower是我的使用者名稱)

# Frame
雖然在hexo s時，可以完整呈現整個檔案，但如果deploy之後，卻會被限制住。
找到位置：`/Users/chiehpower/blog/blog_MacBackup/node_modules/hexo-jupyter-notebook/main.py`
裡面更改高度為：
```
<iframe id='ipynb'   marginheight="0" frameborder="0" width='924px' height='680px' srcdoc="%s"  style="scrolling:no;">
</iframe>
```
- 參考文章：[在hexo中写的文章支持jupyter-notebook显示](http://huanyouchen.github.io/2018/05/30/hexo-support-jupyter-notebook-in-blog/)

# 展示
以下只是隨意找一個檔案來做範例ＸＤ
請別管內容 😉
<script src="http://code.jquery.com/jquery-2.0.0.js"></script>
{% asset_jupyter /Users/chiehpower/anaconda3/bin/python3.7 ../jupyter-demo/test.ipynb %}

# Reference

- [在hexo中写的文章支持jupyter-notebook显示](http://huanyouchen.github.io/2018/05/30/hexo-support-jupyter-notebook-in-blog/)
- [hexo-jupyter-notebook](https://www.npmjs.com/package/hexo-jupyter-notebook)
