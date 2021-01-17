---
description: 预警!不支持win，只能在macOS尝鲜
---

# Flutter桌面端体验篇

> 总体感觉一般，功能上和Electron还差的很远，性能上也不见得多么流畅，各种桌面端的扩展和API几乎没有，目前就是桌面端的壳子套了一个APP这个样子，flutter在桌面端还有很长的路要走。

### 安装环境

```bash
#如果安装过flutter开发环境，前两步可以跳过
flutter channel master
flutter upgrade
flutter config --enable-macos-desktop
```

### 创建项目目录

```bash
mkdir app
cd app
```

### 初始化项目

```bash
flutter create .
```

### 运行项目

```bash
flutter run -d macOS
```

### 构建发行版本

```bash
flutter build macos
```

### 对已有项目封装桌面端

```bash
flutter create .
flutter run -d macOS
```

