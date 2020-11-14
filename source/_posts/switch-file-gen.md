---
title: 利用Shell進階產生 .switch檔 | 利用Fortran簡易程式生產
description: <center> Shell腳本分享[.switch]檔的生產，可推廣應用於重複動作輸出到txt檔內容</center>
photos:
  - 'https://lh3.googleusercontent.com/X9rv991u-rnJP4KTgOXTt4DLa3pcf3W_VDpaXl1htbmvS8upz2cQBXh-4g1gEHrklif4X3jRtFwSlVd1W5KL4eveV8GJ0nMufoySC9XrF5JYcEHDILQ6awH8nmNrpTb4g8HzgTHuz2LXMwc6DxRUNXekjZB-BIeWGhNHfxxuFkzqp8SZfq-vV2WGdaMujvbrHnwLKiKiFtYrEs2SNe7taIYD2c1tUNCx_oOxTCl3f2yd7OloL0XPSm96BxypupToYa0OFyQC5fow0uA1n-6Yry_rLhRYfu71aPrnAIcr0ie0y3sYtc2TkLCSD9j8WblHAw63yPmBtoBfu-UX5fF08zICfRDa4Vk05ORtJwOZuBHZGkEarT6npbahJK71i1vTDh33sLhf7nWv0HOhwx22NKu6FHz-8ETsrbPmjadKPmoax5bZ8VmbLzfHaJmFXEoaGzREsrelH3TBUMA9wXc02oV1IHH9b2wIwdLS1Z1hFCnjApDjNDc0Q5PAc1T1LssNtbvBX7vZgNdQ3IqmgSi5UGvgiD8AKfjSQlT1qOHpaYfJiSYXLUASFLNI3aCKRc6D6Lo6_l-1WugwZQ4RHKTptm-chmUMb3mdYwozJIow6Yb31oB47yv2EaIrt8L2GhzcWWuUsgOo26WB4grNOclQIPm46VJ2K2kFp4Jg1JlQZ1-mBbKz_ClMJn3GMpbQAB3eGf9xXWeqY_TH4nJ_lg=w1546-h869-no'
date: 2018-06-10 11:56:08
tags: [ Linux , Shell , Notes , Atom_cutting , CASTEP]
categories: Linux
password:
---
# <center>前提</center>

由於 Atom_cutting 程式的需求，計算之前需準備.switch檔案，如果處理的材料分子數較大較多必須手動重複的列出元素名、半徑、數量等等，如果今天有上百個計算需要做這個動作，並且在vim裡面是沒有辦法快速的告訴操作者已經有幾個(元素)，很容易有多一個或少一個的誤差出現。

# <center>例子</center>

我在這先舉出一般的.switch檔內的內容，以5NU這材料來做示範。
5NU : C 16 H 12 N 12 O 16
可以發現如果是手動是極度耗時的一個事情。

```
%BLOCK ATOM_DOMAIN
H 0.8
H 0.8
H 0.8
H 0.8
H 0.8
H 0.8
H 0.8
H 0.8
H 0.8
H 0.8
H 0.8
H 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
C 0.8
N 0.8
N 0.8
N 0.8
N 0.8
N 0.8
N 0.8
N 0.8
N 0.8
N 0.8
N 0.8
N 0.8
N 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
O 0.8
%ENDBLOCK ATOM_DOMAIN

%BLOCK CUT_ATOM
H cut 0
H cut 0
H cut 0
H cut 1
H cut 1
H cut 1
H cut 1
H cut 1
H cut 1
H cut 1
H cut 1
H cut 1
C cut 0
C cut 0
C cut 0
C cut 0
C cut 1
C cut 1
C cut 1
C cut 1
C cut 1
C cut 1
C cut 1
C cut 1
C cut 1
C cut 1
C cut 1
C cut 1
N cut 0
N cut 0
N cut 0
N cut 1
N cut 1
N cut 1
N cut 1
N cut 1
N cut 1
N cut 1
N cut 1
N cut 1
O cut 0
O cut 0
O cut 0
O cut 0
O cut 1
O cut 1
O cut 1
O cut 1
O cut 1
O cut 1
O cut 1
O cut 1
O cut 1
O cut 1
O cut 1
O cut 1
%ENDBLOCK CUT_ATOM
```

# <center>Fortran程式</center>

