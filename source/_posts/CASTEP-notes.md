---
title: CASTEP notes
date: 2017-12-05 14:22:37
tags: [ CASTEP , Linux , Notes ]
categories: Linux
description: <center> 這篇屬很雜亂的一些紀錄和推薦分享 (持續新增) </center>
photos:
  - "https://lh3.googleusercontent.com/szmRN7Fi41DBW3X5lcoo3b-buUlF1R-SSq4tWcvxHb_6SS_bg_LwCM7bJYOo4JPJhL9xQgQOEQySP83QlGwW1_wOwZpk91BUbXXYhQTQFX1YPKDpPPT9IQMLilWcyhp9TUol9jQqZfdefSLLlktfydO1XSfNxJ7lJg4L2eDSW0C_Zy17ad1GLQAJZRUvUQo0aZ1acUQErTkCVRh_5tBRnopUWvsaTwhg_Uopuv6HxZ9SpNu-Rddc92OQFW0yC-8X0RoEBA_R7wipdskET4sOByKYzmqfyTy9hAO9XmyMxFdZ0_7VuQtw6wzgh2O7nVJoezyNRJyAj2UPBswOrbPyoIfx-rael7MSy4JZC7xPieUP7UH82GgpAbSDMrEFjBnV_bok56En50iZcrUJHTTq33nby-XVBMIuhXAfbwb6SdDNFxNTRMi0gt_bqME71-6B_cklI2uVO-yHWrID78oMG1JzFtugcePXdzT_vZlBm58JIkWNC1vBl8PYjyFC9Q-XtuMRB7RetKjfV2Ra1mxcqmnB0hkwxVY4GqLRUbeH6k3WPzSDvBvUAW3mA2cF9ol1YmupJ6Pt52GqqDlwmLpscd3Msiz6vDtsnfBI9IPDDZEcUPp5UBXPlfyGVlYLmIL1UMmNKS2MjO3lv-cJdTzu_0SUoIDlodtL9R-LAE-t7pEUJ_AaCp7qd_tzOMnlJFBtmkowt3Xc6Y_uwtYS2es=w2160-h1216-no"
---

<!--more-->
# Geometry Optimization
SCF 電子結構收斂 ► 若在這無法收斂 ► Oband DFT 要去動SCF相關的參數
## 步驟
  1. SCF over (每一移動一個原子，就算一次SCF)
  2. 算Force ►作用對象是原子
  3. SCF重做一次
  4. 算Stress應力為0 ► 作用對象為cell
  5. BFGS若不收斂，則為GO state不收斂(但有SCF有收斂)
  ► 最常原因是因為E_cut不夠，尤其在動晶包 (請看Stress是否有小不下來的現象)

長晶包 ► 應力波

> force  微分一次(energy對位置微分)，原子看force
  stress 微分兩次，晶包看stress

臨界阻泥震盪 ► 最快停下來

(2018/02/06)
> force 與總個(晶包，內容物)的受力相關(各方向等等)
  stress (應變=>伸長量) 長度變化量/參考長度(總長) => "沒有單位"

## GO不收斂情況
有幾種，一種是SCF計算，一種是BFGS計算達到次數(預設100次)
要去查看幾個部分。
另外，在判定GO不收斂時，請看Stress值是否持續大而未降下來，以及SCF計算(tolerance)是否有持續漸小。

## 調控tolerance地方是在:
![CASTEP_notes1](/images/castep_notes1.png)
![CASTEP_notes2](/images/castep_notes2.png)
一般medium就夠用，不過還是得考量計算的物性的需求來做決定。

## 精確度的影響因素
1. tolerance ► Q:如何判斷他的值該設多少? A:還是要看計算什麼物性來做決定。
2. stress
3. force

## TPSD (2 points steepest descent)
另外，計算的條件是有固定一軸而另一軸可動時，可使用TPSD代替BFGS的計算，會比較有效率。
TPSD ► 2 points 兩點之意(始=>末)，若要做TPSD castep計算，則需把BFGS的字手動更改為TPSD。或者直接於GO more內做更改。

另外，還有一種也可以嘗試，使用LBFGS也不錯。

## 增加E_cut的時機
不是所有的GO不收斂都適用，增加E_cut時，可以提升波函數的品質，進而可以更好的算出stress值，讓stress能夠小下來。
而如果E_cut不夠，則stress小不下來，就不容易收斂。
所以建議要看stress有沒有持續小不下來的跡象，方建議使用此法解決。

