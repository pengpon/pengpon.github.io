---

layout: post
title:  "PIXI.js 超入門"
date:   2019-09-05 15:06:00 +0800
---



# 前言

去年lag的被**奔跑吧台北**小遊戲燒到(pixel風格，爆炸懷念)，2018年底玩樂性質的去高雄MOPCON也有幸聽到一場PIXI.js的議程。又是一篇想還債的筆記!

附上:

遊戲開發團隊的前端工程師紀錄的精美文章[連結]([https://medium.com/@chiunhau/%E5%A5%94%E8%B7%91%E5%90%A7-%E5%8F%B0%E5%8C%97-%E7%A8%8B%E5%BC%8F%E5%B9%95%E5%BE%8C%E5%88%86%E4%BA%AB-e02d0a565559](https://medium.com/@chiunhau/奔跑吧-台北-程式幕後分享-e02d0a565559))

遊戲網址[連結](<https://game.glory.taipei/>)

正題開始!

### Pixi.js?

Pixi.js使用WebGL，是一個HTML5 2D渲染引擎。

根據官方文件說明的優點像是:

1. 渲染快,效能好
2. 官網提供很多範例應用
3. 可以結合Greensock,create.js



### 設定

#### 安裝Pixi

如同其他library，可於HTML script tag中載入

```
<script src="pixi.min.js"></script>
```

or

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/pixi.js/4.5.1/pixi.min.js"></script>
```

基本的HTML架構:

```HTML
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello World</title>
</head>
  <script src="pixi/pixi.min.js"></script>
<body>
  <script type="text/javascript">
    let type = "WebGL"
    if(!PIXI.utils.isWebGLSupported()){
      type = "canvas"
    }

    PIXI.utils.sayHello(type)
  </script>
</body>
</html>
```

PIXI載入正確的話，在console中可以看到

![pixi_hello](https://imgur.com/jKl0b3q.jpg)

### 建立Pixi Application 以及 **stage**

第一步是建立一個矩形區域，讓圖像在這個區域中顯示。

Pixi有個Application物件(也就是會產生一個canvas元素)，之後產生的所有物件都會放到這個Application中。

Pixi container物件稱作為stage，一個父容器的概念。

首先新建一個Pixi application

```javascript
// 宣告app為一個PIXI的Appliction物件
let app = new PIXI.Application({width: 256, height: 256});
// 在body中會產生一個canvas元素
document.body.appendChild(app.view);
```

除了設定基本的width和height外

還有antialias(去除文字鋸齒),transparent(背景透明)等參數可以設定。

利用Pixi的renderer物件能有更多的視覺效果

```javascript
// 背景色
app.renderer.backgroundColor = 0x061639;
// 設定canvas滿版-範例code
// renderer為PIXI的渲染引擎
// renderer.view是建立的canvas
app.renderer.view.style.position = "absolute";
app.renderer.view.style.display = "block";
app.renderer.autoResize = true;
app.renderer.resize(window.innerWidth, window.innerHeight);
```



### Pixi sprites

上次有提過sprite，可以把很多張小圖合併成一張圖，透過position去決定當下要顯示哪個小圖(很常拿來做動畫)

Pixi有個sprite的class，三種建立方式

1. 單一個圖像檔
2. tileset圖像
3. textture atlas(JSON格式檔案)

圖片需要被格式化成Texture(WebGL-ready image)，GPU才能處理。

```javascript
// 載入的圖像先放入texture cache中
PIXI.utils.TextureCache["images/ooxx.png"];
```

先建模 再放圖

```javascript
let texture = PIXI.utils.TextureCache["images/ooxx.png"];
let sprite = new PIXI.Sprite(texture);
```

### Pixi loader

利用loader物件，可以載入任何類型的圖像

```javascript
PIXI.loader
  .add("images/ooxx.png")
  .load(setup);

function setup() {
  
    let sprite = new PIXI.Sprite(
  PIXI.loader.resources["images/ooxx.png"].texture
);
}
```

來用奔跑吧台北的主角當作練習

![柯先生](https://imgur.com/bY0DBhn.png)

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>Pixi sprites 練習</title>
</head>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pixi.js/4.5.1/pixi.min.js"></script>

<body>
    <script type="text/javascript">

    // 宣告app-設定canvas的大小,透明度    
    let app = new PIXI.Application({
        width: 256,
        height: 256,
        transparent: true,
    });

    //append canvas到HTML中
    document.body.appendChild(app.view);

    //載入圖片& 載完後Run setup function
    PIXI.loader
        .add("../githubPage/Material/koko_example_single.png")
        .load(setup);

    let kpkp;
        
    function setup() {

        //建立sprite
        kpkp = new PIXI.Sprite(PIXI.loader.resources["../githubPage/Material/koko_example_single.png"].texture);

        //將建立好的sprite-kpkp 加入到stage中
        app.stage.addChild(kpkp);
       // ticker物件 用來建立game loop
       // game loop 每秒可刷新60次 (流暢不會卡)
        app.ticker.add(delta => gameLoop(delta));
    }
         function gameLoop(delta) {
        //每次移動2 pixel
          kpkp.vx = 2;
          kpkp.x += kpkp.vx;
    }
    </script>
</body>

</html>
```

小結:

- 宣告一個Pixi application
- append到html (產生canvas)
- loader載入圖片
- 建立sprite(給圖片texture)
- sprite增加到stage中

application(canvas)>stage(container)>sprite>texture

以上 Pixi.js超入門

告一小段落!

