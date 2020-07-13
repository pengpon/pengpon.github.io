---
layout: post
title:  "[Docker]讀書會Part2"
date:   2020-07-11 22:59:00 +0800
author: Pon
categories: docker
tags: Devops
---

> 7/9讀書會，帆哥主講Docker network&image筆記



# Docker Network

> Docker is an open platform for developing, shipping, and running applications.
>
> How do containers communicate with each other?

學了怎麼Run container，接下來要知道的是container之間如何溝通!



## Container Network Model

> 定義container的網路模型所要依循的規範和標準

> With [`libnetwork`](https://github.com/docker/libnetwork), Docker is aiming to provide standard interface to connect containers and satisfy composible needs. `libnetwork` library can be used independent of Docker.
>
>取自[**Libnetwork**](http://nkhare.github.io/data_and_network_containers/libnetwork/)

透過Library-Libnetwork，Docker有一套標準去規範網路模型該要遵守的規範和標準!  而Libnetwork是實作CNM來的!



<br>

# Docker Network

`docker network --help` 萬能的help

docker network default為bridge!

<br>

## 補充知識-Bridge

> 大推這篇，圖多-[中繼器 (Repeater)、集線器 (Hub)、橋接器 (Bridge)、交換器 (Switch) 原理與介紹](https://notfalse.net/66/repeater-hub-bridge-switch#-Bridge)

- 橋接器(Bridge)

![Bridge](https://imgur.com/eBkxP3l.jpg)

> 圖取自[中繼器 (Repeater)、集線器 (Hub)、橋接器 (Bridge)、交換器 (Switch) 原理與介紹](https://notfalse.net/66/repeater-hub-bridge-switch#-Bridge)

如文章提的，傳統是採用Bus Topology(匯流排拓樸)，當用廣播方式傳輸時，幹線上的節點都會收到，資安會有疑慮。

後來發展出集線器(Hub)，佈線採Star Topology(星狀拓樸)

但不管是匯流排或是星狀拓樸都可能會發生**碰撞網域(Collision Domain)**

所以演化史中就出現了像是Bridge(橋接器)或是Switch(交換器)。

Docker預設使用的就是Bridge，切分多個網域，減少碰撞機率!

<br>

---

`docker network ls` 列出網路清單

---

`docker network create <networkname>` 建立網路 -預設driver是bridge

```
// docker network my_app_net
// docker network ls

NETWORK ID          NAME                DRIVER              SCOPE
72cf7a683286        bridge              bridge              local
b2e7e37069ae        host                host                local
8b316da9524b        my_app_net          bridge              local
005a3412f529        none                null                local
```

---

`docker network inspect <networkname>` 檢視網路設定

---

`docker container attach <containername>` 進入container中

- ip addr show 查看IP設定
- Exit會結束container，`Ctrl+P+Q`可跳出container且不會stop container
- ping 同network的container

---

`docker network connect <networkname> <containername>`再掛一個network到container上

如下圖概念:

![container network model](https://imgur.com/1393lxd.jpg)

> 圖取自[Docker Networking – Explore How Containers Communicate With Each Other](https://www.edureka.co/blog/docker-networking/)



<br>

# 精選練習

- 建立名稱為mynet的network
- 檢查mynet是否在清單上
- 啟動三個alpine container (a1,a2,a3)，a1&a3不指定network，a2要使用mynet
- 檢查是否啟動成功
- 檢視mynet設定，瞧瞧a2是否在其中
- 進到a1 container 內部，查看ip設定，嘗試從a1 `ping <a3 IP>` & `ping <a2 IP>`
- a1 和network mynet 連接，再試試看從a1`ping <a2 IP>`

<br>

# 延伸閱讀&參考圖文

[Docker Networking – Explore How Containers Communicate With Each Other](https://www.edureka.co/blog/docker-networking/)

[Practical Design Patterns in Docker Networking](https://www.slideshare.net/Docker/practical-design-patterns-in-docker-networking-81017903)

[中繼器 (Repeater)、集線器 (Hub)、橋接器 (Bridge)、交換器 (Switch) 原理與介紹:圖多大推](https://notfalse.net/66/repeater-hub-bridge-switch#-Bridge)