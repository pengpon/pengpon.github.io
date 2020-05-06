---
layout: post
title:  "真實世界的Event capturing & bubbling"
date:   2020-05-06 19:45:00 +0800
author: Pon
categories: studygroup 
tags: web
---



*上一篇講到event傳遞時的三種phase，形成事件capturing和bubbling*

*再來整理相關的應用，加深印象*

<br>

# Event Delegation(事件代理)

由父元素取代子元素註冊事件

範例: (取自[JavaScript Event Delegation](https://www.javascripttutorial.net/javascript-dom/javascript-event-delegation/))

```html
<ul id="menu">
    <li><a id="home">home</a></li>
    <li><a id="dashboard">Dashboard</a></li>
    <li><a id="report">report</a></li>
</ul>
```

<br>

當每個選單項目都想綁定click事件，可能會這樣寫

```javascript
let home = document.querySelector('#home');
home.addEventListener('home',(event) => {
    console.log('Home menu item was clicked');
});

let dashboard = document.querySelector('#dashboard');
dashboard.addEventListener('dashboard',(event) => {
    console.log('Dashboard menu item was clicked');
});

let report = document.querySelector('#report');
report.addEventListener('report',(event) => {
    console.log('Report menu item was clicked');
});
```

當項目越來越多 or 頁面越來越複雜，可能就會註冊很多個event handler，效能不好

<br>

利用event傳播的機制，可以改寫成:

```javascript
let menu = document.querySelector('#menu');

menu.addEventListener('click', (event) => {
    let target = event.target;

    switch(target.id) {
        case 'home':
            console.log('Home menu item was clicked');
            break;
        case 'dashboard':
            console.log('Dashboard menu item was clicked');
            break;
        case 'report':
            console.log('Report menu item was clicked');
            break;
    }
});
```

當點擊ul中的a連結時，因為`event bubbling`最後會傳遞給ul元素，所以由父元素代為綁定event

而透過target id 可以區分是哪個目標被點擊

<br>

小結event delegation的優點:

- 減少記憶體的消耗, 增加效能

- 減少在頁面中註冊多個event handler

  

<br>

# Event Stop Propagation

這篇[Event Capturing and Bubbling in JavaScript](https://www.kirupa.com/html5/event_capturing_bubbling_javascript.htm)有提到，知道event的傳播機制，**Who care??** (都用預設bubbling就好??)

**看起來不重要，踩到雷就知道**



除了event delegation，最常遇到的應該是彈跳視窗(for 手刻)

彈跳視窗出現後，通常有兩種方式可以關閉

1. 點擊彈跳視窗的x
2. 點擊彈跳視窗以外的區域

範例　(取自 [JavaScript Capture Bubble DOM事件獲取&冒泡](https://iandays.com/2019/03/21/eventpass/))

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="html,result" data-user="pengpon77" data-slug-hash="PoPQzWx" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="popup sample">
  <span>See the Pen <a href="https://codepen.io/pengpon77/pen/PoPQzWx">
  popup sample</a> by pengyushan (<a href="https://codepen.io/pengpon77">@pengpon77</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

<br>

小結:

1. 選定capturing or bubbling傳遞方式
2. target到達後，不再往上或往下傳，使用`e.stopPropagation()`中斷
3. 彈出視窗事件僅綁定在button上，**click不再往下傳!!** 
4. 關閉視窗事件除綁在x span上，也要綁定在整個document上
5. 跳窗本身被點擊後，要阻止事件繼續傳給document! 



<br>

或是利用**event target**來控制跳窗的開啟或關閉

[CodePen範例參考](https://codepen.io/adventuresinmissions/pen/nrhHF)

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="adventuresinmissions" data-slug-hash="nrhHF" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Simple Confirmation Popup">
  <span>See the Pen <a href="https://codepen.io/adventuresinmissions/pen/nrhHF">
  Simple Confirmation Popup</a> by Adventures in Missions (<a href="https://codepen.io/adventuresinmissions">@adventuresinmissions</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

<br>

# 延伸閱讀&參考圖文



[JavaScript Capture Bubble DOM事件獲取&冒泡](https://iandays.com/2019/03/21/eventpass/)

[Event Delegation](https://riptutorial.com/dom/example/12614/event-delegation)

[JavaScript Event Delegation](https://www.javascripttutorial.net/javascript-dom/javascript-event-delegation/)