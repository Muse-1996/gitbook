# 第一步

```text
flutter create --org com.muse --template=plugin --platforms=android -a java try_pkg
```

新建Java语言安卓插件

**`lib/hello.dart` 文件**  
Dart 插件 API 实现。

**`android/src/main/java/com/example/hello/HelloPlugin.kt` 文件**  
Android 平台原生插件 API 实现（使用 Kotlin 编程语言）。

**`ios/Classes/HelloPlugin.m` 文件**  
iOS 平台原生插件 API 实现（使用 Objective-C 编程语言）。

**`example/` 文件**  
一个依赖于该插件并说明了如何使用它的 Flutter 应用。  


