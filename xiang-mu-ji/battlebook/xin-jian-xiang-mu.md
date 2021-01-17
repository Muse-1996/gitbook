# 新建项目

创建beego api项目

```text
beego api battle_book
```

将依赖放置于项目目录

```text
go mod vendor
```

ORM数据库依赖安装

```text
go get github.com/beego/beego/v2/client/orm
go get go get github.com/go-sql-driver/mysql
```

在 `app.conf`中配置数据库地址

```text
appname = battle_book
httpport = 8080
runmode = dev
autorender = false
copyrequestbody = true
EnableDocs = true
sqlconn = root:12345678@tcp(127.0.0.1:3306)/battle_book?charset=utf8&loc=Local

```



