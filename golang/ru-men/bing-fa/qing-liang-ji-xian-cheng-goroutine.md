---
description: 根据需要随时创建的“线程”
---

# 轻量级线程goroutine

goroutine的概念类似于线程，但goroutine由Go程序运行时的调度和管理。

Go程序会智能地将goroutine中的任务合理地分配给每个CPU。

Go程序从main包的main\(\)函数开始，在程序启动时，Go程序就会为main\(\)函数创建一个默认的goroutine。

