---
layout: post
title:  "[Docker]讀書會Part1"
date:   2020-07-4 17:27:00 +0800
author: Pon
categories: docker
tags: DevOps
---

> 下半年正式啟動Docker系列，跟著Udemy Docker captain學!
>
> 紀錄7/2 Docker讀書會系列-Part1



# Docker 簡言

擷取[What Does Docker Do, and When Should You Use It?](https://www.cloudsavvyit.com/490/what-does-docker-do-and-when-should-you-use-it/)內容

*Docker is a tool for running your applications inside containers*

*Docker is similar in concept to virtual Machines, except it's much more lightweight*

<br>

Docker會將應用程式和應用程式所需的環境包一起!

<br>



# Docker Image

- 用來建立Container
- 唯讀

<br>

# Docker Container

- 利用Image執行出來的程序
- 建立在Image層上
- 跟主機共用OS

<br>

# 體驗Docker-免安裝

[Docker playground](https://labs.play-with-docker.com/)

登入後>>>ADD NEW INSTANCE

可以先稍微體驗Docker

![docker playground](https://imgur.com/cHCq7Dc.jpg)



<br>

# 基本指令

[官方文件整理的基本指令](https://docs.docker.com/engine/reference/commandline/docker/)

---



`docker version `

```
Client: Docker Engine - Community
 Version:           19.03.11
 API version:       1.40
 Go version:        go1.13.10
 Git commit:        42e35e61f3
 Built:             Mon Jun  1 09:09:53 2020
 OS/Arch:           linux/amd64
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          19.03.11
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.10
  Git commit:       42e35e61f3
  Built:            Mon Jun  1 09:16:24 2020
  OS/Arch:          linux/amd64
  Experimental:     true
 containerd:
  Version:          v1.2.13
  GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
```

data輸出方式也可以用json顯示`docker version --format '{{json .}}'`



<br>

---



`docker info`

```
Client:
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 19.03.11
 Storage Driver: overlay2
  Backing Filesystem: xfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc version: dc9208a3303feef5b3839f4323d9beb36df0a9dd
 init version: fec3683
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 4.4.0-184-generic
 Operating System: Alpine Linux v3.12 (containerized)
 OSType: linux
 Architecture: x86_64
 CPUs: 8
 Total Memory: 31.4GiB
 Name: node1
 ID: W4YJ:PZGI:Z3OV:S2PV:XJCT:MALD:44WG:AMJ3:SZEM:XD4U:RICS:C56N
 Docker Root Dir: /var/lib/docker
 Debug Mode: true
  File Descriptors: 23
  Goroutines: 42
  System Time: 2020-07-04T10:17:06.957652063Z
  EventsListeners: 0
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: true
 Insecure Registries:
  127.0.0.1
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine

WARNING: API is accessible on http://0.0.0.0:2375 without encryption.
         Access to the remote API is equivalent to root access on the host. Refer
         to the 'Docker daemon attack surface' section in the documentation for
         more information: https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface
WARNING: No swap limit support
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
```



<br>

## run

在Docker 1.13以前 只有支援`docker run`這種寫法

docker run>>> **建立**一個新的container，並**啟動**它

docker run= /containers/create + /containers(id)/start

<br>

cli command 後來寫法進化(?)成 `docker COMMAND SUBCOMMAND`的結構

參考[Introducing Docker 1.13](https://www.docker.com/blog/whats-new-in-docker-1-13/)

<br>

`docker container run --publish 80:80 nginx`

白話:

要利用nginx這個image檔啟動一個container

會先從本機中找有沒有名為nginx的image，沒有的話再到Docker hub上找

<br>

### run Options

`--name test`

將run起來的container取名，沒給的話docker隨機給你一個

<br>

---



`--publish host machine port:container TCP port`

實體主機Port(對外):Container port(內部)

啟動的container若要被其他Host/Container使用!

<br>



![docker container interaction](https://imgur.com/m8LrPC9.jpg)

圖摘自[Run API Portal in Docker containers](https://docs.axway.com/bundle/APIPortal_762_InstallationGuide_allOS_en_HTML5/page/Content/APIPortalInstallGuideTopics/docker_portal_overview.htm)

<br>

---



`--detach, -d`

在背景執行container，並印出container ID



<br>

## 其他

`docker containe ls -a`or`docker ps -a`

列出所有的containers

```
$ docker container ls
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
dd7663ffae5e        nginx               "/docker-entrypoint.…"   10 seconds ago      Up 9 seconds        0.0.0.0:80->80/tcp   sad_mcnulty
```

ps. sad_mcnulty為隨機給的container name

<br>

---



`docker container logs [container id/ container name] `

```
$ docker container logs dd7
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
```

ps. container 不用全打，可以識別就好

<br>

---



`docker container stop [container id/container name]`

<br>

---



`docker container start [container id/container name]`

<br>

---



`docker container rm [container id/container name]`

---



進階`docker container rm $(docker ps -a -q)/$(docker container ls -a -q)` 

會刪除所有停止的container，`docker ps -a -q`會回傳所有存在的container id

將結果pass給rm 指令去執行刪除! rm一樣可以加上`--force,-f`強制執行

執行中的container不會被刪掉~



---

`docker exec`

在執行中的container中run command

進入container的shell中!

ex:`docker container exec -it [container] command `

```
$ docker container exec -it dd7 bash
root@dd7663ffae5e:/# pwd
/
root@dd7663ffae5e:/# ls
bin                   etc    mnt   sbin  var
boot                  home   opt   srv
dev                   lib    proc  sys
docker-entrypoint.d   lib64  root  tmp
docker-entrypoint.sh  media  run   usr
root@dd7663ffae5e:/#
```

`--interactive,-i` Keep STDIN 標準輸入

`--tty,-t` Allcate a pseudo-TTY 

<br>

# 延伸閱讀&參考網站

[What Does Docker Do, and When Should You Use It?](https://www.cloudsavvyit.com/490/what-does-docker-do-and-when-should-you-use-it/)

[虛擬機與Docker有何不同？](https://kknews.cc/zh-tw/code/lpkl3nz.html)