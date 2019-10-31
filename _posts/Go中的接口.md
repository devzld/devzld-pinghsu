---
title: Go中的接口
toc: false
date: 2019-06-30 00:43:42
category: Go
tags: Go
---

Go中的接口

<!--more-->

任何其他类型只要实现了接口中的所有方法就是实现了这个接口

```go
package main

import (
	"fmt"
	"reflect"
)

//接口
type Phone interface {
	call()
}

//结构体
type NokiaPhone struct {
}

//实现接口
func (nokiaPhone NokiaPhone) call() {
	fmt.Println("我是诺基亚，我可以打电话给你")
}

func main() {
	var phone Phone
	phone = new(NokiaPhone)
	phone.call()
}
```

