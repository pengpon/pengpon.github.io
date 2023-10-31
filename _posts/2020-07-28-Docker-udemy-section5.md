---
layout: post
title:  "[Docker]Udemy class:Docker Mastery Section 5"
date:   2020-07-28 22:56:00 +0800
author: Pon
categories: docker
tags: devops
---

> 節錄線上課程`Docker Mastery Section 5`內容

<br>

# Container Lifetime & Persistent Data

前情提要: docker image是由多個layer組成(read-only)，啟動一個container時，Docker會再掛一層Read-write! 

如果在這個執行中的container中異動A文件，其實是從Read-only layer複製到Read-write layer，實際改的是複製出來的副本。

刪除container時，更改也就一起消失。 *p.s. read-only layer 和最頂層的Read-write layer 合稱 Union File System* 

![UFS](https://i.imgur.com/VnpaXyo.png)

圖摘自:[Virtualization-fizalihsan](https://fizalihsan.github.io/technology/virtualization.html)



<br>

- containers **通常**是 immutable, ephemeral 
- 只能re-deploy container, 才有可能改變
- 遇到database or data 想存取時....
- 於是`Persistent data`出現
- 兩種方式- Volumes & Bind Mounts
- volumes: make special location outside of container UFS
- Bind Mounts: link container path to host path

<br>

---

# Persistent Data: Data Volumes

先看看Docker hub>>> mysql image>>> Dockerfile

![check mysql Dockerfile](https://i.imgur.com/0mJrQHZ.png)

---

`docker pull mysql` 載mysql

---

`docker image inspect mysql` 這包image資訊

```
 "Volumes": {
                "/var/lib/mysql": {}
            },
```

---

`docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql` 啟動container

![run container](https://i.imgur.com/MHAOIXN.png)

---

`docker container ls` 確定running

---

`docker container inspect mysql`

```
   "Mounts": [
            {
                "Type": "volume",
                "Name": "46c9a803db3082250ebb375bb02dfcd3893945e85a9386b38741bd5ab4285756",
                "Source": "/mnt/sda1/var/lib/docker/volumes/46c9a803db3082250ebb375bb02dfcd3893945e85a9386b38741bd5ab4285756/_data",
                "Destination": "/var/lib/mysql",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""
            }
        ],
```

---

`docker volume ls`

```
DRIVER              VOLUME NAME
local               46c9a803db3082250ebb375bb02dfcd3893945e85a9386b38741bd5ab4285756
```

---

`docker volume inspect  46c9a803db3082250ebb375bb02dfcd3893945e85a9386b38741bd5ab4285756`

*mounts是本機位置; volume是container中的位置*

![volume inspect](https://i.imgur.com/HKBmAj1.png)

---

再啟動一個 container mysql2

`docker container rum -d --name mysql2 -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql`

---

`docker volume ls` 

```
DRIVER              VOLUME NAME
local               46c9a803db3082250ebb375bb02dfcd3893945e85a9386b38741bd5ab4285756
local               53b07a654678b5af510210a501f7570dd03a8ec9af7059860a471f1828e16f5d
```

---

`docker container stop mysql mysql2` 停止執行container 

`docker container rm mysql mysql2` 刪除container

---

volume 不會隨著container 刪除而消失 

![volume ls](https://i.imgur.com/mrFTmxw.png)

---

**named volumes (friendly way to assign vols to containers)**

`docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql` 在run的同時 給`-v`  替volume取名



![volume named](https://i.imgur.com/gySZOsM.png)

---

`docker volume create`- required to do this before 'docker run ' to use custom drivers and labels

<br>

# Persistent Data: Bind Mounting

- can't use in Dockerfile, must be at `container run`
- `... run -v /users/bret/stuff:/path/container` (mac/linux)
- `... run -v //c/users/bret/stuff:/path/container` (windows)

<br>

---

`docker container run -d --name nginx -p 80:80 -v  $(pwd):/usr/share/nginx/html nginx`

`docker container run -d --name nginx2 -p 8080:80 nginx`

<br>

---

**-v pathA:pathB 用來設定主機的A目錄要同步對應到container的B目錄**

試驗: 開另一個terminal, 進到nginx container中的`/usr/share/nginx/html`

隨意新增一檔案 `touch test.txt`

到本機mount的路徑，也可以看到多了一個`test.txt`檔案。





<br>

# 小結

![volume & bind mount](https://i.imgur.com/k1gEGXr.png)

圖摘自[官方文件](https://docs.docker.com/storage/volumes/)

- volume會將data存到預設的docker area下
- bind mount可以指定filesystem的位置 

<br>

# 延伸閱讀&參考圖文

[深入理解Docker Volume（一）](http://dockone.io/article/128)

[Virtualization-fizalihsan](https://fizalihsan.github.io/technology/virtualization.html)