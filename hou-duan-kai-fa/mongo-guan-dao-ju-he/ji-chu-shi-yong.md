# 基础使用

### 表结构

`users`用户表

```javascript
{ 
    "_id" : ObjectId("609e468709a4967e9e3c16e0"), 
    "userName" : "Alice", 
    "token" : null, 
    "avatar" : ""
}
```

`im_relation_ask`好友申请表

```javascript
{ 
    "_id" : ObjectId("60b2f740f02694d3cd7b4dce"), 
    "fromUserId" : ObjectId("609e468709a4967e9e3c16e0"), 
    "toUserId" : ObjectId("609e468709a4967e9e3c16e0"), 
    "remark" : "加一下呗", 
    "pass" : NumberInt(0), 
    "passTime" : NumberLong(0), 
    "createTime" : NumberLong(1622341440868)
}
```

1. 查找用户

![](../../.gitbook/assets/image%20%2834%29.png)

    2. 数据聚合

![](../../.gitbook/assets/image%20%2836%29.png)

    3. 数据拆分

![](../../.gitbook/assets/image%20%2831%29.png)

    4. 数据处理

![](../../.gitbook/assets/image%20%2832%29.png)

