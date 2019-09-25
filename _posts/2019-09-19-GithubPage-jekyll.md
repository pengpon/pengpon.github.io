---
layout: post
title:  "Github Pages & Jekyll"
date:   2019-09-19 14:14:00
author: Pon
categories: web
tags: blog jekyll 
---
創建網站前，除了需要一個網域外，還要虛擬主機(Web hosting，來存放檔案和資料夾)

最基本的流程就包含：

1. 註冊/購買網域

1. 設定DNS
2. 租用虛擬主機
3. 安裝架設軟體

[SiteGround](<https://www.siteground.com/domain_names.php>)

[GoDaddy]([https://tw.godaddy.com/domains/domain-name-search?cvosrc=affiliate.house.iapoff15&utm_campaign=affiliates_iap_uk_discount_15offnp&utm_source=internal%20Affiliate%20Program&utm_medium=internal%2BAffil&utm_content=iapoff15&isc=iapoff15](https://tw.godaddy.com/domains/domain-name-search?cvosrc=affiliate.house.iapoff15&utm_campaign=affiliates_iap_uk_discount_15offnp&utm_source=internal Affiliate Program&utm_medium=internal%2BAffil&utm_content=iapoff15&isc=iapoff15))

[namecheap](<https://www.namecheap.com/>)

記得貨比三家!!!

![擷取自what is GitHub Pages](https://imgur.com/N61c0ec.jpg)

如果只是想練習，又考量到花費&bla bla bla 以上這些事.......

很棒的是，Github有提供Github Pages的服務，可以存放靜態網頁，也提供了github.io這個domain使用。



# Github Pages

<https://pages.github.com/>

簡單來說，

1. 註冊GitHub會員
2. New repository建立專案
3. Settings>GitHub Pages中 可以選擇主題
4. 建立完成，https://帳號+github.io
5. 或是其他repo 新增**gh-pages** branch，https://帳號.github.io/其他專案名稱

[What is GitHub Pages 影片](<https://youtu.be/2MsN8gpT6jY>)

- there are no database to set up
- no servers to configure 
- Jekyll is an open source tool that transforms plain text files into websites

# Jekyll 

<https://jekyllrb.com/>

GitHub Pages也推薦使用jekyll撰寫!!

Jekyll是利用Ruby開發的static site generator，和一般直接用HTML編寫靜態網站不同是，要修改網站的layout時，只要切換到新的theme就好，平常寫文章只要新增md檔，不需要修改其他config檔。

網路上也可以找到非常多jekyll theme

<http://jekyllthemes.org/>

<https://jekyllthemes.io/>

<https://learn.cloudcannon.com/jekyll-templates/>

<https://drjekyllthemes.github.io/>



在Ruby的世界中，使用**gem** 來管理/安裝套件



而bundler也是ruby的套件，用來解決套件相依性問題

使用gem安裝 bundler後，專案folder中會建立一個**Gemfile**

裡面會註明了這個專案中RubyGems套件的版本

當執行bundle install or bundle 

bundler會照gemfile的內容去下載

(跟angular的 npm install一樣的～)



##　環境建置

1. Ruby

> ​	Ruby version 2.4.0以上 

​	*如果是較舊的Ruby版本，必須手動再安裝[Devkit](<https://github.com/oneclick/rubyinstaller/wiki/Development-Kit>)

​	安裝Ruby+Devkit [RubyInstaller Downloads](<https://rubyinstaller.org/downloads/>)

2. 開啟cmd 

   執行 gem install jekyll bundler 

3. 建立一個新的blog 專案

   執行 jekyll  new [blog name]

4. 本機local端跑

   執行 bundle exec jekyll serve

# 菜鳥談

這篇文章, 僅是想紀念這幾個禮拜的撞牆.....

斷斷續續的在挑theme

剛開始傻傻的看看demo,覺得舒服,排版喜歡

就傻傻地換了

換了之後發現, 說明文件很簡潔....不適合菜菜的我

很多檔案都是自動產生的, 直接去改html也沒用

或是上github一看, theme上次的更新日期超過一年....

最後, 冷靜下來 blog 就好好是blog的形式就好

挑了個theme

- 說明文件清楚
- 近期有持續更新, 
- 作者也有用自己的theme在寫blog

於是非常順暢的換了主題!!!



# 延伸閱讀







