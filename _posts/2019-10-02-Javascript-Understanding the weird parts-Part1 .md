---
layout: post
title:  "Javascript-Understanding the weird parts-[上]"
date:   2019-10-02 14:18:00 +0800
author: Pon
categories: class
tags: javascript udemy
---
> Udemy課程筆記，以及無數個發散出去的延伸閱讀....

------



# 開始之前

- Brackets.io

[Brackets官網](http://brackets.io/)

講師所使用的文字編輯器，內建sever可即時顯示

- Syntax Parser (語法解析器)

  **A program that reads your code and determines what it does and if its grammar is valid.**

- Lexical Environment (詞彙環境)

  **Where something sits physically in the code you write!**

- Execution context(執行環境)

  **A wraper to help manage the code that is running**

  一個包裹的概念，一個由其他人已經寫好的程式

  驗證和執行code

  - Global執行環境
    1. Javascript創造出**Global Object**和**this**變數可以用
    2. 對瀏覽器而言，全域物件為window
    3. Global=Not Inside a Function


------



# 執行環境 (Execution context)

創造執行環境 兩階段:

1. creation phase- **設定記憶體空間**

   - "Hoisting": setup memory space for variables and functions 
   - 所有的Javascript變數一開始被設定為undefined
   - 函數是完全被存放在記憶體中

2. execution phase

   - 逐行執行code
   - 例如 =等號 賦值

   ``` javascript
   function b(){
       console.log('b是我');
   }
   b();
   console.log(a);//第一個console a
   var a ='Hi Hi';
   console.log(a);//第二個cosole a
   //Result
   //b是我
   //undefined
   //Hi Hi
   ```

   在第一個創造階段時

   - 設定b這個函數
   - 並宣告a這個變數，a初始值為undefined

   接著第二個執行階段，逐行執行

   - b() >>執行b函數
   - 執行console.log(a)>>要輸出變數a到console，**在創造階段時, a為undefined**
   - 執行a ='Hi Hi', 把記憶體中a的值設為'Hi Hi'字串
   - 在接著輸出變數a到console, 此時a的值為'Hi Hi'



菜鳥小結:

忘了過去因為什麼原因曾經查過什麼是hoisting提升，在速食文化下的壞習慣，只想趕快找到淺顯易懂的解釋，喔~ "想像變數的宣告 會被搬到 被提升到最上面，但變數賦值這件事還是依照code的順序 " 

現在重新用運作原理來看Hoisting這件事，似乎更懂了一些些!

**JS Engine先進行編譯階段會處理變數和Function宣告**(creation phase)

**接著進入執行階段 逐行run code**(execution phase)

推推延伸閱讀有補上的[我知道你懂 hoisting，可是你了解到多深？](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/) 這篇文章內容很多很豐富,也有很多Reference

****

# 單執行緒&同步執行( Single threaded & synchronous execution)

- single threaded: one command at a time

  **Javascript為單執行緒，不是指瀏覽器**

  **一次執行一個指令**

  **Single threaded means that only one thing happens at a time.**

- synchronous: one at a time

  照順序, 一次一個
  
  **you need to wait for something, then everything stops until the wait is over.**

------



# 函數呼叫&執行堆 (Function invocation & Execution stack)

- Invocation : running a function

  using parentheses ()

  **每一次在Javascript呼叫函數->就會創造一個新的執行環境，這個執行環境被放入執行堆中**

  **每一個執行環境會有自己的記憶體空間存放變數和函數**

  **每當函數被呼叫，一個新的執行環境就被創造給函數，this變數被創造給那個函數**

------



# 範圍鍊 (Scope chain)

**每個執行環境有一個外部環境參照**

**不是execution stack的順序**

外部環境(Outer environment)與詞彙環境有關

**當在執行環境內找不到變數時，會到外部環境尋找變數**

```javascript
function a(){
    function b(){
        console.log(pon);
    }
    b();
}
var pon = '菜鳥';
a();
```

 b函數 外部環境為 a 

a的執行環境找不到 pon

再到a的外部環境 也就是全域環境中找pon

scope : 代表能夠取用變數的地方，where a variable is available in your code

chain: 參照的外部環境

**一層一層往外找**

------



# 非同步 (Asynchronous)

![非同步-browser](https://imgur.com/sVp53VC.jpg)

Javascript engine內等待的清單稱為Event queue(事件佇列)

例如click事件或是http request

Event queue 直到Execution stack是空的時候，才會處理。

直到 Javascript逐行執行完程式。

**不是真正的非同步**

**而是瀏覽器非同步的把東西放到Event queue中，程式還是一行一行執行，當stack空了，再來處理事件**

------

## 補充 

- Javascript Runtime Environment

  **JRE is responsible for making JavaScript asynchronous. It is the reason JavaScript is able to add event listeners and make HTTP requests asynchronously.**

  1. the heap

     **This is the physical memory space that is used to store variables, functions, and objects**

     **和C不同，Javascript有自動回收記憶體的機制**[Garbage collection](https://javascript.info/garbage-collection)

  2. the stack

     **This is where function and API calls (Web API in browsers and C/C++ API on local machines via NodeJs) are stored**

     似stack的資料結構(last-in-first-out)

  3. API (Web API) 

     **This is where the actual functionality for built-in functions like `setTimeout()` and `fetch()` are located**

     其他常用像是:

     - DOM API >> document.getElementById, addEventListener

     - AJAX calls or XMLHttpRequest
     - Timer functions >> setTimeout,setInterval

  4. callback queue

     **Some functions like `setTimeout()` that contact the API’s require a callback function to be provided to it so that it knows what to do after the API function has been run.**

     似queue資料結構(first-in-first-out)

  5. event loop

     **constantly checks the call stack to see if there are any function calls that need to be run.**

     主要做兩件事:持續去監測 execution context stack是不是空的&如果是空的就把callback queue的第一個method移到execution context執行!

  ![asynchronous magic](https://imgur.com/dCXPvrv.jpg)

```javascript
console.log('1');
function timer(){
console.log('I am timer');
}

setTimeout(timer,10000);

console.log('last one');

// 將字串'1'輸出在console
// 宣告一個timer function
// 執行web api-setTimeout, 10秒後執行timer function
// 計時器啟動 開始在背景倒數10秒
// 將字串'last one'輸出在console
// 1s 2s 3s -------10s
// 時間一到 timer function 被放入 callback queue中
// event loop- check stack已空,將callback queue第一個method 移至stack執行
```

------



# 延伸閱讀&圖文出處

[AST for Javascript developers](https://itnext.io/ast-for-javascript-developers-3e79aeb08343)

[Compiler in Javascript using ANTLR](https://medium.com/dailyjs/compiler-in-javascript-using-antlr-9ec53fd2780f)

[Browser Engines: The Crux Of Cross Browser Compatibility](https://www.lambdatest.com/blog/browser-engines-the-crux-of-cross-browser-compatibility/)

[TechBridge 技術共筆部落格-我知道你懂 hoisting，可是你了解到多深？](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/)

[You Don't Know JS Yet (book series) - 2nd Edition](https://github.com/getify/You-Dont-Know-JS)

[Javascript and Asynchronous Magic — Explaining the JS Engine and Event Loop](https://levelup.gitconnected.com/javascript-and-asynchronous-magic-bee537edc2da)

[Garbage collection](https://javascript.info/garbage-collection)

[Introduction to web APIs ](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Introduction)

[JavaScript Internals: JavaScript engine, Run-time environment & setTimeout Web API](https://blog.bitsrc.io/javascript-internals-javascript-engine-run-time-environment-settimeout-web-api-eeed263b1617)