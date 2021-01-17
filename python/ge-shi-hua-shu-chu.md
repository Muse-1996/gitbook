# 格式化输出

基本输出格式

```python
print("Muse今天要写代码")
print("Alax今天要吃包子")
print("Pink今天要玩王者")
```

抽取

```python
print("xxxx今天要xxxx")
```

实践

```python
name = input("请输入你的名字")
work = input("请输入你要干什么")

print(name+"今天要"+work)
#注意%左右空格
print("%s今天要%s" % (name,work))

# % 转义
print("%s今天%%dshd" $ (name))
```

| 写法 | 描述 |
| :--- | :--- |
| %s | 字符串、任何内容 |
| %d | 数字 |



