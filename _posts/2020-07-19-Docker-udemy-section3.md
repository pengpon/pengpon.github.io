---
layout: post
title:  "[Docker]Udemy class:Docker Mastery Section 3 "
date:   2020-07-19 17:14:00 +0800
author: Pon
categories: docker
tags: Devops
---

> Review 線上課程 `Docker Mastery Section3`內容

<br>



# Udemy- Docker mastery Note

## Docker Install and Config

`docker version` verified cli talk to engine

`docker info` most config values of image

<br>

docker 指令的組成結構(新)

docker <command> <sub-command> (options)

ex: docker container run 

## Starting a Nginx Web Server

> image is the application we want to run
>
> container is an instance of that image running as a process

<br>

`docker container run --publish 7777:80 nginx`

> starts a new container from an image

![Docker container run](https://imgur.com/MIfPrjC.jpg)

<br>

`docker container run  --publish 7777:80 nginx`實際上做了????

- 從docker hub download一個名為`nginx`的image
- 利用這個image建立並啟動一個新的container
- Host ip 開7777 port
- 指向Container ip 的 80 port

<br>

`docker container run --publish 7777:80 --detach nginx` container running in background

`docker container ls` list running containers

`docker container stop`  stops the container process but doesn't remove it

![container run&stop](https://imgur.com/0UVPVaa.jpg)

<br>

### **[註]**run和start差異

`docker container run ` 每次都會建立啟動一個全新的container

`docker container start` 啟動一個停止的container

<br>

`docker container run -publish 80:80 --detach --name webhost nginx`

`docker container logs ` show logs for specific container 

`docker container top webhost` 

`docker cotainer rm <container id> <container id>` 刪除被停止的container 

`docker container rm -f <container id>`強制刪除 (running container 也會被刪除)

<br>

## What Happens When we run a container

拆解`docker container run `發生的事情

1. 先在本機尋找image cache
2. 找不到預設會到Docker hub上找image
3. 下載最新或是指定的版本
4. 利用下載下來的image建立一個新的container (準備啟動)
5. 在Docker engine中的private network給一個虛擬IP
6. 啟動本機的Port A，並指向container Port B (--publish A:B)
7. 利用image Dockerfile中的指令去啟動container

例如:

`docker container run --publish 8080:80 --name webhost -d nginx1.11 nginx -T`

<br>

## Container VS. VM

> container just **processes**
>
> Exit when process stops



`docker run --name monfo -d mongo`

`ps aux` show all running processes

![查看程序](https://imgur.com/1KgFExA.jpg)

`ps aux | grep mongo`

<br>

## What's Goning On in Containers

`docker container top` process list in one container 

`docker container inspect` details of one container config

> show metadata about the container 
>
> (startup config, volumes, networking,.....)

`docker container stats` performance stats for all containers

<br>

## Getting a Shell Inside Containers

`docker container run -it` start new container interactively

`docker container exec -it` run additional command in existing container 

> -t, --tty: allocate a pseudo-TTY
>
> -i, --interactive: keep session open to receive terminal input

<br>

`docker container run -it --name proxy nginx bash`

`docker container run -it ubuntu ubuntu`

`docker container start start -ai ubuntu`

> -a, --attach

`docker container exec -it mysql bash`

<br>

**Alpine Linux**: a small security-focused distribution

`docker pull alpine`

> alpine liniux: 輕量!!  使用apx管理! 

`docker container run -it alpine sh`

<br>

## Docker Networks: Concepts

> Each container connected to a private virtual network "brige"

> each virtual network routes through NAT firefall on host IP

> All container on a virtual network can talk to each other without `-p`

`docker container run -p 80:80 --name webhost -d nginx`

`docker container port webhost`

`docker container inspect --format '｛｛.NetworkSettings.IPAddress}}' webhost`

`ifconfig en0`

<br>

## Docker Networks: Management

`docker network ls` show networks

`docker network inspect` inspect a network

`docker network create --driver` create a network

`docker network connect` attach a network to container 

`docker network disconnect` detach a network from container

<br>

`docker network create my_app_net`

`docker container run -d --name new_nginx --network my_app_net nginx `

`docker network connect` dynamically creates a NIC in a container on an existing virtual network

`docker network connect my_app_net  webhost`

<br>

##  Docker Networks: DNS 

> Docker daemon has a built-in DNS server that containers use by default

`docker container run -d --name my_nginx --network my_app_net nginx `

`docker container exec -it my_nginx ping new_nginx`



