# 函数变量

```go
package main

import "fmt"

func testFn ()(int){
	return 1
}
func main() {
	f := testFn
	a := f()
	fmt.Println(a)
}

```

