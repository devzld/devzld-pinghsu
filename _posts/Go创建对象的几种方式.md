---
title: Go创建对象的几种方式
toc: true
date: 2019-06-26 10:16:16
tags: Go
category: Go
---

Go创建对象的几种方式：

<!--more-->

```go
package main

import (
	"fmt"
	"reflect"
)

type Car struct {
	color string
	size  string
}

func main() {
  //方式一：使用T{...}方式，结果为value类型
	c := Car{}
	fmt.Println(reflect.TypeOf(c))

  //方式二：使用new的方式，结果为指针类型
	c1 := new(Car)
	fmt.Println(reflect.TypeOf(c1))

  //方式三：使用&方式，结果为指针类型
	c2 := &Car{}
	fmt.Println(reflect.TypeOf(c2))

  // 以下为创建并初始化
	c3 := &Car{"红色", "1.2L"}
	fmt.Println(reflect.TypeOf(c3))

	c4 := &Car{color: "红色"}
	fmt.Println(reflect.TypeOf(c4))
  
  c5 := Car{color: "红色"}
	fmt.Println(reflect.TypeOf(c5))
}
```

构造函数：

在Go语言中没有构造函数的概念，对象的创建通常交由一个全局的创建函数来完成，以
NewXXX 来命名，表示“构造函数” ：

```go
func NewCar(color,size string)*Car  {
	return &Car{color,size}
}
```

