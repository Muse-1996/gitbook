---
description: Go语言中的所有循环类型均可以使用for关键字来完成。
---

# 循环

初始语句是在第一次循环前执行的语句，一般使用初始语句执行变量初始化，如果变量在此处被声明，其作用域将被局限在这个for的范畴内。

```go
for 初始语句;条件表达式;结束语句{
    循环体代码
}
```

for循环可以通过break、goto、return、panic语句强制退出循环。

{% hint style="warning" %}
在结束每次循环前执行的语句，如果循环被break、goto、return、panic等语句强制退出，结束语句不会被执行。
{% endhint %}

```go
package main

import "fmt"

func main() {
	sum := 0
	for i:=0;i<10;i++ {
		sum += i
	}
	fmt.Println(sum)

	sum2 := 10
	for ;sum2<100;{
		sum2+=10
	}
	fmt.Println(sum2)

}

```

#### 结束循环时带可执行语句的无限循环

```go
var i int
for ; ; i++{
    if i>10 {
        break
    }
}
```

#### 无限循环

上面的代码还可以改写为更美观的写法

```go
var i int
for {
    if i>10 {
        break
    }
    i++
}
```

#### 只有一个循环条件的循环

```go
i := 0

for i<=10 {
    i++
}
```

#### 九九乘法表

```go
package main

import "fmt"

func main() {
	for i:= 1;i<=9;i++{
		for s:=1;s<=i;s++{
			fmt.Printf("%d*%d=%d ",s,i,i*s)
		}
		fmt.Println()
	}
}
```

