---

layout: post
title:  "重構的原理 Chapter2 筆記"
date:   2019-08-26 18:22:00 +0800
excerpt: "筆記一下重點中的重點"
---



> 怠惰已久的筆記 
>
> Turn on!!
>
> 讀書會熱身，筆記一下重點中的重點
>
> 綜合網路上巨人們的讀書心得
>
> 依序由What-Why-When-How的層面來說說
>
> ![3w1h](https://imgur.com/xViUgDk.jpg)

## What is "重構" (Refactoring)

> Refactoring is a disciplined technique for restructuring an existing body of code, altering its internal structure without changing its external behavior.
>
> 不負責翻譯: 透過重組既有的程式，影響程式內部結構，但不改變既有的功能。

條列重構 能幫助我們什麼??:

1. 提高可理解性

2. 降低修改成本

簡言之:

**在既有設計中想盡辦法改善它!!!!!!** 

**在過程中，每一個重構本身都非常非常小型，所以在重構的時候，並不會造成程式碼處於無法運作的狀態！**



### 兩頂帽子(Two Hats of programming )

> Refactoring V.S. Adding Function
>
> You can only wear one hat at a time!!!

當使用重構的方式開發時，會常在程式重構及加新功能這兩個mode中互相切換。

Ex:開發時發現若改變結構，可以更容易加入新功能，所以就會先做重構調整架構；又或者是加入新功能後，雖然可以正常Work，但發現寫的讓別人滿頭問號看不懂，這時候就再進行重構！

所以用帽子來比喻這兩件事，不要貪心，一次一個就好!!!!



所以　什麼是重構??

**對軟體內部結構進行變動，目的是在不改變它的可見行為前提之下，提高它的可理解性，並降低修改它的成本。**





## Why ??

1. 改善軟體的設計

  > "當人們出於短期目的而修改程式時，經常不仔細瞭解整體架構，導致程式結構開始劣化，讓人更難以藉由閱讀程式碼來瞭解設計"
  >
  > "程式碼結構的劣化是累積性的，當越難看出程式碼的設計，越難維持它的結構，它的劣化速度就越快"
  >
  > "不良的設計經常用更多程式碼做同一件事，通常是因為會有許多地方的程式碼做相同的事"



> 不進行重構，不會怎麼樣，但你的軟體會一步一步崩壞！
>
> 補充小小心得:
>
> 過去幾乎一個人開發比較多，而自己寫的程式總是很難看出什麼要修改的
>
> 沒跑版、功能正常，只要趕得上死線
>
> 就算是同樣一段code重複複製貼上 也願意!!!
>
> 心中os:
>
> 天啊 寫得真爛  千萬不要交出我的code 
>
> 幸好客戶只要能用 就好!
>
> 等上線後 再來好好還債.....
>
> 如果這債是放給高利貸 應該已經斷手斷腳了...

當因為配合客戶心血來潮的功能增修，而修改程式時，會因為不瞭解整體架構，造成程式經年累月的劣化!!

小結: 不想要遺害同事的話  定期重構程式碼吧!!!!



不知道怎麼下手的話，就開始消除重複的、多餘的程式碼吧！！



2. 讓軟體更容易瞭解

> "程式設計就是準確地指出期望的事項，但source code可能會有其他使用者，嘗試閱讀code，並做一些修改，這個使用者才是最重要的人"
>
> 謎之音:為什麼要幫未來開發者著想?

3. 幫忙找出bug

> "重構程式碼可以深入瞭解程式碼的行為"
>
> "清楚程式結構可以幫助釐清之前的假設"

4. 提升coding速度

> "具備優良設計的軟體可在加入新功能時輕鬆地找出如何進行修改"
>
> "將精力投注在內部設計良好的程式時，開發軟體的耐力就會增加，可以走的更快速、更長遠。"

![設計耐力假說](https://imgur.com/VXeBMj4.jpg)

所以  為什麼要重構??

- **可以改善軟體的設計**

- **可以讓軟體更容易瞭解**

- **可以幫忙找出bug**

- **可以提升coding速度**

  小結:開發時，忍住雀躍的心情!！良好的設計才能走得長久~

  ![設計模式](https://imgur.com/A04jWLd.jpg)



## When ??

- 預備性重構(Preparatory Refactoring)

  > Refactor first before adding any new features.
  >
  > 在加入新功能前 是重構的最佳時機!
  >
  > 透過既有的程式碼 假想如果它的結構不同 會不會有助於未來的增修
  >
  > 有個function 經常性地被使用，僅有幾個常數值需要修改，思考是否不要複製貼上這個function，而是重構function，讓呼叫function時，傳入需要的參數!

- 理解性重構

  > 瞭解程式碼的作用及行為
  >
  > 像是瞭解變數的作用 而修改名稱，或是修改不良的條件邏輯
  >
  > 將自己的理解寫入code中，並執行看看，測試是否正常運作!

- 打掃性重構

  > 發現像是邏輯無謂的複雜
  >
  > 有好幾個相同的函式，可用參數化的函式取代

以上 比較屬於機動性的重構，在新增功能或是Debug時，順便重構~

> For each desired change, make the change easy, then make the easy change. -Kent Beck,2012
>
> 每一次修改前，先讓"修改"(這件事)變容易，再來輕輕鬆鬆的(動手)"修改"
>
> 要成為優秀開發人員，得知道
>
> 　**要加入新功能最快速做法是修改code，讓它更容易的加入功能**
>
> 

- 長期重構

  > "較大規模的重構需要花費一個團隊好幾周的時間"
  >
  > 更換library 或是要將某段code打包讓其他team使用時
  >
  > "修改複雜的依賴關係"
  >
  > 

- Review時重構

  > code review可以幫助開發團隊傳遞知識
  >
  > 幫助資深前輩傳授知識給經驗較少的後輩
  >
  > 在過程中會收到各方建議，並實作它!!

  

## 重構的難題

- 減緩新功能的完成速度

  > "進行重構是為了獲得它帶來的經濟效益，開發者、主管與客戶越瞭解重構，會看到更多優秀設計曲線"

- code ownership

  > "很多重構的修改動作不但會影響模組內部，也會影響它與系統其他部分的關係"
  >
  > ​	Ex:更改一個function的名稱，但呼叫方是由別的團隊管理，又或者是API名稱，可以採Rename function 當作中間人!
  >
  > 

- 分支

  > 透過持續性整合(Continuous Integration, CI) 防止任何分支差異太大
  >
  > 每天都至少需和master整合一次

- 測試

  > 重構的主要重點就是不會改變程式的可見行為
  >
  > 也就是它原有的功能
  >
  > 寫測試好處多多，不僅支援重構，在加入新功能時安全感大增!!
  >
  > 測試失敗時，利用版本控制比對修改的部分，快速找bug!!

- 老舊的code



## YAGNI(you aren't going to need it)

> wiki: a programmer should not add functionality until deemed necessary
>
> "不應該為程式碼加入尚未用到的功能"
>
> "根據經驗-在使用軟體之後才真正瞭解希望軟體提供什麼功能"
>
> "不猜測將來需要怎樣的彈性，只需要針對已知需求建構軟體，**精心設計**滿足需求"
>
> ![YAGNI](https://imgur.com/I2v7U98.jpg)

## 最後~範例

> 參考線上範例 有感一下!!

```javascript
// 修改前
//巢狀寫法
if(NULL != pBuf)
{
	if(false != func1())
	{
		if(false != func2())
			{
				func3();
			}
	}
}
```

```javascript
// 修改後
//巢狀不易閱讀 觀察異常條件
// pBuf!=null 且 func1()!=false 且 func2()!=false
// 三個條件都符合時 執行 func3()
//反之 只要有一個不符合 return false

if(NULL == pBuf)
return false;

if(false == func1())
return false;

if(false == func2())
return false;

func3();
```



```javascript
// 修改前

if(nHour <0 || nHour > 60)
return false;

if(nMinute  < 0 || nMinute  >  60)
return false;

if(nSec <0 || nSec > 60)
return false;

```

```javascript
// 修改後

// 合併成獨立function
if(false == isTimeValid(nHour, nMinute, nSec))
{
	return false;
}

isTimeValid(nHour,nMinute,nSec)
{
	if(nHour < 0 || nHour > 60 || nMinute  < 0 || nMinute  > 60 || nSec <0 || nSec > 60)
	{
		return false;
	}
	return true;
}
```



### 同場加映

[重構作者Martin Fowler經營的網站](<https://martinfowler.com/>)

[Clean Code 摘錄名言](<https://www.itread01.com/content/1550092703.html>)



以上 !!!



