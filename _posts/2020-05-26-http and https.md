---
layout: post
title:  Http V.S. Https差異
date:   2020-05-26 14:12:00 +0800
author: Pon
categories: studygroup 
tags: web
---

> 淺淺談HTTP和HTTPS的差異!



# HTTP

*Hypertext Transfer Protocol* 超文本傳輸協議

在網址列的輸入domain name的前頭 **http://**example.com，意在告訴browser要透過HTTP來進行連線

HTTP協議建立在**TCP協議**之上，預設使用80 port ，在網路世界中去傳送及接收資料封包

P.S. 協議是client 和server雙方要使用的，不是各訂各的

遵守約定好的協議，讓我們(client)可以和網站(server)溝通

<br>

![OSI和TCP/IP協定](https://imgur.com/NH53o7z.jpg)

圖取自鳥哥

<br>

![TCP/IP Protocol](https://imgur.com/MdyKyuT.jpg)

圖片取自[Introduction to internetworking](https://wiki.mikrotik.com/wiki/Testwiki/Introduction_to_internetworking)

---



起初HTTP的建立，目的是提供我們去傳送接收在WWW(World Wide Web)的**HTML內容**。

將html放在web server上，client透過browser輸入url，取得頁面內容

client端在TCP handshake後，送出request給HTTP server，server 回應資訊包含狀態等等~ex:`HTTP/1.1 200 OK`

![http2-vs-http1](https://imgur.com/T8kGVNL.jpg)

圖取自[cheapsslsecurity](https://cheapsslsecurity.com/p/http2-vs-http1/)

<br>



## TCP協議

建立連結三次握手，斷開連結四次揮手

![TCP建立/中止連線](https://imgur.com/vy4FTad.jpg)

圖取自[wiki.mikrotik.com](https://wiki.mikrotik.com/wiki/Manual:Connection_oriented_communication_(TCP/IP))

<br>

---



## HTTP演化

第一版HTTP在1991年出現 ，HTTP/0.9 只包含了一個method `GET`，沒有header!

1996年 HTTP/1.0出現，有`GET` `HEAD` `POST`可用

1997年 HTTP/1.1出現 

1999年 HTTP/1.1廣泛應用，五個新的method `OPTIONS` `PUT` `TRACE` `CONNENT` `DELETE`

2010年 多了`PATCH`

推推[HTTP/1.x vs. HTTP/2 – The Difference Between the Two Protocols Explained](https://cheapsslsecurity.com/p/http2-vs-http1/)

![發展史](https://imgur.com/pBJHpuj.jpg)

圖取自[cheapsslsecurity](https://cheapsslsecurity.com/p/http2-vs-http1/)



<br>

---



## 現今HTTP

存在的問題:**延遲**

- 瀏覽器阻塞(HOL blocking)

  瀏覽器對於同一個域名，同時只能有4~6個連結(不同瀏覽器內核可能有差異)，超過連線數的限制後，後面的Request卡住了....

- DNS查詢(DNS Lookup)

  瀏覽器要知道目的地server IP才能建立連線，DNS負責將域名轉換成IP，可以利用Cache來減少查詢的時間

  ex: windows 清除DNS cache

  ```
  ipconfig/flushdns
  ```

- 建立連結

  因為HTTP基於TCP協議，也就是必須經過三次握手後才能傳送真正的Request，

<br>

---



# HTTPS

Hypertext Transfer Protocol Secure，也可以稱作 HTTP透過TLS或是SSL來傳輸

一般網站如果是提供https 假設輸入的是http:// ，都會重導到安全連線

HTTPS也是利用TCP協議去傳送和接收封包，資料需經過加密和解密的動作

利用**加密的傳輸層SSL/TLS**作為HTTP應用層的子層，透過443 port來傳送資料

![protocol stack](https://imgur.com/JVjPTyr.jpg)

圖片取自[researchgate](https://www.researchgate.net/figure/The-Hypertext-Transfer-Protocol-HTTP-and-Hypertext-Transfer-Protocol-Secure-HTTPS_fig1_320479973)

<br>

HTTPS實際上是由Netscape(網景)在1994在自家的瀏覽器所用

起初是使用SSL協議，最終才演化成使用TLS

<br>

## 特點

- 公私鑰 (鎖箱開箱)

  建立安全的通道，確保數據傳輸

- 憑證 (證書)

  可確認網站的真實性，查看網站的憑證內容

---



## 簡易概念



憑證認證階段:**非對稱加密**(公鑰加密)

1. CA機構 (Certificate Authority)發行公鑰給瀏覽器供應商

2. 每個一個browser都有自己信任的CA機構清單(內建根憑證機構清單)，有CA公鑰的副本

3. Server啟用SSL前，找到CA，要求給我證書

4. CA收到請求，照程序跑，完成後發憑證(序號、擁有人名稱、公鑰、數位簽章等)，Server收到憑證後加到config中

   *數位簽章:將網站公鑰透過CA的私鑰加密後的資料*

5. 我想要瀏覽這個server上的網站

6. server回覆SSL憑證給Browser，瀏覽器會從憑證中抓出CA的資訊，從內建清單中找到這個CA的公鑰，利用這個公鑰解出憑證中的數位簽章內容，得到Server的公鑰，將網站送來的公鑰和自己解出的公鑰比對

![how ssl works](https://imgur.com/cCjfATW.jpg)

圖取自:[那些關於ssl-tls的二三事]([https://medium.com/@clu1022/%E9%82%A3%E4%BA%9B%E9%97%9C%E6%96%BCssl-tls%E7%9A%84%E4%BA%8C%E4%B8%89%E4%BA%8B-%E4%BA%8C-how-ssl-works-a9d6720bdd48](https://medium.com/@clu1022/那些關於ssl-tls的二三事-二-how-ssl-works-a9d6720bdd48))

<br>

瀏覽器 what to do?

- 核對當初發憑證的機構是誰

- 找到Root Certificate Authority 向他的伺服器驗證 這張憑證是否合法



Server what to do?

- https 需要TLS憑證 安裝在server端

- 這個憑證可以用在不同的協議上像是HTTP(web), SMTP(email), FTP

---



數據傳輸階段:**對稱加密**(加解密用同一把)

1. browser發出請求，我想要建立連線
2. server給browser公鑰
3. Browser產生session key (第三把key)
4. 利用server的公鑰將session key**加密**
5. 將加密後的session key傳給server
6. server利用私鑰解密，雙方都有session key
7. 使用session key進行雙向的對稱加密通訊!

推推:[How Does HTTPS Work? RSA Encryption Explained](https://tiptopsecurity.com/how-does-https-work-rsa-encryption-explained/)

---



## 加密演算法

- 對稱加密:只有一個私鑰，AES、RC4、3DES
- 非對稱加密:公私鑰各一，RSA、DSA/DSS
- HASH演算:MD5、SHA1、SHA256

*老高名言:這個內容有機會以後再做介紹(?!)*

---



## 怎麼讓網站使用HTTPS更安全



### 1.加裝憑證

​		主要有三種憑證類型

1. domain validation (DV)

   signgle domain or subdomain，只需要信箱認證，便宜，幾分鐘搞定!

2. busuness/organization validation (OV)

   需要business verification 安全性更高 ，1-3天

3. extended validation (EV)，2-7天

   

p.s. [Let's Encrypt](https://letsencrypt.org/zh-tw/)，有免費SSL/TLS憑證服務，三個月簽發一次 

---

### 2. 設定Web Server

Apache, Nginx設定....

懶人>>修改DNS，讓連線先經過cloudFlare伺服器，這段是加密的傳輸連線~

---

### 3. 替換HTTP網址成HTTPS

存取資源的網址都要改成https://

---

### 4. 檢查

TLS/SSL憑證: [SSL Server Test](https://www.ssllabs.com/ssltest/)，輸入要評分的網址或網域

HTTP/2啟用: [HTTP/2 Test](https://tools.keycdn.com/http2-test)

<br>

---

# 補充

## 1.HTTP/2

Google開發的網路傳輸協定**SPDY**(發音:speedy)，基於TCP的應用層協定，HTTP/2的前身

- 多工(multiplexing)

  利用一個TCP連結，在同一個連線中發出多個請求，不用一直三方交握

- 壓縮Header! 傳輸量變小
- 直接用二進位傳送資料(http1為文字格式，需經過server將二進位資料轉文字,browser將文字轉回二進位)

速度差異參考:http://www.http2demo.io/

只要升級和設定Web server，加上使用支援HTTP/2的瀏覽器!!

推推[ALPHAcamp技術筆記](https://tw.alphacamp.co/blog/2016-07-12-http2)

<br>

## 2.封包攔截

[Whireshark](https://www.wireshark.org/download.html)

<br>

---

# 小結-比較

![http and https network protocol stacks](https://imgur.com/5nlMll9.jpg)

圖取自[oreilly](https://www.oreilly.com/library/view/http-the-definitive/1565925092/ch04s01.html)

<br>

| HTTP                 | HTTPS             |
| -------------------- | ----------------- |
| http://              | https://          |
| unsecured            | secured           |
| port 80              | port 443          |
| application layer    | transport layer   |
| no SSL certificate   | SSL certificate   |
| no domain validation | domain validation |
| no encryption        | data is encrypted |

<br>

# 延伸閱讀&參考圖文

[What Is the Difference Between HTTP and HTTPS?](https://www.keycdn.com/blog/difference-between-http-and-https)

[How to Migrate from HTTP to HTTPS - Complete Guide](https://www.keycdn.com/blog/http-to-https#1-buying-an-ssl-certificate-or-using-let-s-encrypt)

[How does HTTPS work? What's a CA? What's a self-signed Certificate?](https://www.youtube.com/watch?v=T4Df5_cojAs)

[How HTTPS works](https://www.youtube.com/watch?v=w0QbnxKRD0w)

[How HTTPS Works to Keep You Secure 🔐 and How it Differs From HTTP](https://love2dev.com/blog/how-https-works/)

[HTTP的起源與發展](https://www.jianshu.com/p/d4767b797e57)

[HTTP/1.x vs. HTTP/2 – The Difference Between the Two Protocols Explained](https://cheapsslsecurity.com/p/http2-vs-http1/)

[那些關於SSL/TLS的二三事(二) — How SSL works?]([https://medium.com/@clu1022/%E9%82%A3%E4%BA%9B%E9%97%9C%E6%96%BCssl-tls%E7%9A%84%E4%BA%8C%E4%B8%89%E4%BA%8B-%E4%BA%8C-how-ssl-works-a9d6720bdd48](https://medium.com/@clu1022/那些關於ssl-tls的二三事-二-how-ssl-works-a9d6720bdd48))