---
description: 可以快速增删的非连续空间的容器
---

# 列表List

列表是一种非连续存储的容器，由多个节点组成，节点通过一些变量记录彼此之间的关系。列表有多种实现方法，如单链表、双链表等。

### 初始化列表

{% hint style="danger" %}
列表与切片和map不同的是，列表并没有具体元素类型的限制。因此，列表的元素可以是任意类型。这既带来便利，也会引来一些问题。给一个列表放入了非期望类型的值，在取出值后，将interface{}转换为期望类型时将会发生宕机。
{% endhint %}

通过container/list包的New方法初始化list

```go
listOne := list.New()
```

通过声明初始化list

```go
var listTwo list.List
```

#### 在列表中插入元素

双链表支持从队列前方或后方插入元素，分别对应的方法是`Push Front`和`PushBack`。

{% hint style="info" %}
这两个方法都会返回一个_list.Element结构。如果在以后的使用中需要删除插入的元素，则只能通过 \*_list.Element配合Remove\(\)方法进行删除，这种方法可以让删除更加效率化，也是双链表特性之一。
{% endhint %}

```go
var listTwo list.List
//从队列后方插入元素
listTwo.PushBack("a")
//从队列前方插入元素
listTwo.PushFront("b")
```

#### 从列表中删除元素

{% hint style="info" %}
列表的插入函数的返回值会提供一个\*list.Element结构，这个结构记录着列表元素的值及和其他节点之间的关系等信息。从列表中删除元素时，需要用到这个结构进行快速删除。
{% endhint %}

```go
node := listTwo.PushBack("X")
listTwo.InsertAfter("XX",node)
listTwo.InsertBefore("XXX",node)

listTwo.Remove(node)
```

#### 遍历列表

```go
//遍历列表
	for i:=listTwo.Front();i!=nil;i=i.Next() {
		fmt.Println(i) //&{0xc0000902a0 0xc0000901e0 0xc000090180 XXX}
		fmt.Println(i.Value)  //XXX
	}
```

