---
layout: post
title:  "[Docker]Udemy class:Docker Mastery Section 7 &讀書會紀錄"
date:   2020-08-20 22:49:00 +0800
author: Pon
categories: docker 
tags: Devops
---

> 筆記線上課程Docker Mastery Section 7內容及8/20+8/27讀書會內容

<br>

# Swarm Intro

> 官方推的容器叢集管理工具

*swarm:名詞-a large group of insects all moving together，不是天鵝(swarn)也不是蚯蚓(earthworm)*

<br>

## 要解決

- 到處散亂的container 
- 讓container的生命週期自動化
- 輕鬆的擴充/刪減container 
- Tracking container status
- 確保container是run在信任的server上



<br>

## 工具

*兩大熱門container管理工具*

- Kubernetes (k8s)

  *知識:原來是k+中間有8個字母+s的縮寫，同i18n*

  - 由Google開發的開源專案

- Swarm
  - 由Docker開發
  - 簡單易用好上手

<br>

# Docker Swarm

- 管理&調度container的平台
- Docker 1.12版後，內建**Docker Swarm Mode**
- 透過CLI/API來建立或管理swarm cluster
- 隨時調整container的運作數量

<br>

![swarm manager ca ](https://imgur.com/Q8djbXu.jpg)

*Docker swarm 預設Node主機之間會採用TLS進行認證和加密*

<br>

---

```shell
docker swarm ca
```

查看憑證內容

![CA Content](https://imgur.com/ZBpQC9T.jpg)

---

## 2種角色Node

- Manager Node
  - 負責資源調度
  - mantain cluster
  - management tasks
- Worker Node
  - 負責運作容器
  - 不參與資源調度
  - receive and execute tasks from manager node

![2 type node](https://imgur.com/RR2jbS4.jpg)

*Raft 共識演算法:推出manager leader*

推推:[動畫了解Raft共識演算法](http://thesecretlivesofdata.com/raft/)

---

## Create Serivce

由swarm manager建立Service，Service定義manager或worker node上要執行的task(任務)。

![Service ](https://imgur.com/RMuabuH.jpg)

---

在swarm manager執行`docker service create`，依序分配IP位址給tasks，task會再指派給node；worker node執行task!

![](https://imgur.com/5IRQFxA.jpg)

## Swarm初始化

查看information 預設swarm mode是沒有被啟動的

```shell
docker info
```

![init status](https://imgur.com/U4evMEm.jpg)

*要初始化後才有swarm相關指令可以用*

EX:

- docker swarm <command>
- docker node <command>
- docker service <command>
- docker stack <command>
- docker secret <command>

---

## 練習Time

1. `docker info`:確認swarm狀態
2. `docker swarm init`:啟動swarm
3. `docker node ls`:確認node目前狀態

![docker swarm init](https://imgur.com/PtrZCI3.jpg)

*init時 記得給ip*

---

`docker service create alpine ping 8.8.8.8 `

```shell
$ docker service create alpine ping 8.8.8.8
fwnuamylf06ee6gb4b4eswhy4
overall progress: 1 out of 1 tasks 
1/1: running   [==================================================>] 
verify: Service converged 
```

*建立一個新的service，run alpine這個image執行container*

---

`docker service ls`

```shell
$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
27dd224e9781        alpine:latest       "ping 8.8.8.8"      14 seconds ago      Up 13 seconds                           quizzical_cartwright.1.n412481vqc2ejbb1s36bs6pws
```

---

`docker service ps <service name>`:查看task

```shell
$ docker service ps fwn
ID                  NAME                     IMAGE               NODE                DESIRED STATE       CURRENT STATE           ERROR               PORTS
n412481vqc2e        quizzical_cartwright.1   alpine:latest       node1               Running             Running 5 minutes ago 
```

---

`docker service update <service id> --replicas 3`:更新service,共要建立三個複本

```shell
$ docker service update fwn --replicas 3
fwn
overall progress: 3 out of 3 tasks 
1/3: running   [==================================================>] 
2/3: running   [==================================================>] 
3/3: running   [==================================================>] 
verify: Service converged 
```

---

`docker container ls`

![container 執行狀況](https://imgur.com/YTdwfoQ.jpg)

*一鍵複製多個複本!*

---

`docker container rm -f <name>.1.<id>`刪除其中一個container 

swarm偵測到container少一個，會即時再Run一個新的，維持service run三個alpine container的狀態

![維持service狀態](https://imgur.com/qMEtNaT.jpg)

---

# Creating 3-Node Swarm

有三種方式可以模擬多台虛擬機的情境

- play-with-docker.com
  - docker playground初學者的好朋友
- docker-machine + virtualBox
  - 在本機利用docker-machine create建立多台虛擬機
- [Digital Oocean](https://www.digitalocean.com/)
  - 講師推薦(不貴,對入門者很夠用)
  - VPS主機商, SSD固態硬碟
  - 處理快又穩定

*懶人如我，當然先選擇docker playground(?)*

---

前面提到在swarm的世界裡，Node主機有兩種角色可以選擇

- Manager
- Worker

<img src="https://imgur.com/I7aBwGZ.jpg" alt="Manager node" style="zoom:50%;" />

<img src="https://imgur.com/wDjBL1t.jpg" alt="Manager node" style="zoom:50%;" />

圖摘自[Docker Swarm Docker Swarm Tutorial  What Is Docker Swarm? Docker Swarm Setup Simplilearn](https://www.youtube.com/watch?v=Tm0Q5zr3FL4)

**擔任Manager的主機指派Task給Worker主機，主機之間透過HTTP傳輸**

---

## 練習Time

> 目標:建立4台主機分別指定2台為manager,2台為worker

建立4台Host (playground快樂建立)

![create host](https://imgur.com/PgkqKfw.jpg)

---

在node 1主機執行swarm 初始化

`docker swarm init --advertise-addr <ip> --listen-addr <ip>`

node主機溝通靠 `advertise-addr`

service監聽連線靠`listen-addr`

可參考[What’s the Docker Swarm “–advertise-addr”?](https://boxboat.com/2016/08/17/whats-docker-swarm-advertise-addr/)



![swarm init](https://imgur.com/NJsVmAH.jpg)

swarm會建立兩組token，分別for Manager和Worker

貼心顯示要加入manager和worker要用哪個指令哪個token

---

node1主機加入manager行列(?)

![add manager](https://imgur.com/fSxUERV.jpg)

---

切換到node2主機

將node2也加入manager中，記得要加上自己的ip，讓其他node知道 who are you

![add manager](https://imgur.com/HEK31nT.jpg)

---

切換到node3,4主機

加入worker行列

![add worker](https://imgur.com/3gyoOD0.jpg)

---

`docker info`查看資訊 (check swarm的相關設定)

```shell
Swarm: active
  NodeID: 9v6mjw7mi4443fsr4s03bu085
  Is Manager: true
  ClusterID: 2kccke7zrcz6jxsddwicg16bq
  Managers: 2
  Nodes: 4
  Default Address Pool: 10.0.0.0/8  
  SubnetSize: 24
  Data Path Port: 4789
  Orchestration:
   Task History Retention Limit: 5
  Raft:
   Snapshot Interval: 10000
   Number of Old Snapshots to Retain: 0
   Heartbeat Tick: 1
   Election Tick: 10
  Dispatcher:
   Heartbeat Period: 5 seconds
  CA Configuration:
   Expiry Duration: 3 months
   Force Rotate: 0
  Autolock Managers: false
  Root Rotation In Progress: false
  Node Address: 192.168.0.10
  Manager Addresses:
   192.168.0.10:2377
   192.168.0.13:2377
```

---

進到其中一台manager主機中，執行`docker node ls`查看各node主機狀態

*manager才有權限可以看到node 主機狀態*

![docker node ](https://imgur.com/79DC5AD.jpg)

---

<br>

# 讀書會知識補充

## 好書推薦區

帆哥推薦資工系演算法用書:[Introduction to Algorithms Hardcover – 1 Jan. 2009](https://www.amazon.co.uk/Introduction-Algorithms-Thomas-H-Cormen/dp/0262033844)

*演算法好炸人.....*

---

昱廷推薦MS SQL書:[Microsoft SQL Server 2016 設計實務](https://www.books.com.tw/products/0010742033)

---

## Coding速度區

昱廷推薦:[英打練習遊戲](https://www.keybr.com/multiplayer)

帆哥推薦:[正確使用鍵盤-闖關遊戲](https://www.typingclub.com/)

<br>


