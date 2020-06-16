---
layout: post
title:  "Linux基本指令[下]"
date:   2020-06-16 13:38:00 +0800
author: Pon
category: Linux
tag: linux
---

> 長達近一年讀書會的Linux帶狀課程，畫下一個暫時的逗點，順帶筆記在工作上遇到的指令。

<br>

# wildcard 

用來表示一個字元以上的符號! 常用來替代字串中的任何字元。

例如可以利用wildcard得到某路徑下檔名都是o開頭的檔案清單。

## 常用的三種型式

- `?`

  對應的1個任何字元，1個是1個!

  ex:`o??d` 會找到任何開頭是o、結尾是d以及中間有兩個字元的字串(`oind`, `oggd`)

- `*`

  對應到任何0個以上的字元，0個是0個!!

  ex:`o*d`會找到開頭是o、結尾是d，中間有幾個字元不重要! (`ofeifhefheuid`, `od`)

- []中括號

  必須要和中括號裡的字元匹配，任一個字元! 

  ex: `o[ac]d`符合的是`oad`,`ocd`，`[abcd]`===a or b or c or d

  也可以用range表達, ex: `o[a-c]d`符合的是`oad`,`obd`,`ocd`



<br>

# Brace expansion

範例取自[Bash Brace Expansion](https://www.linuxjournal.com/content/bash-brace-expansion)



`{}`通常被用來產生

用`,`當區隔, `..`表示區間

`{aa,bb,cc,dd}` ===> aa bb cc dd

`{0..12}`			===> 0 1 2 3 4 5 6 7 8 9 10 11 12

`{3..-2}`			===> 3 2 1 0 -1 -2

<br>

有特定開頭或是結尾也ok

`a{0..3}b` 		===>a0b a1b a2b a3b

<br>

巢狀也行

`{a,b{1..3},c}`，外到內拆 ===> a b1 b2 b3 c

<br>

不使用`brace expansion`也行

```shell
# Three expression for loop:
for (( i = 0; i < 20; i++ ))
do
    echo $i
done
# While loop:
i=0
while [[ $i -lt 20 ]]
do
    echo $i
    let i++
done
# For loop using seq:
for i in $(seq 0 19)
do
    echo $i
done

```

使用`brace expansion`

```shell
for i in {0..19}
do
    echo $i
done
```

除了產生連續數字外,連續的字母也可以

```shell
for i in {a..z}
do
    echo $i
done
```

<br>

## 練習精選

- 產生目錄，名稱為jan_2017,feb_2017,mar_2017 ~dec_2022(月份1~12月, 年份2017~2022)

  ```shell
  mkdir {jan,feb,mar,apr,may,jun,jul,aug,sep,oct,nov,dec}_{2017..2022}
  ```

- 在上述目錄下建立1~100.txt

  ```
  touch {jan,feb,mar,apr,may,jun,jul,aug,sep,oct,nov,dec}_{2017..2020}/{1..100}.txt
  ```



<br>

# Schedule jobs

## 1. crontab

cron 是Linux用來定期執行工作任務的program

cron program會每分鐘去check設定檔，並執行設定檔中的command

```shell
00 21 * * * root rm /home/bob/trash/*
```

由左到右可以切成七個欄位看

- 分 (0-59)
- 小時 (0-23)
- 每月中的第幾日 (0-31)
- 月份 (1-12)
- 一周中的第幾天 (0-7, 0和7代表星期天)
- 執行command的帳號
- 要被執行的command

<br>

`*`代表所有值

`,`用來區隔每個值

`-`用來表示範圍

`/`代表間隔

所以`00 21 * * * root rm /home/bob/trash/*`

代表`rm /home/bob/trash/*`這個指令會在每個月的每一週的每一天的21:00由root執行!

p.s. 周和日月不能共存

如同鳥哥範例:`30 12 11 9 5 root echo "just test"`無錯誤寫法，照翻雖然可以解釋為9/11且為星期五那天的12:30要執行，但系統可能會誤判成每周五或是每到9/11要執行!

鳥哥也說這個不共存原因已修正，用[crontab guru](https://crontab.guru/#0_12_11_9_5)驗證也好像沒事，但依舊不推這種指定特定日期執行方式，畢竟crontab是用來設定週期工作!



<br>

`crontab -e` 編輯工作排程

`crontab -l` 檢視目前工作排程

<br>

## 2. anacron

anacron會去偵測系統未執行的crontab工作，適合用在一些沒辦法總是保持關機的系統。

當重新開機時，anacron程式啟動後，anacron會去檢查anacron中的工作是否有執行，如果未執行，會在anacron設定好的delay時間執行一次!

> with **anacron**, you can be sure that the job will run once the system comes back up

```shell
1 3 rm.command rm /home/bob/tmp/*
PERIOD DELAY JOB-IDENTIFIER COMMAND
```

PERIOD: anacron執行當下和時間戳記相差的天數，超過設定的天數就執行指令

DELAY: 當超過天數要執行工作排程時，執行的delay時間，避免大家都在開機後通通同時執行

JOB-IDENTIFIER:工作名稱命名

COMMAND 實際要執行的指令

所以`1 3 rm.command rm /home/bob/tmp/*`解釋成 script每天只會run一次，當anacron啟動後三分鐘執行。這項工作排程名稱為`rm.command`，實際會執行`rm /home/bob/tmp/*`

<br>

# 其他Note

`rmdir`只能刪空目錄

`rm filename`可以刪資料夾或檔案

`rm *[2]*.txt`刪除檔名中有2的txt檔案

---

`cp file1 [file1 file3..] dest`

`cp -r srcfolder destfolder`

**destfolder不存在會幫你建!!**

----

`mv srcfile destfile` 複製或是改名

----

`locate` 尋找檔案

`find`多元查詢

~type, ~name, ~size

---

`cat file1 [file2 file3]`檔案合併

----

`touch {cat,dog}.txt` 建立檔案

----

`tac`由檔案偉開始讀 (行數倒過來)

`rev` 每一行字元反向讀

`less`限制輸出結果

`head`顯示前幾行

```shell
find ~ | head 
// default 10

find ~ | head -n
head -n 10 filename
```

`tail`顯示最後幾行

```shell
tail -n 40 filename
tail -f filename
// -f:會持續顯示檔案更新資訊
```

`sort file`

-r:反序

```shell
ls /etc 列出etc目錄檔案
ls /etc | head -n 20 限制顯示20筆
ls /etc | head -n 20 | sort -r 透過pipe排反序
```

-k:指定欄位排序 (第一欄為1)

-h:human readable (ex:檔案大小以k表示)

-M:日期排序

-n:以數字排序(小到大)

----

`grep`尋找關鍵字

-i: case insensitive不分大小寫

-c: line count

-v: invert match

**補充昱廷踩到雷**

mac git版控不分大小寫，ex:變動內容為把appservice改成Appservice

對git來說，不算異動~

`git config core.ignorecase ture`參考

----

`archive`打包

```shell
tar [option] file src
-c:create
-x:extract
-t:list content of archive
-v:訊息印出
-f:輸出檔名
tar不會壓縮檔案
```

<br>

`gzip` 壓縮，壓縮比不高，速度快

```shell
gzip tarfile
gunzip gzfile

-k 保留原始檔案
```

<br>

`bzip2` 壓縮比高

<br>

`zip` 常用在mac/windows

p.s.: gzip,bzip用在Linux

<br>

```shell
tar -cvzf file.tar.gz srcfile
// 自己打完整檔名
```



<br>

# 延伸閱讀&參考圖文

[Wildcard](https://geek-university.com/linux/wildcard/)

[Bash Brace Expansion](https://www.linuxjournal.com/content/bash-brace-expansion)

