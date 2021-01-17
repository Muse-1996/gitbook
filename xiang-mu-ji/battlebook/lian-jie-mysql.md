# 连接MySQL

在 `main.go`中连接数据库

```go
package main

import (
	_ "battle_book/routers"
	//引包
	"github.com/beego/beego/v2/client/orm"
	//引包
	_ "github.com/go-sql-driver/mysql"
	beego "github.com/beego/beego/v2/server/web"
)

func init() {
	//注册
	orm.RegisterDriver("mysql",orm.DRMySQL)
	//获取配置文件的数据库连接
	conn,_ := beego.AppConfig.String("sqlconn")
	//连接数据库
	err := orm.RegisterDataBase("default", "mysql", conn)
	if err!=nil {
		panic(err)
	}
	//自动建表
	err = orm.RunSyncdb("default",false,true)
	if err!=nil {
		panic(err)
	}
}

func main() {
	if beego.BConfig.RunMode == "dev" {
		beego.BConfig.WebConfig.DirectoryIndex = true
		beego.BConfig.WebConfig.StaticDir["/swagger"] = "swagger"
	}
	beego.Run()
}

```



