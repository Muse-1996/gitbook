# 类型内嵌和结构体内嵌

结构体允许其成员字段在声明时没有字段名而只有类型，这种形式的字段被称为类型内嵌或匿名字段。

```go
package main

import "fmt"

type Test struct {
	int
	bool
	string
}

func main() {
	test := Test{
		10,  //实际上 是 int:10
		false,
		"asas",
	}

	fmt.Println(test)
}

```

#### 声明结构体内嵌

```go
package main

import "fmt"

type BasicColor struct {
	R,G,B float32
}

type Colors struct {
//结构体内嵌
	BasicColor
	Alpha float32
}

func main() {

	//col := new(Color)
	var col Colors
	col.R = 222
	col.G = 223
	col.B = 224
	fmt.Println(col)

	col.Alpha = 2
	fmt.Println(col)
}

```

#### 结构内嵌特性

1. 内嵌的结构体可以直接访问其成员变量
2. 内嵌结构体的字段名是它的类型名

#### 声明

```go
c := Colors{
		BasicColor:BasicColor{
			R:23,
			G:24,
			B:25,
		},
	}
	fmt.Println(c)
```

