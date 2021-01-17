# 映射

Go语言提供的映射关系容器为map。map使用散列表（hash）实现。

{% hint style="info" %}
大多数语言中映射关系容器使用两种算法：散列表和平衡树。

散列表可以简单描述为一个数组（俗称“桶”），数组的每个元素是一个列表。根据散列函数获得每个元素的特征值，将特征值作为映射的键。如果特征值重复，表示元素发生碰撞。碰撞的元素将被放在同一个特征值的列表中进行保存。散列表查找复杂度为O\(1\)，和数组一致。最坏的情况为O\(n\)，n为元素总数。散列需要尽量避免元素碰撞以提高查找效率，这样就需要对“桶”进行扩容，每次扩容，元素需要重新放入桶中，较为耗时。平衡树类似于有父子关系的一棵数据树，每个元素在放入树时，都要与一些节点进行比较。平衡树的查找复杂度始终为O\(log n\)。
{% endhint %}

#### 创建一个map

```go
package main

import "fmt"

func main() {
	mapA := make(map[string]int)
	mapA["key1"]=1
	fmt.Println(mapA)
	fmt.Println(mapA["key1"])
	fmt.Println(mapA["key2"])
}

```

#### 查询某个值是否存在

```go
//查询某个键是否存在
v,ok := mapA["key2"]
fmt.Println(v,ok) //0 false
```

#### 声明时填充内容

```go
mapB := map[string]string{
    "A":"a",
    "B":"b",
    "C":"c",
}

fmt.Println(mapB) //map[A:a B:b C:c]
```

#### 遍历map映射

```go
for k,v:=range mapB{
    fmt.Println(k,v)
}

//A a
//B b
//C c
```

#### 使用delete\(\)函数从map中删除键值对

```go
delete(mapB,"A")
delete(mapB,"F")
fmt.Println(mapB)   //map[B:b C:c]
```

#### 能够在并发环境中使用的map——sync.Map

Go语言中的map在并发情况下，只读是线程安全的，同时读写线程不安全。

两个并发函数不断地对map进行读和写而发生了竞态问题。map内部会对这种并发操作进行检查并提前发现。

sync.Map有以下特性：

1. 无须初始化，直接声明即可。
2. sync.Map不能使用map的方式进行取值和设置等操作，而是使用sync.Map的方法进行调用。Store表示存储，Load表示获取，Delete表示删除。
3. 使用Range配合一个回调函数进行遍历操作，通过回调函数返回内部遍历出来的值。Range参数中的回调函数的返回值功能是：需要继续迭代遍历时，返回true；终止迭代遍历时，返回false。

{% hint style="info" %}
sync.Map没有提供获取map数量的方法，替代方法是获取时遍历自行计算数量。sync.Map为了保证并发安全有一些性能损失，因此在非并发情况下，使用map相比使用sync.Map会有更好的性能。
{% endhint %}

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	var asyncMap sync.Map

	//存 sync.Map将键和值以interface{}类型进行保存
	asyncMap.Store("name","Alice")
	asyncMap.Store("age",1)
	asyncMap.Store("sex","boy")
	fmt.Println(asyncMap)

	//读
	fmt.Println(asyncMap.Load("name"))

	//删
	asyncMap.Delete("name")
	fmt.Println(asyncMap)

	//遍历 每次Range()在遍历一个元素时，都会调用这个匿名函数把结果返回。
	asyncMap.Range(func(key, value interface{}) bool {
		fmt.Println(key,value)
		return true
	})
}

```

