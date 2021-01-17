---
description: 调整并发的运行性能（GOMAXPROCS）
---

# 多核运行

在Go程序运行时（runtime）实现了一个小型的任务调度器。这套调度器的工作原理类似于操作系统调度线程，Go程序调度器可以高效地将CPU资源分配给每一个任务。传统逻辑中，开发者需要维护线程池中线程与CPU核心数量的对应关系。同样的，Go地中也可以通过runtime.GOMAXPROCS\(\)函数做到。

```go
runtime.GOMAXPROCS(CPU数量)
```

1. &lt;1：不修改任何数值。
2. =1：单核心执行。
3. &gt;1：多核并发执行。

#### 获取CPU数量

```go
runtime.NumCPU()
```

#### 满核运行

```go
runtime.GOMAXPROCS(runtime.NumCPU())
```

