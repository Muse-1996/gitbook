# bson

`D`在顺序很重要的情况下使用

`M`无序。它与D相同，只是它不保持顺序

`A`list

`E`D中的一个元素

`Raw`用于验证和检索字节片中的元素

### BSON ---&gt; M\D的映射关系

| Bson | D or M |
| :--- | :--- |
| int32 | int32 |
| int64 | int64 |
| double | float64 |
| string | string |
| boolean | bool |
| embedded document 内嵌文档 | D-&gt;D M-&gt;M |
| array | A |
| objectId | primitive.ObjectID |
| datetime | primitive.DateTime |
| binary 二进制文件 | primitive.Binary |
| regular expression 正则表达式 | primitive.Regex |
| JavaScript | primitive.JavaScript |
| code with scope 作用域代码 | primitive.CodeWithScope |
| timestamp 时间戳 | primitive.Timestamp |

### D/M ---&gt; BSON的映射关系

| D or M | BSON |
| :--- | :--- |
| time.Time | datetime |
| int8 int16 int32 | int32 |
| 如果在MinInt32-MaxInt32之外 | int64 |
| int64 | int64 |

### 聚合查询

| 操作符 | 作用 |
| :--- | :--- |
| $project | 修改文档的结构，也可以用于创建计算结果以及嵌套文档，处理字段显示 |
| $unwind | 将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值 |
| $match | 过滤数据，只输出符合条件的文档 |
| $limit | 限制MongoDB聚合管道返回的文档数 |
| $skip | 在聚合管道中跳过指定数量的文档 |
| $group | 将集合中的文档分组，可用于统计结果 |
| $sort | 文档排序输出 |
| $sum | 计算总和 |
| $lookup | 对同一数据库中的另一个集合执行左外部联接 |
| $geoNear | 根据与地理空间点的接近程度返回有序的文档流 |

### exp1. ObjectId关联查询

users表结构

```javascript
{ 
    "_id" : ObjectId("60ae246294661c8745d543f5"), 
    "name" : "Muse", 
    "age" : NumberInt(0), 
    "weight" : NumberLong(0), 
    "type" : "60ae246294661c8745d543f3", 
    "tags" : [
        "60af614e57f1b4d73b23aa7e", 
        "60af614457f1b4d73b23aa7d"
    ]
}
```

types表结构

```javascript
{ 
    "_id" : ObjectId("60ae246294661c8745d543f3"), 
    "name" : "类型1"
}
```

Go聚合联表

```go
userDB := dao.NewBaseMongo("demoDB", "users")
defer userDB.DisConnect()


```

### 新增数据

```go
type UserSchema struct {
	Name string `bson:"name"`
	Age int32 `bson:"age"`
	Weight int32 `bson:"weight"`
	Types primitive.ObjectID `bson:"type"`
	Tags []primitive.ObjectID `bson:"tags"`
}

func createOne(){
	userDB := dao.NewBaseMongo("poker", "users")
	defer userDB.DisConnect()
	typeObjId,_ := primitive.ObjectIDFromHex("60ae246294661c8745d543f3")
	tagOneObjId,_ := primitive.ObjectIDFromHex("60af614457f1b4d73b23aa7d")
	tagTwoObjId,_ := primitive.ObjectIDFromHex("60af614e57f1b4d73b23aa7e")
	var tagList []primitive.ObjectID
	s := append(tagList, tagOneObjId,tagTwoObjId)
	fmt.Println(s)
	fmt.Println(tagList)
	newUser := UserSchema{
		Name: "Muse3",
		Age: 18,
		Weight: 50,
		Types: typeObjId,
		Tags: s,
	}
	res,err := userDB.InsertOne(newUser)
	if err == nil{
		fmt.Println(res)
	}
}
```

![](../../.gitbook/assets/image%20%2833%29.png)

### 删除数据

```go
func DeleteOne(){
	userDB := dao.NewBaseMongo("poker", "users")
	defer userDB.DisConnect()
	delObjId,_ := primitive.ObjectIDFromHex("60b2ed30b07b9127c0245efb")
	userDB.Cli.Remove(userDB.Ctx,bson.D{{"_id",delObjId}})
}
```

### 修改数据

```go
func UpdateOne(){
	userDB := dao.NewBaseMongo("poker", "users")
	defer userDB.DisConnect()
	updateObjId,_ := primitive.ObjectIDFromHex("60b28bc0ab26324fdf6c67bc")
	err := userDB.Cli.UpdateOne(userDB.Ctx,bson.M{
		"_id":updateObjId,
	},bson.M{
		"$set":bson.D{
			{"name","Alcie1"},
			{"age",18},
		},
	})
	if err != nil{
		fmt.Println(err)
	}
}
```

### 查找数据

#### 查找单条数据

```go
func FindOne(){
	userDB := dao.NewBaseMongo("poker", "users")
	defer userDB.DisConnect()
	findObjId,_ := primitive.ObjectIDFromHex("60ae246294661c8745d543f5")
	user := UserSchema{}
	userDB.Cli.Find(userDB.Ctx,bson.M{"_id":findObjId}).One(&user)
	fmt.Printf("%+v\n",user)
	fmt.Println("----------------")
}
```

#### 查找指定字段 Select

```go
func FindOne(){
	userDB := dao.NewBaseMongo("poker", "users")
	defer userDB.DisConnect()
	findObjId,_ := primitive.ObjectIDFromHex("60ae246294661c8745d543f5")
	user := UserSchema{}
	userDB.Cli.Find(userDB.Ctx,bson.M{"_id":findObjId}).Select(bson.M{"name":1}).One(&user)
	fmt.Printf("%+v\n",user)
	fmt.Println("----------------")
}
```

