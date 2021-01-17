# 数据表操作

#### 新建表

create table 表名\(字段名1 字段类型,....字段名n 字段类型n\);

```sql
create table test_user(
    name varchar(10),
    phone int(11)
);
```

#### 新建表时指定表引擎和字符集

```sql
create table test_user(
    name varchar(10),
    phone int(11)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

#### 查看表结构

```sql
desc test_user;
```

#### 修改表名

```sql
alter table user rename db_user;
```

#### 删除表

```sql
drop test_user;
```

