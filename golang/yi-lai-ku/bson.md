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

