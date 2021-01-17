# 数据字段操作

#### 修改数据表字段类型

```sql
alter table user modify name varchar(20);
```

#### 增加表字段\(first/after\)

```sql
alter table user add column sex int(2);
```

```sql
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| name  | varchar(20) | YES  |     | NULL    |       |
| phone | int         | YES  |     | NULL    |       |
| sex   | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
```

#### 在指定位置插入新字段\(first/after\)

```sql
alter table user add column password varchar(16) AFTER phone;
```

```sql
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| name     | varchar(20) | YES  |     | NULL    |       |
| phone    | int         | YES  |     | NULL    |       |
| password | varchar(16) | YES  |     | NULL    |       |
| sex      | int         | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
```

#### 删除表字段

```sql
alter table user drop column sex;
```

#### 表字段改名\(first/after\)

```sql
alter table user change name username varchar(8);
```

```sql
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| username | varchar(8)  | YES  |     | NULL    |       |
| phone    | int         | YES  |     | NULL    |       |
| password | varchar(16) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
```

