---
title: Mac OS × Terminal Colour
description: <center> Simple way to adjust the terminal colour on MAC OS. </center>
photos:
  - 'https://lh3.googleusercontent.com/OGhrng29-ydrkz2P3DGhZCwHJ3bgtsObXaSykLT8ruNheN2hcsaAuiBW-jTr9pJFO8WTyRFo7JYEQDl6XLfd2F2e7KhV7uuKIop3jjjJfVsWUdE8GVCxsuvSRi1ucLU9ljYaER_JxCRcf8LwLxtPyuW8zq9HCnOAsobCU209E2ld7BGCGwhtPsJBl3d2l8sfyhQ_RyhFwFieEl_ci3F4TZKdrOu876wIUgQC68Iy-u3igD7Y8b3VKSsF_t2EjFMwk6pfrmuLGZUSkmN5ee2L2KU2FoCBqxQ8z2Zq-z15yMH3TtmNtks_n9h3VNg1zuA8m9XGoLIit4ntQhXa3xTPzgnJr1E6tYxyWnNlXub1rgAwZMNgZmeTiPewD0C90mrvCMHCgCTD5H0J4aG2d0PjbvIF5fCaa9C71gVUAcXgyjvFjpr1RET8R3vBAdneYqslZO-DEbch6jRgt6TmC1JC5NJyzamifZeOMv4Ay2XB2ZS2pbjH7F6PcUyF25srG-Y1qe3vDFFqfCWPL64TUA71NfcNWxejA_U_1wy3mAkursL_gpeMJvmEGbz5mqeFL52prot31xtdpgB9h9wMAbTK7i7VPuAcATKlSzcviCZIsdWgNHET84YhLHm2qVXDm1h__0RDMpffKkobyLTqEiMNaesdta5133z5tAPFda_cuGAWl8sFDWm0DhXQ1NoEN54r8pTYMauwdrH959_F8CLLxa1dCQ=w2164-h1218-no'
date: 2019-03-13 14:40:33
tags: [Mac, OS, Terminal, Notes]
categories: Notes
password:
---
For MAC OS系統。

簡易方式`Mac Os`上調整終端器的顏色，是看到有人用`oh-my-zsh`來打造環境
- [超簡單！十分鐘打造漂亮又好用的 zsh command line 環境](https://medium.com/statementdog-engineering/prettify-your-zsh-command-line-prompt-3ca2acc967f)

如果喜歡的朋友，可以參考一下，看起來確實很漂亮心動！

不過對我來說實在太麻煩了，而且對於環境設定不熟悉的人可能需要花很多時間來排除意外發生的bug，如果只是想要簡單的把資料夾這類的顏色做替換的話，就可以參考一下這種export方式非常簡單。

- 文章出自：[Mac OS Terminal 终端使用颜色区分文件目录](https://blog.csdn.net/dongwuming/article/details/51853653)

# Steps

```
vim ~/.bash_profile
```
最後一行加入下方的指令
```
export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]\$ "
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad
alias ls='ls -GFh'
```
加完之後在
```
source ~/.bash_profile
```

用完的效果如下。

![os_terminal](/images/os_terminal.png)

---
# 解釋
這篇有寫每個顏色的代號，可以參考一下。

- [让Mac终端着色](https://blog.csdn.net/meiceatcsdn/article/details/80390115)
