---
layout: post
title:  "[Docker]讀書會Part3"
date:   2020-07-22 21:15:00 +0800
author: Pon
categories: docker
tags: devops
---

> 7/16 帆哥主講network&image讀書會筆記

<br>

# Docker Networking

container 之間要溝通可以透過:

- container拿到的虛擬ip位置  (缺點-container 重啟ip會變)
- host主機ip:port  (docker container run -p xx:xx設定)
- docker的link機制

前兩種Part有試過，所以來記錄第三種

## --link用法

<br>

1. create new container 'mysql' , 並指定名稱

   `docker container run --name mysql -e MYSQL_ROOT_PASSWORD=server -dit mysql`

   ![run mysql](https://i.imgur.com/TjITDgM.png)

2. create other container, 使用link連接到剛剛建立的container 

   `docker container run --name nginx --link mysql:aliasmysql -dit nginx`

   > aliasmysql是自訂的別名/綽號
   >
   > 透過`--link`連接到mysql這個container，並取一個別名給它

   ![run nginx](https://i.imgur.com/hkLXtMG.png)

<br>

進到nginx container內部，試著連到mysql container 

`docker container exec -it  nginx bash`

`ping mysql` or `ping aliasmysql`，都會連成功

p.s. maybe會出現 ping:command not found，透過apt-get安裝就好!

```
apt-get update
apt-get install iputils-ping
```

![ping ping](https://i.imgur.com/MYgTUaf.png)

<br>

也就是在hosts設定檔中，幫我們多加一組對應

![](https://i.imgur.com/WqzIlDK.png)

> hosts檔放置位置
>
> windows: `C:\WINDOWS\system32\drivers\etc\hosts`
>
> Linux: `/etc/hosts`
>
> hosts可以自訂domain和IP的對應，找不到才會去向DNS找!

<br>

`docker container run --name nginx --link mysql:aliasmysql -dit nginx`，在run的時候就把mysql資訊寫進nginx中

所以link的設定屬於**單向連結**，且要搭配run使用!

## 共用變數

進到mysql container 內，查看環境變數

`docker container exec -it mysql bash`

輸入`env`

![mysql-env](https://i.imgur.com/0YqQvi9.png)

會看到當初在run時傳入的MYSQL_ROOT_PASSWORD

<br>

再到nginx container內，檢視環境變數

![nginx-env](https://i.imgur.com/H6Wb7dI.png)

可以看到aliasmysql的相關環境變數也被加進來了

也許就可以把一些需要共用的變數放這(?)

## 小結--link

link主要提供了:

- 使用alias別名連線
- 注入環境變數

重要的是 **link在之後版本會移除，還是使用network connect較好**

<br>

# Image

`docker image ls`

`docker pull ${image}[:tag]>` 從docker hub下載image至本機

docker hub搜尋image (有標official為官方出)

![nginx-image](https://i.imgur.com/OC4cHs5.png)

<br>

會註明support哪些tags

![nginx-tags](https://i.imgur.com/4nb6vYt.png)

- `docker image pull nginx:1.19.1-alpine`
- `docker image pull nginx:alpine` 
- `docker image pull 1.19-alpine`

**從image id 看出，三個對應到的是同一個image** 

**只有第一次是從docker hub上下載，其他都是用本機的image**

![pull image](https://i.imgur.com/L2WwKn0.png)

![same image](https://i.imgur.com/gUxsLhJ.png)

<br>

`docker image push ${image name}[:tag]` 將local的image推上docker hub

**記得要登docker hub**

<br>

## build image

Dockerfile負責記錄如何建立一個docker image

`docker image build -t custom-nginx .`

**最後一個`.`代表當下目錄**

Dockerfile中的`FROM`, `ADD`,`RUN`會增加layer

太多層會造成image太大

太少層就無法跟別的image share layer

<br>

# container V.S image

![container create](https://i.imgur.com/SbgQwmO.png)

圖取自[Docker - Storage drivers](https://adon988.logdown.com/posts/7801780-docker-storage-drivers)

image是由多個layer組成，而container是根據image再建立出來的

container是在image之上的`writable layer`，異動是儲存在`writable layer`中。

![writable layer](https://i.imgur.com/kK6u7N2.png)

圖取自[How to Create Docker Container using Dockerfile](https://linoxide.com/linux-how-to/dockerfile-create-docker-container/)

<br>

# 參考圖文

[Docker - Storage drivers](https://adon988.logdown.com/posts/7801780-docker-storage-drivers)

[How to Create Docker Container using Dockerfile](https://linoxide.com/linux-how-to/dockerfile-create-docker-container/)
