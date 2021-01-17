---
description: 分支选择（switch）——拥有多个条件分支的判断
---

# Switch

在Go语言中的switch，不仅可以基于常量进行判断，还可以基于表达式进行判断。

#### 基本写法

```go
package main

import "fmt"

func main() {
	str := "A"

	switch str {
	case "A":
		fmt.Println("is A")
	case "B":
		fmt.Println("is B")
	default:
		fmt.Println("unknow")
	}
}

```

#### 一分支多值

```go
str2 := "A"
switch str2 {
case "A","C":
	fmt.Println("is ok")
default:
	fmt.Println("unknow")
}
```

#### 分支表达式

```go
var r int = 8
switch {
case r>5 && r<10:
	fmt.Println("is ok")
default:
	fmt.Println("err num")
}
```

#### 跨越case的fallthrough——兼容C语言的case设计

在Go语言中case是一个独立的代码块，执行完毕后不会像C语言那样紧接着下一个case执行。但是为了兼容一些移植代码，依然加入了fallthrough关键字来实现这一功能。

```go
str3 := "hello"

switch {
case str3 == "hello":
	fmt.Println("is true")
	fallthrough
case str3 != "world":
	fmt.Println("is true too")
}
```

