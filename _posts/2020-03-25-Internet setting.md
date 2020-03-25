---
layout: post
title:  "如何查看家中網路設定"
date:   2020-03-25 20:22:00 +0800
author: Pon
categories: web 
tags: internet
---



> 如同demo魔咒般，分享完網路篇後，家裡網路就斷了
>
> 於是剛好來瞧瞧家裡網路怎麼牽的



# 網路設備

一般來說，會跟電信商申請網路

以我們家的例子，是向中華電信申請網路

利用電話線路分離低頻的電話語音&高頻的ADSL訊號

於是，在ADSL這樣的架構下，家中就會有一台數據機(modem 俗稱小烏龜) 機型很多種

大致會長得像這樣

![數據機](https://imgur.com/CCBuhjP.jpg)

背面-圖片取自(https://blog.xuite.net/aa801862/wang/85400197-I-004-使用重裝備架設高速區域分享)

![背面](https://imgur.com/OyW6oh9.jpg)

- 變壓器: 即power
- Ethernet 1~4連接路由/電腦 (黃色孔): 提供需要上網的設備，連到桌機 or 中華電信mod 
- VDSL2: 外部的牽進家裡的網路線
- POTS: 牽進家裡的電話線

**除了會有一台modem，還會有個分歧器的裝置，因為線路是電話和網路共用，需要透過分歧器過濾頻段**

像是這樣

![網路設備](https://imgur.com/MaWKUGZ.jpg)

1. 牆壁電話線牽進家裡
2. 這條線進到分歧器，並接上數據機的VDSL孔 (分歧器會區分電話和網路的頻段)
3. 用一條電話線連接數據機的POTS孔和電話  
4. ETHERNET連接家裡的設備(ex:桌機&MOD機上盒)
5. 有的數據機具有wifi功能，設定後，數據機本身可以發送無線波訊號給裝置連線用; 如果沒有就是再接一條ETHERNET連到無線分享器，發送訊號!





# 查看網路

假設遇到家裡wifi網路無法對外但可以連線，可以登進數據機看相關設定

1. 連到家裡wifi，瀏覽器開啟設定數據機/路由器畫面　(預設會是192.168.1.1，帳密user/user)

   ![登入畫面](https://imgur.com/Nmw3fcV.jpg)

2. 系統設定的基本資料

   ![基本設定](https://imgur.com/DaCxDOX.jpg)

這台數據機是對外的路由器，正常情況下，它會拿到一組中華電信配發的IP位址

路由器再動態分配IP給區域網路中的裝置!

但可以看到網際網路資訊中，網際網路的IP是空的

所以種種跡象:

- 有出現wifi名稱可以連
- 接有線的設備也無法使用(MOD機上盒)
- wifi連上後，無法正常上網

合理推斷:

- 數據機的wifi功能沒壞
- 同網段的設備還是可以連線(能利用wifi連上數據機設定畫面)
- 沒有拿到對外ip

所以排除完接觸不良或是數據機壞的的可能，撥打中華電信客服報修!



# 其他

這個設定頁面還有幾項設定或是資訊可以看

- wifi設定

  ![wifi](https://imgur.com/ruzIdOp.jpg)

- 無線網路的連線列表(列出裝置MAC位址，路由器靠MAC來辨識在它旗下的裝置)

  ![連線列表](https://imgur.com/nC3NR5U.jpg)



# 延伸閱讀&參考圖文

http://kung.byethost31.com/web/sonet/about_adsl.html?i=1

http://www.vr.ncue.edu.tw/esa/a1012/ch09.pdf





