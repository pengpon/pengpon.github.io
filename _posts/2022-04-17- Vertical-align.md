---
layout: post
title:  "消除圖片底下萬惡的空白"
date:   2022-04-17 12:46:00 +0800
author: peng
categories: web
tags: css
comments: true
---


以 [How to get rid of the gap under the image ](https://www.geeksforgeeks.org/how-to-get-rid-of-the-gap-under-the-image/) 這篇文章來做心得筆記

剛開始切版的時候，肯定很常遇到圖片底下有個不知名空白

## 造成原因
來自瀏覽器的預設造成，`<img>` 預設為 `inline element`

所以圖片會比照一般的字母文字來做處理&顯示

也就是以 baseline 為對齊基準

像是 g, y 這樣的字母有 Descenders (小尾巴?!) (Wiki稱:降部)

字母會有超過 baseline 向下延伸的部分

所以當圖片也是以 baseline 為基準時

底下就會有一小段的空白

**(白話: 把圖片當作一個沒有 Descenders 的字母)**


![文字基準線](https://i.imgur.com/k7myQR0.png)
圖取自 [Wiki](https://zh.wikipedia.org/wiki/%E9%99%8D%E9%83%A8)



## 解法

消除的作法有三種

1. display
2. vertical-align
3. line-height

### display
最常見的處理方式

將包在 div 中的 img

display 屬性 從 inline 改為 block



### vertical align
原本預設會以這些 inline element 父元素的 baseline 為基準

將 vertical-align 屬性從 baseline 改為 bottom

### line-height

將容器的 line-height 設為 0


## 補充

### inline elements

所有的元素預設都是 `inline`, 大部分的瀏覽器會把許多元素重置為 block 

元素分類成 block-level 或是 inline-level 

inline element 中只會有 data 或其他 inline element

不能將 block element 放置在 inline element 中

預設 inline element 不會強制換新行, block element 則會

可以透過 display 這個屬性, 改變元素的外觀 or 顯示方式
(但不會真的改變元素的分類)



### vertical-align

照字面的意思, 為了讓內容物可以垂直置中排列, 很容易會把他誤用在子元素或是父容器上

但其實是 **用來控制在同一行中彼此相鄰元素要如何排列!**


引用 MDN 官網上的一段話

> The vertical-align CSS property sets vertical alignment of an inline, inline-block or table-cell box.

有兩個對象可以使用這個屬性:

1. inline element, inline-block element
2. table-cell box


以下情境會使用到:
1. line box中的 inline element's box (例如: 一段文字中的 image)
2. 表格中的 cell 內容

**切記: vertical-align 用在 block-level element 是無效的!!**



### 範例
<script async src="//jsfiddle.net/shanpeng33/hkyL6wn4/4/embed/html,css/"></script>

## 參考
[vertical-align](https://css-tricks.com/almanac/properties/v/vertical-align/)

