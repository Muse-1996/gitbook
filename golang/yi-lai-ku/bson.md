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



