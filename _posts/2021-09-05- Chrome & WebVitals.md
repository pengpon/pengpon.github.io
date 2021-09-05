---
layout: post
title:  "I/O Extended 2021 系列: Chrome & WebVitals 筆記"
date:   2021-09-05 15:35:00 +0800
author: Pon
categories: web
tags: chrome
color: seagreen
author: peng
excerpt_separator: <!--more-->
comments: true
---



> 如題 - 直播筆記! 

<!--more-->

---


### 2021 所需要知道的 Web Vitals (上半場)
講者: Richard



#### 什麽是 Web Vitals?

如何優化網站效能?
出現各種說法: 
Ex 用 CDN?　用ooxx框架?


於是於是... Google & Google Chrome 2020年 4月底-5月初 推出  **Web Vitals**

制定一系列衡量方式 (數值化 & 度量衡概念)


> 相關內容推薦到 web.dev 入門 (針對網頁開發有各式新知)


Google 提出的倡議 針對**使用者體驗**提供統一量測標準

Google 自家展品已有應用
- Page Speed Insight
- Search Console
    - 以前叫 Google Webmaster
    - 免費SEO工具
    - SEO 成效分析
- Chrome User Research Report

---

Web Vitals 怎麼看:
- 直接使用 DevTools 看數據
- 安裝 Chrome/ Firfox Extension
- npm 套件 [web-vitals](https://www.npmjs.com/package/web-vitals) 可以在網頁前端計算各項數值



---

[Lighthouse Scoring Calculator](https://googlechrome.github.io/lighthouse/scorecalc/)
可以清楚知道各個指標的權重
知道哪個要優先修，容易灌分!
隨著 Web Vitals 讓 SEO 分數越來越清楚透明

![scoring](https://i.imgur.com/IQaLsD9.png)



---

### Core Web Vitals / Web Vitals


最有代表性的三個

- LCP 網站載入速度
第一的畫面最大物件什麼時候畫出來
當輸入網址一直到圖出來的時間
Good 2.5s
Poor 4s
難在前後端都有關
Ex:query 時間長短


(FCP: 第一個被畫出來，跟使用者能用沒意義，例如第一個叉叉?)

**2021新增:**
背景圖片可不算
橫向卷軸以外的也不算 (沒看到不應該計分)

---

- FID 可開始互動的時間
使用者開始互動(點擊/滾動)到實際有反應的時間
js 會擋在 main thread 上
Good 100ms 

沒有 code 最好 盡量刪JS
比如舊版瀏覽器用的JS or 遇到舊版再載入

---

- CLS 頁面穩定性
頁面飄移 (飄移的大小&距離)
Google 會給與每個偏移區塊一個位移分數，所有的分數加總便稱為 CLS
ex: 圖把字推開

物件大小位置要寫好 (給一個框)
動畫用 CSS transform 

**2021新增:**
減少同一頁累加計算
在這之前 沒有Refresh 前 一直動作 會一直累計 (SPA吃虧)
翻閱多頁 分數一直被累計
改成時間間隔夠久 就斷開


#### 如何優化
透過 Page Speed Insights
底層是 Lighthouse

##### Field V.S. Lab Data
1. Google 使用的是 Field 資料
收集真實使用者實際數據


2. Lab data 是當下蒐集
模擬環境下跑的
數字比較好看


![](https://i.imgur.com/WuUG9AT.png)
不同的資料來源，不同測法，不同工具


Lab data 快速知道有沒有優化
Field Data 知道使用者有無感


#### 懶人包
步驟:
1. 先量測分數 Page Speed Insight
2. 詳讀 web.dev 文章
- 思考前端架構
    - Server Side  Render 較好
4. PSI 建議
5. 導入 Chrome UX Report 每月監測 (Lab Data)

進階
1. Lighthouse CI /calibre
2. Sentry


#### 學習資源
- web.dev
- perf.email 訂閱
- Google 搜尋更新摘要
- web vital 相關議程

----

## Chrome DevTools (下半場)
講者: jecelyn

### DevTools

- DevTools = Developers
Ex: 
透過 Chrome Devtools web 
利用寫好的 script 搶登記註冊

- DevTools = DesTools = DesignerTools
Ex:
Elements 改背景色

### 2021 新功能

- CSS Grid and Flexbox toolings
 ![](https://i.imgur.com/lqRSVG6.png =300x)
 
 ​	取自[Inspect CSS Grid](https://developer.chrome.com/docs/devtools/css/grid/)

----



- 增加 Layout panel  Ex: show area names

![grid layout](https://i.imgur.com/NREsM7K.png =200x)



---

- Color Theme emulation

  <br>

  模擬 Light / Dark Theme
  `More tools -> Rendering -> prefers-color-scheme`

  Ex: Github 有支援 Light / Dark Theme
  ![dark theme](https://i.imgur.com/2IAIPXP.png)



---
- Discover and fix low contrast texts

  字體和背景色對比度，提供工具協助檢測

  ![color contrast](https://i.imgur.com/iBvivlQ.png =300x)
  	會顯示 Contrast ratio

​	AAA 是更嚴格的標準，有提供建議色



一次檢查顏色給一個Report (實驗功能)
`Setting ->Experiments -> CSS overview`
![](https://i.imgur.com/FA90oLX.png =300x)



---

- 每次Refresh直接給建議 (實驗功能)

  `Enable automatic contrast issue reporting`

![](https://i.imgur.com/9ajNcHk.png =300x)

要注意的Issue
![](https://i.imgur.com/v4TR803.png =300x)



---

- 體驗感受不同世界

  `Rendering -> Emulate vision deficiencies`

![](https://i.imgur.com/KY9dzmV.png =300x)

---



- Font editor (實驗功能)
![](https://i.imgur.com/fGIvpBf.png =300x)

----




- Core Web Vitals
`Rendering > Core Web Vitals `
![CWV](https://i.imgur.com/cnuWYvO.png)