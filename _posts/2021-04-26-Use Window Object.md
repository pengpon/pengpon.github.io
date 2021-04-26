---
layout: post
title:  "window 物件的點點滴滴"
date:   2021-04-26 13:12:00 +0800
author: Pon
categories: web
tags: web
---



## Window物件

代表瀏覽器開啟的視窗，如果 document中有包含`<iframe>標籤`，瀏覽器會建立一個 window物件。

### 常用屬性

- `window.closed` 視窗是否關閉
- `window.opener`返回開啟目前視窗的母視窗參考
  - ex:  A視窗開啟B視窗, `B.opener`會回傳A

- `window.document` 當HTML被瀏覽器載入，會建立一個根節點，即 document物件。

  - Document物件讓我們可以透過指令對HTML中的元素進行操作
  - 常見: `getElementById()` `getElementsByName()` `querySelector()` `querySelectorAll()` `addEventListener()`

- `window.frameElement` 若當下視窗是嵌在`<iframe>`中，回傳該 iframe元素，反之回傳null

  ```javascript
  var frame = window.frameElement;  // Get the <iframe> element of the window
  
  if (frame) {   // If the window is in an <iframe>, change its source
    frame.src = "https://www.w3schools.com/";
  }
  ```

  - `contentWindow` 返回HTMLIFrameElement的window，再利用這個window去操作iframe內部的document和DOM

    範例:

    ```javascript
    var x = document.getElementsByTagName("iframe")[0].contentWindow;
    //x = window.frames[0];
    
    x.document.getElementsByTagName("body")[0].style.backgroundColor = "blue";
    // this would turn the 1st iframe in document blue.
    ```

    

- `window.frames`  返回當下window的所有frames 

  ```javascript
  // 修改window中第一個iframe的網址
  window.frames[0].location = "https://www.w3schools.com/jsref/";
  ```

  

- `window.history`回傳一個 history物件

   ```javascript
  var historyObj = window.history;
  history.back();     // 相當於按下上一頁按鈕
  history.go(-1);     // 相當於 history.back();
   ```

  

- `window.location` 用來取得或設定 window當下位址的物件

  ```javascript
  var locationObj = window.location;
  window.location = newLocation;
  ```

  - 屬性

    - hash
    - host
    - hostname
    - href
    - pathname
    - port
    - protocol
    - search

    範例: 

    ```javascript
    // https://developer.mozilla.org/zh-TW/docs/Web/API/Window/location#location_object
    
    
    // location物件
    let locationObj = window.location;
    
    console.log (locationObj.hash); // 包含#的hash值
    // #location_object
    
    console.log (locationObj.host); // 主機名稱+port號
    // developer.mozilla.org
    
    console.log (locationObj.hostname); // 主機名稱
    // developer.mozilla.org
    
    console.log (locationObj.href); // 完整網址
    // https://developer.mozilla.org/zh-TW/docs/Web/API/Window/location#location_object
    
    console.log (locationObj.pathname); // 路徑
    // /zh-TW/docs/Web/API/Window/location
    console.log (locationObj.port); // port號
    // 無
    
    console.log (locationObj.protocol); // 通訊協定
    // https:
    console.log (locationObj.search); // 包含?的搜尋
    // 無
    
    ```

    補充網址中的hash

    - 代表網頁中的一個位置
    - 對server無作用，請求不會包含`#`
    - 改變`#`後的內容，不會 Reload網頁，但會在history增加紀錄

    

  - 方法

    - assign(url)  載入url的內容
    - reload(forceget) 刷新當下頁面
      - reload(true) 強制從server抓取頁面資源
      - reload() / reload(false) browser可以從cache中抓取頁面內容
    - replace(url) 取代目前document的內容，和assign()的差異在於，replace()不會將當下頁面存進history中，使用者無法用back返回。
    - toString() 返回URL字串，相當於location.href

    

- `window.innerWidth` 取得視窗內網頁**內容**寬度，包含垂直捲軸

- `window.innerHeight` 取得視窗內網頁**內容**高度，包含水平捲軸

- `window.outerWidth` 取得整個視窗外部的寬度

- `window.outerHeight` 取得整個視窗外部的高度

  圖示: 

  ![inner vs outer](https://imgur.com/opUMLay.jpg)

  > 圖取自[MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerHeight)

- `window.pageXOffset` 返回目前頁面相對於整個頁面原點的X距離(水平)

  - 等同於`scrollX`

- `window.pageYOffset` 返回目前頁面相對於整個頁面原點的Y距離(垂直)

  - 等同於`scrollY`

- `window.parent` 回傳當下window物件的 parent，如果window沒有parent，會回傳自己本身

- `window.top`　返回當下window最頂層的window



### 常用方法

- `window.open()`

  ```javascript
  // Open a new window
  var myWindow = window.open("", "myWindow", "width=200, height=100");
  ```

  window.open("新視窗網址", "新視窗名稱", [設定])

- `window.close()` 關閉視窗

- `window.open()`開啟視窗

- `window.postMessage()` 跨源傳送資料

  - `window.postMessage(message, targetOrigin, [transfer]) ` 傳送資料
  - `window.addEventListener("message","callback")` 接收資料

- `window.prompt()` 顯示可輸入文字的對話框

- `window.requestAnimationFrame()` 讓動畫更順暢，省電

  - 採用系統時間，保持最佳的畫面繪製
  - 隱藏或是不可見的元素，不會進行重繪

- `window.scrollTo()` 捲定document到特定位置

- `window.scroll()` 相當於`window.scrollTo()`

- `window.scrollBy()` 捲動document特定距離 (px)

  - `window.scrollBy(100, 0)` 右移100px

    

## 應用

### 計算頁面百分比

```javascript
const originalTitle = document.title;
window.addEventListener("scroll", () => {
  let scrollTop = window.scrollY; // 視窗捲動距離
  let docHeight = document.body.offsetHeight; // body內容高度
  let winHeight = window.innerHeight; // 視窗可視高度
  console.log(scrollTop, docHeight, winHeight );
  let scrollPercent = scrollTop / (docHeight - winHeight);
  let scrollPercentRounded = Math.round(scrollPercent * 100);
  document.title = `(${scrollPercentRounded}%) ${originalTitle}`;
});


```



---

### 跨window溝通

用在頁面及彈跳視窗之間或是頁面和內嵌的iframe之間

範例:

```javascript
// parent.html
var childwin;
const childname = "popup";
function openChild() {
childwin = window.open('child.html', childname, 	  'height=300px, width=500px');
}

function sendMessage(){
    let msg = {name : "shan", age: "00"};
    childwin.postMessage(msg,'*') // 向child發送訊息
    childwin.focus();
}
```

```javascript
// child.html
window.addEventListener("message" , (event)=>{
	console.log(event.data); 
})
```





## 參考文章



[window.location Cheatsheet](https://www.samanthaming.com/tidbits/86-window-location-cheatsheet/)

[**HTML5’s window.postMessage API**](https://davidwalsh.name/window-postmessage)