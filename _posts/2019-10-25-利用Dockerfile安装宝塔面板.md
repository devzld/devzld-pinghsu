---
layout: post
title: 利用Dockerfile安装宝塔面板
date: 2019-10-25 00:00:00 +0800
category: 技术教程
thumbnail: /public/thumbs/5.jpg
icon: book
---
编写Dockerfile文件如下：
```dockerfile
FROM centos:latest
MAINTAINER zldyes@gmail.com

EXPOSE 20 21 80 443 888 8888

RUN yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh -c '/bin/echo -e "y" | sh install.sh'
```
注意后面是修改sh install.sh成sh -c '/bin/echo -e "y" | sh install.sh'。
其中y表示输入y同意安装一次，主要参考这个https://blog.csdn.net/leon_wzm/article/details/78260795。

然后进入Dockerfile文件目录运行
```shell script
docker build .
```
就生成了镜像
利用
```shell script
docker images
```
查看，然后启动镜像
```shell script
docker run -i -t -d --name baota -p 20:20 -p 21:21 -p 80:80 -p 443:443 -p 888:888 -p 8888:8888 --privileged=true -v ~/www:/www/wwwroot centos
```
其中centos替换成刚刚的镜像ID，这样就运行了一个容器，然后执行如下命令
```shell script
docker exec -it baota /bin/bash
```
进入容器，然后再执行一下启动宝塔命令，https://www.bt.cn/btcode.html中的
```shell script
/etc/init.d/bt start
```
再执行
```shell script
bt default
```
查看宝塔面板信息，将IP换成localhost在本机访问即可。




