---
title: Go基础
toc: true
tags: Go
category: Go
---

## Go基础

<!--more-->

### 变量

+ 声明

~~~go
var a int     //0值
var s string  //空值
~~~

+ 声明并赋值

~~~go
var a, b int = 3, 4
var s string = "abc"
~~~

+ 省略类型声明

~~~go
var a, b, c, s = 3, 4, true, "def"
~~~

+ 省略var关键字

~~~go
a, b, c, s := 3, 4, true, "def"
~~~

+ 声明多个变量

~~~go
var (
	aa = 3
	ss = "kkk"
	bb = true
)
~~~

+ 常量

~~~go
const (
		filename = "abc.txt"
		a, b     = 3, 4
)
~~~

+ 枚举类型

~~~go
const (
		cpp = iota   //0
		_            //跳过1
		python			 //2
		golang       //3
		javascript   //4
)
~~~

+ 枚举

~~~go
const (
		b = 1 << (10 * iota)
		kb
		mb
		gb
		tb
		pb
)
~~~

----

### if和switch语句

+ 条件没有括号
+ 赋值可放到if里面

~~~go
if contents, err := ioutil.ReadFile(filename); err != nil {
		fmt.Println(err)
} else {
		fmt.Printf("%s\n", contents)
}
~~~



+ 可省略条件

~~~go
func grade(score int) string {
	g := ""
	switch {
	case score < 0 || score > 100:
		panic(fmt.Sprintf(
			"Wrong score: %d", score))
	case score < 60:
		g = "F"
	case score < 80:
		g = "C"
	case score < 90:
		g = "B"
	case score <= 100:
		g = "A"
	}
	return g
}
~~~



----

### 循环

+ 省略初始条件

~~~go
for ; n > 0; n /= 2 {
		lsb := n % 2
		result = strconv.Itoa(lsb) + result
}
~~~

+ 省略初始和递增条件

~~~go
for scanner.Scan() {
		fmt.Println(scanner.Text())
}
~~~

+ 省略所有，死循环

~~~go
for {
		fmt.Println("abc")
}
~~~



----

### 函数

- 返回值在后面

- 可以有多个返回值

~~~go
func div(a, b int) (q, r int) {
	return a / b, a % b
}
~~~

+ 可变长参数

~~~go
func sum(numbers ...int) int {
	s := 0
	for i := range numbers {
		s += numbers[i]
	}
	return s
}
~~~

+ 传递函数

~~~go
func apply(op func(int, int) int, a, b int) int {
	p := reflect.ValueOf(op).Pointer()
	opName := runtime.FuncForPC(p).Name()
	fmt.Printf("Calling function %s with args "+
		"(%d, %d)\n", opName, a, b)

	return op(a, b)
}
~~~



----

### 数组

~~~go
//声明
var arr1 [5]int
//声明并赋值
arr2 := [3]int{1, 3, 5}
//自动确定大小
arr3 := [...]int{2, 4, 6, 8, 10}
//二维数组
var grid [4][5]int
~~~

+ 遍历数组

~~~go
for i, v := range arr {
		fmt.Println(i, v)
}
~~~



----

### 切片

~~~go
arr := [...]int{0, 1, 2, 3, 4, 5, 6, 7}
//切片
arr[2:6]
arr[:6]
arr[2:]
//切片声明
var s []int    //是nil
//生成切片
s2 := make([]int, 16)     //长度
s3 := make([]int, 10, 32) //长度，容量
//切片长度 和 容量
len(s1), cap(s1)
//切片增加元素
s3 := append(s2, 10)
~~~



----

### map

+ 声明

~~~go
//声明并赋值
m := map[string]string{
		"name":    "ccmouse",
		"course":  "golang",
		"site":    "imooc",
		"quality": "notbad",
}
~~~

+ make

~~~go
m2 := make(map[string]int) // m2 == empty map

var m3 map[string]int // m3 == nil
~~~



