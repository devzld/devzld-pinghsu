---
title: php数组
toc: true
tags: PHP
category: PHP
---

## php数组

<!-- more -->

### 如何创建数组？

数值数组：

	关键字定义：
	$cars = array("Volvo", "BMW", "Toyota");
	
	直接定义：
	$cars[0] = "Volvo";
	$cars[1] = "BMW";
	$cars[2] = "Toyota";

关联数组：

	关键字定义：
	$age = array("Peter" => "35", "Ben" => "37", "Joe" => "43");
	
	直接定义：
	$age["Peter"] = "35";
	$age["Ben"] = "37";
	$age["Joe"] = "43";

多维数组：
	
（见后面文章）


​	
### 如何访问数组？

使用下标访问：

	echo $cars[0] . " " . $cars[1] . " " . $cars[2];

### 如何获取数组的长度？

使用count()函数：

	echo count($cars);

### 如何遍历数组？

for循环遍历数组数组：

	$arrlength = count($cars);
	
	for ($x = 0; $x < $arrlength; $x++) {
	    echo $cars[$x];
	    echo "<br>";
	}

foreach循环遍历关联数组：

	foreach ($age as $x => $x_value) {
	    echo "Key=" . $x . ",Value=" . $x_value;
	    echo "<br>";
	}


​	