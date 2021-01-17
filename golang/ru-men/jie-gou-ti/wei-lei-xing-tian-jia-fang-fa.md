# 为类型添加方法

在Go语言中，使用type关键字可以定义出新的自定义类型。之后就可以为自定义类型添加各种方法。

如同在JavaScript中对Date对象处理\(示例在前端开发-代码片段=日期格式化\)

```go
package main

import "fmt"

type powerInt int

func (m powerInt) isZero()bool{
	return m == 0
}

func main() {
	var num powerInt = 0
	fmt.Println(num.isZero()) //true
	num = 1
	fmt.Println(num.isZero()) //false
}

```

