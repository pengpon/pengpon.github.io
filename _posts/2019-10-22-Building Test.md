---
layout: post
title:  "Refactoring Ch.4-Building Test"
date:   2019-11-13 17:09:00 +0800
author: Pon
categories: studygroup
tags: refactoring testing
---

> 關於重構ch.4-建構測試程式
>
> *為了正確的進行重構，需要一套可靠的測試工具來發現難以避免的錯誤*
>
> 這篇筆記一併介紹測試種類，以及利用Jest&Peppeteer實作

# Building Test-建構測試程式

章節分成七個部分:

1. The value of Self-Testing Code-自檢程式的價值
2. Sample Code to Test-測試的範例
3. A First Test-初次測試
4. Add Another Test-加入其他測試
5. Modifying The Fixture-修改fixture
6. Probing the Boundaries-探測邊界
7. Much More Than This-點到為止?(淺嘗輒止)

---

## The Value of Self-Testing Code

**修復bug很快，但找出bug的原因像惡夢** / **修好一個bug還有千千萬萬個bug，而且不知道什麼時候發作**

實現頻繁的測試，讓每一次的測試只相距幾分鐘，可以知道bug來自不久前寫的code，也因為記憶猶新，容易找出bug。

開始coding時就是寫測試的好時機! 

**先寫測試程式才實作功能**的程式開發技巧稱為**測試驅動開發(Test-Driven Development)**，透過Test/Coding/Refactor (Red–Green–Refactor)的循環。

### Red-Green-Refactor

One of the most widely used techniques for code refactoring is the red/green process used in Agile test-driven development. Applying the Red-Green-Refactor method, developers break  refactoring down into three distinct steps:

1. think about what you want to develop. [RED]

2. think about how to make your tests pass. [GREEN]

