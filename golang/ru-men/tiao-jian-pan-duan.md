# 条件判断

基本和其他语言的判断写法一致

```go
package main

import "fmt"

func main() {
	a := 12
	if a<10 {
		a+=3
	}else{
		a+=6
	}
	fmt.Println(a)
}

```

if还有一种特殊的写法，可以在if表达式之前添加一个执行语句，再根据变量值进行判断

```go
package main

import "fmt"

func sumNum(x,y int)int{
	return x+y
}

func main() {
	if count:=sumNum(6,5);count>10{
		fmt.Println("大于10")
	}else{
		fmt.Println("小于10")
	}
}

```

