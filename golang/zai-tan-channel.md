---
description: 不要通过共享内存来通信，而应该通过通信来共享内存
---

# 再探channel

Go从语言层面保证同一个时间只有一个goroutine能够访问channel里面的数据，为开发者提供了一种优雅简单的工具，所以Go的做法就是使用channel来通信，通过通信来传递内存数据，使得内存数据在不同的goroutine中传递，而不是使用共享内存来通信。

```go
package main

import (
	"fmt"
)

func main() {
	//声明通道
	var c chan int
	fmt.Println(c) //nil
	if c == nil {
		c = make(chan int)
		fmt.Printf("数据类型是： %T, %p\n", c,c)  //chan int  0xc00008c060
	}

	go func() {
		for i:=0;i<10;i++{
			time.Sleep(1*time.Second)
			//将i发送至通道中
			c <- i
		}
		close(c)
	}()

	for{
		//循环接收通道的返回值
		_i,ok := <- c
		fmt.Println(_i,ok)
		//当通道关闭后 跳出循环
		if !ok{
			break
		}
	}
}

```

