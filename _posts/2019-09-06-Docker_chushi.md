---
layout:     post
title:      Docker 概述
subtitle:    "Docker"
date:       2019-09-06
author:     Cosmo-Ma
header-img: img/post-default.jpg
catalog: true
tags:
    - Docker
---

## Docker 容器生态

Docker公司的一个核心哲学思想被称为”含电池，但可拆卸“。意思是Docker内置的组件都可以用第三方的组件替换。

- 查看docker 版本

```bash
~ docker version
Client: Docker Engine - Community
 Version:           19.03.8
 API version:       1.40
 Go version:        go1.12.17
 Git commit:        afacb8b
 Built:             Wed Mar 11 01:21:11 2020
 OS/Arch:           darwin/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.8
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.17
  Git commit:       afacb8b
  Built:            Wed Mar 11 01:29:16 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.2.13
  GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
➜  ~
```

## 镜像

将Docker镜像理解为一个包含了OS文件系统和应用的对象会很有帮助。镜像实际上等价于未运行的容器。镜像包含了基础的操作系统，以及应用程序运行所需要的代码和依赖包。
查看主机中的运行镜像 docker image ls

```bash
➜  ~ docker image ls
REPOSITORY                                                             TAG                 IMAGE ID            CREATED             SIZE
artifactory.dev.adskengineer.net/autodeskcloud/cerv2-automation-test   latest              f94ca0f0f462        7 weeks ago         1.01GB
➜  ~
```

在Docker主机上获取镜像的操作被称为拉取（pulling）.如何使用linunx，则会拉取ubuntu:latest镜像。如歌使用windows，则会拉取microsoft/powershell:nanoserver镜像。

## 容器

假设以及拥有一个拉取到本地的镜像，可以使用docker container run 命令从镜像来启动容器

```bash
docker container run -it ubuntu:latest /bin/bash
```
 
- -it 参数会将shell切换到容器终端，现在已经是在容器内部了
- 接下来命令告诉Docker，用户想基于ubuntu:latest镜像启动容器
- 最后用户想在容器内部运行哪个进程（Bash Shell）
