# strconv包

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	var a int = 10
	var s string = "67"

	//fmt转字符串
	iToStr := fmt.Sprintf("%d",a)
	fmt.Printf("%#v\n",iToStr) //"10"

	//字符串转数字 -> 值 进制 位数bitSize
	i,err := strconv.ParseInt(s,10,64)
	fmt.Println(err)
	fmt.Printf("%#v %T\n",i,i) //67 int64

	//字符串转数字
	i1,_ := strconv.Atoi(s)
	fmt.Printf("%#v %T\n",i1,i1) //67 int

	//数字转字符串
	s1 := strconv.Itoa(a)
	fmt.Printf("%#v %T\n",s1,s1) //"10" string

	b := "true"
	//字符串bool转bool
	b1,_ := strconv.ParseBool(b)
	fmt.Printf("%#v %T\n",b1,b1) //true bool

	b2 := true
	s2 := strconv.FormatBool(b2)
	fmt.Printf("%#v %T\n",s2,s2) //"true" string
}
```

