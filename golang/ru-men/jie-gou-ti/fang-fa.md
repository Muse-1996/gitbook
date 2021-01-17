# 方法

Go语言中的方法（Method）是一种作用于特定类型变量的函数。这种特定类型变量叫做接收器（Receiver）。

如果将特定类型理解为结构体或“类”时，接收器的概念就类似于其他语言中的this或者self。

Go语言建立的“接收器”强调方法的作用对象是接收器，也就是类实例，而函数没有作用对象。

### 为结构体添加方法

#### 面向过程实现方法

```go
package main

import "fmt"

type Bag struct {
	items []int
}

//将一个物品放入背包
func setStToBag(b *Bag,item int)  {
	b.items = append(b.items,item)
}

func main() {
	//面向过程实现方法
	bag := new(Bag)
	setStToBag(bag,1)
	fmt.Println(bag)	//&{[1]}
	setStToBag(bag,2)
	fmt.Println(bag)	//&{[1 2]}
}

```

#### Go语言的结构体方法

```go
package main

import "fmt"

//为结构体添加方法

type Bag struct {
	items []int
}

//将一个物品放入背包
func setStToBag(b *Bag,item int)  {
	b.items = append(b.items,item)
}

//Go语言的结构体方法
//将一个物品移出
func (b *Bag)delSth(item int){
	index := 0
	for i, k := range b.items {
		if k == item {
			index = i
		}
	}
	b.items = append(b.items[:index],b.items[index+1:]...)
}

func main() {
	//面向过程实现方法
	bag := new(Bag)
	setStToBag(bag,1)
	fmt.Println(bag)	//&{[1]}
	setStToBag(bag,2)
	fmt.Println(bag)	//&{[1 2]}
	//调用结构体方法删除一个元素
	bag.delSth(2)
	fmt.Println(bag)
}

```

![](../../../.gitbook/assets/image%20%287%29.png)

每个方法只能有一个接收器

#### 接收器——方法作用的目标

接收器变量：接收器中的参数变量名在命名时，官方建议使用接收器类型名的第一个小写字母，而不是self、this之类的命名。例如，Socket类型的接收器变量应该命名为s，Connector类型的接收器变量应该命名为c等。

接收器类型：接收器类型和参数类似，可以是指针类型和非指针类型。

方法名、参数列表、返回参数：格式与函数定义一致。

接收器根据接收器的类型可以分为指针接收器、非指针接收器。两种接收器在使用时会产生不同的效果。根据效果的不同，两种接收器会被用于不同性能和功能要求的代码中。

