# 结构体&JSON

```go
package main

import (
	"encoding/json"
	"fmt"
)

type JsonMode struct {
	Name string `json:"name"`
	Sex int `json:"sex"`
	Age int `json:"age"`
}

func main() {
	_j := JsonMode{
		Name: "Muse",
		Sex: 1,
		Age:25,
	}
	fmt.Println(_j) //{Muse 1 25}

	bt,err := json.Marshal(_j)
	if err != nil {
		fmt.Println("Error")
		return
	}
	fmt.Println(string(bt))  //{"name":"Muse","sex":1,"age":25}
	
	//反序列化
	S := JsonMode{}
	json.Unmarshal(bt,&S)
	fmt.Println(S)
}
```

