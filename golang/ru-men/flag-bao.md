---
description: 获取命令行参数
---

# flag包

```go
package main

import (
	"flag"
	"fmt"
)

//表示要获取命令行中的port参数 参数类型是字符串类型 默认值是:8080 描述是http service port
var addr = flag.String("port",":8080","http service port")
var env = flag.String("env","develop","run at env")
func main() {
	flag.Parse()
	//因为返回的是指针地址 需要通过*取值
	fmt.Println(*addr)
	fmt.Println(*env)
}
```

build出可执行文件后加参数运行

![](../../.gitbook/assets/image%20%2826%29.png)

目前来看可以用于线上环境设定，或者做一些小的命令行工具也可以。

