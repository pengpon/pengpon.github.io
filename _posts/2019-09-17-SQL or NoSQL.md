---
layout: post
title:  "SQL or NoSQL"
date:   2019-09-17 16:50:00
author: Pon
categories: database
tags: database sql 
---
到底怎麼選擇SQL或是NOSQL?

原本沒有想太多只是想試玩firebase，結果發散到SQL和NoSQL。懵懵懂懂只知道兩者架構不一樣，(應該是?)一個有table、有column去儲存資料；一個則是JSON Key-value方式存取資料．透過這次筆記，能稍微知道一些細節或者什麼資料適合SQL or NoSQL?? 



# SQL

**IS not a datebase**

SQL is Structured Query Language

> wiki: 結構化的查詢語言

SQL is a language that allow you to write database queries.

像是**SELECT id,name,price FROM products**

 SELLECT, FROM 為SQL Syntax/Keywords

id,name,price, products 為Data/Parameters

**There are a bunch of commands which you can combine.**



## Database Structure

- relational database
  - works with tables
  - table is like a data bin, a storage container

## Relations

- types of relations
  - one to one
  - one to many 
  - many to many



# NoSQL

Ex: Mongo DB

Database中有Collections

Collections包含documents

## Database Structure

- no schema! 
- different documents in one at the same collection
- super flexible
- 每個document有一個唯一的id值!!
- {key1: value1}

## Relations

- No/ Few Relations!
- Put all the information in one place (造成資料重複性高)
- Have less relation merging going on have super fast and efficient queries. 



# SQL VS NoSQL

沒有一定哪個適合!!

取決於**kind of application you're building**&**kind of data you're storing**!!

**在大型的專案中通常會兩個都用**!!!



比較之前先來說說

- Vertical Scaling
- Horizontal Scaling

### Vertical Scaling

- add more power to existing server
- Has limit!
- 擴充電腦的CPU,記憶體，以增加效能

### Horizontal Scaling

- add more service, add more server
- 增加機器的數量

1. SQL 

   - use Schemas

     > field/欄位都必須定義好，資料無彈性
     >
     > 遇到資料龐大且要變更欄位時，非常耗時

   - relations

   - data is distributed across multiple tables

   - horizontal scaling is difficult/impossible; vertical scaling is possible

   - limitations for lots of read & write queries per second 

2. NoSQL

   - schema-less
   - no relations
   - data is typically merged/ nested in a few collections
   - update some data in multiple collections
   - both horizontal and vertical scaling is possible
   - great performance for mass read  & write requests

拿Relational Database Management System和MongoDB來加速理解的話:

|            | MongoDB    | RDBMS  |
| ---------- | ---------- | ------ |
| 一個資料庫 | DB         | DB     |
| 一個集合   | Collection | Table  |
| 一筆紀錄   | Document   | Record |

# 小結

沒有明確的二分法去說明要用SQL或是NoSQL Database，不過可以根據他們的優缺點，想想以下幾點

1. clear schema ?
2. use a lot of relation ?
3. change frequently ?



還有SQL的**ACID**特性, NoSQL的**CAP**特性 ....

待續....



# 延伸閱讀

[SQL VS NoSQL影片](<https://www.youtube.com/watch?v=ZS_kXvOeQ5Y>)

<https://kknews.cc/zh-tw/tech/g8jk8rl.html>





