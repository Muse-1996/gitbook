# 创建插件

```dart
flutter create --org com.example --template=plugin your_plugin_name

# 支持swift kotlin

flutter create --template=plugin -i swift -a kotlin your_plugin_name
```

Flutter 1.20.0 版本

使用 `--platforms=` 这个选项，后面参数是用逗号分隔的列表，这个参数代表指定插件支持的平台。可用的平台有：`android`、`ios`、`web`、`linux`、`macos` 和`windows`。如果没有指定平台，则生成的项目不支持任何平台。

使用 `--org` 选项，以反向域名表示法来指定你的组织。该值用于生成的 Android 及 iOS 代码。  
使用 `-a` 选项指定 Android 的语言，或使用 `-i` 选项指定 iOS 的语言。

示例：

```bash
flutter create --org com.example --template=plugin --platforms=android,ios -a kotlin hello
```

```bash
flutter create --org com.example --template=plugin --platforms=android,ios -a java hello
```

```bash
flutter create --org com.example --template=plugin --platforms=android,ios -i objc hello
```

```bash
flutter create --org com.example --template=plugin --platforms=android,ios -i swift hello
```

