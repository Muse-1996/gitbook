# 初始化结构体的成员变量

结构体在实例化时可以直接对成员变量进行初始化。初始化有两种形式：一种是字段“键值对”形式及多个值的列表形式。键值对形式的初始化适合选择性填充字段较多的结构体；多个值的列表形式适合填充字段较少的结构体。

#### 使用“键值对”初始化结构体

```go
type Vertex struct {
	x int
	y int
}

v:=Vertex{3,4}
```

使用键值对填充结构体的例子

```go
type People struct {
	name string
	child *People
}

relation := &People{
	name:"大明",
	child: &People{
		name: "小明",
		child: &People{
			name:"李华",
		},
	},
}
```

实例化结构体时，键可省略

#### 初始化匿名结构体

匿名结构体没有类型名称，无须通过type关键字定义就可以直接使用。

```go
a:=&struct{
    name string
}{
    "小明"
}
```

{% hint style="warning" %}
匿名结构体的类型名是结构体包含字段成员的详细描述。

匿名结构体在使用时需要重新定义，造成大量重复的代码，因此开发中较少使用。
{% endhint %}

