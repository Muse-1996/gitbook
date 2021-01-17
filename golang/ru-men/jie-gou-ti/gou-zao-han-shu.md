---
description: 结构体和类型的一系列初始化操作的函数封装
---

# 构造函数

```go
type People struct {
	name string
	child *People
}

func buildStruct(name string) *People{
	user := &People{name:name}
	return user
}
```

