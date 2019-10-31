---
title: Go中的type关键字
toc: false
date: 2019-06-29 23:58:09
category: Go
tags: Go
---

Go中的type关键字用法

<!--more-->

### 1.定义一种类型

如：

```go
package main

import (
	"fmt"
	"reflect"
)

//表示Student是一种类型：结构体
type Student struct {
}

//表示Runnable是一种类型：接口
type Runnable interface {
	run()
}

//表示S是一种类型：string（创造的新类型）
type S string

func main() {
	var a Student
	var b Runnable
	var c S = "abc" //a是新类型S
	fmt.Println(reflect.TypeOf(a))
	fmt.Println(reflect.TypeOf(b))
	fmt.Println(reflect.TypeOf(c))
}
```

打印结果是：

```shell
main.Student
<nil>
main.S
```

### 2.类型别名

```go
package main

import (
	"fmt"
	"reflect"
)

//1.9中引入，表示name是string类型的别名，拥有string类型的所有方法集
type name = string

func main() {
	var a name = "abc"
	fmt.Println(reflect.TypeOf(a))
}
```

打印结果：

```shell
string
```

### 3.类型查询

type还可以用于类型查询：

```go
package main

import (
	"fmt"
)

func main() {
	// 定义一个interface{}类型变量，并使用string类型值"abc"初始化
	var a interface{} = "abc"

	// 在switch中使用 变量名.(type) 查询变量是由哪个类型数据赋值。
	switch v := a.(type) {
	case string:
		fmt.Println("字符串")
	case int:
		fmt.Println("整型")
	default:
		fmt.Println("其他类型", v)
	}
}
```

结果：

```shell
字符串
```

## 定义类型的使用例子

```go
package main

import "fmt"

//handle是一种类型，函数类型
type handle func(str string)

//此函数接收一个函数类型的参数
func exec(f handle) {
	f("hello")
}

func main() {
  //生成参数
	var a = func(str string) {
		fmt.Println("我是处理函数"+str)
	}

  //调用函数
	exec(a)
}

```

结果是

```shell
我是处理函数hello
```

和以下写法等价：

```go
package main

import "fmt"

func main() {
	//参数
	var a = func(str string) {
		fmt.Println("我是处理函数" + str)
	}

	//调用参数
	exec(a)
}

//函数
func exec(f func(str string)) {
	f("hello")
}
```

相比是上面的定义函数更简洁