最初其實是使用Fortran寫出的程式，但在更改上與細修的即時度較差，因為不方便所以才寫了後來的Shell腳本，以下是簡易版本的生產器，可編譯之後使用。
Prpgram Name : produceswitch.f90

```
!=======================!
! Written by Chieh Tsai !
!=======================!

        Program produce_switch
        implicit none
        character(len=100)  ::filename
        integer a , i , x ,d , atom , e
        character(len=2) b
        character(len=5) c
        !real c
        write(*,*) 'Please write your material name.'
        !write(*,*) 'And do not include file extension.'
        read(*,*)  filename
        filename=trim(filename)//'_Optics.switch'
        open(10,file=filename,position='append')
                write(10,*)'%BLOCK ATOM_DOMAIN'

print *,'!--------------ATOM_DOMAIN PARAMETER FORM--------------!'
print *,'![SPECIES]  [CUT RADIUS (in Angstrom)]                 !'
print *,'!------------------------------------------------------!'




        write(*,*)'How many kinds of atoms are in your case?'
        read(*,*) a

        do atom=1,a

        write(*,*) '(1) Which atom do you want to do?'
        read(*,*) b
        write(*,*) '(2) How many atoms do you need?'
        read(*,*) d
        write(*,*) '(3) Please write the radius of atom'  
        read(*,*) c

                do i= 1, d
                write(10,*) trim(b) ,' ',trim(c)
                enddo

print *,'!--------!'
print *,'!  Next  !'
print *,'!--------!'
        enddo
                write(10,*)'%ENDBLOCK ATOM_DOMAIN'
                write(10,*)' '
                write(*,*) ' '
print *,'!-----------CUT_ATOM PARAMETER FORM----------!'
print *,'![SPECIES]  CUT    [NUMBER]                  !'
print *,'![SPECIES]  KEEP   [NUMBER]                  !'
print *,'!                                            !'
print *,'!where [NUMBER]=0,1,or 2                     !'
print *,'!0  conduction bands (keep velance bands)    !'
print *,'!1  velance bands (keep conduction bands)    !'
print *,'!2  both velance bands and conduction bands  !'
print *,'!--------------------------------------------!'

                write(10,*)'%BLOCK CUT_ATOM'

!print *,'Here you should consider what kinds of different events you want to partitions.'
print *,'EX. C cut   1'
print *,'    C keep  2'
print *,'    H keep  2'
print *,'    H keep  0'
print *,'C => 2 kinds H => 2 kinds'
print *,'So we would key in 4.'
print *,'Here you should consider what kinds of different events you want to'
print *,'partitions.'
print *,'How many events?'
        read(*,*) a
print *,'If there are wrong about the steps of (1)(2) ,you can key in greater than 2.'
        do atom=1,a

1000    write(*,*) '(1) Which atom do you want to do?'
        read(*,*) b
        write(*,*) '(2) keep / cut'
        read(*,*) c
        write(*,*) '(3) 0/1/2'
        read(*,*) d
        if ( d .eq. 0 .or. d .eq. 1 .or. d .eq.2 ) then
        write(*,*)'(4) How many quantity?'
        else
print *,'Only 0-2'
        goto 1000
        endif
        read(*,*) e

                do i= 1, e
                write(10,*)trim(b) ,' ',trim(c),' ',d
                enddo

print *,'!--------!'
print *,'!  Next  !'
print *,'!--------!'


        enddo

                write(10,*)'%ENDBLOCK CUT_ATOM'


        stop
        end

```

# <center>Shell script - 進階版本</center>

這版雖然方便，但依舊有一些條件與限制。

> <center>Introduction</center>
1. 可直接產生分別分子個數的switch檔案。Example: Urea內由2個單分子組成，可一次產生出分別屬於2組單分子的switch檔。
2. 可直接產生出 onsite 與 offsite 兩種狀況的 switch檔案。
3. 目前是支援三種與四種元素組成的材料。Example: C16H12O16 與 C16H12N12O16。

**BTW 如果只有三種元素的材料，當腳本詢問第四種元素時，直接Enter跳過空白。**

