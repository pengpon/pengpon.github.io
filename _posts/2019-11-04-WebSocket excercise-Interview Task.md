---
layout: post
title:  "Websocket 小實作"
date:   2019-11-04 16:16:00 +0800
author: Pon
categories: web
tags: interview 
---
> 起源於interview某家公司出的小作業
>
> **實作一個桌機與手機互動的小demo**
>
> 紀錄其中的過程

# 起源

公司提供了一個參考影片，影片中的桌機畫面是一個web動畫，以及一個行走中的小角色

影片中的人拿著手機，以橫向翻轉手機時，桌機動畫裡的場景會改變，ex:白天-黑夜

可能也會改變動畫故事的發展

---

# 發想

首先survey了手機內含的感測器，主要常見的像是

- 近距感測器(Proximity Sensor)

  透過接受到的紅外線強度判斷距離，可以偵測通話時是否貼在耳朵，決定是否關閉螢幕。

- 環境光(光度)感測器(Ambient Light Sensor)

  感測環境光線的強度，用來調節手機螢幕亮度

  白天提高螢幕亮度；夜晚降低螢幕亮度

  提高使用者舒適程度也能延長電池壽命

- 加速度計(Accelerometer)

  切換橫直向螢幕或是計步

- 磁感測器(Magnetism)

  測量電阻來判斷磁場強度，應用在指南針或是地圖導航

- 陀螺儀感測器(gyroscope)

  常看到的應用像是:用手機模擬方向盤的賽車遊戲、槍擊遊戲，GPS導航，拍照時會偵測裝置晃動程度以方便處理出穩定的照片

- GPS

  裝置裡的GPS模組透過衛星的瞬間位置計算距離，用在定位、測速、測量距離。

要讓使用者最能上手操作的變因，首選應該就是**裝置的方向**

## 互動內容

既然決定讓使用者透過裝置的方向或是加速度來改變某些事件

下一步就是關於**到底要做什麼內容**

過去有關的經驗不外乎就是利用裝置當作方向盤的賽車遊戲

模擬出一種**身歷其境**的體驗

開始想...現實生活中有哪些事情

或有需要搖晃或是控制方向的事物/物體

配合生活經驗，剛好這陣子迷上幸運餅乾籤詩，但幸運餅乾沒有可以模擬的動作

於是決定改類似概念-採用**廟裡搖籤抽運勢和籤詩**作為方向

---

# 素材

決定內容後，上網開始找圖庫找素材找靈感

