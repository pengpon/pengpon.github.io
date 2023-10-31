---
layout: post
title:  "Linux Beginner"
date:   2019-09-02 20:59:00
author: Pon
categories: Linux
tags: OS
---
# 前言

複習無數個上周前的帆哥Linux起手式&搭配鳥哥網路資源

- What is Linux?
- Unix歷史
- Linux發展
- Linux目前應用
- How to learn?



## 在開始之前-計算機概論應該知道些什麼??

計算機定義:

**接受使用者輸入指令與資料，經過中央處理器的數學與邏輯單元運算處理後，以產生或儲存成有用的資訊**

**因此只要有輸入及輸出設備，讓使用者可以輸入資料使機器產生資訊的，就是一部計算機**

硬體拆解來看可分成:

- 輸入

  > 鍵盤、滑鼠、讀卡機...

- 輸出

  > 螢幕、印表機

- 系統(主機)

  > CPU(Central Processing Unit)、主記憶體(RAM)

  整台主機最核心重點在於CPU，CPU主要工作為管理和運算，所以CPU可分為**算數邏輯單元**（負責程式運算和邏輯判斷）和**控制單元**（協調各元件的工作）。

  CPU容量V.S.速度

  ​	以有沒有通電來判斷資料，0/1這樣的二進位單位稱為bit。

  - 1 Byte=8bits
  - K=1024 byte
  - M=1024 K

  

  ​	運算速度常用MHz或是GHz的單位(Hz=秒分之一，赫茲)

  CPU時脈:**CPU每秒鐘可進行的工作次數**

  EX:i7-4790 時脈為3.6GHz 表示CPU在一秒內可進行3.6 X 10^9次工作

  

  CPU讀取的資料來自主記憶體，處理完的資料也是寫回主記憶體中。

  推推[TED-Ed Inside-your-computer](<https://www.youtube.com/watch?v=AkFi90lZmXA>)動畫版

  > 1. 按下滑鼠
> 2. 發送滑鼠位置的資訊
  > 3. 電腦接收訊息
  > 4. 由Input-Output sub-system(BIOS) 負責收訊息 (似電腦的守門員)
  >
  > * sub-system提供電腦一個方法去和電腦環境做互動 (同時也是buffer的角色)，防止CPU被不重要的程式霸佔住
  >
  > 5. sub-system通知CPU
  >
  > - CPU主要的工作:從記憶體拿取指示並執行
  > - CPU處理的每一個事物，都有一個程式，滑鼠有個專門的程式、處理鍵盤Key的文字也有
  > - 這些程式是人撰寫出來的，程式會被整合並縮小，以0和1的方式儲存在記憶體中。
  >
  > 6. CPU需要指示去處理滑鼠被點擊的事情
  > 7. CPU查詢滑鼠的程式
  > 8. 發送請求給記憶體的sub-system讀取儲存在那的指示
  > 9. 拿到滑鼠驅動程式的每一個指示並執行
  > 10. 若點擊時的游標有經過畫面上的按鈕
  > 11. CPU同樣也會要求記憶體提供顯示器的程式，判斷出滑鼠按了哪裡
  > 12. CPU再要求提供按鈕的程式，判斷是否要改變畫面的顯示

   BIOS:Basic Input Output System是一套程式，寫死在主機板上的一個記憶體晶片中，開機時BIOS控制各項硬體參數。

  

### Linux起手式筆記

> 計算機概論 自己讀!!

作業系統 會統籌各個硬體 軟體 

- 應用程式>系統呼叫>核心>硬體
- [作業系統] : 系統呼叫+核心

#### UNIX

> 為Linux原生
>
> 推推恐龍書 Operation system

- 批次型作業系統

  > 以讀卡機為輸入設備 印表機為輸出

- 相容分時作業系統

  > 允許多個使用者切換使用 快速切換資源

- Multics計畫

  > 以組合語言寫出小型檔案系統 即UNIX原型

**以C語言改寫UNIC 成為現在的UNIX **



#### UNIX演化

> AT&T 推出SystemV 第七版 UNIX 可移植到X86個人電腦
>
> 限制政策開始
>
> Minix出現 
>
> Torvalds推出Linux0.02版
>
> 後續有大量"駭客"加入 共同協做
>
> 1994年 推出 Linux 1.0  並加入X Windows System (Linux的GUI介面)

#### Linux distributions

> 自行整合其他功能 再發佈出來
>
> 整合Linux kernel 自己的軟體

- 常見distribution
  - RHEL >企業
  - Ubuntu >個人
  - CentOS > 個人
  - Fedora >個人

#### 磁碟分割

> 實體裝置: /dev/sd[a-]
>
> 虛擬裝置: /dev/vd[a-p]
>
> a槽>軟碟機

- MBR 主要開機記錄區 (最多支援到2.2.T磁碟分割)
- GPT (GUID partition table)



8 bits= 1 bytes

磁碟上第一個磁區(512 bytes):

1. 紀錄MBR (446)
   - 用4組記錄區
   - 主要vs 延伸(邏輯分割)
2. 分隔表 (64)

> 分割好處: index概念 搜尋快速



GPT:可記到8ZB (8 *2^30)



#### 電腦開機順序

- BIOS
- MBR
- Boot Loader
  - 提供開機選單
- 執行系統核心檔案



