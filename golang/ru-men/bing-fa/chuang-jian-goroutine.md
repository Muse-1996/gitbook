# 创建goroutine

```go
go函数名( 参数列表 )
```

```go
package main

import (
	"fmt"
	"time"
)

func loopFn (){
	t := 0
	for{
		t++
		fmt.Println("Tick",t)
		time.Sleep(time.Second)
	}
}

func main() {
	go loopFn()

	var str string
	fmt.Scanln(&str)
}

```

