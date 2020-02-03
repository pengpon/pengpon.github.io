---
layout: post
title:  "淺談Hoisting"
date:   2020-02-02 14:00:00 +0800
author: Pon
categories: web javascript
tags: web 
---



> 筆記~筆記~**克服 JS 的奇怪部分** 



# 開始之前

- 為什麼要了解Hoisting??

  因為面試會考?

  因為大家都說重要?

  因為想更了解javascript?

  因為有助於debug?

  因為想變強?

  

- 要怎麼做??

  上網google大神們的文章/討論?

  去書店翻書?(犀牛書....)

  讀書會交流?

  找線上課程?

小測驗先:

```javascript
console.log('name is', name);
var name;
console.og('name is', name);
name='peng';
console.log('name is', name);
```





# 了解Javascript 運作前.....

- 直譯/編譯?

Javascript為直譯式的程式語言，代表code不需要先compile才能執行

但電腦如何知道script中敘述的code要做什麼?

因為......

這是**Javascript engine**的工作

Javascript 引擎負責轉譯我們的source code,並執行轉譯後的結果

![Javascript engine](https://imgur.com/cNYu6GC.jpg)

遙想.....開始寫javascript時，不需要安裝任何額外的軟體

因為現在每一個瀏覽器都有Javascript engine, 可以很輕鬆的執行我們寫的script!

- Chrome V8: google chrome
- SpiderMonkey: Firefox
- Nitro: Safari
- Chakra: Edge



<br>



## Syntax parser-語法解析器

> *A Program that reads your code and determines what it does and if its grammar is valid.*
>
> 逐字讀取我們所撰寫的程式碼，解析語法是否正確，轉譯成電腦指令.

中間的角色: 編譯器/ 直譯器 >>>語法解析器

*也就是browser中javascript engine負責!*

![syntax parser](https://imgur.com/Tz1ZkD8.jpg)

## Execution context-執行環境

> *A wrapper to help  manage the code that is running.*
>
> 管理正在執行的程式



## Lexical environment-詞彙環境

> *Where something sits physically in the code you write.*
>
> 程式碼在程式中實際的位置.
>
> 對javascript，程式碼寫的位置不同代表不同意思，所謂的**詞彙環境**就顯得很重要
>
> **不是每個程式語言都存詞彙環境**!!

依code所在位置、周圍環境，幫助解析器決定變數/函數

根據詞彙環境幫助我們想像變數/函數在電腦記憶體的位置!!



# Global execution context-全域執行環境

*the javascript engine creates the global execution context before it starts to execute any code.*



**可以在任何地方取用他**

初始化時，創造global object以及變數this

執行javascript時，永遠會有一個全域物件

(for browser>> window物件; 每個視窗有各自的執行環境自己的全域物件)

全域環境下，this變數參照到global object(window)

如果變數和物件不在函數中，就是全域物件~



# 所以執行環境???

**Hoisting 即執行環境的creation階段做的事**

```javascript
var a ="hihihihi"
function b(){
    console.log('called b');
}
b();
console.log(a);

```

```javascript
b();
console.log(a);
var a ="hihihihi"
function b(){
    console.log('called b');
}
// 某些程式會報錯>>> 未宣告就要用b
// output
// called b
// undefined
```

網路解釋: javascript的變數和函數被提升到程式碼最上面

不能說錯但....容易造成誤解...程式碼會搬動?

<br>

## 執行環境運作

執行環境被創造有兩階段

- creation phase

  全域物件和this存在記憶體中& 創造外部環境

  **setup memory space for variables and function**

  這個步驟稱為**hoisting**

  逐行執行前 替變數在記憶體中建立一個空間

  當程式被逐行執行時, 才可以找到這些變數

- execution phase

  逐行執行程式碼

```javascript
function b(){
    console.log('called b!')
}
b();
console.log(a);
var a ='hihihiihihi';
console.log(a);
// 將function b & variable a在記憶體建立空間(只有空間 沒有值 沒有內容)
// 呼叫b() 建立function b 執行環境
// 印出 'called b'
// 找出a的值 並印出
// 將'hihihiihihi'賦值給變數a (a的記憶體位址指向字串hihihiihihi)
// 找出a的值 並印出
```

# 單執行緒&同步執行

javascript不是瀏覽器唯一的東西

javascript為單執行緒不是指瀏覽器, 

同步:程式碼會依照出現順序一次執行一行

<br>

# 函數呼叫&執行堆

```javascript
function b(){
    
}
function a(){
    b();
}
a();

```

一個新的執行環境創造-->被放進stack中

誰在最上面就是就是正在執行的東西

會有自己的記憶體空間給變數和函數

<br>

## 函數&環境&變數環境

- 變數環境:描述創造變數的位置以及和其他變數的關係

```javascript
function b(){
    var myvar;
    console.log(myvar);
}
function a(){
    var mywar=2; // 創造myvar在自己的變數環境中
    console.log(myvar);
    b(); // 呼叫函數 創造出他的執行環境
}
var mywar=1;
console.log(myvar);
a();
console.log(myvar);
```

<br>

## scope chain

> scope:能取用變數的地方
>
> chain: 外部環境參照的連結

```javascript
function b(){
    console.log(myvar);
}
// 從詞彙上來看, 在全域環境中!

function a (){
    var myvar=2;
    b();
}
var myvar=1
a();

```

處理變數時, javascript 不只會在執行環境的變數環境中尋找

外部環境的參照

每個執行環境都有一個外部環境

當你需要某個執行環境內的程式碼變數, 如果找不到變數, 他會到外部環境尋找變數

外部環境是根據函數實際上的位置

![scope chain](https://imgur.com/ZDYFpjk.jpg)

```javascript
function a (){
   var myvar=2;
   function b(){
   		console.log(myvar);
	}
    // 從詞彙上來看, a()環境中!
    // 外部參照為a()
}

var myvar=1
a();
```

# 範例

```javascript
function test(){
	console.log();
	console.log(foo());
	var a=1;
	function foo(){
		return 2;
	}
}

test();
// 全域環境下:宣告函數test
// 呼叫test()
// 建立test執行環境 
// 宣告a變數及foo函數
// 印出() >>> undefined
// 呼叫foo() 並印出
// 建立foo執行環境
// 逐行執行 回傳2

```

<br>

# 題外話-Javascript發展歷史

> 推薦[The Weird History of JavaScript](https://dev.to/codediodeio/the-weird-history-of-javascript-2bnb)&[從ES6開始的JavaScript學習生活-歷史篇](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part1/history.html)

## 1990-1999

- 1990

  第一個web browser [WorldWideWeb](https://worldwideweb.cern.ch/browser/), 由Tim Berners Lee開發 (後來改名Nexus)

- 1993

   Marc Andreessen and Eric Bina 開發Mosaic Browser

- 1994

  - Marc 成立網景

  - 網景推出第一款Netscape Navigator瀏覽器, 市佔達70%
  - 微軟發展自家瀏覽器IE, 搭著windows 95一起

- 1995

  - 網景公司瀏覽器市占80%
  - 微軟進軍瀏覽器市場(買作業系統送IE瀏覽器)

  - Brendan Eich 在面對微軟的壓力之下，利用10天創造出名為Mocha的語言
  - 為了市場考量，改名為Javascript
  - 

- 1996
  - 微軟發布JScript (模仿Javascript語言的產品)
  - Netscape(網景)公司向ECMA國際組織提交Javascript (搶當標準~)

- 1997 

  產生第一個Javascript標準規範(ES1)，ECMA-262/ECMAScript

- 1998-**第一次瀏覽器大戰**

  - IE取得瀏覽器市場90%
  - 因壟斷微軟遭政府起訴 (在自家作業系統綁定IE瀏覽器)-反托拉斯法

  - 發布ES2
  - 網景公司被AOL收購
  - 網景開放瀏覽器及相關產品的**原始碼** (Mozila基金會Firefox的前身)

- 1999

  發布ES3

## 2000-2008

- 2000開始.....

  - ES4,加入classes, interface...等很大幅度的改變，被認為太複雜......擱置.....
  - 微軟IE仍是瀏覽器市場第一(不太甩ECMAScript,在自己的瀏覽器中用自己的JS新功能)

- 2002

  IE瀏覽器達到90%以上的市場佔有率

- 2003

  - Apple發佈Safari瀏覽器 (支援Mac平台外，也支援Windows作業系統)
  - 網景公司解散

- 2004-**第二次瀏覽器大戰**
  - Mozilla基金會發表Firefox 1.0瀏覽器
  - Opera瀏覽器，與Mozilla共同參與了推動瀏覽器相關規格的開放標準化
  - 對戰Microsoft

- 2006

  John Resig開發了JQuery

- 2008

  Google進軍瀏覽器市場釋出chrome瀏覽器以及V8 engine(開放其原始碼)

## 2009-2015

- 2009

  - Ryan Dahl利用google的V8 Project開發NodeJS

  - 隔了10年, 發布了ES5

- 2010

  AngularJS和Backbone框架出現

- 2012
  - Chrome超越IE, 成為世界上使用最多的瀏覽器
  - apple停止safari for windows

- 2013

  - Facebook釋出ReactJS

  - 在這段期間frontend, backend, and fullstack框架出現

    ( Angular, Ember, Meteor, Sails, Vue, Svelte, Mithril, Knockout, Polymer...)

## 2015-Now

- 2015

  - ES6釋出

  - 微軟發布Edge(成為win 10 預設瀏覽器)

- 2016

  ES7釋出

- 2017

  ES8釋出

- 2018

  ES9釋出

# 延伸閱讀&參考圖文

[我知道你懂 hoisting，可是你了解到多深?](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/)

[The JavaScript runtime environment](http://dolszewski.com/javascript/javascript-runtime-environment/)

[The Weird History of JavaScript](https://dev.to/codediodeio/the-weird-history-of-javascript-2bnb)

[從ES6開始的JavaScript學習生活-歷史篇](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part1/history.html)

[The History of Web Browsers-1994~2011演化圖](http://www.testking.com/techking/infographics/browser-evolution-the-history-of-web-browsers-infographic/)

