---
title: Shell
date: 2018-02-02 13:34:18
tags: [ Linux , Shell , Notes ]
categories: Linux
description: <center> 讓腳本來替勞這些大量且重複的事情吧! </center>
photos:
  - "https://lh3.googleusercontent.com/MJ-Ujvugso1AwXPPMsN2gjofse0G12oi_NPiyyNKTl0PqBSmIVcE3qiNETSNuKKpbtCQfVyAgblWYBtvPUR6hY1ijz1REwdqXHdnJ6fJUpYGmCjSFpt-TDudHnEZV8iRhSqhS6zvPXx-tCmPMvTOfSOhFgQf9rkOXznGZKYfThzsQ9VTzMHnHQZR60G4OLUWI_KKz0oUJwtCG9KuXYy-Fjo0YJHWYE1f7t4w-QIh0BtNjquhMEI-9pxy77-rWQdvTlLd8U0RJJ4HhJOK4eIKtHWOfShH5r7yA46aM4xiiUfcE-w4eOXpaszCYp_hLtiz1-ZgH1zKuRE_GiWMyqh-TiIcsas4qUcGKddErD-nIgcPYmxlNvubQhLbp9MAmtCogv2KsZAVoQmyhLs_GDZNeJobnCRyF28j0QBYkEZY5b207ySEvJH3NNMQJPmY7lBHFzIeglhWQ5ku4Nh5bdXvfsvUboGgqr4T1b6-VrrSMIleMbBaG3EUa5k0d8sMYDoLz2hhZtyhkbrly7qYIjdC-30ShPUhf0g2o26BUuyqOsFWpyry1Bz9wQaNjSOYL0cbe-J0UxnwO_IbwoQejPO_cmEiwkpxcW43d1NeKIqh__1-XI_Nzr4e8X0Ozy-9blHVV3Qz2ilV0ZFqpcLEIsMCv1_yK55JAkT8ZjEhlheKNIDP_Ah81YF2WKrZj3jvQd6szSogZL572fy5uTQPN2w=w2160-h1368-no"
---
<!--more-->
在處理大量且重複的事情的時候，你會很希望你能有個腳本來當你的左右手。

英文裡叫腳本為 Script ，這裡不講一些細節，有需要學習的可以買書或上網自行閱讀。
主要以記錄與推薦為主。我覺得有需要有目的才會促使自己變強與改進，我在腳本上的訓練也是一樣，不斷有新的目標與需求，然後不斷的去想到底能不能更好更方便，學習並且改進不好的程式處。

不過據說其實shell已經慢慢落伍了QAQ，現在應該是改用Python居多啦...畢竟更簡單易懂且方便。
但是無論哪一種，只要你能精通都是很方便的。

---
# 重點
1. Shell第一行 務必為
  ```
  #!/bin/bash
  ```
  當然如果你的bash不是安裝於這個位置，或者不是安裝這個版本，就不會是這個位置。(一般都是這裡)
  你可以在裡面先行輸入好你希望要在command line裡做的指令，寫在script裡，而當執行時便會一行一行的執行下去。
2. 在Shell內的註釋是使用 "#" (在fortran裡面則一般是"!")
3. 可以在command line上放置shell腳本name後面接續你要放的參數。 (fortran在這部分則需要引用其他的函式)
4. 簡單介紹幾個基本的Shell指令
  ```
  echo :是顯示(呼叫)，類似於fortran內的write,print指令
  read :讀取，類似於Fortran內的read
  $    :變數之意，在shell內有一方便也特別的就是，變數不需要宣告。而記住這概念 "A=$B" 等於後面放變數  
  for  :類似於fortran內的do迴圈之意，用法有很多種且很活(陸續介紹)。
  if   :if判定很好用，可以用來做一些邏輯檢查。  
  ```
5. 在shell內若要處裡字串，則要靠awk與sed的幫助。
6. 腳本每次啟動是進入一個新的bash，也就是進入一個子程序，當你在子程序內做一些環境的export，程序結束之後退回父程序就沒有了。
7. 完成後，記得把這個shell腳本賦予可執行的權限
  ```
  chmod +x (name).sh
  ```

---
# 指令介紹
## for指令
```
for a in 0 1 2 3
do
done
```
這意思是從a=0做到a=3，不過如果你的數字很大的時候就會很麻煩，所以後來我都改用下面這個
```
for a in `seq 0 3`
do
done
```
如果你是要從0做到100，就把3改成100就好，很方便。
如果要做矩陣迴圈(也就是雙迴圈意思)，你就可以在for裡面再放一個for迴圈。

## if指令
```
if [ 判定事項 ]; then
else
fi
```
這是基本式，可以不必有else但是then-else之間一定要有指令
判定事項可以加上"邏輯判定"
```
if [ a -eq a ]; then
else
fi
```
記住裡面的左右都需要空格，不要連接再一起。如果a值是一個變數，也就是你希望他是會隨你的外部參數改變的話，就把它改為"$a"

