---
description: 匿名函数经常被用于实现回调函数、闭包等。
---

# 匿名函数

匿名函数的定义就是没有名字的普通函数定义。

#### 在定义时调用匿名函数

相当于JavaScript中自执行函数的写法

```go
package main

import "fmt"

func main() {

	func(i int){
		fmt.Println(i)
	}(1)
	
}

```

#### 将匿名函数赋值给变量

```go
package main

import "fmt"

func main() {
	func(i int){
		fmt.Println(i)
	}(1)

	fn := func(i int){
		fmt.Println(i)
	}
	fn(1)
}

```

