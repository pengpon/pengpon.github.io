---
layout: post
title:  "面試紀錄 持續更新ing"
date:   2019-10-17 14:35:00 +0800
author: Pon
categories: web 
tags: interview
---
> 書到用時 方恨少
>
> 當一直被問到一個明明知道很重要的東西時
>
> 就會想挖洞跳!



# x力資訊

這家是自己主動投遞的

在104職缺名稱為前端工程師

所需的技能也敘述的很恰當(不會包山包海)

官網做得算用心，有自家產品也有接專案

專案包含壽險業、銀行金融業、電信業

產品是自家AI團隊負責研發

以及公司有一個技術交流平台，

公司員工(?)會分享技術，其實就是鼓勵工程師們寫Blog

還有公司也會對外辦技術交流的研討會

公司環境看起來也不錯!!!!!

在還沒面試前 印象加分!

## 筆試

跟大部分公司一樣 邏輯+JS試題



邏輯大約10題  有單選+複選

自己的感覺就是文字敘述的數學題.....



JS試題是選擇+簡答

這部分真的是花比較多時間 (猶豫不決)

觀念包含 

- JS的轉型運算

- ES6 Rewrite
- bind()
- promise

幾乎都是給一段code 問console.log 印出什麼

爆炸想打開電腦

後悔沒多刷幾題 (網路上一堆)

不過很多觀念確實是在前陣子 看udemy **Javascript weird part**才建立的!!

```javascript
function test() {
  console.log(a);
  console.log(foo());
  var a = 1;

  function foo() {
    return 2;
  }
}
test();

// 結果會印出
// undefined
// 2

// 記得在creation phase時:
// setup memory space for variables and functions!!
// 執行到console.log(a)時 a只被宣告 還沒被賦值 所以印出undefined
// 而foo()函數已經被放入記憶體中! 所以印出2
```

還有經典的let v.s. var

```javascript
 for (var  i = 1; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
} 
// 結果會印出4次5
// var 會將變數宣告為global
// 當執行到setTimeout時 i為5

```

後來**技術顧問**問到內容 包含:

- ES6的部分 用過哪些
- Webpack的原理 以及調過那些設定
- 說明一下const, arrow function用來?
- SASS優點, 用來做??
- 比較或是說明前端框架差異

包含筆試和口試 整體下來 感覺公司很強調ES6

不斷要求說明用過那些ES6 覺得好在哪....



總之 又是一次經驗的累積!!







