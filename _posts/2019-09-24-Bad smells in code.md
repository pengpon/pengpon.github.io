---
layout: post
title:  "Bad smells in code 筆記"
date:   2019-09-24 09:24:00 +0800
author: Pon
categories: studygroup
tags: refactoring 
---



> If it stinks, change it!

臭掉時，就換掉它吧!



# Mysterious Name

* 神秘的名稱

程式不是偵探小說，必須清晰明瞭。

替函式、模組、變數、類別想個好名稱，一眼可以看出它的功用&如何使用。



# Duplicated Code

* 重複的程式碼/ 功能,作用一樣

> **Don’t Repeat Yourself!!**

同一專案同時多人開發時，或是正值菜鳥時期的工程師，最常發生。



# Long Method(Function)

* 冗長的函式，活的好又長壽的程式都用**短函式**

> 不需要看function內容，藉由function name就可以知道function的作用。
>
> 一般來說，盡量不超過10行的function。
>
> 不用擔心呼叫function會影響效能!



# Long Parameter List

* More than three or four parameter for a method!

> 太冗長的參數列，不易理解!
>
> 可以傳遞整個object資料或是藉由呼叫函式。



# Global Data

* Global data危險在於，它能被程式的任何地方修改!

> 將資料包在函式中，移到類別或是模組中，限制它的範圍。



# Mutable Data

* Can update some data here, **not realizing that another part of the software expects something different and now fails** — a failure that’s particularly hard to spot if it only happens under rare conditions.



# Divergent Change

* 發散式修改，同一個class經常因為不同的原因被用不同的方式修改。

> When we make a change, we want to be able to jump to a single clear point in the system and make the change.
>
> Many changes are made to a single class!



# Shotgun Surgery

* 散彈式修改，每次修改時都要在許多不同類別裡面進行小規模的編輯。

> Making any modifications requires that you make many small changes to many different classes.
>
> Single change is made to multiple classes simultaneously.



# Feature Envy

* 一個模組內的函式經常與另一個模組的函式或資料互動。

> When we modularize a program, we are trying to separate the code into zones to maximize the interaction inside a zone and minimize interaction between zones.



# Data Clumps

* Different parts of the code contain identical groups of variables.(相同的參數常常在不同地方出現)



# Primitive Obsession

* 基本型態偏執(只給純量)

> ex:貨幣金額, 計算物理量時,不給單位



# Repeated Switches

* Whenever you add a clause, you have to find all the switches and update them



# Loops

* Use Replace Loop with Pipeline!

![pipeline](https://imgur.com/POu4JgQ.jpg)



# Lazy Element

* Sometimes, it’s a class that used to pay its way, but has been downsized with refactoring. Either way, such program elements need to die with dignity.



# Speculative Generality

* 畫大餅，"Oh, I think we’ll need the ability to do this kind of thing someday"

  沒有未來式!!!



# Temporary Field

* Sometimes you see a class in which a field is set only in certain circumstances.

> 沒有作用的欄位，有時有值有時沒值。



# Message Chains

* You see message chains when a client asks one object for another object, which the client then asks for yet another object, which the client then asks for yet another object, and so on.

> 過於耦合，物件之間的關係有變化，使用方/呼叫方就要修改。



# Middle Man

- **If a class performs only one action, delegating work to another class, why does it exist at all?**

> This can go too far. You look at a class’s interface and find half the methods are delegating to this other class.



# Insider Trading

> Modules that whisper to each other by the coffee machine need to be separated by using *Move Function* and *Move Field* to reduce the need to chat.



# Large Class

* 龐大的類別

> A class contains many fields, methods, lines of code. 
>
> Extract class, subclass, interface



# Alternative Classes with Different Interfaces

* 異曲同工的類別

> two classes perform identical functions but have different method names.
>
> The programmer who created one of the classes probably didn’t know that a functionally equivalent class already existed.
>



# Data Class

* A data class refers to a class that contains only fields and crude methods for accessing them

> These are classes that have fields, getting and setting methods for the fields, and nothing else. Such classes are dumb data holders and are often being manipulated in far too much detail by other classes.



# Refused Bequest

* 被迫接繼承所有父類別的屬性與方法

不要繼承沒有任何共同點的繼承!

# Comments

* 過多註解

> The best comment is a good name for a method or class.



# 常見解決方法



##　1. Extract Method

> Smell: **Have a code fragment that can be grouped together!**



重構前:

```typescript
printOwing(): void {
  printBanner();

  // Print details.
  console.log("name: " + name);
  console.log("amount: " + getOutstanding());
}
// keypoint:太多行的程式碼,比較難看出function的用途
```

目的:

**Move code to a separate new method and replace the old code with a call to the method.**



重構後:

```typescript
printOwing(): void {
  printBanner();
  printDetails(getOutstanding());
}

printDetails(outstanding: number): void {
  console.log("name: " + name);
  console.log("amount: " + outstanding);
}
// 可讀性提高
// 讓method可重複使用
// 拆成獨立的兩個method,容易找bug!
```



## 2. Form Template Method

> Smell: **the duplicate code is similar, but not completely identical**

![form template method before](https://imgur.com/Cl0jnHG.jpg)

觀察出兩個子類別都有都有相似的邏輯運算



目的:處理邏輯運算的部分移到父類別中

![form template method-after](https://imgur.com/cti51tk.jpg)

> Forming a template method is an example of the **Open/Closed Principle**. (開放封閉原則)
>
> 軟體要可以被擴充但是不能被修改!
>
> should be open for extension, but closed for modification!!
>
> 當要增加新的功能或是邏輯運算時，建立一個新的子類別就可以完成，而不需要去異動到原有的code!



## 3. Replace Parameter with Method Call

> Smell: **傳入參數的值，為其他method的產生結果**

> Placing a query call inside the method!!!!

   重構前:

```typescript
let basePrice = quantity * itemPrice;
const seasonDiscount = this.getSeasonalDiscount();
const fees = this.getFees();
const finalPrice = discountedPrice(basePrice, seasonDiscount, fees);
// 太多的參數難以理解
// 參數值來自太多個method,很難去得知最後傳進method的值為多少
// value-getting code doesn't use parameters
```

重構後:

```javascript
let basePrice = quantity * itemPrice;
let finalPrice = discountedPrice(basePrice);
// 在discountedPrice method中再去取得seasonDiscount和fees的值
```



## 4. Preserve Whole Object

> Smell:**get serveral values from an object and then pass them as parameters to a method**
>
> Passing the whole object!!!



重構前:

```typescript
let low = daysTempRange.getLow();
let high = daysTempRange.getHigh();
let withinPlan = plan.withinRange(low, high);
```

重構後:

```typescript
let withinPlan = plan.withinRange(daysTempRange);
```



## 5. Introduce Parameter Object

> Smell: **contain a repeating group of parameters**
>
> Replace the parameter with an object!!

重構前:

![introduce parameter object-before](https://imgur.com/l1pp7pG.jpg)

重構後:

![introduce parameter object-after](https://imgur.com/dkNn920.jpg)



# 延伸閱讀&圖文出處

https://refactoring.guru/refactoring/smells





