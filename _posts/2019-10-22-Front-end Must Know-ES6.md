---
layout: post
title:  "ES6 複習彙整[上]"
date:   2019-10-22 14:21:00 +0800
author: Pon
categories: web 
tags: interview
---


# ES6 

ECMAScript 6 (ES6): ECMAScript第6版，2015年發布

重點新語法如下:

## 變數宣告 let, const  (block scope)

- const常數，不能變動其記憶體位置
- 指向的**內容**是可以變動的
- let在宣告前不能使用
- let,const 作用域在{}中

---



##  Template Literals 

- 可將變數放入 ${}

- ```javascript
  // ES5寫法
  var name = 'Your name is ' + first + ' ' + last + '.'
  var url = 'http://localhost:3000/api/messages/' + id
  
  // ES6寫法
  var name = `Your name is ${first} ${last}.`
  var url = `http://localhost:3000/api/messages/${id}`
  ```

---



## Destructuring assignment  解構賦值

- value assignment 

- array的第幾個值assign給變數

- object對應的key值assign給變數

- ```javascript
  // Array
  const [a,b]=[1,2] // a=1, b=2
  const [a, ,b]=[1,2,3] // a=1, b=3
  const [a,...b]=[1,2,3] // a=1, b=[2,3]
  
  const str="hello"
  const [a,b,c,d,e]=str 
  ```

- ```javascript
  // Object
  let obj={
      website:"pengpon.github.io",
      country:"Taiwan"
  }
  let {website,country}=obj;
  
  // 完整寫法
  let {website:websiteValue,country:countryValue}=obj;
  // 根據屬性名稱來給變數值
  // 值是給冒號後的變數
  ```

- 陣列的解構賦值要注意順序

- 物件的解構賦值要注意key值，**常用來處理JSON data**

- 可以給預設值

- ```javascript
  const [missing = true] = []
   console.log(missing)
   // true
  
   const { message: msg = 'Something went wrong' } = {}
   console.log(msg)
   // Something went wrong
  
   const { x = 3 } = {}
   console.log(x)
   // 3
  ```

- ```javascript
  // 
  const { a ='hello' } = 'hello'
  const [ b ='hello' ] = 'hello'
  
  console.log( a, b)
  // 結果會是a=hello, b=h
  
  // 宣告a變數 預設值為字串 hello
  // {a}='hello' 尋找有無a這個屬性
  // 'hello'並無a這個屬性 所以a的值為一開始的預設值"hello"
  
  //宣告b變數 預設值為字串 hello
  // [b]='hello'
  // b的值為字串的第一個字元 'h'
  
  
  ```

---



## Default Parameters 參數預設值

- 幫函式的參數加上預設值

- 可防止exception出現

- ```javascript
  // ES5
  var link = function (height, color, url) {
      var height = height || 50
      var color = color || 'red'
      var url = url || 'http://azat.co'
      ...
  }
      
  // ES6
  var link = function(height = 50, color = 'red', url = 'http://azat.co') {
    ...
  }
  ```

---

## Multi-line String 多行字串

- 透過`，輸入多行字串

---



## Object Literals 

- ES6提供新的語法 讓物件更簡潔

- 物件屬性初始化

  ```javascript
   // ES5
   function getProfile(name, age, gender) {
          return {
              name: name,
              age: age,
              gender: gender
          }
       // 變數名稱和屬性名稱一樣 
      }
  
    console.log(getProfile("peng", "18", "F"));
  // {name: "peng", age: "18", gender: "F"}
  ```

  ```javascript
  // ES6
  function getProfile(name, age, gender) {
          return {
              name,
              age,
              gender
          }
      // 若屬性名稱和賦值的變數名一樣, ES6提供簡寫
      }
  
    console.log(getProfile("peng", "18", "F"));
  // {name: "peng", age: "18", gender: "F"}
  ```

  

- 物件函式簡寫

  ```javascript
   //ES5
      function getHello(name) {
          return {
             sayHello : function() {
                  return `Hi, I am ${name}`;
              }
          }
      }
  
     console.log(getHello("peng").sayHello()); 
  //"Hi, I am peng"
  ```

  ```javascript
  //ES6
  // 省略function關鍵字和冒號
   function getHello(name) {
          return {
             sayHello() {
                  return `Hi, I am ${name}`;
              }
          }
      }
  
     console.log(getHello("peng").sayHello());
  ```

  

- 屬性名稱可運算

  ```javascript
      var type= "type";
      var i = 0;
      const book = {
          [type + ++i]: "html",
          [type + ++i]: "css",
          [type + ++i]: "javascript"
      }
  
      console.log(book);
  //{
  //	type1:"html",
  //  type2:"css",
  //  type3:"javascript"
  //}
     
  ```

---

## Arrow Function 箭頭函式

- ```javascript
  // 簡單比較
  // with arrow function
  hello = () =>{
      return "hello world!"
  }
  
  //before
  hello = function(){
      return "hello world!"
  }
  
  //如果function只有一行statement,而statement是要return一個值
  //可以省略{}和return不寫
  hello = () => "hello world";
  
  ```

- 在一般的function中, **this**通常為呼叫函式所代表的物件, **誰呼叫了function, this就指向誰**

  ```javascript
  function A() {
  console.log(this)
  }
  A();//Window
  
  // function A在全域環境中執行 
  // 全域物件window呼叫此函式
  // this指向window
  ```

  ```javascript
  var b = {
  getThis:function(){
  console.log(this)
  }
  }
  b.getThis()//b
  ```

- 在arrow funtion中的this代表arrow function所在的物件

- 有關this,call,apply bind 期待會記得..再寫一篇

---

## Promises

> The **Promise** object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.
>
> 待續.....新的筆記

---

## Classes

> Use the keyword `class` to create a class, and always add a constructor method.
>
> The constructor method is called each time the class object is initialized.

---

## Modules

> import & export 

---

## Spread Operator

...表示，將陣列展開成個別數值or合併

```javascript
let fruit=['apple','banana','orange'];
console.log(...fruit)
// apple banana orange
```

---

## Rest Operator

...表示，將剩餘的值轉為陣列

```javascript
const [a,...b]=[1,2,3,4,5,6]
// b=[2,3,4,5,6]
```



---



# 延伸閱讀

[Top 10 ES6 Features Every Busy JavaScript Developer Must Know](https://webapplog.com/es6/)

[你不可不知的 JavaScript 二三事#Day23：ES6 物件實字威力加強版 (Enhanced Object Literals)](https://ithelp.ithome.com.tw/articles/10208316)

[淺談 JavaScript 頭號難題 this](https://blog.techbridge.cc/2019/02/23/javascript-this/)

