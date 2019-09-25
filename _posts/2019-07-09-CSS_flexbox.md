---
layout: post
title:  "CSS Flexbox　硬翻譯筆記 "
date:   2019-07-09 23:31:00
author: Pon
categories: web
tags: css layout
---

> 在這個裝置尺寸百百種的時代下，產生了Flexible Box的排版模式。
>
> 必須稍稍微的認識一下!!!



# 前言

> 一張圖勝過千言萬語!!
>
> 在邊複習css邊google查資源的同時
>
> 發現了一個介紹[html&css的網站](<https://internetingishard.com/>) (叫做Internet is hard)很喜歡!
>
> 風格、圖表、排版和文字　都很對胃口
>
> 會再挑幾篇　寫成筆記(硬翻譯?!)分享分享!!
>
> 

## Box model v.s. flex model?

先來說說一般基本排版主要是Box model或是稱為區塊模型，把html的元素想像為一個一個盒子，可以去控制padding、margin或是border。由內而外依序是content>padding>border>margin

圖片參考自[Internet is hard](<https://internetingishard.com/>)

![Box Model](https://imgur.com/vyQwPjz.jpg)

這樣的Box Model要排版時，就會常使用到display:inline-block、float或是position等方法。遇到不同裝置時，就有可能爆出裝置尺寸，萬惡的橫軸就出現了!!!或是需要根據不一樣的media修改class

於是出現了**Flex box** (也稱彈性盒子)，顧名思義他能控制item的長或高，以符合空間大小!!!　還有空間時就幫忙補滿空隙，空間不夠時，就幫你自動換行顯示。



## What is Flex box ?

Flexbox model與box model不同在於，Flexbox排列方向是用**Main Axis** 和 **Cross Axis** 的概念!!

想像成在一個Flex Container的容器中，裡面放著一個個item，可以透過**Main**或是**Cross**這兩條軸線去控制item的位置。[圖片參考來源](<https://developer.mozilla.org/zh-TW/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes>)

![flexbox axis](https://imgur.com/xsVQW3y.jpg)

### Flex Container 

**以下圖片皆自[Internet is hard](<https://internetingishard.com/>)**



它是flexbox排版的第一步，利用**display:flex**將html元素轉變成flex container。用意是在告訴browser，所有在這容器裡的東西都要轉換成flexbox，而非預設的box model。

當設定好flex container後，下一步就可以決定內容物item該如何排列

依序介紹:

1. 對齊 (alignment)
2. 換行 (wrapping)
3. 排列方向 (direction)
4. 排列順序 (order)



#### 對齊

- justify-content: center/flex-start/flex-end/space-around/space-between

  > justify-content 即每一個item的水平對齊方式
  >
  > center:置中對齊
  >
  > flex-start:靠左對齊
  >
  > flex-end:靠右對齊
  >
  > space-around:分散對齊(頭尾留白)
  >
  > space-between:分散對齊(頭尾不留白)

![justify-content](https://imgur.com/9X8h6ER.jpg)

![justify-content](https://imgur.com/SGjsvAB.jpg)

- align-items:center/flex-start/flex-end/stretch/baseline

  > align-items 即垂直對齊的方式
  >
  > center:垂直置中
  >
  > flex-start:靠上對齊
  >
  > flex-end:靠下對齊
  >
  > stretch:拉高對齊

![align-items](https://imgur.com/EFOdpaY.jpg)

#### 換行

- flex-wrap:wrap/nowrap(default)

  > 換行與否

  ![wrap](https://imgur.com/i2uhKph.jpg)

#### 排列方向/反序

- flex-direction:row/column

  > 橫列/直欄排列

- flex-direction:row-reverse/column-reverse

  > 橫列反序/直欄反序

  ![flex-direction](https://imgur.com/IHa5Pkr.jpg)

截至目前的內容，都是在透過flex container修改內部item的排列位置，如果想特定改變特定item的排列，也是很ok的!!!

每個item都帶有一個order值，預設是0，**值越大越往右排** (數線的概念～)

> EX:想要放在最左邊的item就可以把order設為-1!　(<-1>-----<0>-----<0>----<0>----<1>----<2>)
>
> 如果在container設定了row-reverse 那麼由左至右的order，就會從大到小排列 (<0>----<0>----<0>-----<-1>)



最後一個屬性**flex**

flex 屬性其實是 **flex-grow** 、**flex-shrink** 、**flex-basis**的縮寫　　(flex-shrink和flex-basis為optional)

flex只給一個值的話 ，也就是flex-grow可以決定item在container中的寬，又或者是說這個屬性讓item具有非常彈性的寬度值!!!

用法類似權重的概念，假設container中有三個item，flex依序為1,1,2，item所佔的寬就為25%、25%、50%!!

![flex](https://imgur.com/jE7JBNE.jpg)



以上．．．．



