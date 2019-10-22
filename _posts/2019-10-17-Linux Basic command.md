---
layout: post
title:  "Linux基本指令[上]"
date:   2019-10-17 22:00:00 +0800
author: Pon
categories: studygroup
tags: Linux
---



10/17讀書會筆記

主講人:帆哥

# Linux基本指令

指令構成 command [-options] param1 param2

-簡寫

--全名

-y =--year  (可能有例外)

option and param用**空格**區分隔

太長的指令 用\跳脫enter字元

ex: ls +enter 

ex: ls \   >>不會執行 **等待繼續輸入**

反斜線指跳脫下一個字元 

ls \enter 和 ls \ enter

**有區分大小寫**

cd CD不同!! 



## 常用指令-檔案和目錄管理

---

### ls:List

- ls
- ls -al 
- ls     -al ~   波浪符號代表home的位置
- ls -a  -l   ~

**列出當前目錄的東西**

-a 代表全部(包含隱藏檔案)

-l 用row方式表示

---

### pwd: print word directory

印出目前工作目錄

---

### cd: change directory

移動進入某資料夾

---

### mkdir: make directory

建立新資料夾

---

### cp: copy

複製檔案

---

### mv : move or rename files

移動或是重新命名檔案

---

### tail 

顯示檔案最後幾行

**常用於debug**

ex: tail -f catalina.out 代表持續偵測catalina.out的內容

---

### rm: remove file

刪除檔案

- rm -rf / 
- 刪除根目錄下所有檔案 f>force r>遞迴(所有資料夾下所有檔案)

---

## 其他工具

### cal

顯示月曆

- cal [month] [year]
- cal 6 1989

---

### bc

計算機

- scale=3 設定浮點數
- quit 或是ctrl+c 離開bc

---

### date

顯示日期

- date
- date +%Y/%m/%d
- date +%H:%M

---

## 重要熱鍵

- tab 自動補完 (命令補全或檔案補全)
- ctrl +c 中斷 
  - find /   按下ctrl +c 中止
- ctrl +d 登出 = exit
- shift +[fn] +up or down



---

## 錯誤訊息

- command not found 出現原因
  - 指令不存在
  - 軟體未安裝

---

## 求助指令

- --help 建議是用過的指令

- man date 詳細說明 空白鍵下一頁
  - /string 向上搜尋關鍵字
  - ?string 向上搜尋

---

## 指令文檔查詢

- man  -f  ls  用command查詢
- man -k keyword 用keyword查詢
  - 如果出現nothing appropriate 執行mandb or makewhatis
- whatis command = man -f
- apropos command = man -k
- info 將文章拆多段落顯示 每個頁面為node
- info ls  (lnfo下按h有使用說明)

---

## nano 文書編輯器

其他 vi , vim

vi

- esc > : > w > q
- write quit

who: 查看誰在線上

netstat -a 查看連線狀態

---

## 關於關機

cpu 從記憶體抓資料

當cpu執行完 也是先放入記憶體 才放入硬碟

資料遺失的原因

建議沒有人在線 才執行關機

強制將資料寫入硬碟 sync

**cpu只能處理記憶體中的資料**

重開機 reboot/ halt/ shutdown 皆會在執行前執行sync

一般帳號使用sync只會同步自己帳號的資料回硬碟

root使用sync會同步整個系統資料

**如果是透過putty工具遠端登入主機 只有root可以下關機指令**

shutdown -h 10 'will shutdown'

可以提示訊息

shutdown -k 不會真的關機

底層都是執行 **systemctl poweroff** or **systemctl reboot**



---

# 延伸閱讀

[Linux 基本指令介紹-鳥哥](http://linux.vbird.org/linux_basic/redhat6.1/linux_06command.php/)

[Linux Command 命令列指令與基本操作入門教學](https://blog.techbridge.cc/2017/12/23/linux-commnd-line-tutorial/)

[首次登入與線上求助-鳥哥 Chapter 4](http://linux.vbird.org/linux_basic/0160startlinux.php#date)