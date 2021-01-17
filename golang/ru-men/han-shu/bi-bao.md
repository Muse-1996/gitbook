---
description: 引用了外部变量的匿名函数，函数+引用环境=闭包
---

# 闭包

闭包是引用了自由变量的函数，被引用的自由变量和函数一同存在，即使已经离开了自由变量的环境也不会被释放或者删除，在闭包中可以继续使用这个自由变量。概念与JavaScript一致。

一个函数类型就像结构体一样，可以被实例化。函数本身不存储任何信息，只有与引用环境结合后形成的闭包才具有“记忆性”。函数是编译期静态的概念，而闭包是运行期动态的概念。

{% hint style="info" %}
闭包（Closure）在某些编程语言中也被称为Lambda表达式。
{% endhint %}

闭包对环境中变量的引用过程，也可以被称为“捕获”，在C++ 11标准中，捕获有两种类型：引用和复制，可以改变引用的原值叫做“引用捕获”，捕获的过程值被复制到闭包中使用叫做“复制捕获”。

#### 在闭包内部修改引用的变量

```go
package main

import "fmt"

func main() {
	str := "Hello"

	changeStr := func (){
		str = "Golang"
	}

	fmt.Println(str)  //Hello

	changeStr()

	fmt.Println(str)  //Golang
}

```

#### 闭包的记忆效应

被捕获到闭包中的变量让闭包本身拥有了记忆效应，闭包中的逻辑可以修改闭包捕获的变量，变量会跟随闭包生命期一直存在，闭包本身就如同变量一样拥有了记忆效应。

```go
package main

import "fmt"

func AccFn(val int)func() int{
	return func() int {
		val++
		return val
	}
}

func main() {
	
	//这一步会将初始值代入内部的匿名函数并返回 后续调用的实际是返回的匿名函数
	accFn := AccFn(1)
	fmt.Println(accFn()) //2
	fmt.Println(accFn()) //3
	
}

```

#### 闭包实现生成器

闭包的记忆效应进程被用于实现类似于JavaScript设计模式中[工厂模式](../../../qian-duan-kai-fa/qian-liao-she-ji-mo-shi.md#gong-chang-mo-shi)的生成器。

```go
package main

import "fmt"

func newPlayer(name string)func()(string,int){
	hp:=100
	return func()(string,int){
		return name,hp
	}
}

func main() {

	player1 := newPlayer("空手接高爆")
	name,hp := player1()
	fmt.Printf("玩家[%v]的血量为%d",name,hp)
	
}

```

