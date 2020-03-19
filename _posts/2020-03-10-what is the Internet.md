---
layout: post
title:  "網路? 蛤?-基礎篇"
date:   2020-03-10 20:45:00 +0800
author: Pon
categories: web 
tags: web
---

# 什麼是網際網路?

一個平常沒有就會渾身不對勁的**東西**，要解釋它的時候，又不知道怎麼描述...



The internet is a massive network of networks, a networking infrastructure.*

-由數量龐大的network組成



It connects millions of computers together globally, forming a network in which any computer can communicate with any other computer as long as they are both connected to the internet.*

-將全球數以百萬的電腦連結在一起所形成的network，在同一network下任何一台電腦都跟其他電腦溝通、傳送訊息



Information that travels over the internet does so via a variety of languages known as protocols.*

-資訊藉由各種不同的協定在網際網路中傳輸



## 很久很久以前...

**1970年代前期，Vint和Bob Kahn為了國防部研究計畫ARPANET(Advanced Research Projects Agency Network)開始設計，希望建立一個能抵擋核彈攻擊的通訊系統，他們的概念是把訊息拆成一個一個區塊，然後利用各種可能的方向-網格狀(Mesh network)來發送。**

![types of networks](https://imgur.com/I4YfWcS.jpg)

由非常大量且獨立運作的網絡組成！一個分散式的系統！



## 訊息是傳什麼??

*要知道電腦透過網路傳什麼訊息前，先知道電腦儲存什麼樣的資料??*

電腦的主要記憶體，由電晶體(transistors)構成，電晶體在高電壓和低電壓之間切換 (0----1切換)

![電晶體](https://imgur.com/D5nv2BU.jpg)

電腦的處理器(processor/ CPU)負責讀取數值，根據電晶體的狀態和軟體指令來控制電腦的其他裝置



-影像由像素組成，彩色圖片中，每一個像素用三個二進位的序列表示，對應到三原色(紅+綠+藍)

序列的數字決定顏色的強度，影片驅動程式將這些二進位序列傳給螢幕上的數百萬個液晶體，最後在使用者面前顯示各種顏色。

<img src="https://imgur.com/xHf8uKR.jpg" style="zoom:50%;" />

聲音也是利用二進位資料儲存，利用**脈衝編碼(pulse code modulation)**，將連續的聲波數位化，每幾毫秒就擷取一次聲波的振幅，每一秒的聲音會有44,000個數字，電腦的影音軟體讀取這些資料，決定喇叭要震動多快，創造不同頻率的聲音。

<img src="https://imgur.com/KDSsoQp.jpg" style="zoom:50%;" />



用二進位制的數據來傳遞資訊 一個位元能表示兩種狀態,所以稱為二進制碼

8個位元>>>組成一個位元組(Byte)

8 bits=1 Bytes

1024 Bytes= 1 KB

1024 KB= 1MB

<img src="https://imgur.com/E3hYF1S.jpg" style="zoom:50%;" />



補充:

類比 V.S. 數位訊號

- 類比訊號:

  大自然裡一切的訊號，包括我們聽到的聲音、看到的影像，都屬於類比訊號。得到一個連續的電壓變化，這種「連續的訊號」稱為類比訊號。

- 數位訊號:

  經由加工以後可以將連續的類比訊號變成 0 與 1 兩種不連續的訊號，例如：電腦在運算的時候只有低電壓（0V 代表二進位的數字 0）與高電壓（1V 代表二進位的數字 1），訊號可以由 0（0V）直接跳到 1（1V），也可以由 1（1V）直接跳到 0（0V），得到一個不連續的電壓變化。

訊號數位化:

​		類比訊號數位化以後都只剩下 0 與 1 兩種數位訊號。在使用數位訊號的時候，「0 與 1 的排列順序」可能代表一個文字、一段聲音或一張圖片。

![訊號數位化](https://imgur.com/6IxxWIU.jpg)



## 靠怎麼傳送訊息??

**現在已經在利用電力、光、無限電波來傳遞二進制數據**

![3 ways](https://imgur.com/NyeDeYE.jpg)

#### 補充:

頻寬(Bandwidth)-可以傳遞訊號的頻率範圍/ 訊號佔據的頻帶寬度

For 類比訊號: 頻寬以Hz為單位 EX:3100Hz~3500Hz

For 數位訊號: 頻寬指傳輸裝置最大的傳輸資料量(bitrate)，單位時間內可以傳送的二進位數據量,通常以秒為單位(bit per second, bps)

另一個測量速度單位是延遲時間(latecncy),傳送一位元所花的時間

舉例:

下載一首3MB的歌花3秒鐘，或是8Mbps，每秒鐘可以傳送800萬個位元資料!



3G, 4G, 5G (G-Generation)

![演進史](https://imgur.com/kQUmow0.jpg)



1. 電力

   實體網路線 (約100公尺，訊號就會遺失或被干擾)

   ![ethnet](https://imgur.com/jUZ7OhO.jpg)

2. 光

   可以利用光來傳遞資訊, 透過光纖電纜, 使用光纖來送光束

   光訊號在光纖中不斷前進, 直到光訊號被接收端接收

   根據角度不同, 可以同時傳送多組訊號, 所有訊號都以光速(~300,000,000 m/s)前進

   光纖速度快,訊號衰減的很低，所以把光纖電纜裝在海底,連結海洋的兩地(但也很貴....) [海底電纜傳送門](https://www.storm.mg/article/1524745)

   <img src="https://imgur.com/zTG5PGd.jpg" alt="fiber" style="zoom:50%;" />

   ![海底電纜](https://imgur.com/lETGrQi.jpg)

3. wireless-無線電波來傳遞

   必須把一堆0,1訊號傳成無線電波的不同頻率

   接收端收到電波,再把無線電波轉換成電腦可以處理的二進位數據

   ![radio](https://imgur.com/YdC7Z8t.jpg)

   網路世界的所有資料,不管是文字,mail,圖片或影片, 所有資訊都被轉換成無數的1和0

   再利用電子脈衝, 光束 , 無線電波傳遞所有資訊

   **想像在公司利用wifi連線到路由器>>路由器透過實體的網路線連到數據提供商(中華電信])>> 機房透過實體網路傳遞到目的地**



​	**比較各種傳輸方式**

![method](https://imgur.com/4kG4FKD.jpg)



## 網路通訊協定??

節點之間如何溝通訊息? Ans: 透過標準的通訊協定

連接過程好好好複雜,  包含 硬體,軟體資料封包和應用程式的互相連結

網路連接過程分成數個layer，每個階層都有特別的獨立的功能 

### OSI協定

優在哪? 降低網路複雜化、介面標準化、簡化教學.....

越接近硬體為底層layer1，越接近應用程式為高層layer7

透過應用程式把資料放入第七層的包裹, 再將第七層包裹放入第六層.....依序一層一層

每一層都有自己的header

![data flow](https://imgur.com/NpAxQBg.jpg)

<img src="https://imgur.com/aZGg0RF.jpg" alt="OSI Model" style="zoom: 80%;" />

| Layer                       | 內容                                                         |
| --------------------------- | ------------------------------------------------------------ |
| 實體層(Physical Layer)      | 網路最終需要透過媒體傳遞訊號，例如: 規範的內容包含了纜線的規格、傳輸速度，以及資料傳輸的電壓值，用來確保訊號可以在多種物理媒介上傳輸 |
| 資料連結層(Data Link Layer) | 資料連結層將實體層的數位訊號封裝成一組符合邏輯傳輸資料，這組訊號稱為資料訊框（Data Frame）。訊框內包含媒體存取控制（Media Access Control，MAC）位址。而資料在傳輸時，這項位址資訊可讓對方主機辨識資料來源。 |
| 網路層(Network Layer)       | 這一層中最主要的通訊協定是網際網路協定（Internet Protocol，IP），資料在傳輸時，該協定將IP位址加入傳輸資料內，並把資料組成封包（Packet）。在網路上傳輸時，封包裡面的IP位址會告訴網路設備這筆資料的來源及目的地。 |
| 傳輸層(Transport Layer)     | 可以將一個較大的資料切割成多個適合傳輸的資料，替模型頂端的第五、六、七等三個通訊層提供流量管制及錯誤控制<br />傳輸控制協定（Transmission Control Protocol，TCP）是我們常接觸具有傳輸層功能的協定，它在傳輸資料內加入驗證碼，當對方收到後，就會依這個驗證碼，回傳對應的確認訊息（ACK），若對方未及時傳回確認訊息，資料就會重新傳遞一次，以確保資料傳輸的完整性。 |
| 會議層(Session Layer)       | 負責建立網路連線，等到資料傳輸結束時，再將連線中斷           |
| 展示層(Presentation Layer)  | 應用層收到的資料後，透過展示層可轉換表達方式，例如將ASCII編碼轉成應用層可以使用的資料，或是處理圖片及其他多媒體檔案，如JPGE圖片檔或MIDI音效檔<br />除了轉檔，有時候當資料透過網路傳輸時，需要將內容予以加密或解密，而這個工作就是在展示層中處理 |
| 應用層(Application Layer)   | 使用者常見的通訊協定，有DHCP（Dynamic Host Configuration Protocol）、FTP（File Transfer Protocol）、HTTP（HyperText Transfer Protocol）及POP3（Post Office Protocol-Version 3）等，依據不同的網路服務方式，這些協定能定義各自的功能及使用規範等細部規則。 |

簡言之:

- 實體層(物理層):定義物理設備的標準!

- 資料連結層: 將傳輸資料分裝成frame&加上MAC位址提供設備之間辨識!

- 網路層: 加上IP位址! 讓網路透過IP協定識別電腦!

- 傳輸層: 提供連接埠號(port)，指定目的端電腦的功能(包含TCP/UDP協定)

  ![常用port號](https://imgur.com/gfFkcdq.jpg)

- 會議層: 負責兩部電腦之間的連線(建立和結束連線)&傳輸模式(單工simplex、半雙工half-duplex、全雙工full-duplex)

- 展示層: 轉換資料、處理加解密、壓縮解壓縮

- 應用層: 提供服務，對應各種應用程式該有的協定(HTTP-網頁存取、FTP-檔案傳輸、DNS-網域名稱)



補: 傳輸層有兩個很重要的協定-TCP協定&UDP協定

TCP傳送機制:三方交握，連線請求,連線確認,連線成功

UDP:提供非可靠的非連線型資料流傳輸服務，不通知傳送目標要開始傳送訊息的情況下,突然開始送訊，但速度快,適合即時服務

待續........

OSI只是一個參考模型,但很少作業系統使用

OSI嚴謹,適合學習,但程式太難撰寫

而APRANET發展出的TCP/IP一樣有OSI七層協定觀念,只是簡化成四層

通訊協定是讓通訊雙方所必須依據的規範, 一部電腦可同時存在許多協定

![compare model](https://imgur.com/8mtJ5Hs.jpg)





## 其他

### DSL, Cable, Fiber

- ADSL,用一般銅質傳統電話線來進行高速上網

- 光纖(optical fiber)用光線在導線內反射傳送訊號

  可以大量 衰減較慢 訊號穩定 不受電磁波干擾 

  只要機房到家裡/公司中有一段是使用光纖就稱為光纖上網, 其他段用比ADSL快的VDSL電話線傳輸

- CABLE是使用有線電視的纜線作為傳輸的載體 價格便宜適中 



### IP位址組成

可由0.0.0.0~255.255.255.255

*同一個網段內，主機IP具有相同的網路位址*

同一個網段的好處: 網卡對網卡的傳送資料

在TCP/IP通訊協定中會使用**Netmask子網路遮罩**，來決定目的地主機是在本機子網路上/ 遠端網路上，如果運算後發現不是同網段，會將資料封包傳到Gateway!

**利用子網路遮罩和IP位址推算出網路位址**

IP: 192.168.1.3

11000000.10101000.00000001.00000011

子網路遮罩: 255.255.255.0

11111111.11111111.11111111.00000000

做AND運算(11-->1, 10/01/00-->0)

11000000.10101000.00000001.00000000

192.168.1.0

AND運算結果相同，代表兩台主機同網段

<br>

### Gateway

來連接兩個不同網段! 如果只要和內部同網段的電腦互通，Gateway可以不用設





# 延伸閱讀&參考圖文

[what is the Internet?](https://www.youtube.com/watch?v=Dxcc6ycZ73M)-youtube-video

[The Internet: Wires, Cables & Wifi](https://www.youtube.com/watch?v=ZhEf7e4kopM)-youtube-video

[TCP/IP vs. OSI: What’s the Difference Between the Two Models?](https://viettechgroup.vn/tcp-ip-vs-osi-whats-the-difference-between-the-two-models.nvp)

[DSL vs Ethernet Cable vs Fiber Optic Cable Speed](http://www.fiber-optic-tutorial.com/dsl-vs-ethernet-cable-vs-fiber-optic-cable-speed.html)

[The Difference Between the Internet and World Wide Web](https://www.webopedia.com/DidYouKnow/Internet/Web_vs_Internet.asp)

[二進位運作](https://www.ted.com/talks/jose_americano_n_l_f_de_freitas_how_exactly_does_binary_code_work/transcript?language=zh-tw#t-165461)-video

[What is OSI Model?](https://www.youtube.com/watch?v=Ilk7UXzV_Qc)

[擁有它就進入深海資訊天堂！](https://www.storm.mg/article/1524745)