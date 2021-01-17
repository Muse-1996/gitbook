---
description: for range 直接获得对象的索引和数据
---

# 键值循环

Go语言可以使用for range遍历数组、切片、字符串、map及通道（channel）

通过for range遍历的返回值有一定的规律：

1. 数组、切片、字符串返回索引和值。
2. map返回键和值。
3. 通道（channel）只返回通道内的值。

#### 特点

1. Go语言的for包含初始化语句、条件表达式、结束语句，这3个部分均可缺省。
2. for range支持对数组、切片、字符串、map、通道进行遍历操作。
3. 在需要时，可以使用匿名变量\_对for range的变量进行选取。

#### 遍历数组、切片——获得索引和元素

```go
for key, val := range []int{1,2,3,4} {
		fmt.Printf("key:%d,val:%d\n",key,val)
	}
}

//key:0,val:1
//key:1,val:2
//key:2,val:3
//key:3,val:4
```

#### 遍历字符串——获得字符

```go
str := "Hello"
for i2, i3 := range str {
	fmt.Println(i2,string(i3))
}
```

#### 遍历map——获得map的键和值

```go
mapA := make(map[string]int)
mapA["A"]=1
mapA["B"]=3
mapA["C"]=5
for key, val := range mapA {
	fmt.Println(key,val)
}
```

#### 遍历通道（channel）——接收通道数据

```go
//创建了一个整型类型的通道
c:=make(chan int)
//启动了一个goroutine
go func() {
//往通道中推送数据1、2、3，然后结束并关闭通道
	c<-1
	c<-2
	c<-3
	close(c)
}()
//不断地从通道中取数据，直到通道被关闭
for v := range c {
	fmt.Println(v)
}
```