## continus & break指令
說明:
>這個指令滿特別的，當你的do迴圈裡面可以放一個if判定後接續continue，意即當你滿足這判定完接續continue之後會掠過以下的過程，進行下一次的do迴圈。
而break則是會直接跳出do迴圈

# let & expr指令
說明:
>在Shell內做計算，不像是fortran內那樣精密與方便，
但是做一些簡易的計算還是可以的，可以使用這兩個指令。

---
# Website
1. [Shell符號的意義](http://www.cnblogs.com/xuxm2007/archive/2011/10/20/2218846.html)
2. [echo指令用法](http://blog.csdn.net/lizhi200404520/article/details/8819762)
3. [Shell的for,while,until循環](http://blog.csdn.net/taiyang1987912/article/details/38929069) 裡面有continue的用法。(不錯)
4. [Shell教程](https://www.linuxdaxue.com/linux-shell/)
5. [Shell的awk & sed](http://www.delightpress.com.tw/bookRead/skns00004_read.pdf) 推薦要初學sed與awk者可看這個。

---
# 腳本範本 (?)
其實就是我寫的一些腳本記錄一下 XD
這是在計算一個檔案且每次需要重複289次，前前後後大概需要讓腳本跑2~3次這289次循環的動作...
若需要人為來做這動作光是想想就覺得後怕...(很懶阿誰會有這毅力!)

```
#!/bin/bash
# Program:
# 	Using for cal opium
# History:
# 2017/10/20		First release
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH

#this for boson2 using


# source environment

#source /opt/intel/impi/5.0.0.028/intel64/bin/mpivars.sh # 01
source /opt/intel/impi/4.1.0/bin64/mpivars.sh            # boson2

#First stage
echo "!------------------------!"
echo "! 歡迎來到自動化腳本大營 !"
echo "!------------------------!"
echo ""

#read -p "S軌域,想要混和多少比例 0->1 :" b
#read -p "P軌域,想要混合多少比例 0->1 :" c
#read -p "D軌域,想要混合多少比例 0->1 :" j
#read -p "F軌域,想要混合多少比例 0->1 :" h

f=1
g=0

read -p "(Fisrt atom)Seedname :" Aname
read -p "(Second atom)Seedname :" Bname
read -p "How many cores :" n
read -p "CPU total number :" mm
read -p "你要計算CASTEP的檔案名子 :" Filename
read -p "要跳過Opium step? (1:no 2:yes) :" step


if [ -f "$step" -eq 1 ]; then


if [ -f "$Filename.0001.err" ]; then
rm *.err
fi

rm -r $Aname\_S*

rm -r origin_firstatomfile

#--------------- S & P orbitals ------------------

mkdir origin_firstatomfile
cp ./$Aname.param origin_firstatomfile
cp ./$Bname.param origin_firstatomfile

cd origin_firstatomfile


#if this produceVPS put in local folder,please improve here.
(路徑) ~/produceVPS_sp $g $g $f
# it will produce alcwnl.txt, pc.txt and pcen.txt.
#Because keyin f=1  it will produce Wps1_s.txt, Wps1_p.txt and en.txt
(路徑) ~/opium  $Aname.param $Aname.log all rpt recpot >$Aname\_opium.txt

mv Wps2_s.txt Wps1_s.txt
mv Wps2_p.txt Wps1_p.txt

cd ..

m=1

for a in `seq 0 16`
do
r=$(awk "BEGIN{print $a/16 }")

for aa in `seq 0 16`
do
rr=$(awk "BEGIN{print $aa/16 }")


#-------------- count --------------------

nn=`expr $mm + 1`
let "temp2=m%$nn"
#echo "temp2=$temp2"

if [ "$temp2" -eq 0 ]
then
echo -n "!==========!"
echo -n "! Sleeping !"
echo -n "!==========!"
sleep 120
fi
let "m++"

#-------------- continue  ----------------

mkdir $Aname\_S$a\_P$aa\_$Bname
cp ./origin_firstatomfile/* $Aname\_S$a\_P$aa\_$Bname

#-------------- Second stage ------------------

cd $Aname\_S$a\_P$aa\_$Bname

b=$r
c=$rr


(路徑) ~/produceVPS_sp $b $c $g


# it will produce alcwnl.txt, pc.txt and pcen.txt.
#Because keyin g=0 it will not produce Wps1_s.txt, Wps1_p.txt Wps1_d.txt Wps1_f.txt and en.txt.

# Now Wps1_s.txt , Wps1_p.txt and en.txt are Aname files.

(路徑) ~/opium $Bname.param $Bname.log all rpt recpot >$Bname\_opium.txt &


cd ..


done
done

# copy recpot into all_potential
mkdir all_potential

for a in `seq 0 16`
do

for aa in `seq 0 16`
do


mv ./$Aname\_S$a\_P$aa\_$Bname/$Bname.recpot ./$Aname\_S$a\_P$aa\_$Bname/$Aname\_S$a\_P$aa\_$Bname.recpot
cp ./$Aname\_S$a\_P$aa\_$Bname/$Aname\_S$a\_P$aa\_$Bname.recpot ./all_potential/

done
done

#------------------------------------- Finish Pseudopotential --------------------------
#cd ./all_potential/
else
if [ -f "$step" -eq 2 ] ; then

for a in `seq 0 16`
do
r=$(awk "BEGIN{print $a/16 }")

for aa in `seq 0 16`
do
rr=$(awk "BEGIN{print $aa/16 }")

b=$r
c=$rr

# it will produce alcwnl.txt, pc.txt and pcen.txt.
#Because keyin g=0 it will not produce Wps1_s.txt, Wps1_p.txt Wps1_d.txt Wps1_f.txt and en.txt.

# Now Wps1_s.txt , Wps1_p.txt and en.txt are Aname files.

#(路徑) ~/opium $Bname.param $Bname.log all rpt recpot plot ke plot wp plot logd plot vi >$Bname\_opium.txt
      #mv $Bname.recpot $Aname\_S$a\_P$aa\_$Bname.recpot

cd ./$Aname\_S$a\_P$aa\_$Bname/

echo "========== Check Files =========="
cp ../$Filename/* .

if [ -f "$Filename.cell" ]; then
echo "File $Filename.cell exists."
else
echo "File $Filename.cell does not exist."
exit
fi

if [  -f "./$Filename.param" ]; then
echo "File $Filename.param exists"
else
echo "File $Filename.param does not exist."
exit
fi

#----- improve recpot name in .cell files -----------------------------
echo "========== Potential Name =========="
echo "$Aname\_S$a\_P$aa\_$Bname"

sed -e "/^.*_.[^a-zA-Z]_.[^a-zA-Z]_.*\.recpot/c\ $Aname $Aname\_S$a\_P$aa\_$Bname.recpot" $Filename.cell > $Filename\_new.cell

mv $Filename\_new.cell $Filename.cell

#------ CASTEP calculation
echo "========= Start to calculate SCF ========="
#mpirun -np $n (路徑) ~/RunCASTEP.sh $Filename
mpirun -np $n (路徑) ~/castep.mpi $Filename

awk  '/alpha | beta | gamma/ {print $1 , $2 , $3} ' $Filename.castep  > $Filename\_length.txt

N=3  # line N from the bottom
tail -n $N $Filename\_length.txt > $Aname\_S$a\_P$aa\_$Bname\_length.txt
#mv length.txt $Aname\_$r\_$Bname\_$a\_length.txt
#cp $Aname.castep $Aname\_$r\_$Bname\_$a.castep # I consider that we don't need to open now.
#cp $Aname\_BandStr.castep $Aname\_$r\_$Bname\_$a\_BandStr.castep #If you want to calculate, you open it.
#sed ' /a|b|c/w length.txt ' $Aname\_$r\_$Bname\_$a\_length.txt # open #try to close

namename=$Aname\_S$a\_P$aa\_$Bname\_length
sed ' 1w xmgrace1.txt' $namename.txt # open # print file just one line

#awk '{print name, $0 >> "length.txt"}' name=$Aname\_$r\_$Bname\_$a $Aname\_$r\_$Bname\_$a\_length.txt # no requirement work

#---- real

awk '{print name >> "length.txt"}' name=$Aname\_S$a\_P$aa\_$Bname $Aname\_S$a\_P$aa\_$Bname\_length.txt #open
awk '{print $0 >> "length.txt"}' $Aname\_S$a\_P$aa\_$Bname\_length.txt # open
rm $Filename\_length.txt

#---- xmgrace requirement input file
#awk '{print name >> "xmgrace.txt"}' name=$r $Aname\_$r\_$Bname\_$a\_length.txt # don't open
#awk '{print name,$3 >> "xmgrace.txt"}' name=$r $Aname\_$r\_$Bname\_$a\_length.txt # currently don't open
awk '{print name,$3 >> "xmgrace.txt"}' name=$r xmgrace1.txt

#----- combine all the individual .txt files --------------------------

sed '$!N; /^\(.*\)\n\1$/!P; D' length.txt > $Aname\_$Bname\_analysis_length.txt   # open
rm length.txt # need?
rm xmgrace1.txt


mv $Filename.castep $Aname\_S$a\_P$aa\_$Bname.castep
mv $Filename.cell $Aname\_S$a\_P$aa\_$Bname.cell

cd ..

done
done

echo "====== Job Finish ======"

fi
fi

#End
```

主要一個技巧就是先把你要做的一整個流程想好，之後把整個流程動作指令寫入你的script裡面就對了。

---
# 使用的工具書
我使用的工具書是 [Linux命令行與shell腳本編程大全（第3版](http://www.books.com.tw/products/CN11369414)
Shell工具書非常之多，有的其實也找的到pdf檔
不過覺得實體的工具書應該買一本，還是有它方便之處的。


以上 若有想到會再繼續補充...
