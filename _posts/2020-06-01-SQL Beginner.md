---
layout: post
title:  "[SQL系列] 初識資料庫"
date:   2020-06-01 22:00:00 +0800
author: Pon
categories: database
tags: web
---



> 剛好最近有個契機發生，剛好來複習? 或說重學SQL...
>
> 筆記查到網路上的各種文章&III老師精華~

<br>

# 資料庫

有目的有為什麼就會有學習的動力(?)

資料庫(Database)是資料的集合，但又不是把所有資料開在同一張表格(Table)般的簡單。

為了將來能有效的查詢，勢必要將資料整理一番，好好的分門別類!

於是資料庫設計(Database Design)又是另一門學問，真的下手建資料庫前，(通常?or視專案規模大小複雜度)會先畫E-R Model/**ER Diagram** (Entity Relationship Diagram)。E-R Model是關聯式資料庫設計的重要工具。

資料庫代表的資料是真實世界中的實體，必須去描述這些實體的屬性或是之間關係，才能有好棒棒的資料庫設計出來。



<br>

## 1. Entity 

一個能擁有資料的實體，例如一個人、一個物件、一個事件。把它想成一個*名詞*~

常見的可能是電商網站中的**顧客**、**產品**

在圖中會用**矩形**代表它!

<br>

## 2. Relationship 

每個實體之間的關係

把它想成一個*動詞*~

例如:學生要選修某堂課程

兩個實體，分別是**學生**和**課程**就產生了

而**註冊**就是連結兩個實體的Relationship!

在圖中會用**菱形**代表它!

<br>

## 3. Attribute

實體具有的屬性或是特性，在圖中會用橢圓或是圓形代表它!

<br>

## 4. Key attribute

指**屬性值**有唯一性，不重複

例如:學生的學號、訂單編號

所以學號或是訂單編號就稱為**key**

- PK(Primary key)

  唯一且不為空值，在圖中將屬性加底線表示

- FK(Foreign key)

  建立不同實體/資料表的關係

  

<br>

## ER Model的符號

必須描述有多少個實體參與，稱作基數(**Cardinality**)

例如: 一對一、一對多及多對多

![chen notation style](https://imgur.com/ogf9ruP.jpg)

其中一種表示方式，圖取自:[What is an Entity Relationship Diagram (ERD)?](https://www.lucidchart.com/pages/er-diagrams)



<br>

於是簡單的ER Model可能會長得像這樣

![sample](https://imgur.com/UqAUhR7.jpg)

圖取自:[Entity Relationship Diagram – ER Diagram in DBMS](https://beginnersbook.com/2015/04/e-r-model-in-dbms/)

<br>

如果選擇的是關聯式資料庫管理的話

實體--表格

屬性--欄位

關係--FK (Foreign key)

<br>

簡述E-R Model建立的基本步驟:

1. 從需求中找出實體
2. 找出實體間的關係
3. 定義關係的種類(一對一/一對多/多對多)
4. 定義實體的屬性和PK

產出E-R Model後可以再進一步畫成ER Diagram

簡略的會長得像這樣

![ERD](https://imgur.com/m4foM1I.jpg)

圖取自:[What is Entity Relationship Diagram (ERD)?](https://www.visual-paradigm.com/guide/data-modeling/what-is-entity-relationship-diagram/)

有三個表格Shipment, Courier, Order

每個表格中的欄位名以及資料型態

每個表格都有個ID欄位為PK

Order中的ShipmentID和CourierID為FK

可以利用這個FK去串起和Shipment或Courier的**關係**

所以才叫**關聯式資料庫**(RDBMS)

<br>

要畫ER-Model or ERD線上有很多工具可以使用

例如:

[visual-paradigm](https://online.visual-paradigm.com/tw/diagrams/solutions/free-erd-tool-online/)、draw.io、Gliffy



<br>

# 資料庫管理系統

Data Base Management System，簡稱DBMS

用來**管理**資料庫的軟體系統，是使用者和資料庫的中介。

於是我們可以透過DBMS下指令，做新增、修改、刪除、搜尋等等的動作。

廣義的話分成兩種:

- 關聯式資料庫 RDBMS

  用二維矩陣的方式來儲存資料，有欄有列

  支援SQL，可以使用較複雜的查詢

  資料量巨大的話，效能差

  Ex: mySQL, Oracle, MS SQL Server...

- 非關聯式資料庫 NOSQL

  key-value方式儲存資料

  不支援SQL，存取速度快

  EX:MongoDB



推這篇[比較文](https://www.kshuang.xyz/doku.php/database:sql_vs_nosql)，還有語法的使用比較

自己的感覺RDBMS比較嚴謹，因為建資料庫前可能需要先把ERD畫出來，才知道要建幾張表，建那些欄位

查詢語法也很多元，又或是說可以下很複雜的條件(?)

SQL長的很嚇人之類的..但也因為這樣而影響效能

<br>

而物件方式儲存的NOSQL，因為物件要增加刪減都很彈性，用Document的概念去儲存資料。

像是A用戶資料可能就是用一個Object去儲存，而不是分散在各個表格中

有點用空間換取查詢時間的味道~

<br>





## 資料庫溝通

繼續推推[ALPHA camp的文章](https://tw.alphacamp.co/blog/sql-nosql-database-dbms-introduction)

實務上在應用的時候，即使選擇的是RDBMS也是有方法不用寫到SQL也可以對資料做操作。

也就是ORM(Object Relation Mapping)技術，用程式語言中的**物件**來包裝SQL，透過ORM它會幫我們轉成SQL~

ex:

```
// 使用ORM  查詢語法如下:
Todo.find ({ name: '買蘋果'})
```

<br>

其實會被轉換成

```
SELECT * FROM Todos WHERE name='買蘋果' ;
```

例子取自[ALPHA camp](https://tw.alphacamp.co/blog/sql-nosql-database-dbms-introduction)

不過SQL語法還是有基本認識比較好~



<br>

# SQL學習資源

推推這篇文章[What is SQL? A Beginner’s Guide to the SQL Language](https://learntocodewith.me/posts/sql-guide/)

整理蠻多SQL線上資源還有一些基本的認識



剛開始一定需要例子跟著下指令才會加深印象

不用急著在電腦建環境，使用線上的就好~

- codecademy平台

  提供很多語言的學習，切分很多個單元

  當然也有[sql](https://www.codecademy.com/learn/learn-sql)

  覺得很適合入門，畢竟不用建環境或是建檔案

  認識語法使用先，都會有一段小介紹然後跟著實作

  小闖關的感覺
  
  



待續---

<br>

# 延伸閱讀&參考圖文

[What is an Entity Relationship Diagram (ERD)?](https://www.lucidchart.com/pages/er-diagrams)

[Entity Relationship Diagram – ER Diagram in DBMS](https://beginnersbook.com/2015/04/e-r-model-in-dbms/)

[零基礎快速自學SQL](https://www.finereport.com/tw/data-analysis/sql-3.html)

[SQL語法(中文)](http://tw.gitbook.net/sql/sql-syntax.html)