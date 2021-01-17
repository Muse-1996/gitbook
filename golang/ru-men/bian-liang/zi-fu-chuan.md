# 字符串

```go
var c string = "中文"
fmt.Printf(c)
```

#### strings.Index 获取字符在字符串中的索引

```go
//获取字符串的某一段字符
	str := "Test String"

	sliceStr := strings.Index(str,"S")

	fmt.Println(sliceStr)  //5
```

#### 字符串切割

```go
cupStr := str[4:]
```

#### 高效的字符串连接

```go
//字符串拼接
	str1 := "abc"
	str2 := "def"
	//声明缓存区
	var stringBuilder bytes.Buffer
	//写入
	stringBuilder.WriteString(str1)
	stringBuilder.WriteString(str2)
	//buffer转字符串输出
	fmt.Println(stringBuilder.String())
```

