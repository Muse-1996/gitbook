# 延迟执行语句defer

Go语言的defer语句会将其后面跟随的语句进行延迟处理。在defer归属的函数即将返回时，将延迟处理的语句按defer的逆序进行执行，也就是说，先被defer的语句最后被执行，最后被defer的语句，最先被执行。

这有点压栈，后进先出的感觉了

```go
package main

import "fmt"

//执行结果  a d c b

func main() {
	fmt.Println("a")

	defer fmt.Println("b")

	defer fmt.Println("c")

	fmt.Println("d")
}

```

