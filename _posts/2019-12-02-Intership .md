---
layout: post
title:  奇幻之旅-實習觀察
date:   2019-12-02 14:09:00 +0800
author: Pon
categories: web
tags: interview advertising
---

> 原來行動廣告業是這麼一回事??
>
> 很有趣的收到xxx公司邀請去公司實作幾天
>
> 為了讓公司還有應徵者更了解彼此!
>
> 記錄這有趣的三天

# 第二印象

扣除第一次去公司面試的3小時，又再次來到了這個橘橙橙的辦公室

第二次的印象觀察又更多層面一點!!!

上班時間彈性，桌子很寬廣、樓板高度也很剛好，不會有壓迫的空間感

辦公室沒有OA板，跨team溝通沒有太嚴肅的氣氛

(os:　整體而言給人很新創很活潑的味道?!!)

<br>

# 開始之前-廣告??

youtuber竄起的這個年代，很大很大一部分的原因是頻道或是影片的高訂閱高觀看數可以帶來**商機**!

隨著趨勢，廣告也有了另一個管道增加它的曝光率! 現在人手一機的時代，過去在報章雜誌或是公車捷運上刊登廣告轉變為現在的行動(數位)廣告! 

## 展示型廣告-Display Advertising

> **出現在第三方網站或部落格上，結合文字、logo、圖像等形式的廣告，主要用於把流量導入合作網站中，或者提升消費者對品牌產品的認知意識**  
>
> *摘自*[什麼是展示型廣告（Display Advertising）?](https://www.inside.com.tw/article/6261-what-is-display-advertising)

包含路上、大樓、貼的大型看板，傳單、海報、報章雜誌都算；隨著網路的普及，廣告開始結合聲音、影像，也能透過數據進一步追蹤使用者的喜好或是行為，做出更精準的投放廣告!

也就是一個數位廣告開始呈現的同時，就在蒐集使用者的數據

停留的時間? 點擊率? 多少人把內容/影片看完? 等等等

透過訂定目標去計算轉換率(CVR)! 進一步修正廣告的內容或是策略! 對廣告主而言也更能控制廣告花費!!

<br>

# 實作

> 來之前主管mail一些數位廣告相關的knowhow給我
>
> 並說最後一天要做一個簡單的presentation

基本上就是team的成員針對不同的廣告類型做介紹，重點整理如下

<br>

## Interstitial Video Ad (插頁ISVY)

In-APP 就是在APP中會跳出的廣告

ex:背景可能是一張圖片，最下面放上宣傳的影片

點擊圖片可以導到活動的網站，點擊影片可以直接觀看影片或是暫停

<img src="https://imgur.com/LwLxEOZ.jpg" alt="ISVY" style="zoom:67%;" />

像是這樣的廣告中，使用者進行相關的動作時要送出相關資訊給分析數據的平台(GA or DMP)

要埋下code包含

- 使用者點擊圖片時，除了要透過SDK另開瀏覽器視窗外，還要pass click訊息出去

- 使用youtube iframe的api監測影片觀看秒數，因為可以把進度條關閉，可以準確掌握使用者看完影片25%, 50%, 75% 或是看完的人數是多少

  

## Landing Site Ad (一頁式)

web-就是mobile透過browser瀏覽網站或網頁

<img src="https://imgur.com/zJi6NC0.jpg" alt="Landing site" style="zoom:67%;" />

要埋下的code包含:

- 基本的GA Tracking ID
- 追蹤按鈕的點擊次數
- 追蹤scroll的百分比.....

<br>

## Interstital Ad (底部插頁)

 一樣也是web型式，在底部大約1/3的位置輪播廣告內容

<img src="https://imgur.com/Ymb8epW.jpg" alt="interstitial ad" style="zoom:67%;" />

一樣是基本的GA tracking ID或是其他第三方的tracking

<br>

# 小結

一開始收到邀請確確實實嚇到了，以為這是最近徵才的特色?!

能有機會觀察一家公司確實很不一樣，畢竟有時候面試透過人資或是主管敘述公司文化、工作內容可能只能當**參考**

透過實際的觀察，比較有踏實的感覺

再來是公司的分工蠻細的(我覺得)，不是一個team一條龍的感覺

有機會能認識新的產業是一件很有趣的事

廣告是每個人每天一定都會接觸的事物，同時你的產品對象也就是自己

雖然有時會心生恐懼，有種被數據盯上的感覺，不斷的Retargeting....

但這就是目前的趨勢，掌握數據、分析數據，從龐大的數據中找出可以利用的資料，找出規則~

Even 如果最後收到感謝信，也是感溫有這次奇幻之旅的體驗～～

<br>

# 延伸閱讀&參考圖文

[什麼是展示型廣告Display Advertising?](https://www.inside.com.tw/article/6261-what-is-display-advertising)

[Google Ads關鍵字廣告教學，看完這篇就懂怎麼投放！](https://transbiz.com.tw/google-adwords%E9%97%9C%E9%8D%B5%E5%AD%97%E5%BB%A3%E5%91%8A%E6%95%99%E5%AD%B8/)

[Programmatic Advertising Technology Landscape](https://getpocket.com/redirect?url=https%3A%2F%2Fadtagmacros.com%2Fprogrammatic-display-advertising-technology-landscape%2F)

[Google Tag Manager 教學，一篇搞懂如何設定和管理網站追蹤碼]([https://transbiz.com.tw/google-tag-manager-gtm-%E6%95%99%E5%AD%B8/](https://transbiz.com.tw/google-tag-manager-gtm-教學/))

[點選關閉按鈕以前 — 數位廣告怎麼運作？]([https://medium.com/@hellojoy/%E9%BB%9E%E9%81%B8%E9%97%9C%E9%96%89%E6%8C%89%E9%88%95%E4%BB%A5%E5%89%8D-%E4%B8%8A-%E6%95%B8%E4%BD%8D%E5%BB%A3%E5%91%8A%E6%80%8E%E9%BA%BC%E9%81%8B%E4%BD%9C-a5715ba4d651](https://medium.com/@hellojoy/點選關閉按鈕以前-上-數位廣告怎麼運作-a5715ba4d651))

[Display Advertising – The Ultimate Beginner’s Guide](https://blog.bannersnack.com/display-advertising-guide/)