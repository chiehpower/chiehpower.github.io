---
title: Xmgrace 基礎篇
date: 2017-10-05 13:52:33
tags: [ Xmgrace , Linux ]
categories: Linux
photos:
- "https://lh3.googleusercontent.com/Cg4l94uA5ug9kBNhVghybnSfDEwmJgX7fxbFoAP3J3shFAaT7Ihk97omQgYzse1f-REf7fpgf3aGnnb6PoIiIE5YxkF3a60b31Cc7Lv6D1fchwtWnW_eWpL2BkEWNQaH9j-8ON2U51r8diD_5csUHAZu4W8Px95nqJv65mi6CJw1SNv7xXpOvka_Q5_NVoT762QuNVsJuU9Qf-UjceCaevHLgQ2BXCmFkkLHhF5zhGtRcbQWQ0_klTONe8lylnXUjPCje-1-rZuyg2EPFB9AiQDMLaMR_kuNdDVazCeq2Yoit4MKiFODnmOCC-m593n82uKdE29GS28ARCR71rdw-XtgZtufWHFSUqwXObPWKpfbfADvW5x5DPKDWzc_OXLENfRzNmlNaSWO7um3_uhTuptJod7HZ2Ocu3R8Y3YhQu34ubX1Kz0ARXGNZMc1nhapl_FsUhKORW5AnrxmtLodgTeb8KOBo2eb7c0LoIljFlWxPxOemjZJAiMcZCm3ducjFno6rfiaFacHSiKMgIXLjtNg5Xq2rR7O_Eoi2ZvUSj8M74p9vC4jhIXCX5U4nXW3KdPRiQFd3xt7MN-UQysY5QK7TzynO-PBLBM9FDnaIVo21EYSVcoP0_Gc1KUPfgS_RPFMqnZPb7wcJXsU-SobTwKxuRKd_4BE_uDlo4zPngSeEUagzpynNmUJK62zaVQXl16mX3PTG5XpLTKQYFNfoLAtP_HYxvQEv4AzuqLYn7BDkTyyHw=w2162-h1218-no"
---
**本篇介紹 教學操作Xmgrace基本流程**
>前言:
Xmgrace是一個免費的數據處理軟體，同時也是非常古老的一個軟體，現在大多數的人都改使用 Origin 這種先進的軟體，也比較人性化一點...
(老實說xmgrace真的很麻煩阿!不人性QAQ)
但是越是麻煩，

<!--more-->

以下只是個人基本初階的流程(也沒有實用教學)
想要看進階一點的用法(?)可以到我寫的另一篇「[進階篇](https://chiehpower.github.io/2017/11/25/xmgrace-advanced/)」

# 啟動Xmgrace之登入步驟操作教學

```
ssh -Y (帳號)@(ip)
```
輸入密碼，登入伺服器之後
輸入xmgrace即可開啟xmgrace

---
# 匯入數據
*[前提]由於本人是要做CHI2的數據繪圖，因此以下是拿本實驗室所開發的執行檔工具所計算出結果檔案來做說明*

1. 首先，用NewSHG算出來的檔案名子會是
```
xxx(檔名)\_Optics.shg_br_ve(或者vh，此為單位)\_xxx(數字即為方向)
```
2. 打開xmgrace時，於 *data* 的地方點開，*import* 開啟上述的那個檔案(雙擊)，
  即可於畫面上呈現出最原始的數據圖。

---
# 儲存數據
儲存的時候，可以到 *print as* 的地方，副檔名改為 *jpg* 的格式
輸出到你想要的地方，再到 *print* 那個地方做輸出，照片就直接匯出到指定的位置出現


>初學者想要先入門建議可以先從 [**倫大**](http://xination.pixnet.net/blog/post/27714581-a-brief-introduction-to-xmgrace-and-its-demo) 網站先學簡單的(倫大有影片可看)
至於其他功能再慢慢摸索~
倫大裡面也有講到可以先看 *help* 裡面，看看xmgrace可以做到怎麼樣的地步?
簡單說就是有很多模板啦! 可以拿來使用!
先了解Xmgrace他的極限、他的功能之後，當你有需要再來學你需要的部分。

---
# Xmgrace的數據操控語法

Control code | Description
:---:|:---
\f{x} | switch to font named "x"
\f{n} | switch to font number n
\f{}  | return to original font
\R{x} | switch to color named "x"
\R{n} | switch to color number n
\R{}  | return to original color
\\#{x} |treat "x" (must be of even length) as list of hexadecimal char codes
\t{xx xy yx yy} | apply transformation matrix
\t{}  | reset transformation matrix
\z{x} | zoom x times
\z{}|return to original zoom
\r{x}|rotate by x degrees
\l{x}|slant by factor x
\v{x}|shift vertically by x
\v{}|return to unshifted baseline
\V{x}|shift baseline by x
\V{}|reset baseline
\h{x}|horizontal shift by x
\n|new line
\u|begin underline
\U|stop underline
\o|begin overline
\O|stop overline
\Fk|enable kerning
\FK|disable kerning
\Fl|enable ligatures
\FL|disable ligatures
\m{n}|mark current position as n
\M{n}|return to saved position n
\dl|LtoR substring direction
\dr|RtoL substring direction
\dL|LtoR text advancing
\dR|RtoL text advancing
\x|switch to Symbol font (same as \f{Symbol})
\+|increase size (same as \z{1.19} ; 1.19 = sqrt(sqrt(2)))
\-|decrease size (same as \z{0.84} ; 0.84 = 1/sqrt(sqrt(2)))
\s|begin subscripting (same as \v{-0.4}\z{0.71})
\S|begin superscripting (same as \v{0.6}\z{0.71})
\T{xx xy yx yy}|same as \t{}\t{xx xy yx yy}
\Z{x}|absolute zoom x times (same as \z{}\z{x})
\q|make font oblique (same as \l{0.25})
\Q|undo oblique (same as \l{-0.25})
\N|return to normal style (same as \v{}\t{})
\\|print \
\n|switch to font number n (0-9) (deprecated)
\c|begin using upper 128 characters of set (deprecated)
\C|stop using upper 128 characters of set (deprecated)

---
# 常用的指令[個人常用]

Control code | Description
:---:|:---
\n|可以於標題換行
\N|可以讓上標(次方)跑下來
\x|可以呈現希臘字
\c|chi
\S|上標(次方)
\s|下標
\f{}|還原字體
\f{symbol}|

>ex.
上標與下標同時存在語法(先小m到大M)
```
\xc\m{0}\s\f{}VE\N\M{0}\S(2)
```
