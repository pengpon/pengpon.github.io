---
layout: post
title:  "[筆記] 微互動 Microinteractions"
date:   2023-07-22 22:35:00 +0800
author: peng
categories: web
tags:
comments: true
---

![microinteraction-cover](/assets//img/micriinteractions.webp)

2014 年出版的書，偶然在公司書架看到，很多概念都很適合時時刻刻提醒自己，共勉之。

<!--more-->


## 重點

『 一般人每天會接觸到很多不同的使用經驗，唯有最清楚的互動會將一個新的使用經驗轉化成使用者喜愛的產品。』

『 整體性很重要，但細節也是，注意細節才能創造出流暢的完成感。』

『 喜愛的產品和勉強可接受的產品，差別往往就在我們跟它之間的微互動。』

『 漂亮、好用的小事物能帶來快樂，這種快樂會同時存在於使用者和創造者身上。』

**『 細節主宰了片刻的體驗，適時的細節造就使用者跟我們的產品產生無縫的互動；忽略那些細節會導致使用者沮喪、不耐煩，最後很討厭產品。』** - 最喜歡的一句


### 觸發

從策略觀點來看，了解使用者的任務、何時想做、在什麽情境下想做是很重要的。這決定了手動觸發應該在何時何地出現。

介紹有價值的資訊！

```
最多人、最常使用的微互動應該最明顯

部分人、常使用的微互動應該容易發現

少數人、偶爾使用的微互動應該要花點時間尋找
```

人類會使用兩種方式來感知環境的事物：

```bash
# 1. 事物藉由`移動` 或 `聲音` 來引起注意

可藉由移動觸發或是發出聲音，來吸引使用者注意
但是，這樣做會引起使用者的反感！！！

應該把移動或是發生聲音套用在重要性高的事物上，例如：錯誤或警告

# 2. 主動尋找某個事物 `目標導向`

在辨識物件的過程中，會分類環境裡的東西。
例如：眼睛會尋找熟悉的幾何形狀，所以一般常把圖示設計成幾何圖案，比較容易找到目標。
```

#### 隱形觸發
不管哪一種介面，使用者都不會立刻發現每樣東西，把全部設計成有形、明顯的，往往代表非常凌亂、複雜、不容易掃視的畫面。

把東西隱藏起來，會讓畫面或物件看起來簡單，而不會犧牲功能性。

隱形控制項能凸顯什麽是有形的，產生重要性的優先順序！

### 規則

如果無法輕易地寫出或畫出微互動的規則，使用者將難以勾勒出它的心智模型。

如果價值不是立即顯而易見的話，你的微互動會變得沒必要，只是噱頭。
『只為求不同而不同的東西很少會更好，但更好的設計往往是特別的。』


在設計規則前，必須以最簡單、最清楚的詞彙來決定微互動的目標，最好的目標是可理解、可達成的，記得所定義的目標不只是一個步驟，它是最終的狀態。

> 登入微互動的目標不是要使用輸入他們的密碼，目標是要讓他們登入、進入應用程式。
>
> 把焦點放在目標上而不是步驟，微互動就越可能成功
>
> 目標驅動著規則

規則決定：
- 微互動回應觸發的方式
- 使用者對進行中微互動的掌控能力
- 動作的順序和時間安排
- 使用哪些資料以及資料的出處
- 微互動處於哪個模式
- 微互動結束時會發生什麽事


制定規則，商品頁的按鈕標籤有三種可能 `再買一個` `再買一次` `加入購物車` 

### 動詞和名詞
用一個句子來思考整個微互動是有幫助的，動詞是使用者會參與的動作，名詞則是驅使那些動作的物件。

微互動的每個物件(使用者介面的每個部分、每個表單元素、每個控制項) 都是有特性和狀態的名詞，規則是在定義那些特性和狀態。

微互動設計師要注意每個狀態，因為每個狀態可以把正在發生什麽事情的資訊傳達給使用者--即使正在發生的事情微不足道。


### 理解複雜性
Tesler 的複雜守恆原則，指所有活動都有其複雜性，一個流程能被簡化的程度是有限度的，剩下的唯一問題是該如何處理複雜性。要不由系統處理，拿掉使用者的控制權，要不由使用者處理，把更多決策權或是更多控制權交給使用者。

### 有限的選項和智慧預設
『假如你可以掌控使用者的視線，就能掌控他們將會移動的方向。』


### 預防錯誤
Poka-Yoke 防錯驗證，指產品和流程應該經過設計。
因此使用者不可能送出錯誤，因為產品/流程不允許它發生。


理想情況是 微互動應該經過設計！
使用者操作正確時 才不會顯示錯誤訊息。只有在系統本身無法適當回應時 才顯示錯誤訊息！
如果錯誤真的發生 微互動應該盡全力修正！


### 微文案
幾乎所有的微互動 要先確認任何文字 是否真的有助理解。

避免使用多重否定，避免讓使用者產生困惑。
例如：如果不希望不訂閱我們的電子報，不要取消打勾。

### 回饋彰顯規則
微互動回饋的真正目的是為了幫助使用者了解規則運作的方式。

回饋不需要告訴使用者微互動真正的運作方式、真正的規則是什麽，應該提供使用者適當的回饋。

回饋應該讓使用者知道他們可做和不可做的事。

不要用回饋疲勞轟炸使用者。
要問一個問題：起碼要有多少回饋，才能傳達正在進行的事。


回饋也應該發生在使用者輸入附近或輸入時。
當注意力在某件事上時，視野會縮小，會忽略視野外的任何東西。
如果需要把視覺回饋放在焦點外，加上移動，可以把使用者的注意力轉移到他身上。


### 使用動畫的原因
- 改變內容時維持在同樣的情境裡
    - 捲動清單或是翻動圖片
- 解釋剛發生的事
    - 煙可以代表項目被刪除
- 顯示物件間的關係
    - 拖放最後，用動畫把項目一到另一個區塊裡
- 抓住注意力
    - 數值改變時
- 改善感覺到的效能
    - 進度列不會減少下載時間，但可以讓時間看起來沒那麼長
- 創造虛擬空間的幻覺
    - 面板轉場，轉場會提供位置和導航的感覺
- 鼓勵更深的參與



作為回饋文字應該要簡短清楚，避免使用像錯誤和警告之類的字眼，它們無法提供資訊，只會增加焦慮，錯誤訊息的回饋文字應該不只要指出錯誤是什麽，而且要說明如何修正錯誤。