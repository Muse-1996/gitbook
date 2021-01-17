# 新建项目

```text
    flutter create components
```

1.  使用vscode打开项目
2. PC 连接手机 可以直接连接着数据线进行开发，也可以使用adb连接

```bash
# wifi adb 查看设备列表

$ adb devices

# muserdeMacBook-Pro:Flutter muser$ adb devices
# List of devices attached
# fd01d3a6	device

$ adb tcpip 5555

#restarting in TCP mode port: 5555

# 手机和PC在同一局域网下，在手机上查看IP地址

$ adb connect 192.168.1.100:5555

# connected to 192.168.1.100:5555
# 连接成功
```

 3. 运行

```bash
flutter run
```

最后会在手机自动安装并且打开APP，显示自带的示例内容

