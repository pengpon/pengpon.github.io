---
layout: post
title:  "Line Bot 筆記"
date:   2019-07-18 23:59:59
author: Pon
categories: studygroup
tags: LineBot
---



# 前言

> 紀錄7/18 雞湯老師 分享的Line Bot

# 原理

在實做Line Bot前有幾個很重要角色需要先認識

1. Line Bot

   > 進入到[LINE Developers](<https://developers.line.biz/en/>)註冊一個LINE Channel
   >
   > 也就是可以讓使用者加入好友的一個帳號
   >
   > 主要是用來取得*channel secret* *access token*
   >
   > 以及最重要的 要在channel中設定webhook!!

2. Line Platform

   > Line bot會將訊息(或是其他格式的資訊)傳給Line Platform

3. Webhook

   > LINE Platform 將訊息傳給我們所設定的webhook 
   >
   > 實作中是由heroku提供一個webhook URL

4. Bot application

   > 接收訊息，把要顯示給使用者內容透過webhook丟給Line Platform
   >
   > 最後由Line Bot回傳內容

> 一圖勝過千言萬語
>
> 圖片修改自[google 到日本勤勞工程師 blog](<https://qiita.com/Hirosaji/items/4c136c13660bb1217662>)



![Line bot 簡介](https://imgur.com/fWO2xUu.jpg)

實作可參考雞湯老師的[精美說明](<https://yuting3656.github.io/yutingblog/ndoe/line-bot>)



以上!!!!!
