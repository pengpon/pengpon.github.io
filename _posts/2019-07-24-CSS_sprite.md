---

layout: post
title:  "CSS Sprites 筆記"
date:   2019-07-24 21:33:00 +0800
excerpt: "為了降低Request次數，減輕Server的負擔，sprite常常出現 在使用多個icon或是有小型動畫的網站中"
---



# 原理

CSS Sprites 是把多個圖片合併 是減少下載圖片次數的方法之一

在處理連續圖片做出動畫時也很適合!!

Sprites 就是一張合併出來的大圖

只要透過CSS控制X,Y的定位即可!!

![CSS Sprite 原理圖](https://imgur.com/rP2kR2h.jpg)

[圖片出自maxcdn.com]



# Animation參考範例

<https://blog.teamtreehouse.com/css-sprite-sheet-animations-steps>

除了將每個影格的圖片合併成一張圖外

還要搭配css的animation

以這個範例來說 

- 第一步 產生sprite圖檔

  ![作者怪獸圖](https://imgur.com/zmroYnd.jpg)

利用illustrator將10個190x240的影格合併



- 第二步 animation屬性內容

作法是 這張圖會當做background image

定義元素的寬高 =每次可以看到的範圍= width:190px; height:240px

```html
<div class="monster"></div>
```



```css
.monster {
  // 打開可看見背景圖的框框
  width: 190px;
  height: 240px; 
  //背景圖位置由水平方向置左&垂直置中
  background: url('monster-sprite.png') left center;
}
```

動畫內容即是移動背景圖位置

圖片往左移動1900px

**background 預設會重複出現**

 ```css
// 定義動畫每個影格的屬性 
@keyframes play {
   100% { background-position: -1900px; }
}
 ```



```css

.monster {
    ...省略
    animation: play .8s steps(10) infinite;
    ...省略
}
```

- 執行 keyframes名稱為play的劇本

- 用0.8秒跑完一次劇本

- 使用**step** time-function的效果

  > (淡入淡出 也是一種time-function) 
  >
  > step不幫忙處理轉場的效果!!!!
  >
  > step中的數字 代表要跳幾次才到最終狀態!!

- infinite指動畫要永遠重複播放



### 參考圖片及網站

<https://www.maxcdn.com/one/visual-glossary/css-sprites/>





