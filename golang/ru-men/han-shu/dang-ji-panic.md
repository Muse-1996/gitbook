---
description: 程序终止运行
---

# 宕机panic

#### 手动触发宕机

Go语言可以在程序中手动触发宕机，让程序崩溃，这样开发者可以及时地发现错误，同时减少可能的损失。

Go语言程序在宕机时，会将堆栈和goroutine信息输出到控制台，所以宕机也可以方便地知晓发生错误的位置。

```go
package main

func main() {
	panic("crash")
}
```

错误信息

```text
panic: crash

goroutine 1 [running]:
main.main()
        /Users/muse/StudyWork/Go/studyAgain/panic.go:4 +0x39

Process finished with exit code 2

```

#### 在宕机时触发延迟执行语句

```go
package main

import "fmt"

func main() {
	defer fmt.Println("宕机了啊")
	defer fmt.Println("可咋整啊")
	panic("crash")
}
```

错误信息

```text
可咋整啊
宕机了啊
panic: crash

goroutine 1 [running]:
main.main()
        /Users/muse/StudyWork/Go/studyAgain/panic.go:8 +0xdb

Process finished with exit code 2

```

宕机前，defer语句会优先被执行，这个看起来就很秀了。

