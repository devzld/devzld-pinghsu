---
layout: post
title: 使用jsdelivr免费CDN加速你的网站
date: 2019-10-24 00:00:00 +0800
category: 技术教程
thumbnail: 
icon: book
---
jsDelivr 是国外的一家优秀的公共 CDN 服务提供商，也是首个打通中国大陆（网宿公司运营）与海外的免费 CDN 服务。jsDelivr 有一个十分好用的功能——它可以加速 Github 仓库的文件。借此我们可以用来加速我们的网站。
首先在Github上建一个公开的仓库，比如我建的名为static的库，
在Github上访问路径是
```
https://github.com/devzld/static/blob/master/asset/js/jquery.js
```
对应jsdelivr访问路径是：
```
https://cdn.jsdelivr.net/gh/devzld/static@master/asset/js/jquery.js
```
和
```
https://cdn.jsdelivr.net/gh/devzld/static@master/asset/js/jquery.min.js
```
缩小版本功能，将“.min”添加到任何JS / CSS文件中，jsdelivr将自动生成文件。

