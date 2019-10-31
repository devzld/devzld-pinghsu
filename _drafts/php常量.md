---
title: php常量
toc: true
tags: PHP
category: PHP
---

## php常量

<!-- more -->

### 如何定义常量

使用define函数：

语法如下：

	bool define ( string $name , mixed $value [, bool $case_insensitive = false ] ) 

true表示不区分大小写
	
例子：

	define("GREETING", "欢迎访问", true);
	echo GREETING;
	echo greeting;

### 常量默认是全局的，可以在运行脚本的任何地方使用	