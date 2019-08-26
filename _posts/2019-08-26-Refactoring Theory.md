---

layout: post
title:  "重構的原理 Chapter2 筆記"
date:   2019-08-26 18:22:00 +0800
---



# 前言

> 怠惰已久的筆記 
>
> Turn on!!
>
> 為了周四的讀書會熱身，筆記一下重點中的重點
>
> 綜合網路上巨人們的讀書心得



## What is "重構" (Refactoring)

> Refactoring is a disciplined technique for restructuring an existing body of code, altering its internal structure without changing its external behavior.
>
> 不負責翻譯: 透過重組既有的程式，影響程式內部結構，但不改變既有的功能。

條列重構的優點:

1. 提高可理解性

2. 降低修改成本

簡言之:

**在既有設計中想盡辦法改善它!!!!!!** 

在過程中，每一個重構本身都非常非常小型，所以在重構的時候，並不會造成程式碼處於無法運作的狀態！



## 兩頂帽子(Two Hats of programming )

> Refactoring V.S. Adding Function
>
> You can only wear one hat at a time!!!

當使用重構的方式開發時，會常在程式重構及加新功能這兩個mode中互相切換。

Ex:開發時發現若改變結構，可以更容易加入新功能，所以就會先做重構調整架構；又或者是加入新功能後，雖然可以正常Work，但發現寫的讓別人滿頭問號看不懂，這時候就再進行重構！

所以用帽子來比喻這兩件事，不要貪心，一次一個就好!!!!

## Why 重構??

> 不進行重構，不會怎麼樣，但你的軟體會一步一步崩壞！
>
> 過去幾乎一個人開發比較多，而自己寫的程式總是很難看出什麼要修改的
>
> 沒跑版、功能正常，只要趕得上死線
>
> 就算是同樣一段code重複複製貼上 也願意!!!
>
> 心中os:
>
> 天啊 寫得真爛  我千萬不要交出我的code 
>
> 幸好客戶只要能用 就好!
>
> 等上線後 我再來好好還債.....
>
> 如果這債是放給高利貸 應該已經斷手斷腳了...

當因為配合客戶心血來潮的功能增修，而修改程式時，會因為不瞭解整體架構，造成程式經年累月的劣化!!

小結: 不想要遺害同事的話  定期重構程式碼吧!!!!

不知道怎麼下手的話，有一點改善的方式可以試試看:

- 消除重複的程式碼



## When to do that??

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
> 每一次修改前，先讓"修改"變容易，再來輕輕鬆鬆的"修改"
>
> 要成為優秀開發人員，得知道
>
> 　**要加入新功能最快速做法是修改code，讓它更容易的加入功能**
>
> 

- 長期重構

  > 更換library 或是要將某段code打包讓其他team使用時

- Review時重構

  > code review可以幫助開發團隊傳遞知識
  >
  > 幫助資深前輩傳授知識給經驗較少的後輩
  >
  > 在過程中會收到各方建議，並實作它!!

  

## 重構的難題

- 減緩新功能的完成速度

- code ownership

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



## 範例

> 參考線上範例 有感一下!!

```javascript
// 修改前
//巢狀寫法
if(NULL != pBuf)
{
	if(false != func1())
	{
		if(false != Func2())
			{
				Func3();
			}
	}
}
```

```javascript
// 修改後
//巢狀不易閱讀 觀察異常條件
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



以上 !!!









