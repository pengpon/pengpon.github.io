---
layout: post
title:  "[Docker]Udemy class:Docker Mastery Section 6"
date:   2020-08-06 09:56:00 +0800
author: Pon
categories: docker
tags: devops
---

> 筆記線上課程 Docker Mastery Section 6內容

<br>

> Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. 
>
> "Compose是用來管理多個container的工具，可以透過YAML檔案來設定Service，利用指令就可以建立以及啟動服務"
>
> by-[官方文件說明](https://docs.docker.com/compose/)



# Udemy- Docker mastery Note

## Docker Compose and The-docker-compose.yml File

之前要啟動container時，都要一個一個下`docker container run -p xx:xx -v xxxx imagename` blabla，在寫volume的folder時可能會打錯。 `docker compose`工具的產生可以解決這件事!

<br>

- why: configure relationships between containers
- why: save our docker container run settings in easy-to-read file
- why: create one-liner developer environment startups
- comprised of 2 separate but related things
  - YAML formatted file that describes our solution options for
    - containers
    - networks
    - volumes
  - a CLI tool `docker-compose` used for local dev/test automation with those YAML files

為什麼?

- 用來配置多個container
- 讓啟動container時要傳入的參數好讀好懂?)
- 利用一行指令可以迅速建立所需的環境

怎麼使用?

	- YAML檔案來定義container, network, volume
	- yml檔案中定義的服務，可以透過`docker-compose`指令來執行啟動、停止

<br>

---

### docker-compose.yml

- compose YAML format has it's own version:1,2,2.1,3,3.1
- YAML file can be used with `docker-compose` command for local docker container or..
- with docker directly in production with Swarm
- `docker-compose --help`
- `docker-compose.yml` is default filename, but any can b used with `docker-compose -f`

---

講者提供的template.yml

```yaml
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

---

實際yml:

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

```yaml
version: '2'

services:

  wordpress:
    image: wordpress
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: mysql
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_DB_USER: example
      WORDPRESS_DB_PASSWORD: examplePW
    volumes:
      - ./wordpress-data:/var/www/html

  mysql:
    image: mariadb
    environment:
      MYSQL_ROOT_PASSWORD: examplerootPW
      MYSQL_DATABASE: wordpress
      MYSQL_USER: example
      MYSQL_PASSWORD: examplePW
    volumes:
      - mysql-data:/var/lib/mysql

volumes:
  mysql-data:
```

<br>

---

## Basic Compose Commands

**docker-comppose CLI**

- CLI tool comes with Docker for windows/mac, but separate download for linux
- not a production-grade tool but ideal for local development and test
- two most common commands are
  - `docker-compose up`-setup volumes/networks and start all containers
  - `docker-compose down`-stop all containers and remove cont/vol/net
- if all your projects had a Dockefile and docker-compose.yml, then "new developer onboarding" would be:
  - `git clone github.com/some/software`
  - `docker-compose up`

<br>

---

啟動兩個container，nginx和apache 

nginx當proxy (守門員), apache當web server(提供內容者)

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
    image: httpd  # this will use httpd:latest
```

**指令沒有下 `-d` ，可以直接從log看到請求**

![docker-compose up](https://imgur.com/2rwc65D.jpg)



<br>

## 小結

在windows中使用docker toolbox，docker是Run在虛擬機上，有時候遇到volume掛不上，可以試試看先連進docker內。

`docker-machine ls`

`docker-machine ssh xxx`

![ssh docker machine](https://imgur.com/qxwwXm9.jpg)

<br>

# 參考圖文&文章

[Overview of Docker Compose](https://docs.docker.com/compose/)

[利用 Docker Compose 管理多個容器](https://www.coderbridge.com/@Jemmy1234/6d48f03f39284fe98ae9808f1243ef98)