## Fractional coordinates
原子的位置表示，是分數座標。
Real Lattice 是(直或橫)的為A、B、C向量，而是由 uA(向量)+vB(向量)+wC(向量)所組成。

>舉例:
```
!======================================!
!           Real Lattice(A)            !    
!    2.5448282  -1.4697230   0.0001380 !    
!   -0.0004034   2.9387474  -0.0001380 !      
!    0.0002992  -0.0005183   8.0000000 !     
!======================================!
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
x  Element         Atom        Fractional coordinates of atoms  x
x                 Number           u          v          w      x
x---------------------------------------------------------------x
x  C                 1         0.666572   0.333428   0.449079   x
x  C                 2         0.333428   0.666572   0.550921   x
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
>如果今天要計算兩個碳原子的C軸方向高度差計算，則是
0.449079\*(0,0,8)
0.550921\*(0,0,8)
兩相減則為 0.814736 angstrom。 (這時才有單位)

---
# Other notes
DFT-D means Van-der_Waals.
lo-to ► 用於離子晶體計算，在左右移動上補計算
凡德瓦利是屬於激發態，瞬間對偶極，總的來說就是吸引力
DFT ► 屬基態
dft-dispesion
constraint ► 適用於固定原子 (需打開勾選最下面)
restraint ► 適用於表面重構
BFGS delocalize internals自由度較小

---
# 極化率計算
極化率分兩種
1.電場(or電子)
2.離子

## 算極化率
計算極化率的時候，可先儲存file，再到Efield裡面task，刪去 phonon，留下 efield，再做計算較快

以及做極化率計算時候，把原子fix住之後，就不會算低頻電場的值
(metal不可點選 因為計算電場若使用金屬 會有電流產生)

電場做出來的極化率 沒分頻率 相當於極高頻

---
# 與計算材料相關及其他類型程式推薦

## [OVITO](https://ovito.org/index.php/about/what-is-ovito)
Description:

    Molecular dynamics (MD), molecular statics and Monte-Carlo based simulations are nowadays standard methods for modeling materials with atomic-scale resolution.
    Such atomistic simulation models generate three-dimensional atomic configurations or trajectories, which usually need to be further analyzed in order to generate new scientific insights.
    Powerful analysis and visualization techniques play a key role in this process as simulated systems become larger and more complex.
    Without the right software tools, key information would remain undiscovered, inaccessible and unused.
    The task of visualization packages such as OVITO is to translate the raw atomic coordinates into a meaningful graphical representation and enable an interpretation by the scientist.

    OVITO is a freely available visualization and data analysis software for atomistic datasets as output by large-scale molecular dynamics/statics and Monte-Carlo simulations.
    Its name is an acronym for Open Visualization Tool, emphasizing that flexibility and extensibility were important goals in the development of this software.
  (截取官網Introduction)

## [ASE](https://wiki.fysik.dtu.dk/ase/index.html)
Description:

    ASE is an Atomic Simulation Environment written in the Python programming language with the aim of setting up, steering, and analyzing atomistic simulations.

  (截取官網About)

## [Quantum-Espresso](http://www.quantum-espresso.org/)
Description:

    Quantum ESPRESSO is an integrated suite of Open-Source computer codes for electronic-structure calculations and materials modeling at the nanoscale.
    It is based on density-functional theory, plane waves, and pseudopotentials.

    Quantum ESPRESSO has evolved into a distribution of independent and inter-operable codes in the spirit of an open-source project.
    The Quantum ESPRESSO distribution consists of a “historical” core set of components, and a set of plug-ins that perform more advanced tasks, plus a number of third-party packages designed to be inter-operable with the core components.
    Researchers active in the field of electronic-structure calculations are encouraged to participate in the project by contributing their own codes or by implementing their own ideas into existing codes.

    Quantum ESPRESSO is an open initiative, in collaboration with many groups world-wide, coordinated by the Quantum ESPRESSO Foundation.
    Present members of the latter include Scuola Internazionale Superiore di Studi Avanzati (SISSA) , the Abdus Salam International Centre for Theoretical Physics (ICTP), the CINECA National Supercomputing Center , the Ecole Polytechnique Fédérale de Lausanne, the University of North Texas, the Oxford University.
    Courses on modern electronic-structure theory with hands-on tutorials on the Quantum ESPRESSO codes are offered on a regular basis in collaboration with ICTP.
    (Last updated Sep. 29, 2017)
  (截取官網About)

## [Xcrysden](http://www.xcrysden.org/)
  *非常推薦使用這個程式*
Description:

    XCrySDen is a crystalline- and molecular-structure visualisation program.
    The name of the program stands for Crystalline Structures and Densities and X because it runs under the X-Window environment.
    It facilitates a display of isosurfaces and contours, which can be superimposed on crystalline structures and interactively rotated and manipulated.
    It also possesses some tools for analysis of properties in reciprocal space such as interactive selection of k-paths in the Brillouin zone for the band-structure plots, and visualisation of Fermi surfaces.

    The graphical user interface of XCrySDen was developed to provide an easy to use and learn interface.
    Casual users should be able to exploit more than just the basic functionality without devoting more than a few hours of effort to the task of learning the use of the program.
    XCrySDen also provides a (partial) graphical user interface for CRYSTAL ab initio program, and a visualization system for PWscf and WIEN2k and initio programs.
  (截取官網)

## [lyx](https://www.lyx.org/)
Description:

    LyX is a document processor that encourages an approach to writing based on the structure of your documents (WYSIWYM) and not simply their appearance (WYSIWYG).
    LyX combines the power and flexibility of TeX/LaTeX with the ease of use of a graphical interface.
    This results in world-class support for creation of mathematical content (via a fully integrated equation editor) and structured documents like academic articles, theses, and books.
    In addition, staples of scientific authoring such as reference list and index creation come standard.
    But you can also use LyX to create a letter or a novel or a theatre play or film script.
    A broad array of ready, well-designed document layouts are built in.

    LyX is for people who want their writing to look great, right out of the box.
    No more endless tinkering with formatting details, “finger painting” font attributes or futzing around with page boundaries.
    You just write. On screen, LyX looks like any word processor; its printed output — or richly cross-referenced PDF, just as readily produced — looks like nothing else.

    LyX is released under a Free Software/Open Source license, runs on Linux/Unix, Windows, and Mac OS X, and is available in several languages.
  (截取官網)

## [VESTA](http://jp-minerals.org/vesta/en/)
Description:

    VESTA is a 3D visualization program for structural models, volumetric data such as electron/nuclear densities, and crystal morphologies. Some of the novel features of VESTA are listed below.
  (截取官網)

## [Crystallography Open Database](http://www.crystallography.net/cod/)    
Description:

    Open-access collection of crystal structures of organic, inorganic, metal-organic compounds and minerals, excluding biopolymers.
  (截取官網)

## [USPEX](http://uspex-team.org/en/uspex/overview)
Description:

    USPEX (Universal Structure Predictor: Evolutionary Xtallography...and in Russian "uspekh" means "success" - owing to the high success rate and many useful results produced by this method) is a method developed by the Oganov laboratory since 2004.
    The problem of crystal structure prediction is very old and does, in fact, constitute the central problem of theoretical crystal chemistry. In 1988 John Maddox wrote that:

    "One of the continuing scandals in the physical sciences is that it remains in general impossible to predict the structure of even the simplest crystalline solids from a knowledge of their chemical composition solids such as crystalline water (ice) are still thought to lie beyond mortals' ken".

    USPEX method/code solves this problem and is used by over 4000 researchers worldwide.
    The First Blind Test of Inorganic Crystal Structure Prediction shows that USPEX outperforms other methods in terms of efficiency and reliability.
    The method continues to be rapidly developed. In addition to crystal structure prediction, USPEX can work in other dimensionalities and predict the structure of nanoparticles, polymers, surfaces, interfaces and 2D-crystals.
    It can very efficiently handle molecular crystals (including those with flexible and very complex molecules) and can predict stable chemical compositions and corresponding crystal structures, given just the names of the chemical elements.
    In addition to this fully non-empirical search, USPEX allows one to predict also a large set of robust metastable structures and perform several types of simulations using various degrees of prior knowledge.

    USPEX can also be used for finding low-energy metastable phases, as well as stable structures of nanoparticles, surface reconstructions, molecular packings in organic crystals, and for searching for materials with desired physical (mechanical, electronic) properties.
    The USPEX code is based on an efficient evolutionary algorithm developed by A.R. Oganov's group, but also has options for using alternative methods (random sampling, metadynamics, corrected particle swarm optimization algorithms).
    USPEX is interfaced with many ab initio codes, such as VASP, SIESTA, GULP, Quantum Espresso, CP2K, CASTEP, LAMMPS, and so on.
  (截取官網)

---

# 增加 number of electrons
在 .param 檔案內底部增加一行
```
charge : 數目
```
增加一個一電子 -1
減少一個一電子 1
