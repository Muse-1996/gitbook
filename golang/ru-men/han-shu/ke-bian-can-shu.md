---
description: 参数数量不固定的函数形式
---

# 可变参数

Go语言支持可变参数特性，函数声明和调用时没有固定数量的参数，同时也提供了一套方法进行可变参数的多级传递。特性如下：

1. 可变参数一般被放置在函数列表的末尾，前面是固定参数列表，当没有固定参数时，所有变量就将是可变参数。
2. v为可变参数变量，类型为\[\]T，也就是拥有多个T元素的T类型切片，v和T之间由“...”即3个点组成。
3. T为可变参数的类型，当T为interface{}时，传入的可以是任意类型。

```go
package main

import "fmt"

//可变参数 a为确定传参[string] str为不确定传参[string]
func magicString(a string,str ...string)(string){
	fmt.Println(a) //I
	fmt.Println(str) //[like Golang] 由此可见非固定传参是list承载
	s:=a
	//遍历拼接
	for _, v := range str {
		s+=v
	}
	//返回拼接后的结果
	return s
}

func main() {

	oneStr := magicString("I","like","Golang")
	fmt.Println(oneStr) //IlikeGolang
	
}

```

#### 不确定类型的可变参数

当可变参数为interface{}类型时，可以传入任何类型的值。

```go
package main

import "fmt"

//不确定类型的可变参数
func maginFn(args ...interface{}){

	fmt.Println(args) //[a 1 true]
	
	//瞅下类型
	for _, v := range args {
		fmt.Printf("%v 类型是 %T \n",v,v)
	}
	
	//a 类型是 string 
  //1 类型是 int 
  //true 类型是 bool 
	
}

func main() {

	maginFn("a",1,true)
}

```

