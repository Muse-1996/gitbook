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
fvm install 2.0.3
```

###  使用版本

```text
fvm use 2.0.3
```

### 给版本设置别名

```bash
fvm alias ${name} 2.0.3
```

### 展示所有版本

```text
fvm list
```

![](../../.gitbook/assets/image%20%2829%29.png)

### 列出已发布的版本

```bash
fvm list-remote all
```

