# MongoDB - mongoose库

### Mongoose

#### Mongoose连接数据库

```javascript
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');
```

#### 监听连接状态

```javascript
var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  // we're connected!
});
```

#### 定义模型

```javascript
var kittySchema = new mongoose.Schema({
  name: String
});

...


var Kitten = mongoose.model('Kitten', kittySchema);
```

#### 实例方法

```javascript
var animalSchema = new Schema({ name: String, type: String });

animalSchema.methods.findSimilarTypes = function(cb) {
  return this.model('Animal').find({ type: this.type }, cb);
};

var Animal = mongoose.model('Animal', animalSchema);
var dog = new Animal({ type: 'dog' });
dog.findSimilarTypes(function(err, dogs) {
  console.log(dogs); // woof
});
```

> 使用doc.set\(\)设置属性值 =&gt; save\(\)。

#### Population 表关联

```text
var mongoose = require("mongoose")
mongoose.Promise = require("bluebird")
var schema = mongoose.Schema;
var userSchema = new schema({
  name:String,
  age:Number,
  commet:[{
    type:schema.Types.ObjectId,
    ref:"Comments"
  }]
})
var User = mongoose.model("Users",userSchema)

var commentSchema = new schema({
  title:String,
  content:String,
  author:{
    type:schema.Types.ObjectId,
    ref:"Users"
  }
})

var Comment = mongoose.model("Comments",commentSchema)

var tom = new User({name:"tom",age:19})
var pl = new Comment({title:"pl",content:"this is a content"})

tom.save().then(function(user){
  pl.author = user
  return Promise.all([pl.save(),user])
}).spread(function(comment,user){
  user.comment.push(comment)
  return new Promise(function(resolve,reject){
    resolve(user.save())
  })
}).then(function(){
  console.log("成功")
}).catch(function(err){
  console.log(err)
})
```

#### 查询

> Query.populate\(path,\[select\],\[model\],\[match\],\[options\]\)

select:要查询的字段 model:类型Model,可选，指定关键字段的model，如果没有指定就会使用Schema的ref match:Object,指定附加的查询条件 options:Object,指定附加的其他查询选项，如排序以及条数限制等等

```text
User.find({name:"tom"}).populate("comment").exec(function(err,result){
  console.log(result[0].comment[0])
})
```

```text
$or　　　　或关系
$nor　　　　或关系取反
$gt　　　　大于
$gte　　　　大于等于
$lt　　　　小于
$lte　　　　小于等于
$ne　　　　不等于
$in　　　　在多个值范围内
$nin　　　　不在多个值范围内
$all　　　　匹配数组中多个值
$regex　　　　正则，用于模糊查询
$size　　　　匹配数组大小
$maxDistance　　　　范围查询，距离（基于LBS）
$mod　　　　取模运算
$near　　　　邻域查询，查询附近的位置（基于LBS）
$exists　　　　字段是否存在
$elemMatch　　　　匹配内数组内的元素
$within　　　　范围查询（基于LBS）
$box　　　　范围查询，矩形范围（基于LBS）
$center　　　　范围醒询，圆形范围（基于LBS）
$centerSphere　　　　范围查询，球形范围（基于LBS）
$slice　　　　查询字段集合中的元素（比如从第几个之后，第N到第M个元素
```

**如要查询阅读量大于300小于400的文章**

```text
Article.find({views : {$gte : 300 , $lte : 400}})
```

findById 用来通过id查询单条文档

> Model.findById\(id, \[fields\], \[options\], \[callback\]\)

#### 模糊查询

```text
User.find({'user':{$regex:/w/g}}, function(err, res){
    if (err) {
        console.log("Error:" + err);
    }
    else {
        console.log("Res:" + res);
    }
})
```

#### 更新

语法Model.update\(conditions, update, \[options\], \[callback\]\)

`$set` 指定字段的值，这个字段不存在就创建它。可以是任何MondoDB支持的类型。

> Students.update\({\_id : id}, {$set : {name : "小文"...}}\)

#### 删除

> Model.remove\(conditions, \[callback\]\)

