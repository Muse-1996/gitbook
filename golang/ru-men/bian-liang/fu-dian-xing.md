---
description: Go语言支持两种浮点型数：float32和float64。这两种浮点型数据格式遵循IEEE 754标准
---

# 浮点型

1. float32的浮点数的最大范围约为3.4e38，可以使用常量定义：math.Max Float32。
2. float64的浮点数的最大范围约为1.8e308，可以使用一个常量定义：math.MaxFloat64。打印浮点数时，可以使用fmt包配合动词“%f”

```go
package main
import (
	"fmt"
	"math"
)

func main() {
	fmt.Printf("%f\n", math.Pi)	// 按默认宽度和精度输出整型 3.141593
	fmt.Printf("%.2f\n", math.Pi)	//2位精度输出（小数点后的位数） 3.14
}
```

