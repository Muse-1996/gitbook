---
description: 继续下一次循环
---

# continue

continue语句可以结束当前循环，开始下一次的循环迭代过程，仅限在for循环内使用。在continue语句后添加标签时，表示开始标签对应的循环。

```go
package main

import "fmt"

func main() {

	//定义一组map 记录学生分数
	studentMap := make(map[string]int)
	studentMap["xiaoHong"] = 28
	studentMap["xiaoMing"] = 26
	studentMap["liHua"] = 23

	//打个标签
	studentMapLoop:
		for key, _ := range studentMap {
			//给好学生加分 不给差生加分 所以 如果是李华 就直接下一个
			if key == "liHua"{
				continue studentMapLoop
			}else{
				//给学生加分
				studentMap[key] += 20
			}
		}
	//打印分数情况 map[liHua:23 xiaoHong:48 xiaoMing:46]
	fmt.Println(studentMap)
}

```

