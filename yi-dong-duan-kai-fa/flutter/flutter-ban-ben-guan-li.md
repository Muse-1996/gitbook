# Flutter版本管理

### 安装

```text
brew install fvm
```

### 修改环境变量

![](../../.gitbook/assets/image%20%2828%29.png)

如果之前配置过，需要先关掉之前的flutter环境变量

![](../../.gitbook/assets/image%20%2827%29.png)

### 安装需要的flutter版本

```bash
fvm install - # 安装在项目配置中找到的版本
fvm install { version } - # 安装特定版本 
```

###  使用版本

```text
fvm use 2.0.3
```

### 给版本设置别名

```bash
fvm alias ${name} 2.0.3
```

### 显示有关环境和项目配置的信息

```text
fvm doctor
```

### 展示所有版本

```text
//本地已安装的版本列表
fvm list

//查看所有可供安装的 Flutter SDK 版本。
fvm releases
```

![](../../.gitbook/assets/image%20%2829%29.png)

### 列出已发布的版本

```bash
fvm list-remote all
```

