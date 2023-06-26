---
layout: post
title:  "Schema Markup"
date:   2023-06-26 22:00:00 +0800
author: peng
categories: web
tags:
comments: true
---



結構化資料 (Structured data) 是指一種標準格式，可依照網頁類型做資料分類。透過這樣的結構化資料，將網站內容標記清楚，讓搜尋引擎解析網頁內容。

<!--more-->

> 網站 Schema，全名為 Schema markup。

而資料庫 Schema，指的是資料表及欄位的設計，例如：資料表欄位的數量，資料型態，大小長度，主鍵，外鍵，複合鍵，唯一性，是否可為 null，索引...等。


## 由來

`Schema.org` 是由四大搜尋引擎 Google、Microsoft、Yahoo 與 Yandex 一同創建的組織，目的是制定出網頁結構化的標準規範。目前結構化資料主要即採用 `Schema.org` 制定的這套標準。

### 搜尋引擎

同一個網站/頁面在不同的搜尋引擎可能會有不一樣的排名。可根據所在地區搜尋引擎的市占率作為 SEO 優化的考量。

延伸閱讀：[雅虎SEO攻略｜Yahoo SEO介紹、Yahoo關鍵字排名4大重點教學！](https://welly.tw/serp-rank-optimization/tips-for-yahoo-seo)

![Untitled](/assets/post/schema-0.png)

*圖取自[Top 10 Search Engines In The World](https://www.reliablesoft.net/top-10-search-engines-in-the-world/)*

---

## 結構化資料

可接受的格式為：

- JSON-LD (Google 推薦使用，也最容易導入及維護)
- Microdata
- RDFa

### JSON-LD

全名為 `JavaScript Object Notation for Linked Data` JSON 格式的結構化資料。

```html
<script type="application/ld+json">
  {
        "@context": "https://schema.org",
        "@type": "Person",
        "name": "Kelly"
    }
</script>
```

### Microdata

```html
<div itemscope itemtpye="http://schema.org/Person">
	<p>My name is <span itemprop="name">Kelly</span>.</p>
</div>
```

### RDFa

```html
<p vocab="http://schema.org" typeof="Person">
	My name is <span property="name">Kelly</span>.
</p>
```

---

## 如何產生結構化資料

可透過 Google 提供的 [Structured Data Markup Helper](https://www.google.com/webmasters/markup-helper/u/0/)

1. 勾選資料類型並填上網址或 HTML

    ![Untitled](/assets/post/schema-1.png)


1. 開始標記資料
    
    ![Untitled](/assets/post/schema-2.png)
    

1. 於左側網頁中反白文字，並選擇資料標記為何
    
    ![Untitled](/assets/post/schema-3.png)
    

1. 右側的記錄區塊會有標記的結果
    
    ![Untitled](/assets/post/schema-4.png)
    

1. 完成標記後，點擊建立 HTML
    
    ![Untitled](/assets/post/schema-5.png)
    

1. 選擇輸出的格式 (JSON-LD/Microdata)
    
    
    ![Untitled](/assets/post/schema-6.png)
    
    ![Untitled](/assets/post/schema-7.png)
    

---

## 怎麼檢查結構化資料

**可以利用 [schema.org](http://schema.org/) 所提供的 [validator 工具](https://validator.schema.org/)** 或是 Google 的 [Rich Results Test](https://search.google.com/test/rich-results) 工具。

以 [schema.org](http://schema.org) validator 操作為例。

1. 輸入要檢查的 URL 或是 HTML

![Untitled](/assets/post/schema-8.png)

1. 於右側會顯示此頁面的結構化資料設定
    
    ![Untitled](/assets/post/schema-9.png)
    

---

## Schema 類型

Google 接受 32 種類型的 Schema，可依照網頁的內容選擇適合的 Schema 類型。內容型網站大多會加入結構化資料，其餘網站/網頁可視需求或目的決定要不要加入。

例如：文件型的  **[Spectrum - Adobe’s design system](https://spectrum.adobe.com/) 可能因為沒有提高搜尋排名的必要或是需求，所以沒有埋入結構化資料。**

*以下類型取自 [Structured data markup that Google Search supports](https://developers.google.com/search/docs/appearance/structured-data/search-gallery)*

| Type |
| --- |
| Article |
| Book |
| Breadcrumb |
| Carousel |
| Course |
| Dataset |
| Education Q&A |
| EmployerAggregateRating |
| Estimated salary |
| Event |
| Fact Check |
| FAQ |
| Home Activities |
| How-to |
| Image Metadata |
| JobPosting |
| Learning Video |
| Local Business |
| Logo |
| Math solvers |
| Movie |
| Practice problems |
| Product |
| Q&A |
| Recipe |
| Review snippet |
| Sitelinks Search box |
| Software App |
| Speakable |
| Subscription and paywalled content |
| Video |

---

## 參考資料

[What Is Schema Markup & How to Implement Structured Data](https://www.semrush.com/blog/what-is-schema-beginner-s-guide-to-structured-data/)

[Structured Data and Schema Markup: The Complete Guide](https://marketbrew.ai/structured-data-and-schema-markup-the-complete-guide)