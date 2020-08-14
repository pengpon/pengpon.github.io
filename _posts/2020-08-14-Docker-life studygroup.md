---
layout: post
title:  "[Docker]讀書會part4&分享會 "
date:   2020-08-14 09:51:00 +0800
author: Pon
categories: studygroup 
tags: docker web
---

> 7/30 & 8/19讀書會紀錄



# 0730 Docker volume

[李克強抽硬碟](https://tw.news.yahoo.com/李克強視察數據中心亂抽硬碟-網看傻-為逝去資料送祝福-094000482.html)

> 懶人包:視察數據中心的同時，突然抽出運作中伺服器的一個硬碟

世界上一定會有一個實體地方，儲存資料，就像李克強去考察的貴州數據中心。

<br>

---

Docker 提供volume & bind mounts 兩種選擇

container run時 會幫我們建一個地方，存volume

**萬用`--help`當自己的老師**

`docker image inspect mysql`找volumes 

`docker container run`run完後有mounts的資訊

## 練習

1. git clone Udemy講師的project
2. cd 切換路徑進到`dockerfile-sample-2` 修改index.html
3. 啟動一個nginx container 將當下有index.html檔案的這個目錄和container做bind mounts
4. 當下目錄為$(pwd)，nginx預設目錄為`/usr/share/nginx/html`
5. `-v $(pwd):/usr/share/nginx/html`



<br>

------

# 0819 Docker compose&分享

REID(Radio Frequency IDentification)

- 無線通訊技術
- 感應器(Reader)和RFID標籤(Tag)組成
- 感應器發出無線電波，在感應範圍內觸發RFID標籤，因電磁感應產生電流
- RFID標籤有電流後，晶片運作發出電磁波讓感應器接收
- RFID標籤有分主動/被動，有無電池的差異，主動的訊號傳送範圍也較廣
- EX:圖書館嗶嗶，悠遊卡嗶嗶，ETC

參考[RFID原理與應用](http://www.cc.ntu.edu.tw/chinese/epaper/0002/20070920_2005.htm)

---

昱廷推薦影片-2005年Mark Zuckerberg到哈佛計概課(CS50)演講

[CS50 Lecture by Mark Zuckerberg - 7 December 2005](https://www.youtube.com/watch?v=xFFs9UgOAlE&t=429s)

---

後端強大IDE-[JetBrains](https://www.jetbrains.com/ )

(不同語言有出各自的IDE，要收費)

---

閒聊第12屆鐵人賽可參考主題

- 讓您深刻了解隕石式開發(?)

- DP 動態規劃-演算法
  - [五大常用演算法 —-DP 動態規劃（Dynamic Programming）]([https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/586675/](https://codertw.com/程式語言/586675/))
  - EX:走迷宮，找最佳解，背包問題
  - 推推[Chu-Ling Ko精美筆記](https://hackmd.io/@qR5cY2d3Ql2AdYtLfHFxVg/ByZgGkLpW?type=view)

---

閒聊下班後的進修/休閒 (?)

- [meet up平台](https://www.meetup.com/cities/tw/taipei/events/)有各式各樣的活動
  - ex:與外國人打[太極](https://www.meetup.com/Hiking-in-Taiwan-English-Chinese/events/272393017/?rv=me1&_xtd=gatlbWFpbF9jbGlja9oAJDZhM2Y2OTBjLTg4NzctNDBjMC05NTQ1LTA1NzNjMzY1NWRlNg&_af=event&_af_eid=272393017)or登山

- 0元挑戰不間斷英文課程[voicetube]( https://hero.voicetube.com/)

- 看看國外新聞 [The New York Times](https://www.nytimes.com/)

---

好用library分享

- gantt chart 行事曆甘特圖
  - angular-calendar 
  - fullcalendar推推
  - 關鍵字:gantt calendar scheduler

  **Sammie過來人:react 跟vue的calendar都比angular多**

- 圖表

  - [chart.js](https://www.chartjs.org/)
  - [amcharts](https://www.amcharts.com/)

---

監控專案分享

- [grafana](https://grafana.com/grafana/)
  - 開源專案
  - 監控server用
  - 使用D3.js做視覺化

- psi-probe
  - 監控tomcat
  - for Java

---

# 心得

- 經驗很重要
- 了解需求，14天能上手新工具開發完成
- 記憶連結法
- 被炸會成長







