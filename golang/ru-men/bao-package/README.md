# 包Package

Go语言的包与文件夹一一对应，所有与包相关的操作，必须依赖于工作目录（GOPATH）。

GOPATH是Go语言中使用的一个环境变量，它使用绝对路径提供项目的工作目录。

#### 使用命令行查看GOPATH信息

```bash

musedeMacBook-Pro:paks muse$ go env  #输出当前Go开发包的环境变量状态

GO111MODULE=""
GOARCH="amd64"  #GOARCH表示目标处理器架构
GOBIN=""
GOCACHE="/Users/muse/Library/Caches/go-build"
GOENV="/Users/muse/Library/Application Support/go/env"
GOEXE=""
GOFLAGS=""
GOHOSTARCH="amd64"
GOHOSTOS="darwin"
GOINSECURE=""
GONOPROXY=""
GONOSUMDB=""
GOOS="darwin"
GOPATH="/Users/muse/go"
GOPRIVATE=""
GOPROXY="https://proxy.golang.org,direct"
GOROOT="/usr/local/go"  #Go开发包的安装目录
GOSUMDB="sum.golang.org"
GOTMPDIR=""
GOTOOLDIR="/usr/local/go/pkg/tool/darwin_amd64"
GCCGO="gccgo"
AR="ar"
CC="clang"
CXX="clang++"
CGO_ENABLED="1"
GOMOD=""
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
GOGCCFLAGS="-fPIC -m64 -pthread -fno-caret-diagnostics -Qunused-arguments -fmessage-length=0 -fdebug-prefix-map=/var/folders/l7/_z5r85yd1r54fp7ypm4glslm0000gn/T/go-build504826898=/tmp/go-build -gno-record-gcc-switches -fno-common"
```

