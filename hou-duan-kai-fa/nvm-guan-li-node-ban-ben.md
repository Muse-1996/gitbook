# NVM管理node版本

### 安装nvm\(安装前需卸载安装过的node以及依赖\)

```text
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash

source ~/.bashrc
```

### 常用的nvm操作

```text
nvm list 查看所有的node版本

nvm install stable # 安装最新稳定版 node，现在是 5.0.0

nvm install 4.2.2 # 安装 4.2.2 版本

nvm install 0.12.7 # 安装 0.12.7 版本

nvm use 4 # 切换至 4.2.2 版本

nvm use 0 # 切换至 0.12.7 版本

nvm alias default 0.12.7 #设置默认 node 版本为 0.12.7

nvm current #查看当前版本显示

nvm uninstall v6.6.0 #删除指定版本 node

nvm use 4.2.2 #切换到 4.2.2：

nvm use 4.2  #切换到最新的 `4.2.x`

nvm use node  #切换到最新版

nvm alias awesome-version 4.2.2  #给 4.2.2 这个版本号起了一个名字叫做 awesome-version
nvm use awesome-version

nvm unalias awesome-version  #取消别名

nvm ls #列出已安装实例

```

