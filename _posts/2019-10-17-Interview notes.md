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

**10/25更新**

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

---

#  XX電X

想說早點到, 可以從容一點

但...從帶入房間考試開始就感覺得出來**催促感**

還沒坐下,包包也還沒放下 

只聽見關鍵字 **xx:31分 我會進來收卷**

從容感瞬間消失

筆試共45題 記得是20分鐘作答

- 第一部分是圖形式的邏輯選擇題

  給3~4個圖形，找出規則

  選出下一個可能的圖形

- 第二部分也是很常見的空間算方塊總數



筆試結束後兩位主管進來，似乎是兩個不同部門

一個電腦中心

一個UI/UX

主要都是電腦中心的主管在問

職缺內容有提到使用**angular**

所以不意外很多問題都圍繞在angular相關

被問到像是:

- Observable 和 Ajax差異
- SPA好在哪
- 解釋什麼是跨同源，怎麼解決
- 解釋生命週期
- 用過Redux嗎
- 在Angular中使用過jQuery的經驗嗎? 遇過地雷?
- SQL熟悉程度為何?
- 用過Subject嗎?

小結: 過程中完全沒有問我有沒有其他問題

也沒有在介紹職缺的工作內容

於是 當下大概知道是 無聲卡一張了...

不過 重點是經驗累積!!! 

---

# XX大xx

主要是在yourator博覽會的廠商名單看到這家公司

公司是做行動廣告投放的  行銷相關

不意外大家都愛考試...

這是筆試主要是考HTML5+Javascript 60分鐘

共12題(in English...)

1. 印出1~100, 但遇到3倍數印出abc,5倍數時印出cba,是3又是5倍數時印出abccba
2. 3:15時針分針所夾角度
3. 解釋[GET] [POST]
4. 解釋RESTSFUL
5. == V.S ===有何不同
6. 解釋closure
7. 什麼是NaN, 怎麼檢測數值是不是NaN
8. console.log(0.1+0.2==0.3) 會印出什麼, 並解釋
9. encodeURI() V.S. encodeURIComponent()
10. what reason wrapping the entire content of a javascript source file in a function block
11. How Are First-Party and Third-Party Cookies Different
12. HTML5 特色有哪些



接下來也是一位主管跟資深工程師進來問問題

可能是因為程式相關問題筆試考了

所以面談時 主要都是問一些過去經驗

跟介紹這個職缺的角色

如同人資提供的資料 這個職缺

因為是做廣告專案 時程最小0.5天

都是1人負責

重大節日會需要配合加班

過年大節日會需要留守公司

有一直強調是不是可以接受加班這件事

不知不覺又是談了個兩個小時

最後再由人資進來介紹公司薪資結構

N*15(含年終&績效等等)

最後最後 

主管出了作業.....一周內繳交

Anyway....

尋找方向中.....





