---
description: 七牛云开源的Mongo数据库操作库
---

# Qmgo

### 安装

```bash
go get github.com/qiniu/qmgo
```

### 基础封装

```go
package dao

import (
	"context"
	"fmt"
	"github.com/aws/aws-sdk-go/private/protocol"
	"github.com/aws/aws-sdk-go/private/protocol/eventstream"
	"github.com/qiniu/qmgo"
)

type MongoStruct struct {
	Ctx context.Context
	DB *qmgo.Database
	Coll *qmgo.Collection
	Cli *qmgo.QmgoClient
}


// 固定模式
func NewBaseMongo(dbName,colName string) *MongoStruct {
	ctx := context.Background()
	cli, err := qmgo.Open(ctx, &qmgo.Config{Uri: "mongodb://localhost:27017", Database: dbName, Coll: colName})
	if err != nil{
		fmt.Println(err)
		panic(err)
	}
	return &MongoStruct{
		Cli : cli,
		Ctx: ctx,
	}
}

//创建索引
//cli.CreateOneIndex(context.Background(), options.IndexModel{Key: []string{"name"}, Unique: true})
//cli.CreateIndexes(context.Background(), []options.IndexModel{{Key: []string{"id2", "id3"}}})

func (m *MongoStruct) DisConnect() {
	if err := m.Cli.Close(m.Ctx); err != nil {
		panic(err)
	}
}

func (m MongoStruct) InsertOne(doc interface{}) (result *qmgo.InsertOneResult, err error) {
	result, err = m.Cli.InsertOne(m.Ctx, doc)
	return
}

```

### 初始化使用

```go
func main(){
    mdao := dao.NewBaseMongo("poker", "types")
		types := model.Type{
			Name: "类型1",
		}
		//插入一条数据
		res, err := mdao.InsertOne(types)
		fmt.Println(res)
		fmt.Println(err)
}
```

