---
layout: post
title:  "CSS Display Basic property - Inline and Block "
date:   2019-07-06 23:30:00
author: Pon
categories: web
tags: css layout
---
> 一日不讀書 便覺得面目...
>
> 一步一步把兩年前東西 複習起來



# 前言

## what is 'CSS'???

> CSS(Cascading Style Sheets)，描述文件或是內容**該如何呈現**
>
> 當瀏覽器要顯示一份文件時，就要綜合文件的**內容**和**樣式**
>
> 分成兩個階段處理:
>
> - 瀏覽器轉換html和css成為DOM(Document Object Model)
>
> - 瀏覽器顯示DOM
>
> - DOM就像一個樹狀結構，每一個元素、屬性或是文字內容都可以視作DOM的nodes
>
>   ![css how to work](https://imgur.com/DT6UYHA.jpg)
>
>   **以為瀏覽器這麼簡單的話.....就淺了....
>
>   [送出網址後 what happened??](<https://cythilya.github.io/2018/11/26/what-happens-when-you-type-an-url-in-the-browser-and-press-enter/>)
>
>   



### How to apply CSS in html???

> 有三種套用css到html的方式
>
> 1. External stylesheet(最推薦!!!!!  樣式有變動時 只要改css檔案 就可以套用在多個html上)
>
> > 將css寫成一個style.css的檔案
> >
> > 在<head> 中 使用<link>引用這個style.css
> >
> > ```html
> > <html>
> >     <head>
> >        <meta charset="utf-8">  
> >         //meta中放網站內容描述或是SEO相關關鍵字以及編碼  
> >         <title>Apply CSS in html 'Method 1' </title>
> >         <link rel="stylesheet" type="text/css" href="style.css"> 
> >     </head>
> >     <body>
> >         <h1>我是標題1</h1>
> >     </body>
> > </html>
> > ```
> >
> > 
>
> 2. Internal stylesheet 
>
> > 將css寫在<head>中的<style>
> >
> > ```html
> > <html>
> >     <head>
> >        <meta charset="utf-8">
> >         <title>Apply CSS in html 'Method 2'</title>
> >         <style>
> >             h1{
> >                 font-size:20px;
> >                 color:red;
> >             }
> >         </style>
> >     </head>
> >     <body>
> >         <h1>我是標題1</h1>
> >     </body>
> > </html>
> > ```
>
> 3. Inline styles (爆炸不推薦!!!!!! 如果<p>要統一改字體大小,在html出現100次,就要改100個地方,雖然有取代功能.....)
>
> > 在style屬性中改變單一元素的樣式
> >
> > ```html
> > <html>
> >     <head>
> >        <meta charset="utf-8">
> >         <title>Apply CSS in html 'Method 3'</title>
> >         <style>
> >             h1{
> >                 font-size:20px;
> >                 color:red;
> >             }
> >         </style>
> >     </head>
> >     <body>
> >         <h1 style="color:red">我是標題1</h1>
> >     </body>
> > </html>
> > ```



**在回到正題前.....**



還有一件**必須必須**知道的事

市面上瀏覽器百百種，並沒有規定該如何制訂每一個html tag的樣式...

比如說<a>連結 底線?? 藍字??  bla bla的

所以每一家瀏覽器都有**自己訂定的樣式** !!!!!

所以同一份html和css 用不同的瀏覽器看起來不一樣是很正常的

這個時候 就必須知道 **Reset CSS**

宗旨就是強制把瀏覽器預設的樣式都清除!!!  通通歸零!!!



普遍大家最常用的CSS Reset

NO.1 Eric版本 [Reset CSS](<https://meyerweb.com/eric/tools/css/reset/>)

只要copy paste到css就好



但 缺點是...  Reset CSS 是把一大堆tag的margin padding border 都設成0,h1~h6看起來一樣

使用者必須重新自己設定, 於是.......

出現了[Normalize CSS](<http://nicolasgallagher.com/about-normalize-css/>) (保留瀏覽器的setting, 修正各家瀏覽器的不一致 )



進入 這一篇的重點....

# Display 屬性

>每一個在網頁中的元素 都可以視為**矩形** 
>
>display的屬性 只是用來決定這個矩形 該如何表現



**CSS  常用 屬性**

> - inline   			*所有元素的預設 都是inline     除非User agent stylesheet(瀏覽器樣式) 有覆寫掉
>- block               *UA stylesheet造成的 像是<div>或是<section>被改成block
> - inline-block    *
> - none               *隱藏



1. inline

> - 不會換行
>
> - 想像成**區段**或是**長度**
>
> - 無法撐開高度!!!  所以設定寬高也沒有效
>
> - 大小是被內容所撐開

2. block

> - 瀏覽器將<div>  <section> <ul> <p> <h1>等元素 設成block
>
> - 想像成**區塊**，會從新的一行開始
>
> - 預設會跟父元素同寬度(能多寬就多寬!!)
>
> - 有面積的概念，可以設定height、width、margin及padding等

3. inline-block

> - 綜合inline和block的特性
>
> - 可橫向排列+可設定寬高

4. none

> - 不顯示元素，也不佔空間
>
> - visibility:hidden亦也不顯示，但會保留空間



inline或是inline-block 兩個元素之間會有預設的保留空間
可[參考消除方法](https://css-tricks.com/fighting-the-space-between-inline-block-elements/)



最後重點!!!!!!!!!!!!!!!!!!!!!!

![display basic](https://imgur.com/C8tqaVP.jpg)











除了基本常用的外....還有

- flex
- table
- grid



就留到下幾篇寫 顆顆!!





**參考**

[CSS運作原理](<https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/How_CSS_works>)

[what is css reset](<https://cssreset.com/what-is-a-css-reset/>)

[MDN display](<https://developer.mozilla.org/en-US/docs/Web/CSS/display>)









