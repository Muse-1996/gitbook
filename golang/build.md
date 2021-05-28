# Build

### Mac下打包Linux可执行文件

```bash
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go
```

### Mac下打包Windows可执行文件

```bash
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
```

### Windows下打包Mac可执行文件

```bash
SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=amd64
go build main.go
```

### Windows下打包Linux可执行文件

```bash
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build main.go
```

