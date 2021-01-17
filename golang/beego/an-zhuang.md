# 安装&升级

#### 安装

```bash
go get github.com/beego/beego/v2
```

#### 升级

```text
go get -u github.com/beego/beego/v2
```

#### 秀一脸的安装

需要安装两个东西

```bash
#beego 是一个快速开发 Go 应用的 HTTP 框架
go get github.com/beego/beego/v2
#bee 工具是一个为了协助快速开发 beego 项目而创建的项目，
#通过 bee 您可以很容易的进行 beego 项目的创建、热编译、开发、测试、和部署。
go get -u github.com/beego/bee/v2
```

在安装过程中，本以为在Mac上应该是行云流水的操作，但是

```bash
muserdeMacBook-Pro:pakOne muse$ go get -u github.com/beego/beego/v2
package github.com/beego/beego/v2: cannot find package "github.com/beego/beego/v2" in any of:
	/usr/local/go/src/github.com/beego/beego/v2 (from $GOROOT)
	/Users/muse/go/src/github.com/beego/beego/v2 (from $GOPATH)
```

难道是我的大陆局域网下不了？祭出登云梯后还是不行，异常依旧。

当时就上头了，赶忙看一眼官方文档，并没有什么解释，难道是环境变量问题？果断打开`.bash_profile`

先是一手环境变量配置，不过我感觉跟这个应该没什么关系，因为命令行可以直接调起go的

```text
export GOPATH=/Users/muse/go
export PATH=$GOPATH/bin:$PATH
```

配置完之后，自然是传统的重载一下

```text
source ./.bash_profile
```

报错依旧，当时就懵逼了，果断开启面向搜索引擎搭建开发环境模式，很快啊，一记输入，一记搜索，找到个这么个东西

`go mod 可以通过GO111MODULE来控制是否启用，GO111MODULE有一下三种类型。`

* `on 所有的构建，都使用Module机制`
* `off 所有的构建，都不使用Module机制，而是使用GOPATH和Vendor`
* `auto 在GOPATH下的工程，不使用Module机制，不在GOPATH下的工程使用`

当时就裂开了，怎么官方文档没说这东西

重新打开配置文件，新增一行，看这`GO111MODULE`也是懵的一匹

```text
export GO111MODULE=on
```

之后重载配置，接着下载就正常了，秀到了

