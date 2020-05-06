---
layout: post
title:  "淺談Event傳播機制"
date:   2020-05-06 00:11:00 +0800
author: Pon
categories: studygroup 
tags: web
---



# What is DOM?

Javascript use the *DOM* to access the document and element.

The page content is stored in the DOM and may be accessed and manipulated via JavaScript,

API = DOM + JavaScript

*摘自:[Introduction to the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)*

<br>

Javascript沒有提供網頁的操作方法, 在網頁中所使用的方法都是*Browser*提供的!

包含兩個主要物件BOM&DOM

Browser Object Model(BOM) & Document Object Model(DOM)

- <span style="color:red">BOM</span>

   和內容無關，主要核心是**window物件** (window即是瀏覽器的視窗)

   不需要宣告就可以使用

   所有的全域變數 function、object 都屬於window (所以window可以省略不寫)

   常用window屬性:  

   - closed
   - document
   - history
   - innerheight
   - innerwidth
   - location
   - name
   - navigator
   - pageXOffset/ pageYOffset

   

   常用window方法:

   - alert()
   - blur() / focus()
   - setInterval() / clearInterval()
   - setTimeout() / clearTimeout()
   - close()
   - confirm()
   - scrollBy() / scrollTo()

<br>

- <span style="color:red">DOM</span>

   Javascript 可以藉由DOM API去改變html中的內容或樣式

   用來控制網頁的節點

   

   常用:

   - document.getElementById
   - document.getElement**s**ByTagName
   - document.getElement**s**ByClassName



![BOM&DOM](https://imgur.com/HJusx3g.jpg)

內容&圖片取自[快樂學習程式](https://www.happycoding.today/posts/43)

<br>

# 事件驅動

Javascript是一個事件驅動的程式設計(Event-driven)

對瀏覽器來說: 包含事件(event)&事件處理程序(event handler)

1. event

   表示一個在DOM物件上發生的事件

   Ex:滑鼠點擊,鍵盤輸入,內容載入完成....

2. handler

   DOM元素會監聽某些事件, 對於發生的事件需要執行handler

   <br>

常用標準事件:

- click
- Mousedown/mousemove
- Touchstart/ touchmove/ touched

參考事件列表 [Event reference](https://developer.mozilla.org/zh-TW/docs/Web/Events)



<br>

# 監聽方式

1.寫在html (inline)

```html
<button onclick="console.log('click')">

<body onload="doFirst()">

```

不推!!
<br>

2.寫在js (傳統寫法) 

```javascript
document.getElementById('button').onclick=function(){
console.log('click')
}

window.onload=doFirst();
```

不推!
<br>

3.寫在js (W3C推薦)

```javascript
const element=document.getElementById('button');
element.addEventListener('click',function(){
console.log('hello');
},false)

window.addEventListener('load',doFisrt,false);
```

大推薦!!! 可以撰寫多個程序～

​	語法:

​	`addEventListener( event, handler, useCature)`

​	`removeEventlistener(event, handler, useCature)`

<br>


# 事件觸發/傳遞流程

ex: 三層div, grandma>mama>daughter

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="js,result" data-user="pengpon" data-slug-hash="ExVoEMQ" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="simple Event Flow">
  <span>See the Pen <a href="https://codepen.io/pengpon/pen/ExVoEMQ">
  simple Event Flow</a> by pengpon (<a href="https://codepen.io/pengpon">@pengpon</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
各自綁定監聽事件, 會觸發的handler會是??

- 點擊最內層的daughter?
- 點擊最外層的grandma?
- 點擊中間層的mama?


<br>
# Event Phase

event中有個屬性eventPhase，表示此事件是在哪一個是Phase被觸發

```javascript
// PhaseType
  const unsigned short      CAPTURING_PHASE                = 1;
  const unsigned short      AT_TARGET                      = 2;
  const unsigned short      BUBBLING_PHASE                 = 3;
```

取自[W3C](https://www.w3.org/TR/DOM-Level-2-Events/events.html#Events-interface)

<br>

根據DOM元素的樹狀結構，事件在傳播時:

依序發生

1. 從根節點往下傳遞到Target--->CAPTURING_PHASE
2. 到達目標--->AT_TARGET
3. 再從目標一路往上到根節點--->BUBBLING_PHASE



![event flow](https://imgur.com/Z9vLKVc.jpg)

圖片取自[W3C](https://www.w3.org/TR/DOM-Level-2-Events/events.html#Events-interface)

<br>

`addEventListener(event, handler, useCature)`的第三個參數，代表是否要把listener放到CAPTURING_PHASE，預設為false!

所以預設行為是　當點擊最內層的元素時,會從目標依序往上一一觸發!



*p.s. 有幾種事件沒有支援事件的propagation，Ex:onfocus, onblur*


<br>

## Bubbling 

內部元素觸發時先執行自己的handler 再執行父元素的handler

<br>
## Capturing 

當內部(target)被觸發時 從最外圍的handler執行，再執行本身

<br>

p.s. 當事件傳遞到目標對象時，無論第三個參數為何，**event phase都為at_target**

既然已經是目標就不會再分capturing / bubbling，handler照程式碼執行的順序

<br>
<br>

# 補充

## Event物件

*內容取自[從ES6開始的JavaScript學習生活](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part4/event.html)*

所有在網頁上DOM元素註冊的事件,會進入queue中，等待被觸發>>>做出相對的回應給使用者

由瀏覽器環境實作event loop

<br>

常用Event物件屬性(只讀不能寫)

- currentTarget 目前事件對象
- target 分派事件的原始對象
- type 事件類型
- bubbles 冒泡狀態
- cancelable 事件是否可以被取消

<br>

常用Event物件方法:

- preventDefault() 取消事件的預設行為，ex:取消超連結的跳轉頁面行為
- stopPropagation() 停止事件的傳播行為

<br>

p.s. preventDefault()也會隨著事件傳遞下去

ex: click TargetA 執行`e.preventDefault()`-->click事件接著傳給 Element B，同時也會取消B的預設行為



<br>

## EventTarget物件

*內容取自[從ES6開始的JavaScript學習生活](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part4/event.html)*

可以接收事件/讓監聽者註冊，Ex: DOM元素、window、document

有三個方法可以使用:

- addEventListener
- removeEventListener
- dispatchEvent 送出事件給所有有訂閱的監聽者



<br>

# 延伸閱讀&參考圖文

[Bubbling and capturing](https://javascript.info/bubbling-and-capturing)

[what is a DOM API?-Quora](https://www.quora.com/What-is-a-DOM-API)

[DOM 的事件傳遞機制：捕獲與冒泡-TechBridge 技術共筆部落格](https://blog.techbridge.cc/2017/07/15/javascript-event-propagation/)

[Event Capturing and Bubbling in JavaScript](https://www.kirupa.com/html5/event_capturing_bubbling_javascript.htm)

