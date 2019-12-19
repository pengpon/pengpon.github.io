---
layout: post
title:  "UML-Use case diagram使用案例圖"
date:   2019-12-19 14:13:00 +0800
author: Pon
categories: system
tags: system analysis
---



> UML (Unified Modeling Language) 統一塑模語言
>
> 遙想2年前系統分析
>
> 一下要從網頁切版,動畫特效
>
> 轉化成系統分析的思維....  
>
> 一直都知道它的重要性，　但現實面是很少專案是照理想分工進行的......
>
> 系統分析? 沒這回事  規格書?   先做再說!



# UML

中文譯做 **統一塑模語言**，是一種標準，用在分析、設計、畫軟體藍圖

是一種建立Model的語言(和程式語言php,c++或標記語言html不同)

**UML是軟體系統發展人員用來建造Model，這些Model使團隊能夠將系統-具象化、規格化，並建構系統以及記錄系統發展決策!**

- 具象化(visualization)

  把一個系統的功能或是需求圖像化，畢竟普遍每個人都是視覺動物，一圖勝萬語!

- 規格化(specification)

  精確且清晰 甚至可以作為需求規格書/設計規格書

- 建構(construction)

  概念與java架構一致，可使用UML圖生成Code or code生成UML圖

  ![auto UML](https://imgur.com/DdW1ceM.jpg)

- 記錄(documentation)

  可用在系統使用手冊中...等

![UML diagram type](https://imgur.com/FaSoGrj.jpg)

## 圖表類型

常見的class diagram、activity diagram, **use case diagram**(這篇筆記重點)

- Class Diagram(類別圖)

  ![class diagram](https://imgur.com/SYrLG9N.jpg)

- Activity Diagram(活動圖)

  ![activity diagram](https://imgur.com/8BgZiD5.jpg)

- Use Case Diagram(使用案例圖)

  ![use case diagram](https://imgur.com/DxzKfDd.jpg)

以上圖皆取自https://www.visual-paradigm.com/

<br>

# Use Case Diagram

- what is being described? (**system**)
- who is using the system? (**actors**) 
- what do the actors want to achieve? (**use cases**)

擷取使用者的需求，描述系統是誰會使用? 使用者的目的??

包含兩類基本符號:

- Use case
- Actor

![use case diagram](https://imgur.com/FUHMVJ7.jpg)

每一個使用案例都可以再加上Use case description 以及Activity diagram來描述使用者和系統的互動



## 補充Use case Model

一個完整的Use Case Model包含

- 業務流程描述(Activity diagram)
- 使用者需求和系統功能(Use case diagram)
- 使用案例事件流程(Use case description)
- 使用者故事和驗收測試(User story and Acceptance test)
- 使用案例情節(Activity diagram)
- UI設計



再回到Use case diagram

## Use Case

每一個use case代表在系統內執行的**行動**

記得只要定義行為，先不用管細節 (還沒到開發階段，細節先擺一邊)

使用動詞片語 

ex: 讀者**管理**、線上**購物** 

也不會有流程或是順序的關係出現！

![error use case](https://imgur.com/J4ErqNl.jpg)



Use case之間有三種關係

- 一般化(Generalization)也就是繼承

  ![generalization](https://imgur.com/PsQtYZK.jpg)

  

- 包含(Include)

  ![include](https://imgur.com/zSEc9rL.jpg)

  Ex: **借書** 這個動作背後還**包含**了 確認-讀者預借的書或是-罰款

- 擴充(Extend)

  ![extend](https://imgur.com/hRAZY1Q.jpg)

  Ex: Optional的概念，借不借書是搜尋書目後的**選擇**

## Actor

使用者可以扮演的**角色**，或是存在系統外的實體(另一個系統或是資料庫)

非特定的人也不是一個職務



<br>

Use case diagram為使用者的需求和系統功能建立Model

![use case diagram](https://imgur.com/lJtLrTW.jpg)



# Use Case Description

描述系統做什麼?

每一個Use case 都可以做Use case description

敘述項目

- 使用案例名稱
- 功能簡述
- 先決條件
- 後續狀況
- 特殊需求
- 擴充點
- **事件流程**

最重要的是事件流程，包含主要和例外事件流程

主要>>>描述正常狀況下，使用者會遵循的一個完整路徑 (理想狀態)

例外>>>錯誤狀況的路徑

![use case description](https://imgur.com/MwFwFzy.jpg)



# User Story & Acceptance Test

每一個Use case 也都可以做user story和acceptance test

描述一個動機

標準公式 **As a [persona], I [want to], [so that].**

每一個user story配上驗收測試，作為:

- user story的細節
- coding是否完成的標準

ex: 

User story 1

管理員可以新增一筆商品資料

驗收測試

- 測試新增商品時，必須包括商品名稱、商品種類、規格描述、照片
- 測試所有資料必須完整才可以新增商品資料



# 結論

很喜歡一個比喻

*一個project如果是一座森林，那麼use case diagram就是樹、use case是樹幹而user story就是樹葉*

實際專案也許很難照著這種書本裡的美好執行

不過有時候coding卡住時，或是被錯綜複雜的繼承弄昏頭時

覺得利用UML圖形，可以退一步可以綜觀全場的方式

確實很棒!!



# 延伸閱讀&參考圖文

[Visual Paradigm](https://online.visual-paradigm.com/tw/diagrams/)

III-系統分析課程

