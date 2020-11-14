---
title: Jupyter × Convert to pdf × Nbextension
description: <center> Introduce how to solve the problem of jupyter notebook which output the pdf file and how to extend the jupyter widgets. </center>
photos:
  - 'https://lh3.googleusercontent.com/5clJCXaTh0Ylh8YesDovUvYMCohlxPsfG1i-Ctf_R_ZXsG4WZQXJQB7XP6bvrU9e88PiBrTWDBB--L6cVd78fMxOW7AkccHqy6DIZYzX83DaR3Ked67njMRpqeEHxN1qUI7N0Z4l29LJw0fPiQdPk9_IND5537Gc6JLuMgbtJGmhq4uJUYHkpFBb3LeXGYpQcLW7jhg79Bt8sBmu1tolqJKGgyHidwgCnseV69sSdJJjwXJstOgclbxY3CojbZzDSwaUcd0mGO9ZJZiSSQxdcX0y5dO_bJBHWbaEnFpdCbpvTxZBhVBEeqOxk68510MnBDMSezQa2U8ydi968Wl5Pb_ivVJntW6M6QpoVVE6K7UrWlXKf5BoHwEIWxCvvuV_vFqe3lu---UmxkWqowgo_YXbO194KKcFuXinwFLv3ndGU3Se90DN_WhsgSInbEcUhTmt8bonPrSWqTxZkFDkTnAWjd4BARNbu5bYA8UZC1nW6N-huubR9H61WrIbLGaCzVi5yVodx7Dnte7JilF004inOomBDilSJy04N6JB5wBu-fxyr0r5OEm_EptKrFZl5dYGdv0cBo96yzchT2KHeuserFc6bYLB_S_F1K17zrHLoTMYFJUqa_sLsybf95p1rh2JH_r1TpJwtL8IkHehAT0r0iyGckfcu0Q1TSPW1iHtbvt7DGsTPUUEXUObsUKs_J2_lgejTVAlGTjqcTstl8qeZA=w1707-h960-no'
date: 2019-03-09 13:46:14
tags: [Jupyter notebook, Nbextension, Notes, PDF, Widgets, Program]
categories: Program
password:
---

Jupyter Notebook is very powerful and convenient, but the latest version will happen the error messages when we want to output the pdf file. So I tried some ways to solve this problem, although the results were not really perfect. (When you output the pdf file, the frame will be too small and some codes will be cut by the frame.) Anyway, you just need to use the function of second part in the nbextensions that you can avoid this problem. I will talk about this function later.

# Solve the problem that convert .ipynb to pdf file

1. https://nbconvert.readthedocs.io/en/5.x/install.html
2. Install the MacTex.  File name:`mactex-20180417.pkg` This is quite big (3GB). After installed, it require 5GB stroage. From here: http://tug.org/mactex/mactex-download.html
3. Also install the pandoc. File name: `pandoc-2.7-macOS.pkg`

BTW I saw this method, but I didnt try it yet. From here:https://www.youtube.com/watch?v=bNB3-NcSzIY

---
# Install the nbextensions
It can extend the Jupyter useful widgets.

>Install page:
https://jupyter-contrib-nbextensions.readthedocs.io/en/latest/install.html

Type:
```
conda install -c conda-forge jupyter_contrib_nbextensions
```

Good Reference:
  - [Chinese] https://zhuanlan.zhihu.com/p/52890101
  - Good and useful article in Chinese https://liyang85.com/use-jupyter-notebook-on-macos#MacTeX
  - [English] https://towardsdatascience.com/jupyter-notebook-extensions-517fa69d2231
  - Introduce Vedic:https://www.youtube.com/watch?v=h9DEfxZSz2M

## The problem of autopep8
I recommend this function, `Autopep8) `, that it can make your code more beautiful automatically. Moreover, it can also help you to solve the problem which the words (i.e. the code) exceed the frame.

Meet the problem of `autopep8` widget
> [autopep8]  Error loading library for python: ModuleNotFoundErrorNo module named 'autopep8'  Check that the appropriate library/module is correctly installed (read autopep8's documentation for details)

Solution：
```
pip install autopep8 --user
```

## nbextensions config

If you want to open the interface, you can use the two ways below.
1. localhost:8888/nbextensions/
2. you can click Edit > nbextensions config

Here is what I install the widgets.
![jupyter_function](/images/jupyter_function.png)
