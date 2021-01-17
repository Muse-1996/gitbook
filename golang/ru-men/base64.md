# Base64

```go
import (
	"encoding/base64"
	"fmt"
)

//...
	
	
	str := "this is a string"
	//编码
	baseStr := base64.StdEncoding.EncodeToString([]byte(str))
	fmt.Println(baseStr)
	//解码
	valStrBytes,_ := base64.StdEncoding.DecodeString(baseStr)
	fmt.Println(string(valStrBytes))  //this is ...
	fmt.Println(valStrBytes) //字节码
```

