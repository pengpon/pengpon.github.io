---
layout: post
title:  "WebSocket初介紹"
date:   2019-11-06 15:48:00 +0800
author: Pon
categories: web
tags: real-time html websocket
---

> WebSocket 是一種讓瀏覽器與伺服器進行一段互動通訊的技術。可以直接進行即時的通訊而不用一直輪循(Rolling)-擷自[MDN web docs](https://developer.mozilla.org/)。為了更清楚瞭解websocket，紀錄一下它發展的過程還有背後使用的技術。

# 關於Real-time

web建立在client和server身上，client的工作就是向server請求資料；server的工作則是去回復每一個client的請求(如下圖)。這樣的一來一往的模式持續了多年，2005年隨著AJAX的出現，於是大家開始摸索**client-server**雙向溝通的可能性。

<img src="https://imgur.com/jzEvRJA.jpg" alt="simple" style="zoom:67%;" />

Source:[WebSockets - A Conceptual Deep-Dive](https://www.ably.io/concepts/websockets)

web application開始發展快速，最大的挑戰在於**HTTP model of client initiated transactions**! 於是為了克服，不同的方法開始陸續出現像是**long-polling**-保持HTTP的連線開啟，直到server有data可以傳給client。

出現的解決方式大都是carry the overhead of HTTP.每次送出一個請求，伴隨著一堆header、cookie的資料要傳給server。

# 實現Real-time 

大致上有幾種方式:

1. Long/short polling (Client pull)
2. WebSocket (Server push)
3. Server-Sent Events (Server push)

- client pull- client端週期性的向server詢問，update特定資料

- server push- server端主動告訴client有資料要更新



<img src="https://imgur.com/j63vlB4.jpg" alt="3 ways for real-time" style="zoom:80%;" />

Source:[Polling vs SSE vs WebSocket— How to choose the right one](https://codeburst.io/polling-vs-sse-vs-websocket-how-to-choose-the-right-one-1859e4e13bd9)



## 1. Polling(輪詢)

   > Polling is a technique by which the client asking the server for new data regularly.
   >
   > 分成兩種short polling/ long polling
   >

### Short Polling

   - short polling is **AJAX**-based timer
- A client makes XHR(XMLHttpRequest)/Ajax requests to server **repeatedly at some regular interval** to check for new data.
- 週期性的一直發出Request
- 易實作、無跨瀏覽器問題
- 效率差、浪費頻寬

### Long Polling(comet的改良進化)

   - long polling is based on **Comet**(當server有event發生，server傳送data給client)
- Long polling is technique where the server elects to **hold a client connection open** for as long as possible, delivering a response only after **data becomes available** or **timeout** threshold has been reached. 
- 發出一個長時間的等待Request，當有資料或是timeout時，再發一個新的Request

<img src="https://imgur.com/aWFmzPy.jpg" alt="long-polling" style="zoom:67%;" />

Source:[WebSockets - A Conceptual Deep-Dive](https://www.ably.io/concepts/websockets)

</br>

## 加映:關於AJAX(Asynchronous Javascript and XML)

   與傳統網站不同在於，Browser(Web page)自行建立Request送給Server，並處理傳來的Response。Ajax模組提供一個中間層(Ajax Engine)來控制溝通過程，Ajax engine即向server請求資訊時要呼叫的Javascript物件。

   <img src="https://imgur.com/eBMdNL7.jpg" alt="AJAX theory" style="zoom:50%;" />

### 使用方式

   - XMLHttpRequest(舊式寫法)

     - 取得browser提供的**XMLHttpRequest**物件(XHR) 

     - 不限接受XML類型的資料，亦支援HTTP外的協定(ex:file, ftp)

     - XMLHttpRequest會回傳每次的狀態(readystate):

     - ```javascript
       //產生XMLHttpRequest物件實體
       const xhr = new XMLHttpRequest(); 		
       // readystate狀態
       // 0-已產生xhr,還沒呼叫open
       // 1-已open,尚未傳送出去
       // 2-已send
       // 3-loading-解析內容
       // 4-已收到完整資料
       
       // 每次變化都會觸發readystatechange事件,造成readystate值改變
       xhr.onreadystatechange = function() {
         if (xhr.readyState === XMLHttpRequest.DONE && xhr.status === 200) {
           document.write(xhttp.responseText)
         }
       };
       
       // open('method(get:讀取資料／post:傳送資料到伺服器)',url(要連的資源或檔案),async(true-同步;false-非同步)
       xhr.open('GET',"./xxx.txt",true);
       // true-非同步,不會痴痴等待
       // false-同步,等資料回來,才會繼續執行
       
       xhr.send(null);
       ```

       

   - 利用jQuery的ajax

     - $.ajax(url,[settings])

     - jQuery.ajax()提供的callback:依序為1.beforeSend-> 2.success/error -> 3. complete

     - ```javascript
       $.ajax({
           url: '',                        // 請求要送往的url位置orxxx.php
           type: 'post',                   // post/get
           data: {  },       				// 輸入的資料(Obj,string or array)-送給server的data
          	dataType,						// 期望server傳回的資料格式
           error: function (xhr) { },      // 錯誤->執行的函數
           success: function (response) { }// 成功->要執行的函數
           async:true,						// 同步與否
       });
       ```

---

## 加映:關於Comet

​	如同comet單字解釋一樣，**彗星**！使Request像彗星，拉的很長，於是可以不結束連線，讓server持續回傳data給client。作法有兩種：

- Ajax實現comet
- iframe實現comet

後來出現**改良的comet**，發出一個長時間等待的Request，當server有資料時，立即斷掉在發出一個新的Request。作法也有兩種：

- Long Polling

  browser發出一個request，server讓request持續開啟一段時間。在這段期間內server有資料就會回傳，如果沒有等到時間一到，server就會結束request，browser知道request被結束了，又會再發出一個新的request。

- Streaming

  讓server和client建立一個持續的連線，為了不中斷連線，server會每隔一段時間就發送Response給client，確保連線不中斷，server將資料傳入iframe，讓javascript去負責頁面的更新

---

<br>

有些網站會這樣描述**Polling**:出遠門時，小孩子會一直問**到了嗎到了嗎**，等同發送一個長時間等待的Request，當server端有data時，就發送新的request。

javascript 相關http的library像是**jQuery or Axios**可以使用。而利用**setTimeout & 遞迴**的方式(搭配ajax)一樣可以達到Long-Polling。

<br>

## 2. WebSocket

定義在HTML5中，提供了browser和server進行雙向通訊的技術-**WebSocket**，當連線完成，client端可以隨時send訊息給server，server也可以隨時推送訊息給client端。雙向且全雙工(bi-direction and full-duplex)，特別要注意的是各家瀏覽器的支援程度。



<img src="https://imgur.com/59Ne1Rm.jpg" alt="websocket" style="zoom:67%;" />

Source:[WebSockets - A Conceptual Deep-Dive](https://www.ably.io/concepts/websockets)

## 3. Server-Sent Events(SSE)

server端推送事件，透過HTTP協定，允許server向client發送數據的HTML5技術。如果client端不太需要傳送資料給server，只是負責接收資料，就可以考慮使用SSR單向的傳輸方式。

---

# Review-再回到Websocket

> 不只是應用在我們常聽到的**即時聊天室**上，其他像是要重複性的呼叫RESTful API、需要長時間才會回傳值的呼叫或是一個**live data**必須即時的顯示給使用者。 

1. client傳送一個HTTP請求給server

2. header中的**Upgrade**代表此client希望建立一個websocket連線

   ```http
   GET ws://websocket.example.com/ HTTP/1.1
   Origin: http://example.com
   Connection: Upgrade
   Host: websocket.example.com
   Upgrade: websocket
   ```

3. 如果server支援websocket協議，會回傳包含Upgrade header的response

   ```http
   HTTP/1.1 101 WebSocket Protocol Handshake
   Date: Wed, 16 Oct 2013 10:07:34 GMT
   Connection: Upgrade
   Upgrade: webSocket
   ```

於是**handshake**完成，而最初的HTTP連線被websocket連線取代(TCP/IP connection)。

![websocket lifecycle](https://imgur.com/b1q7IAi.jpg)

Source:http://jar.fyicenter.com/

# 小結

蠻幸運的在面試中，收到一個task實作，而有機會開始了解websocket，整理這篇的過程中有太多可以延伸的東西，**TCP? UDP? 網路層? ** 或是各種Real-time的實作code? 各大家產品是採用哪種方式解決Real-time?

期待再一點一點補齊基礎!!

# 延伸閱讀&參考圖文

[獲得實時更新的方法-Polling, Comet, Long Polling, WebSocket](https://blog.niclin.tw/2017/10/28/%E7%8D%B2%E5%BE%97%E5%AF%A6%E6%99%82%E6%9B%B4%E6%96%B0%E7%9A%84%E6%96%B9%E6%B3%95polling-comet-long-polling-websocket/)

[淺談 Polling, Comet, Websocket](http://f2e-veru.com/%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98/%E6%B7%BA%E8%AB%87%20Polling,%20Comet,%20Websocket/)

[5 ways to build real-time apps with Javascript](https://www.freecodecamp.org/news/5-ways-to-build-real-time-apps-with-javascript-5f4d8fe259f7/) 

[Polling vs SSE vs WebSocket— How to choose the right one](https://codeburst.io/polling-vs-sse-vs-websocket-how-to-choose-the-right-one-1859e4e13bd9)

[WebSocket 通訊協定簡介：比較 Polling、Long-Polling 與 Streaming 的運作原理](https://blog.gtwang.org/web-development/websocket-protocol/)

[An Introduction to WebSockets](https://blog.teamtreehouse.com/an-introduction-to-websockets)

[HTML5 的 Server-Sent Events 串流使用教學](https://blog.gtwang.org/web-development/stream-updates-with-server-sent-events/)

[WebSockets - A Conceptual Deep-Dive](https://www.ably.io/concepts/websockets)

