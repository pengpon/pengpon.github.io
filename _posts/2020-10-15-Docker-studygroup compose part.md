---
layout: post
title:  "[Docker]讀書會Compose Part"
date:   2020-10-21 17:45:00 +0800
author: Pon
categories: docker
tags: devops
---

> 10/15 winnie主講docker compose 筆記

# Docker compose

compose是一個工具，可以去定義/執行多個container。

使用『YAML』檔案去設定service。

一行指令就可以建立並啟動多個service。



<br>

使用Compose三步驟:

1. 應用程式的環境打包成『Dockerfile』
2. 將應用程式的service做拆分，定義在『docker-cmpose.yml』中
3. 執行『docker-compose up』

<br>

**『Compose讓container的設定利用YAML檔案完成』**

<br>

## YAML檔

**key:value**的形式

一個key若有多個值，可以用list方式`-`列出。

<br>

`docker-compose --help`查詢使用說明

`docker-compose.yml `是預設檔名，可以另外使用`docker-compose -f`自訂要執行的yaml檔位置



yaml基本格式

```yaml
# template.yml
version: '3.1'  # if no version is specified then v1 is assumed. Recommend v2 minimum

services:  # containers. same as docker run
  servicename: # a friendly name. this is also DNS name inside network
    image: # Optional if you use build:
    command: # Optional, replace the default CMD specified by the image
    environment: # Optional, same as -e in docker run
    volumes: # Optional, same as -v in docker run
  servicename2:

volumes: # Optional, same as docker volume create

networks: # Optional, same as docker network create
```

- version:一開始要設定，沒給預設是v1，建議使用v2以上!
- services:
  - services基本上就是container，但從application的角度來看，它是來提供服務的，稱service較適合
  - servicename等同於`docker run --name`
- volumes
- networks

---

yaml範例1

```yaml
version: '2'

# same as 
# docker run -p 80:4000 -v $(pwd):/site bretfisher/jekyll-serve

services:
  jekyll:
    image: bretfisher/jekyll-serve
    volumes:
      - .:/site
    ports:
      - '80:4000'
```

一個jekyll專案，使用bind mount

- 作用等同於`docker run -p 80:4000 -v $(pwd):/site bretfisher/jekyll-serve`
- `.:/site` 其中`.`代表當前目錄

---

yaml範例2

```yaml
version: '3'

services:
  ghost:
    image: ghost
    ports:
      - "80:2368"
    environment:
      - URL=http://localhost
      - NODE_ENV=production
      - MYSQL_HOST=mysql-primary
      - MYSQL_PASSWORD=mypass
      - MYSQL_DATABASE=ghost
    volumes:
      - ./config.js:/var/lib/ghost/config.js
    depends_on:
      - mysql-primary
      - mysql-secondary
  proxysql:
    image: percona/proxysql
    environment: 
      - CLUSTER_NAME=mycluster
      - CLUSTER_JOIN=mysql-primary,mysql-secondary
      - MYSQL_ROOT_PASSWORD=mypass
   
      - MYSQL_PROXY_USER=proxyuser
      - MYSQL_PROXY_PASSWORD=s3cret
  mysql-primary:
    image: percona/percona-xtradb-cluster:5.7
    environment: 
      - CLUSTER_NAME=mycluster
      - MYSQL_ROOT_PASSWORD=mypass
      - MYSQL_DATABASE=ghost
      - MYSQL_PROXY_USER=proxyuser
      - MYSQL_PROXY_PASSWORD=s3cret
  mysql-secondary:
    image: percona/percona-xtradb-cluster:5.7
    environment: 
      - CLUSTER_NAME=mycluster
      - MYSQL_ROOT_PASSWORD=mypass
   
      - CLUSTER_JOIN=mysql-primary
      - MYSQL_PROXY_USER=proxyuser
      - MYSQL_PROXY_PASSWORD=s3cret
    depends_on:
      - mysql-primary
```

- environment
  - 對應到多個環境變數值
  - 可用`-`設定每一個value



## docker-compose CLI

Docker compose command line tool和Docker tool是分開獨立的。

目前大部分下載時都包在一起，但在Linux中是分開的。



### 常用的兩個指令

- `docker-compose up`
  - 設定volumes/networks 和啟動所有containers
- `docker-compose down`
  - 停止所有containers以及移除cont/vol/net

---

有利於開發者建置環境

如果專案有『Dockerfile』和『docker-compose.yml』，新的開發者要建置環境只需要

- git clone xx/xxx/software
- 執行docker-compose up

<br>

## 練習 

開啟docker playground，先到[講師github](https://github.com/BretFisher/udemy-docker-mastery) clone專案下來

進入udemy-docker-mastery/compose-sample-2路徑下

先看看`docker-compose.yml`的內容

```yaml
version: '3'

services:
  proxy:
    image: nginx:1.13 # this will use the latest version of 1.13.x
    ports:
      - '80:80' # expose 80 on host and sent to 80 in container
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf:ro
  web:
    image: httpd  # this will use httpd:late
```

執行`docker-compose up` (可使用`-d` log就不會show出)

![docker-compose up](https://imgur.com/HhBiaxs.jpg)

總共會建立

- 1個 default network
- 2個 service
  - compose-sample-2_proxy_1
  - compose-sample-2_web_1

**nginx在這裡是proxy的角色，80 port看到的頁面是Apache回覆的html**



<br>

## 補充depends_on

*內容摘自[官方Compose file version 3 reference](https://docs.docker.com/compose/compose-file/)*

用來表示service之間的相依性，`docker-compose up`會依照依賴性啟動service。

範例

```yaml
version: "3.8"
services:
  web:
    build: .
    depends_on:
      - db
      - redis
  redis:
    image: redis
  db:
    image: postgres
```

- `docker-compose up`
  - 會依照相依性啟動
  - 例如上面的例子，db和redis啟動完才會去啟動**web**
- `docker-compose up SERVICE`
  - 包含該service相依的service也會執行
  - 例如上面的例子，`docker-compose up web`會建立並啟動db以及redis
- `docker-compose stop`
  - 依相依性停止服務
  - 例如上面的例子，web會在db及redis之前停止

『類似積木蓋房子的概念，db和redis是web所需要基礎，有了db和redis，web才能繼續往上建；要拆除也是上往下拆』



---

## 其他

- 讀書會下一個主題[The Python Mega Course: Build 10 Real World Applications](https://www.udemy.com/course/the-python-mega-course/)
- 昱廷分享[side project](https://yuting-daily-seed.appspot.com/music)
  - 登入後，使用youtube連結上傳
  - angular開發
  - [For angular:youtube-player](https://github.com/angular/components/tree/master/src/youtube-player#readme)