[Flaticon](https://www.flaticon.com/)-PPT需要小icon吸睛時，很推! 或是[Freepik](https://www.freepik.com/)

剛開始卡在英文關鍵字不容易下，而且目標物又是比較偏東方的東西

fortune paper , temple, lottery 搜尋出來都不是想要的

於是利用google的圖片搜尋

看到一張日本籤筒的小插圖, 根據上面寫的平假名(Omikuji)，再用google搜尋

找到一張滿意的圖片，決定用illu重製復刻它

把內容項目分圖層、背景圖畫好後，再輸出成圖檔

<img src="https://imgur.com/ckaOmKw.jpg" alt="illu復刻" style="zoom:50%;" />

<img src="https://imgur.com/DfSSgBK.jpg" alt="輸出需要圖檔" style="zoom:50%;" />

---

# Wireframe&Prototype

![wireframe](https://imgur.com/VAeBRKt.jpg)

構思流程大約是

1. 桌機進入首頁畫面，一小段animation(背景淡入and籤筒浮現)

2. 桌機畫面會提示使用者也用手機裝置登入

3. 手機裝置進入同一個網頁後，出現shake的字樣
4. server偵測到手機裝置的加速度值改變，觸發註冊事件(事件為跳窗方式顯示籤詩結果)
5. 桌機畫面出現抽籤結果

---

# 切版

進入到撰寫HTML&CSS的部分

主要用到css-position定位

以及根據呈現方式寫腳本(css-animation-keyframes)

背後大大小小的籤則是使用parallex.js 呈現視差的效果

關於提示訊息或是跳窗的css部分，找了不少在網路上的素材參考(copy-paste...)

推推[Free Frontend](https://freefrontend.com/)-整理很多線上範例都很fancy很可愛~(也許比較適合side project用)

Free-Frontend網站選單分三大項:

1. HTML+CSS

   再細分html example& css example

   比如常需要做的頁面404,500，這個網站也有整理一個主題出來

   ![html-example](https://imgur.com/iL56y1q.jpg)

   EX: 500 Error Page HTML Templates

   這篇主題中整理的了13種500 error page

   ![500 error page](https://imgur.com/qsH2huD.jpg)

   底下會附上一些基本資訊

   最重要的會有demo和code的連結,以及使用的工具(html/css or javascript)

   CSS Code examples的部分，很多都是純css寫出很厲害的效果，很值得看看

2. JAVASRIPT

3. BOOKS

   整理很多線上免費電子書，分類齊全Angular,HTML&CSS,Javascript,NodeJS,React



---

於是頁面拼拼湊湊後逐漸完成



- web開啟的首頁畫面-提示另外再用手機開啟**google**瀏覽器進入此頁面

![Web-首頁](https://imgur.com/QoxTGWX.jpg)

- 手機裝置開啟的畫面-提示使用者shake shake!!

<img src="https://imgur.com/GWITwJm.jpg" alt="mobile-page" style="zoom: 25%;" />

- 最後於web畫面顯示結果

![web-result](https://imgur.com/j5F4tDN.jpg)

---

# Server端&Client端

直到切完版才驚覺這個demo要練的應該是WebSocket(?)

## WebSocket

它是網路協定的一種，讓Client可以透過這個協定與Server溝通

只要連結上了，就可以保持互動

(和Http/Https 要一直發送request 收response不一樣)

當device orientation數值達標時，向server傳訊息

sever收到指定訊息後，再統一向所有的client的推送訊息

(即時聊天室也可以用websocket做)

利用node.js 的websocket

## Server

建立一個本機的server

```javascript
// 匯入express和ws套件
const express = require('express');
const SocketServer = require('ws').Server;

//預設開啟3000 Port
const PORT = process.env.PORT || 3000;

//建立express物件,console中顯示"Listening on xxxx PORT
const server = express()
    .listen(PORT, () => console.log(`Listening on ${ PORT }`));

// 開啟WebSocket服務
const wss = new SocketServer({
    server,
});


//WebSocket 從外部連結時執行
wss.on('connection', ws => {
    //有連結時,即開啟brower進入index.html時(不同分頁算不同client)
    //console顯示"Client connected"
    console.log('Client connected')

    //對 message監聽，接收從 Client 發送的訊息data
    ws.on('message', data => {
        //取得所有連接中的 client
        let clients = wss.clients;

        //發送data訊息至每個 client
        clients.forEach(client => {
            client.send(data)
        })
    })

    //連線關閉時 console顯示"Close connected"
    ws.on('close', () => {
        console.log('Close connected')
    })
})
```

## Client

```javascript
// 在本機run server.js已指定3000 port 
//ex:let ws = new WebSocket('ws://localhost:3000')   
let ws = new WebSocket('ws://xxxxx:3000');
        
// connenction start
ws.onopen = () => {
    //browser console 顯示"open connection"
   console.log('open connection');

    // 是否支援DeviceMotionEvent
   if (window.DeviceMotionEvent) {
       //監聽devicemotion
      window.addEventListener('devicemotion', function (event)  {
         // x,y,z 三個方向的加速度值(m/s^2)
          var x = Math.round(event.acceleration.x);
          var y = Math.round(event.acceleration.y);
          var z = Math.round(event.acceleration.z);
          x = Math.abs(x);
          y = Math.abs(y);
          z = Math.abs(z);
		
          //三個方向的加速度值相乘大於300, 傳送'shake'訊息給server
          if ((x * y * z) > 300) {
              ws.send('shake');
           }
          }, true);

   } else {
     	console.log('only support mobile');
     }
 }

//after close, run something action
ws.onclose = () => {
	console.log('close connection');
}

ws.onmessage = event => {
    if (event.data == 'shake') {
        // Receive the "shake", show the fortunepaper result
        let modal = document.getElementById("open-modal");
        modal.setAttribute('style', "visibility:visible;opacity:1;pointer-events: auto;");
            }
        }
```

目前照這樣的設計，多個Client對到同一個server

只要有一個client觸發了shake, 所有client的modal就會被開啟

要再進一步調整server的寫法

以上!

# 延伸閱讀&參考圖文+code

 [HTML5控制裝置陀螺儀(三軸)](https://www.oxxostudio.tw/articles/201506/html5-device-orientation.html)

 [Using Device Orientation in Html5](https://www.sitepoint.com/using-device-orientation-html5/)

 [Detecting device orientation](https://developer.mozilla.org/en-US/docs/Web/API/Detecting_device_orientation)

 [An Introduction to the Device Orientation API](https://code.tutsplus.com/tutorials/an-introduction-to-the-device-orientation-api--cms-21067)

 [多重感測器陣列加持 行動裝置增添智慧通知功能](https://www.2cm.com.tw/2cm/zh-tw/tech/02E0D418D703490D84A8B84FBDD49D24)

[ 手機傳感器](https://ek21.com/news/2/9655/)

[JavaScript | WebSocket 讓前後端沒有距離](https://medium.com/enjoy-life-enjoy-coding/javascript-websocket-%E8%AE%93%E5%89%8D%E5%BE%8C%E7%AB%AF%E6%B2%92%E6%9C%89%E8%B7%9D%E9%9B%A2-34536c333e1b](https://medium.com/enjoy-life-enjoy-coding/javascript-websocket-讓前後端沒有距離-34536c333e1b)

[Multi-screen Experience : Websites that Sync with Mobile](https://medium.com/@saijogeorge/multi-screen-experience-websites-that-sync-with-mobile-b82f0a90d9aa)

[Bubble感的button](https://codepen.io/leenalavanya/pen/aXMXvz)

[Build website animations and interactions visually](https://webflow.com/interactions-animations)

