# 整型

#### 整型分为以下两个大类。

1. 按长度分为：int8、int16、int32、int64
2. 对应的无符号整型：uint8、uint16、uint32、uint64

{% hint style="info" %}
uint8就是我们熟知的byte型，int16对应C语言中的short型，int64对应C语言中的long型
{% endhint %}

```go
package main
import (
	"fmt"
)

func main() {
	var a int16 = 10000
	fmt.Printf("%d", a)  //100003.141593
}
```

