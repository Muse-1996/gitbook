---
description: 接口定义了对象的行为
---

# 接口interface

接口本身是调用方和实现方均需要遵守的一种协议，大家按照统一的方法命名参数类型和数量来协调逻辑处理的过程。

Go语言中使用组合实现对象特性的描述。对象的内部使用结构体内嵌组合对象应该具有的特性，对外通过接口暴露能使用的特性。

非侵入式设计是Go语言设计师经过多年的大项目经验总结出来的设计之道。只有让接口和实现者真正解耦，编译速度才能真正提高，项目之间的耦合度也会降低不少。

接口是双方约定的一种合作协议。接口实现者不需要关心接口会被怎样使用，调用者也不需要关心接口的实现细节。接口是一种类型，也是一种抽象结构，不会暴露所含数据的格式、类型及结构。

