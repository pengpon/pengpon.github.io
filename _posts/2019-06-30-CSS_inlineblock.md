---
layout: post
title:  "CSS排版技巧之一 inline V.S. block"
date:   2019-06-30 17:40:00 +0800
---

> 一日不讀書 便覺得面目...
>
> 一步一步把兩年前東西 複習起來

​	 

**CSS 關於display屬性**

> 有幾種常用屬性值
>
> - inline
> - block
> - inline-block
> - none



1. inline

> 元素會以同一行的方式呈現
>
> 想像成**區段**或是**長度**
>
> 無法撐開高度!!!
>
> 大小是被內容所撐開
>
> ex: a, span....

2. block

> 元素會以區塊方式呈現
>
> 想像成**區塊**，會從新的一行開始
>
> 預設會跟父元素同寬度
>
> 有面積的概念，可以設定height、width、margin及padding等
>
>  ex: p,h1~h6,div....

3. inline-block

> 綜合inline和block的特性
>
> 可橫向排列+可設定寬高

4. none

> 不顯示元素，也不佔空間
>
> visibility:hidden亦也不顯示，但會保留空間



inline或是inline-block 兩個元素之間會有預設的保留空間
可[參考](https://css-tricks.com/fighting-the-space-between-inline-block-elements/)消除方法



```html
<div>
  <div class="pink">我是block1元素</div>
  <div class="yellow">我是block2元素</div>
</div>

<div >
  <span class="pink">我是inline1元素</span>
  <span class="yellow">我inline2元素</span>
  <span class="green">我是inline3元素</span>
</div>
<div>
  <div class="none">我是none</div>
</div>
<div >
  <div class="inline-block">我是inline-block1</div>
  <div class="inline-block">我是inline-block2</div>
  <div class="inline-block">我是inline-block3</div>
</div>
```

```css
.pink {
  background:#E87688;
  height:100px; 		//block可控制寬高  inline元素即使設定也沒有作用
}
.yellow {
  background:  #FFD178;
}
.green{
  background:#93FF90;
}
.none{
  // display:none;		//不佔空間
  visibility:hidden;	//佔空間
}
.inline-block{
  display:inline-block;	//綜合inline和block特性 可橫向排列+控制寬高
  background:grey;
  // float:left;		//排版技巧之二 float
  // font-size:20px;
}
```

<iframe width="900" height="600" src="https://codepen.io/anon/pen/ewVGbQ" frameborder="0" allowfullscreen></iframe>







