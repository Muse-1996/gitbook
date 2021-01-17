# goto

快速跳转至指定代码标签位置

```go
package main

import "fmt"

func main() {

	for i:=0;i<100;i++{
		for s:=i;s<5;s++{
			if i==4 {
			//跳转至标签位置
				goto breakPointer
			}
		}
	}
	
	//防止条件不满足时向下执行
	return

	fmt.Println("run here?")
	
	//定义标签
	breakPointer:
		fmt.Println("Go to here")

}

```

其实类似于锚点的感觉，可用于集中处理异常