3. think about how to improve your existing implentation. [REFACTOR]

   ![Red-Green Refactor](https://imgur.com/6bEezko.jpg)



## Sample Code to Test

>  利用Academind的影片的測試範例

輸入Name&Age，點擊Add User會出現{}

![example](https://imgur.com/iaf5KMu.jpg)

點擊Add User會出現 {name} ({age} years old)

![example-testing-result](https://imgur.com/vrLbFGl.jpg)

## A First Test-demo

開始寫測試之前...

### Testing setup 

> we need some tools that help us with creating these tests
>
> typically need three kinds of tools!

- Test runners
  - test runner executes your tests and summarizes the results in the terminal.
  - e.g. Mocha / Jest 
- Assertion library
  - define testing logic, conditions
  - also need to be able to define your **expect** actions and ckeck them.
  - e.g. Chai
  - [**Jest**](https://jestjs.io/) is test runner+assertion library combined.
- e2e-testing tools
  - simulation browser interaction
  - e.g. Selenium/ Puppeteer

#### Jest

- npm install  --save-dev jest

  - 利用npm套件管理工具下載Jest

  - Jest will be development dependency of our project

  - ```javascript
    //package.json
    
    "scripts":{
        "test":test
        // "test":"jest --watch"	自動re-run   
    }
    ```

- Jest會自動執行檔名結尾為 .spec.js或 .test.js的檔案

---

- 初次測試**generateText function**

  ```javascript
  // util.js 
  // 回傳name和age組合的字串
  exports.generateText = (name, age) => {
    // Returns output text
    return `${name} (${age} years old)`;
  };
  ```

  

- 試著建立util.test.js 

  ```javascript
  // import欲測試的function (ex:generateText)
  const { generateText } = require('./util')
  
  //定義test function
  //傳入兩個參數:	1.測試的描述	2.一個包含測試邏輯的匿名函式
  test('should output name and age', () => {
    const text = generateText('Max', 29)
    expect(text).toBe('Max (29 years old)')
  })
  // 執行generateText('Max', 29)
  // expect function是由assertion library提供
  // 檢查text是否為預想的結果-'Max (29 years old)'
  // ex: tobe(5)確認值是否為5 	;toBeCalled function是否有被執行	;not.toBe(5)確認值不等於5
  ```

**coding時至少都要看到每一個測試失敗一次，確保該失敗的時候失敗**

---

### Add Another Test & Modifying The Fixture & Probing the Boundaries

```javascript
// util.js
exports.generateText = (name, age) => {
  // Returns output text
  return `${name} (${name} years old)`;
};
```

```javascript
// util.test.js
test('should output name and age', () => {
    const text = generateText('Max', 29);
    expect(text).toBe('Max (29 years old)');
});
```

執行npm test

<img src="https://imgur.com/K0jfbGp.jpg" alt="RED-exapmple" style="zoom: 67%;" />

顯示結果-在"should output name and age"測試中，Received和Expected不同

**測試當資料為空/0/負值等情形時**

```javascript
test('should output data-less text', () => {
    const text = generateText('', null);
    expect(text).toBe(' ( years old)')
})
```

---

#### Puppeteer

- e2e-tests需要安裝額外工具去控制browser

- npm install --save-dev puppeteer

  ```javascript
  const puppeteer = require('puppeteer')
  
  // 利用puppeteer.lanch啟用browser
  // browser物件:	newPage()開啟新頁面 ;goto()導向URL	;click()頁面點擊互動
  test('should create an element with text and correct class', async () => {
    const browser = await puppeteer.launch({
      headless: true,
    })
    // await 確保一個promise物件都resolve/reject才會繼續執行
    const page = await browser.newPage();
    await page.goto('localhost:4000/your-page');
    await page.click('input#name');
    await page.type('input#name', 'Anna');
    await page.click('input#age');
    await page.type('input#age', '28');
    await page.click('#btnAddUser');
    const finalText = await page.$eval('.user-item', el => el.textContent);
    expect(finalText).toBe('Anna (28 years old)');
  }, 10000)
  ```

 # 所以關於*測試*這件事

> 內容取自[JavaScript Testing Introduction Tutorial - Unit Tests, Integration Tests & e2e Tests](https://www.youtube.com/watch?v=r9HdJ8P6GQI)

## What is Testing?

> writing an app and we are creating an application and we simply test it right
>
> we had a feature , we open the browser and we test our application

![what is Testing](https://imgur.com/fwztQEu.jpg)

[圖片來源: Academind]

> we automate the **testing** part , so we automate it so that we don't have to manually test everything in our application

## Why test?

- get an error if you break code
- save time
- think about possible issues & bugs
- integrate into build workflow
- break up complex dependencies
- improve your code

## Different kinds of tests

| **Fully Isolated <br />(ex:testing one function)**           |      **Unit Tests**       | **write thousands of these!**     |
| ------------------------------------------------------------ | :-----------------------: | --------------------------------- |
| **With Dependencies<br /> (e.g. testing a function that calls a function)** |   **Integration Test**    | **write a good couple of these!** |
| **Full Flow <br />(e.g. validating a the DOM after a click)** | **End-to-End(E2E) Tests** | **write a few of these!**         |

- 單元測試(Unit Testing)

  分為TDD(測試驅動開發)及BDD(行為驅動開發)

  測試框架: mocha, jasmine,ava,tap

- 整合測試(Integration Testing)
- 端對端測試(End-to-end Testing)



## Other types about Testing 

<img src="https://imgur.com/J8riL7r.jpg" alt="different types of testing" style="zoom: 50%;" />

​								圖片來源:https://www.softwaretestinghelp.com/



# 延伸閱讀&圖文出處

[Code Refactoring Best Practices: When (and When Not) to Do It](https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/)

[一次搞懂單元測試、整合測試、端對端測試之間的差異](https://blog.miniasp.com/post/2019/02/18/Unit-testing-Integration-testing-e2e-testing)

[Javascript Unit Test: Mocha, Chai, Sinon]([https://medium.com/@evanfang.hi/javascript-%E5%96%AE%E5%85%83%E6%B8%AC%E8%A9%A6%E5%85%A5%E9%96%80-mocha-chai-sinon-50160d332ed4](https://medium.com/@evanfang.hi/javascript-單元測試入門-mocha-chai-sinon-50160d332ed4))

[使用 JEST 進行前端單元測試](https://blog.patw.me/archives/1310/write-frontend-unit-tests-with-jest/)

[The different types of software testing](https://www.atlassian.com/continuous-delivery/software-testing/types-of-software-testing)

[Types Of Software Testing: Different Testing Types With Details](https://www.softwaretestinghelp.com/types-of-software-testing/)

[Academind-Javascript testing introduction](https://academind.com/learn/javascript/javascript-testing-introduction/)

