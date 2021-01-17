# 定义User表

在`models`目录下新建文件 `base_user.go`

```go
package models

import (
	"time"
	"github.com/beego/beego/v2/client/orm"
)

//定义表结构
type BaseUser struct {
	Id 			int
	Name 		string		`orm:"description(姓名)"`
	Birthday 	time.Time	`orm:"description(生日)"`
	Sex 		int			`orm:"default(1);description(性别)"`
	Avatar 		string		`orm:"description(头像)"`
	Phone 		int			`orm:"description(手机号&账号)"`
	Password 	string		`orm:"description(登录密码)"`
}

//重写映射表名称
func (db *BaseUser) TableName() string {
	return "base_user"
}

func init() {
	// 注册定义的model
	orm.RegisterModel(new(BaseUser))
}
```

因为在 `main.go`中配置了自动建表，所有`bee run`后数据库中会生成对象表。

![](../../.gitbook/assets/image%20%288%29.png)