```
#!/bin/bash

echo "!--------------------------------!"
echo "!  Welcome to automatical script !"
echo "! Atom cutting | Produce .switch !"
echo "!      Author:   Chieh Tsai      !"
echo "!     2018/06/05 version:1.0     !"
echo "!--------------------------------!"
echo ""

read -p "Atom_cutting File name (without including Optics) :" Filename
read -p "1. atom name :" A
read -p " Quanty :" AQ
read -p " Radius :" AR

read -p "2. atom name :" B
read -p " Quanty :" BQ
read -p " Radius :" BR

read -p "3. atom name :" C
read -p " Quanty :" CQ
read -p " Radius :" CR

echo ""
echo "If there isn't fourth atom, please let empty until next question."
echo ""

read -p "4. atom name :" D
read -p " Quanty :" DQ
read -p " Radius :" DR

read -p "Molecular quatites :" E



EE=`expr $E - 1`
m=1

################################
# Start to compute about me-me #
################################

for aaa in `seq 0 $EE`
do

> $Filename\_Optics.switch

echo '%BLOCK ATOM_DOMAIN' > $Filename\_Optics.switch &
#echo '' >> $Filename\_Optics.switch &

for a in `seq 1 $AQ`
do
echo "$A $AR" >>$Filename\_Optics.switch &
done

for a in `seq 1 $BQ`
do
echo "$B $BR" >>$Filename\_Optics.switch &
done

for a in `seq 1 $CQ`
do
echo "$C $CR" >>$Filename\_Optics.switch &
done

if [[ -n "$DQ" || "$D"  || "$DR" ]] ; then
for a in `seq 1 $DQ`
do
echo "$D $DR" >>$Filename\_Optics.switch &
done
fi

#echo '' >> $Filename\_Optics.switch &
echo '%ENDBLOCK ATOM_DOMAIN' >> $Filename\_Optics.switch &

echo '' >> $Filename\_Optics.switch &

echo '%BLOCK CUT_ATOM' >> $Filename\_Optics.switch &
#echo '' >> $Filename\_Optics.switch &

# A

r1=$(awk "BEGIN{print $AQ/$E}")
aaaa1=`expr $aaa \* $r1 `
rr1=`expr $AQ - $aaaa1 - $r1 `

if [ $aaa -ne 0 ]
then
for aa in `seq 1 $aaaa1`
do
echo "$A cut 2" >>$Filename\_Optics.switch &
done
fi

for aa in `seq 1 $r1`
do
echo "$A keep 2" >>$Filename\_Optics.switch &
done


if [ $aaa -ne $EE ]
then
for aa in `seq 1 $rr1`
do
echo "$A cut 2" >>$Filename\_Optics.switch &
done
fi

# B

r2=$(awk "BEGIN{print $BQ/$E}")
aaaa2=`expr $aaa \* $r2 `
rr2=`expr $BQ - $aaaa2 - $r2 `


if [ $aaa -ne 0 ]
then
for aa in `seq 1 $aaaa2`
do
echo "$B cut 2" >>$Filename\_Optics.switch &
done
fi

for aa in `seq 1 $r2`
do
echo "$B keep 2" >>$Filename\_Optics.switch &
done


if [ $aaa -ne $EE ]
then
for aa in `seq 1 $rr2`
do
echo "$B cut 2" >>$Filename\_Optics.switch &
done
fi

# C

r3=$(awk "BEGIN{print $CQ/$E}")
aaaa3=`expr $aaa \* $r3`
rr3=`expr $CQ - $aaaa3 - $r3 `

if [ $aaa -ne 0 ]
then
for aa in `seq 1 $aaaa3`
do
echo "$C cut 2" >>$Filename\_Optics.switch &
done
fi

for aa in `seq 1 $r3`
do
echo "$C keep 2" >>$Filename\_Optics.switch &
done


if [ $aaa -ne $EE ]
then
for aa in `seq 1 $rr3`
do
echo "$C cut 2" >>$Filename\_Optics.switch &
done
fi

# D

if [[ -n "$DQ" || "$D"  || "$DR" ]] ; then

r4=$(awk "BEGIN{print $DQ/$E}")
aaaa4=`expr $aaa \* $r4`
rr4=`expr $DQ - $aaaa4 - $r4 `

if [ $aaa -ne 0 ]
then
for aa in `seq 1 $aaaa4`
do
echo "$D cut 2" >>$Filename\_Optics.switch &
done
fi

for aa in `seq 1 $r4`
do
echo "$D keep 2" >>$Filename\_Optics.switch &
done


if [ $aaa -ne $EE ]
then
for aa in `seq 1 $rr4`
do
echo "$D cut 2" >>$Filename\_Optics.switch &
done
fi

fi

#echo '' >> $Filename\_Optics.switch &
echo '%ENDBLOCK CUT_ATOM' >> $Filename\_Optics.switch &

# improve file name

mv $Filename\_Optics.switch $Filename\_Optics.switch_onsite_$m
let "m++"
done

n=1
#################################
# Start to compute about me-you #
#################################
for aaa in `seq 0 $EE`
do

> $Filename\_Optics.switch

echo '%BLOCK ATOM_DOMAIN' > $Filename\_Optics.switch &
#echo '' >> $Filename\_Optics.switch &

for a in `seq 1 $AQ`
do
echo "$A $AR" >>$Filename\_Optics.switch &
done

for a in `seq 1 $BQ`
do
echo "$B $BR" >>$Filename\_Optics.switch &
done

for a in `seq 1 $CQ`
do
echo "$C $CR" >>$Filename\_Optics.switch &
done

if [[ -n "$DQ" || "$D"  || "$DR" ]] ; then
for a in `seq 1 $DQ`
do
echo "$D $DR" >>$Filename\_Optics.switch &
done
fi

#echo '' >> $Filename\_Optics.switch &
echo '%ENDBLOCK ATOM_DOMAIN' >> $Filename\_Optics.switch &

echo '' >> $Filename\_Optics.switch &

echo '%BLOCK CUT_ATOM' >> $Filename\_Optics.switch &
#echo '' >> $Filename\_Optics.switch &

# A

r1=$(awk "BEGIN{print $AQ/$E}")
aaaa1=`expr $aaa \* $r1 `
rr1=`expr $AQ - $aaaa1 - $r1 `

if [ $aaa -ne 0 ]
then
for aa in `seq 1 $aaaa1`
do
echo "$A cut 1" >>$Filename\_Optics.switch &
done
fi

for aa in `seq 1 $r1`
do
echo "$A cut 0" >>$Filename\_Optics.switch &
done


if [ $aaa -ne $EE ]
then
for aa in `seq 1 $rr1`
do
echo "$A cut 1" >>$Filename\_Optics.switch &
done
fi

# B

r2=$(awk "BEGIN{print $BQ/$E}")
aaaa2=`expr $aaa \* $r2 `
rr2=`expr $BQ - $aaaa2 - $r2 `


if [ $aaa -ne 0 ]
then
for aa in `seq 1 $aaaa2`
do
echo "$B cut 1" >>$Filename\_Optics.switch &
done
fi

for aa in `seq 1 $r2`
do
echo "$B cut 0" >>$Filename\_Optics.switch &
done


if [ $aaa -ne $EE ]
then
for aa in `seq 1 $rr2`
do
echo "$B cut 1" >>$Filename\_Optics.switch &
done
fi

# C

r3=$(awk "BEGIN{print $CQ/$E}")
aaaa3=`expr $aaa \* $r3`
rr3=`expr $CQ - $aaaa3 - $r3 `

if [ $aaa -ne 0 ]
then
for aa in `seq 1 $aaaa3`
do
echo "$C cut 1" >>$Filename\_Optics.switch &
done
fi

for aa in `seq 1 $r3`
do
echo "$C cut 0" >>$Filename\_Optics.switch &
done


if [ $aaa -ne $EE ]
then
for aa in `seq 1 $rr3`
do
echo "$C cut 1" >>$Filename\_Optics.switch &
done
fi

# D

if [[ -n "$DQ" || "$D"  || "$DR" ]] ; then

r4=$(awk "BEGIN{print $DQ/$E}")
aaaa4=`expr $aaa \* $r4`
rr4=`expr $DQ - $aaaa4 - $r4 `

if [ $aaa -ne 0 ]
then
for aa in `seq 1 $aaaa4`
do
echo "$D cut 1" >>$Filename\_Optics.switch &
done
fi

for aa in `seq 1 $r4`
do
echo "$D cut 0" >>$Filename\_Optics.switch &
done


if [ $aaa -ne $EE ]
then
for aa in `seq 1 $rr4`
do
echo "$D cut 1" >>$Filename\_Optics.switch &
done
fi

fi

#echo '' >> $Filename\_Optics.switch &
echo '%ENDBLOCK CUT_ATOM' >> $Filename\_Optics.switch &


# improve file name

mv $Filename\_Optics.switch $Filename\_Optics.switch_offsite_$n
let "n++"
done

exit
```
當然，可以發現兩個使用功能不同，目的取向也不同。

如果還有任何問題可再詢問我。
