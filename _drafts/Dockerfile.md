---
title: Dockerfile
date: 2019-05-31 00:26:00
toc: true
tags: Docker
category: Docker
---

Dockerfile

<!--more-->

## 基本结构

```dockerfile
# 一般的，Dockerfile 分为四部分：

# 基础镜像信息(必须在第一行)
FROM centos

# 维护者信息
MAINTAINER docker_user docker_user@email.com

ENV MYPATH /usr/local
WORKDIR $MYPATH

# 镜像操作指令
RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80

# 容器启动时执行指令
CMD echo $MYPATH
CMD echo "success-------ok"
CMD /bin/bash
```

## 指令

+ FROM：创建多个镜像，可使用FROM多次

```dockerfile
FROM <image>:<tag>
```

+ MAINTAINER

```dockerfile
MAINTAINER <name>
```

+ RUN <commond> 或 RUN ["executable", "param1", "param2"]



[参考链接](http://www.dockerinfo.net/dockerfile%E4%BB%8B%E7%BB%8D)



