# 函数基本概念

#### 普通函数声明

Go语言的函数声明以func标识，后面紧接着函数名、参数列表、返回参数列表及函数体。

```go
func FuncName (Arguments) (ReturnData){
    FuncBody
}
```

#### 返回同一种类型

```go
package main

import "fmt"

func returnTwoType()(int,int){
	return 1,2
}

func main() {

	a,b := returnTwoType()

	fmt.Println(a,b)
}

```

{% hint style="warning" %}
纯类型的返回值对于代码可读性不是很友好，特别是在同类型的返回值出现时，无法区分每个返回参数的意义。
{% endhint %}

#### 带有变量名的返回值

Go语言支持对返回值进行命名，这样返回值就和参数一样拥有参数变量名和类型。

命名的返回值变量的默认值为类型的默认值，即数值为0，字符串为空字符串，布尔为false、指针为nil等。

```go
package main

import "fmt"

func namedValue()(a,b int){
	a = 10
	b = 11
	return a,b
}

func main() {

	val1,val2 := namedValue()

	fmt.Println(val1,val2)

}

```

#### 函数中的参数传递

Go语言中传入和返回参数在调用和返回时都使用值传递，这里需要注意的是指针、切片和map等引用型对象指向的内容在参数传递中不会发生复制，而是将指针进行复制，类似于创建一次引用。类似于JS中的浅拷贝。

