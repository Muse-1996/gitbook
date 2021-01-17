---
description: Go语言的协作程序（goroutine）和普通的协作程序（coroutine）
---

# 协作程序（goroutine）

C\#、Lua、Python语言都支持coroutine特性。coroutine与goroutine在名字上类似，都可以将函数或者语句在独立的环境中运行，但是它们之间有两点不同：

1. goroutine可能发生并行执行；但coroutine始终顺序执行。
2. goroutine间使用channel通信；coroutine使用yield和resume操作。

