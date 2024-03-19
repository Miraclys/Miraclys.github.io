---
title: docker
date: 2024-03-18 00:01:38
tags:
- docker
description: 
---

#### Docker 命令

##### 容器生命周期管理

1. docker run IMAGE 运行镜像

    docker -d run IMAGE 后台运行，并返回容器 ID，其中 d 表示 detach
    docker --name="xxx" IMAGE 为容器指定一个名字

2. docker start CONTAINER 启动一个或者多个已经被停止的容器

3. docker stop CONTAINER 停止一个运行中的容器

4. docker restart CONTAINER 重启一个容器

5. docker rm CONTAINER 删除一个或者多个容器

    docker rm -f CONTAINER 强制删除容器

6. docker exec CONTAINER 在运行的容器中执行命令

    docker -d exec CONTAINER 分离模式，在后台运行

    docker -i exec CONTAINER 保持 stdin 打开

    docker -t exec CONTAINER 分配一个伪终端

    所以可以使用 docker -it exec CONTAINER 以命令行交互的形式进入一个docker终端

    例如：docker exec -it myngix /bin/bash

#### 容器操作

1. docker ps 列出所有的容器

    docker ps -a 显示所有的容器，包括未运行的。
    
2. docker inspect 获取容器或者镜像的元数据

    docker inspect NAME | ID 表示最后写 ID 或者 NAME 都可以

3. docker top CONTAINER 查看进程运行中的信息

#### 镜像仓库

1. docker login -u xxx -p xxx 登陆到一个 Docker 镜像仓库，如果没有指定镜像仓库地址，则默认为官方仓库，Docker Hub

2. docker pull NAME 从镜像仓库中拉取或者更新指定的镜像

#### 镜像操作

1. docker images 列出本地所有的镜像

    docker images -a 

2. docker rmi IMAGE 删除本地一个或者多个镜像

    docker rmi IMAGE -f 强制删除

