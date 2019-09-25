---
layout: post
title:  "Canvas Review"
date:   2019-09-03 10:05:00
author: Pon
categories: web
tags: canvas design
---



# 前言

Canvas-->HTML5的新tag之一，類似小畫家，提供畫布

在固定的長寬中，繪製任何形狀。

基本包含:矩形、線條、文字、陰影、上色、漸層

進階包含:動態圖表、基本動畫 

## canvas元素

canvas只有width和height兩個屬性，預設寬為300 px、高150 px。

<canvas></canvas> 需要close tag

產生一個自定大小的畫布、畫紙，在上面可以有多個Rendering context(繪圖環境or渲染環境)。

一開始canvas是空白的，必須先取得Rendering context才能開始繪圖。

canvas元素有個method **getContext()**，透過它可以取得rendering context還有相關的繪圖function。getContext()需要給定一個參數，說明這個環境的類型，getContext('2d')代表規劃一個2d的繪圖環境。

基本雛形範例:

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>Hello World-canvas</title>
    <script type="text/javascript">

    function draw() {
    //透過id找出canvas
        var canvas = document.getElementById('hello');
        
        if (canvas.getContext) {
            //宣告繪圖環境為2D
            var context = canvas.getContext('2d');
        }
    }
    </script>
    <style type="text/css">
    canvas {
        border: 1px solid black;
    }
    </style>
</head>

<body onload="draw();">
	<!-- 在html中 設定canvas的長寬屬性 -->
    <canvas id="hello" width="300" height="300"></canvas>
</body>

</html>
```



## 基本方法

### 繪製線條

- beginPath() -->開始路徑;重設路徑

- closePath() -->關閉路徑

- stroke() -->輸出外框.線條

- fill() -->輸出填滿的內容

  **移動畫筆**

  - moveTo(x,y) -->移動到某個位置 (畫筆落點)
  - lineTo(x,y) -->畫線

步驟: 

1. 建立路徑(beginPath)
2. 利用commands 繪製路徑(座標位置)
3. 路徑建立完成後,選擇填滿或是描框

```javascript
function draw() {
      //找出canvas畫布
      var canvas = document.getElementById('hello');
     
    if (canvas.getContext) {
        // 宣告context為2d類型的rendering環境
        var context = canvas.getContext('2d');
      }
     
      context.beginPath();  	// 新建一個路徑
      context.moveTo(50, 50); 	//起始點(50,50)
      context.lineTo(100, 100);	//移動到(100,100)
      context.lineWidth=5;
      context.strokeStyle='orange';
      context.stroke();			//畫出形狀 (輸出線條)
      context.closePath();		//關閉路徑
     
      context.moveTo(200,200);
      context.lineTo(250,200);
      context.lineTo(250,250);
      context.fill();			//填滿路徑
    }
```

![canvas-paths](https://imgur.com/cAwMrEb.jpg)

### 繪製矩形

- rect(x,y,width,height) -->矩形 (座標為矩形左上的座標)

![canvas origin](https://imgur.com/KXwN6EY.jpg)

- strokeRect(x,y,width,height) -->輸出矩形-框
- filllRect(x,y,width,height) -->輸出矩形-填滿
- clearRect(x,y,width,height)-->清除矩形,變透明

### 其他

- clip() -->裁切

> 在clip內的範圍，圖形才會顯示
>
> ~遮罩效果

### 繪製曲線

- arc(x,y,radius,startAngle,endAngle,anticlockwise) 

> 以弧度表示 radians = (Math.PI/180) * degrees
>
> anticlockwis-> true為逆時鐘針
>
> ```javascript
>   function draw() {
>       var canvas = document.getElementById('hello');
>       if (canvas.getContext) {
>         var context = canvas.getContext('2d');
>       }
>       context.beginPath();  	
>       context.arc(150,150,50,0,0.5*Math.PI,0);
>       context.stroke();
>     }
> ```

- arcTo(x1,y1,x2,y2,radius)

  >搭配moveTo(x0,y0) ->開始點
  >
  >開始點 & 點1 & 點2，3個點所夾的角，描繪和夾角兩邊相切且半徑為r的弧 
  >
  >```javascript
  > function draw() {
  >      //找出canvas畫布
  >      var canvas = document.getElementById('hello');
  >      if (canvas.getContext) {
  >        // 宣告context為2d類型的rendering環境
  >        var context = canvas.getContext('2d');
  >      }
  >  	context.strokeStyle = 'red';
  >	context.lineWidth = 5;
  >	context.moveTo(100,250);
  >	context.arcTo(200,100,300,210,100);	
  >	context.stroke();
  >
  >	context.strokeStyle = 'blue';
  >	context.lineWidth = 1;
  >	context.beginPath();
  >	context.moveTo(100,250);
  >	context.lineTo(200,100);
  >	context.lineTo(300,210);
  >	context.stroke();
  >    }
  >```
  >
  >![arcTo](https://imgur.com/MTrQ5Sm.jpg)

- quadraticCurveTo(cx,cy,x1,y1) -->貝茲二次曲線

- bezierCurveTo(cx0,cy0,cx1,cy1,x1,y1) -->貝茲三次曲線

  ![bezierCurve](https://imgur.com/vxMEVDn.jpg)

### 套用樣式

#### 顏色

- fillStyle=color
- strokeStyle=color

#### 線條

- lineWidth=value
- lineCap=type (線條開始和結尾的樣式)
- lineJoin=type (線條接合的樣子)

#### 漸層

- createLinearGradient(x1,y1,x2,y2)
- createRadialGradient(x1,y1,r1,x2,y2,r2)



### 補充

[HTML 5 Canvas Uses](<https://www.lifewire.com/why-use-html5-canvas-3467995>)

[Canvas v.s.SVG](<https://www.sitepoint.com/canvas-vs-svg-choosing-the-right-tool-for-the-job/>)
 附上笑臉一枚

```javascript
  function drawSmile() {
      //找出canvas畫布
      var canvas = document.getElementById('hello');
      if (canvas.getContext) {
        var context = canvas.getContext('2d');
      }
     
    context.lineCap='round';//線圓頭
	context.lineJoin='round';//線接圓頭
	context.fillStyle = '#F3C445';//臉的顏色(外圈-深)
	context.beginPath();
    context.arc(143,108,80,2*Math.PI,false);
    context.fill();
    context.closePath();

    context.fillStyle = '#FAD578';//臉的顏色(內圈-淺)
    context.beginPath();
    context.arc(143,103,73,2*Math.PI,false);	
    context.fill();
    context.closePath();	

    //左眼
    context.strokeStyle = '#2F374C';
    context.lineWidth= 6;
    context.beginPath();
    context.moveTo(97,88);
    context.quadraticCurveTo(118,50, 128,92);
    context.stroke();
    context.closePath();

    //右眼
    context.beginPath();
    context.moveTo(156,91);
    context.quadraticCurveTo(168,50, 187,87);
    context.stroke();
    context.closePath();

    //嘴上橫直線
    context.fillStyle = '#e4eeeb';
    context.beginPath();
    context.moveTo(99,119);
    context.lineTo(186,119);
    context.stroke();
    context.closePath();

    //嘴下圓弧
    context.beginPath();
    context.arc(143,105,46,0.1*Math.PI,0.9*Math.PI,false);
    context.fill();
    context.closePath();
    context.stroke();

    }
```

