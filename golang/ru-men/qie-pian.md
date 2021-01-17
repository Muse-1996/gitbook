# 切片

Go语言切片的内部结构包含地址、大小和容量。切片一般用于快速地操作一块数据集合。如果将数据集合比作切糕的话，切片就是你要的“那一块”。切的过程包含从哪里开始（这个就是切片的地址）及切多大（这个就是切片的大小）。容量可以理解为装切片的口袋大小。

声明切片

```go
//var NAME []T

var strSlice []string  //nil
var numSlice []int     // !nil
```

声明但未使用的切片的默认值是nil

#### 从数组或切片生成新的切片

```go
package main

import "fmt"

func main() {
	arr := [6]int{1,2,3,4,5,6}
	fmt.Println(arr[2:4])  //[3,4]
}
```

从数组或切片生成新的切片拥有如下特性:

1. 取出的元素数量为：结束位置-开始位置。
2. 取出元素不包含结束位置对应的索引，切片最后一个元素使用slice\[len\(slice\)\]获取。
3. 当缺省开始位置时，表示从连续区域开头到结束位置。
4. 当缺省结束位置时，表示从开始位置到整个连续区域末尾。
5. 两者同时缺省时，与切片本身等效。
6. 两者同时为0时，等效于空切片，一般用于切片复位。
7. 根据索引位置取切片slice元素值时，取值范围是（0～len\(slice\)-1），超界会报运行时错误。生成切片时，结束位置可以填写len\(slice\)但不会报错。

生成切片的格式中，当开始和结束都范围都被忽略，则生成的切片将表示和原切片一致的切片，并且生成的切片与原切片在数据内容上是一致的

```go
package main

import "fmt"

func main() {

	arr := [6]int{1,2,3,4,5,6}
	fmt.Println(arr[:])  //[1 2 3 4 5 6]
	
}

```

#### 使用make创建切片

```go
//使用make函数构建  make(T,size,cap)
//T：切片的元素类型。
//size：就是为这个类型分配多少个元素。
//cap：预分配的元素数量，这个值设定后不影响size，只是能提前分配空间，降低多次分配空间造成的性能问题。

slice1 := make([]int,2,10)
fmt.Println(slice1)  // [0 0]
```

{% hint style="info" %}
使用make\(\)函数生成的切片一定发生了内存分配操作。

但给定开始与结束位置（包括切片复位）的切片只是将新的切片结构指向已经分配好的内存区域，设定开始与结束位置，不会发生内存分配操作。
{% endhint %}

#### 使用append\(\)函数为切片添加元素

当空间不能容纳足够多的元素时，切片就会进行“扩容”。“扩容”操作往往发生在append\(\)函数调用时。切片在扩容时，容量的扩展规律按容量的2倍数扩充。

```go
//使用make函数构建
slice1 := make([]int,2,10)  //[0 0]
fmt.Println(slice1)
fmt.Printf("cap is %d",cap(slice1))  //cap is 10

slice1 = append(slice1,6,6,6,6,6)
fmt.Println(slice1)  //[0 0 6 6 6 6 6]
//slice1的容量
fmt.Printf("cap is %d",cap(slice1))  //cap is 10

slice1 = append(slice1,6,6,6,6,6)
fmt.Println(slice1)  //[0 0 6 6 6 6 6 6 6 6 6 6]
//slice1的容量
fmt.Printf("cap is %d",cap(slice1))  //cap is 20
```

#### 切片合并

```go
slice2 := []int{8,8,8,8,8,8}
slice1 = append(slice1,slice2...)
fmt.Println(slice1)
```

#### 复制切片元素到另一个切片

```go
resouce := make([]int,10)
for i,_ := range resouce{
	resouce[i] = i+100
}
fmt.Println(resouce)

//赋值操作 指向相同指针
copyResouce := resouce
copyResouce[0] = 666
fmt.Println(copyResouce)
fmt.Println(resouce)

deepCopyResouce := make([]int,10)
//copy操作 内存空间分离
copy(deepCopyResouce,resouce)
fmt.Println(deepCopyResouce)
fmt.Println("------------")
deepCopyResouce[0] = 999
fmt.Println(deepCopyResouce)
fmt.Println(resouce)
```

#### 从切片中删除元素

Go语言中切片删除元素的本质是：以被删除元素为分界点，将前后两个部分的内存重新连接起来。

```go
index := 2
strs := []string{"a","b","c","d","e"}
fmt.Println(strs[:index])
fmt.Println(strs[index+1:])
strs1 := append(strs[:index],strs[index+1:]...)
fmt.Println(strs1)
```

