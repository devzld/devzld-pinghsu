---
title: php数组排序
tags: PHP
category: PHP
---

## php数组排序

<!-- more -->

### 数组排序有哪些函数？

	sort() - 对数组进行升序排列
	rsort() - 对数组进行降序排列
	asort() - 根据关联数组的值，对数组进行升序排序
	ksort() - 根据关联数组的键，对数组进行升序排序
	arsort() - 根据关联数组的值，对数组进行降序排列
	krsort() - 根据关联数组的键，对数组进行降序排列

例如：

	$age["Peter"] = "35";
	$age["Ben"] = "37";
	$age["Joe"] = "43";
	
	arsort($age);
