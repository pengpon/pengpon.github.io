---
layout: post
title:  "Linux基本指令[中][I/O Redirection]"
date:   2019-11-07 21:30:00 +0800
author: Pon
categories: studygroup
tags: linux
---

11/7讀書會筆記

主講人:帆哥

# Review


## echo取用變數

利用**echo**讀出變數的內容，且變數在取用時，必須加上$符號。

> echo $PATH　或是 echo ${PATH}
>
> PATH為執行檔的搜尋路徑，目錄之間會以冒號分隔
>
> 相同指令, 會先從先找到的目錄內的執行

![echo $PATH](https://imgur.com/jFSNwjD.jpg)

## which指令(找重複指令)

> cal -a -b- -c = cal -abc (簡寫才能合併)
>
> cal --univesal --test (full name)
>
> man -k command  (k=keyword)



# 今日重點-I/O Redirection

Redirection用來處理standard input、standard output及standard error的重要功能。

將指令執行的輸出導向到檔案或是把程式/指令需要的參數由檔案導入。也可以處理執行時產生錯誤訊息的導向。



## command-Input

- command argument
- standard input

## command output

- standard output (簡稱stdout)
  - 指令執行回傳的正確訊息
- standard error (簡稱stderr)
  - 指令執行失敗後回傳的錯誤訊息

**無論正確或失敗，未指定都是輸出在terminal(螢幕)上!**

可以透過**Redirection**(資料流重導向)將stdout和stderr指定分別輸出的位置!

Data string number:

- 0: standard input，<或<<
- 1: standard output，>或>>
- 2: standard error，2>或2>>

## 關於cat(concatenate)

印出檔案內容或是合併多個檔案

cat指令依照順序讀取每個檔案並把內容送到standard output(terminal)。

Ex: cat test.txt 是將test.txt內容輸出到螢幕上顯示。沒有給檔名或是arguments時，cat指令會從standard input(鍵盤)讀取資料。

Ex: cat test1.txt test2.txt > testall.txt 是將test1&test2內容合併放入test3中。

---

## cat 實作output

將輸出結果移至別的地方-->Redirection

cat 1>dest 輸出的內容轉到dest  ，寫法等於= cat > dest  (1是預設)

cat >dest (覆寫dest)

cat >>dest (append累加至dest中)

cat 1>> out.txt 2>>err.txt  (stdout寫入out.txt中; stderr寫入err.txt中)

sssss 1>>output.txt 2>>error.txt (執行sssss，執行後將正確訊息輸出到out.txt; 錯誤訊息輸出到error.txt)

因為並沒有sssss這個檔案可執行，所以**-bash:sssss: command not found**這串訊息會被存入error.txt.中

cat 0<input.txt = cat <input.txt

ctrl_alt_f2

> 另開一個terminal (dev/tty2)
>
> 在tty1 >cat >/dev/tty2 會在tty2 terminal出現output

## cut擷取字元

把指定欄位抓出來

-d 分隔字元

-f 輸出範圍

cut <out.txt --delimiter " " --fields 1-2 (以空格為分隔，輸出第一個及第二個欄位)

---

## piping

> date | cut --delimiter " " --fields 1-2
>
> date > output.txt | cut --delimiter " " --fields 1-2

## tee 雙向Redirection

">"會將資料流**整個**傳給檔案

將收到的資料分成兩份，1份給file，1份給螢幕(stdout)

<img src="https://imgur.com/WogWCfR.jpg" alt="tee" style="zoom: 50%;" />

> ls -l 
>
> ls -l  >>temp.txt | grep john   (X)
>
> redirection 會破壞pipeline

(grep 擷取關鍵字)

> ls -l | tee temp.txt | pipe command
>
> date | tee date.txt | cut --delimiter' ' ' --fields 1-3



## XARGS參數代換

=x(乘號)+arguments(參數)

產生某個指令需要的參數!

會使用**xargs**是因為很多指令不支援pipe指令，所以可以透過xargs提供指令要的input!

ex: rm不支援pipe

cat deletedlist.txt | xargs rm

(deletedlist.txt中 存有兩個檔案名稱 test1.txt & test2.txt )

(cat deletedlist.txt 讀入此檔案，將資料分隔成arguments，作為下一個指令的input)

# 延伸閱讀&參考圖文

[Linux Terminal:the tee command](https://linuxaria.com/pills/linux-terminal-the-tee-command)

[鳥哥ch.10 認識與學習BASH](http://linux.vbird.org/linux_basic/0320bash.php#redirect)





