---

layout: post
title:  "Server to Client"
date:   2019-08-29 13:02:00 +0800
---



# 前言

關於瀏覽器怎麼運作??

輸入網址後發生了那些事??

網路運作的原理??

看起來在稀鬆不過的事，也是有很多眉角在其中

一點一點　補齊一點小小知識

![web browser work](https://imgur.com/NlpWPOl.jpg)

這篇主要想筆記 一年多前看到的文章https://alistapart.com/article/server-to-client/

**輸入網址後 發生了那些事?????**



### Server to Client

>  在browser渲染任何內容前，它必須知道它要去哪兒向誰要資料!

有三種方式可以做到:

1. 在網址列輸入網址 (Entering a URL in the address bar)
2. 點擊連結(clicking on a link on a page)
3. 點擊我的最愛中的項目(clicking on a favorite)

不管是哪一種，都叫做**Navigation**(先稱它為導向)

Navigation是第一步，有了它才有後續一連串的動作可以讓網頁載入!

### Initiating the request

> 一旦URL提供給browser後，會有以下事情開始動作!!

- Check for HSTS
- Check for service workers
- Check the network cache
- Check for connection 
- Establish connection
- Send the request to the server
- Handle the response



1. Check for HSTS

   首先瀏覽器必須判斷是否為HTTP request，如果是就需進一步check此網域有沒有儲存在HSTS (HTTP Strict Transport Security)清單中。

   > 在 SSL 中有一個很重要的機制叫做「**HSTS**」（**HTTP Strict Transport Security**），中文翻譯為「**HTTP 強制安全傳輸**」，就是告訴瀏覽器這個網站強制使用 HTTPS 協定，藉此減少連線過程可能遭遇的風險。開啟 HSTS 後未來瀏覽器就會自動將 HTTP 轉為 HTTPS 請求，即使憑證失效，使用者也無法忽略警告繼續瀏覽網站。

2. Check for service workers

   瀏覽器必須決定service worker是不是能夠處理當下的request，特別是在使用者離線以及沒有網路的情況下。

   如果

   在網頁被造訪過一次後，Service workers 就能夠被註冊。

   **示意圖取自https://dev.opera.com/articles/offline-with-upup-service-workers/**

   ![service worker 示意圖](https://imgur.com/PhUlDRX.gif)

3. Check the network cache

   瀏覽器透過網路層，可以確認是否有新的response在cache中。

   > 在Response header中的 **Cache-control**可以設定max-age或是設成no-store。

   ​	**什麼是瀏覽器的cache機制**

   ​	https://blog.techbridge.cc/2017/06/17/cache-introduction/

   ​	Expires 、 Cache-Control 、 Last-Modified 、If Modified-Since

    	又是另一個故事.....

   

4. Check for connection

   check是否已建立過這個request host&port的連線，如果沒有瀏覽器就會透過DNS找出符合的IP位置，讓瀏覽器去連線!

   

5. Establish connection

   瀏覽器可以與server建立連線，所以server可以回傳訊息給client或是從client接收訊息。

   

6. Send the request to the server

   通常第一個request會是Server回傳html檔案給client

   

7. Handle the response

   當資訊都顯示給client後，開始一步步分析Response。

   check　Response的header，接著Browser會將相關資訊寫進cache。

   

一圖勝千言萬語

附上alistapart的精美圖

![server to client flowchart](https://imgur.com/yWQGGfO.jpg)