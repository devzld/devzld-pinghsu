---
title: Go语言的变量和常量
toc: false
date: 2019-07-24 11:17:55
category: Go
tags: Go
---

转载

<!--more-->

# Go语言的变量和常量

# **1.变量**

变量是几乎所有编程语言中最基本的组成元素。从根本上说，变量相当于是对一块数据存储空间的命名，程序可以通过定义一个变量来申请一块数据存储空间，之后可以通过引用变量名来使用这块存储空间。

## 1.1 变量声明

对于纯粹的变量声明，Go语言引入关键字var，而类型信息放在变量名之后，形如:

```
var variableName type
var vname1, vname2, vname3 type
```

示例：

```
var v1 int
var v2 string
var v3 [10]int // 数组
var v4 []int // 数组切片
var v5 struct {
    f int
}
var v6 *int // 指针
var v7 map[string]int // map，key为string类型，value为int类型
var v8 func(a int) int
```

- 简短声明 
  **:=** 这个符号可以直接取代var关键字和变量类型，这种形式只能用在函数内部，并且左侧的变量不应该是已经声明过的。形如:

```
 vname:=value
```

示例：

```
v3 := 10 //编译器可以自动推导出v3的类型
```

- 分组声明

在Go语言中，同时声明多个常量、变量，或者导入多个包时，可采用分组的方式进行声明。

```
var (
    v1 int
    v2 string
)
```

## 1.2 变量初始化

对于声明变量时需要进行初始化的场景，指定类型已不再是必需的,Go编译器可以从初始化表达式的右值推导出该变量类型。 
形如：

```
var vname type=value
var vname =value //自动推导变量类型
var vname1, vname2, vname3 type= value1, value2, value3
var vname1, vname2, vname3 = value1, value2, value3 //自动推导变量类型 
```

示例:

```
var v1 int = 10 // 正确的使用方式1
var v2 = 10 // 正确的使用方式2，编译器可以自动推导出v2的类型
```

## 1.3 变量赋值

在Go语法中，变量初始化和变量赋值是两个不同的概念。

声明一个变量并赋值:

```
var v10 int
v10 = 123
```

Go语言的变量赋值与多数语言一致,但支持**多重赋值**，示例:

```
v1,v2 = 1,2
```

## 1.4 匿名变量

_（下划线）是个特殊的变量名，任何赋予它的值都会被丢弃。示例：

```
_ , b := 34, 35
```

------

Tip :

- Go对于已声明但未使用的变量会在编译阶段报错
- 大写字母开头的变量是公用变量，小写字母开头的是私有变量。
- 大写字母开头的函数也是一样，相当于class中的带public关键词的公有函数；小写字母开头的就是有private关键词的私有函数。

------

# **2. 常量**

常量，就是在程序编译阶段就确定下来的值，而程序在运行时则无法改变该值。在Go程序中，常量可以是数值类型（包括整型、浮点型和复数类型）、布尔类型、字符串类型等。

## 2.1 定义常量

通过const关键字，可以定义一个常量，语法如下

```
const constantName [type]= value
```

Go的常量定义可以限定常量类型，但不是必需的。如果定义常量时没有指定类型，那么它是无类型常量。只要这个常量在相应类型的值域范围内，就可以作为该类型的常量，比如常量-12，它可以赋值给int、uint、int32、int64、float32、float64、complex64、complex128等类型的变量

示例:

```
const Pi float64 = 3.14159265358979323846
const zero = 0.0 // 无类型浮点常量
const (
    size int64 = 1024
    eof = -1 // 无类型整型常量
)
const u, v float32 = 0, 3 // u = 0.0, v = 3.0，常量的多重赋值
const a, b, c = 3, 4, "foo" // a = 3, b = 4, c = "foo", 无          类型整型和字符串常量
```

常量定义的右值也可以是一个在编译期运算的常量表达式，比如 
const mask = 1 << 3 
由于常量的赋值是一个编译期行为，所以右值不能出现任何需要运行期才能得出结果的表达式，比如试图以如下方式定义常量就会导致编译错误：

```
const Home = os.GetEnv("HOME")
```

原因很简单，os.GetEnv()只有在运行期才能知道返回结果，在编译期并不能确定，所以 
无法作为常量定义的右值。

## 2.2 预定义常量

Go 语言预定义了这些常量：true、false 和 iota。 
iota 比较特殊，可以被认为是一个可被编译器修改的常量，它默认开始值是0，每调用一次加1。遇到 const 关键字时被重置为 0。

示例:

```
const (       // iota被重设为0
    c0 = iota // c0 == 0
    c1 = iota // c1 == 1
    c2 = iota // c2 == 2
)

const (
    a = 1 << iota // a == 1 (iota在每个const开头被重设为0)
    b = 1 << iota // b == 2
    c = 1 << iota // c == 4
)

const (
    u = iota * 42         // u == 0
    v float64 = iota * 42 // v == 42.0
    w = iota * 42         // w == 84
)

const x = iota // x == 0 (因为iota又被重设为0了)
const y = iota // y == 0 (同上)
```

如果两个const的赋值语句的表达式是一样的，那么可以省略后一个赋值表达式。因此，上面的前两个const语句可简写为：

```
const (       // iota被重设为0
    c0 = iota // c0 == 0
    c1        // c1 == 1
    c2        // c2 == 2
)
const (
    a = 1 <<iota // a == 1 (iota在每个const开头被重设为0)
    b            // b == 2
    c            // c == 4
)
```

## 2.3 枚举

枚举是指一系列相关的常量 。Go语言并不支持众多其他语言明确支持的enum关键字。在 const 后跟一对圆括号的方式定义一组常量，这种定义法在Go语言中通常用于定义枚举值。

比如关于一个星期中每天的定义,下面是一个常规的枚举表示法，其中定义了一系列整型常量：

```
const (
    Sunday = iota
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday
    numberOfDays // 这个常量没有导出
)
```