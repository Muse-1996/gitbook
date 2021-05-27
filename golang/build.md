# Build

Mac下打包Linux可执行文件

```bash
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go
```

