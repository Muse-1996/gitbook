# break

break语句可以结束for、switch和select的代码块。break语句还可以在语句后面添加标签，表示退出某个标签对应的代码块，标签要求必须定义在对应的for、switch和select的代码块上。

```go
package main

import "fmt"

func main() {
	testForBlock:
		for i:=0;i<10;i++{
			for s:=0;s<i;s++ {
				if s==6{
					break testForBlock
				}
				fmt.Printf("s is %d\n",s)
			}
			fmt.Printf("i is %d\n",i)
		}

	fmt.Println("break test over")
}

```

