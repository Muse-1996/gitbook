# Python基础

#### Hello Python

```text
#!/usr/bin/env python3
#第一行可以在Mac和Linux直接运行

print('hello python')

# 注释

'''
多
行
注
释
'''

if True:
	print('true')
else:
	print('false')
```

#### 获取控制台输入内容

```text
name = input("what is your name?")
print("hello "+name+"!")
```

#### 判断某元素是否在数组中

```text
array = ['hello','hi','bay']

print('hi' in array)

print('sorry' in array)

str = 'muse'

print('m' in str)
print('b' in str)
print('M' in str)
```

#### 数组常用操作

```text
testList = list('hello')
print(testList)

testList[0] = 'x'
print(testList)

del testList[1]
print(testList)

# 切片赋值
testList[2:] = 'a'
print(testList)

testList[2:] = list('defer')
print(testList)


# push
testList2 = [1,2,3,4,5,6,7]
testList2.append(8)
print(testList2)

# clear
testList2.clear()
print(testList2)

# copy
a1 = [1,2,3]
b1 = a1
print(a1)
print(b1)
a1[0] = 0
print(a1)
print(b1)

a2 = [5,6,7]
b2 = a2.copy()
print(a2)
print(b2)
a2[0] = 9
print(a2)
print(b2)

# count 查看元素在列表中出现了多少次
longList = [1,1,1,3,3,55,888,888,888,888,00,99,87,5,6,4,5]
countOne = longList.count(888)
print(countOne)

# extend 扩展序列
listOne = [1,2,3]
listTwo = [7,8,9]
listOne.extend(listTwo)
print(listOne)

# index 索引 类似js的indexOf
listThree = list('Muser')
print(listThree.index('e'))

# insert 插入
listFour = [1,2,3,4]
listFour.insert(2,'Defer')
print(listFour)

# pop 删除一个元素
listFive = [1,2,3,4,5,6,7]
delOne = listFive.pop()
print(delOne)
print(listFive)

delTwo = listFive.pop(0)
print(delTwo)
print(listFive)

# remove 删除序列中的一个元素
print('remove')
listSix = [1,2,3,4,5,6]
listSix.remove(1)
print(listSix)

# reverse 倒序序列
listSenve = [1,2,3,4,5,6]
listSenve.reverse()
print(listSenve)


# sort 排序
listEight = list('182734596')
print('sort',listEight)
# listEight.sort()
listEightBack = sorted(listEight)
print(listEight)
print(listEightBack)
```

#### 字符串常用方法

```text
# # 转换说明符
# format = "hello,%s. %s enough for ya?"
# values = ('world','Hot')
# print(format % values)


from string import Template
format2 = Template("name is $name,age is $old")
print(format2.substitute(name="Defer",old=18))


print("{},{},or{}".format("1","2","3"))
print("{3},{1},or{2}".format("6","7","8","9"))

from math import pi
print("{name} is approximetely {value:.10f}".format(value=pi,name="?"))


print("{pi!s}".format(pi="π"),'π!r','π!a')

print("{test:10.2f}".format(test = 9999.999999))

print("{:,}".format(10**100))

print("{:$>15}".format('dis'))
print("{0:$>15}".format('dis'))

print("Defer".center(20,"="))

print("hello".find('o'))

seq = "haha","heihei","hehe","xixi"
print('/'.join(seq))

Ustr = "HEllO WorLd"
print(Ustr.lower())

Tstr = "will be ok"
print(Tstr.replace('ok','right'))

Sstr = "1,2,3,4,5"
print(Sstr.split(','))

Pstr = "        here is some space   !****      "
print(Pstr.strip())
print(Pstr.strip(' *!'))

# Translate
table = str.maketrans('u','0')
# 替换
print(table)
print("Muse".translate(table))
# 第三个参数是删除
table = str.maketrans('u','0','e')
print("Muse".translate(table))

#################################################

s1 = '\'hello, world!\''
s2 = '\n\\hello, world!\\\n'
print(s1, s2, end='')

str1 = 'hello, world!'
# 通过内置函数len计算字符串的长度
print(len(str1)) # 13
# 获得字符串首字母大写的拷贝
print(str1.capitalize()) # Hello, world!
# 获得字符串每个单词首字母大写的拷贝
print(str1.title()) # Hello, World!
# 获得字符串变大写后的拷贝
print(str1.upper()) # HELLO, WORLD!
# 从字符串中查找子串所在位置
print(str1.find('or')) # 8
print(str1.find('shit')) # -1
# 与find类似但找不到子串时会引发异常
# print(str1.index('or'))
# print(str1.index('shit'))
# 检查字符串是否以指定的字符串开头
print(str1.startswith('He')) # False
print(str1.startswith('hel')) # True
# 检查字符串是否以指定的字符串结尾
print(str1.endswith('!')) # True
# 将字符串以指定的宽度居中并在两侧填充指定的字符
print(str1.center(50, '*'))
# 将字符串以指定的宽度靠右放置左侧填充指定的字符
print(str1.rjust(50, ' '))
str2 = 'abc123456'
# 检查字符串是否由数字构成
print(str2.isdigit())  # False
# 检查字符串是否以字母构成
print(str2.isalpha())  # False
# 检查字符串是否以数字和字母构成
print(str2.isalnum())  # True
str3 = '  jackfrued@126.com '
print(str3)
# 获得字符串修剪左右两侧空格之后的拷贝
print(str3.strip())
```

#### 字典

```text
# 类似于JSON 键值对
maps = {'a':1,'b':2,'c':3}
print(maps['a'])

# nameArr = ('Muse','Defer','Alex')
# agesArr = (10,11,12)
# # soltArr = dict([nameArr,agesArr])
# items = [('Muse','Defer','Alex'),(10,11,12)]
# soltArr = dict(items)
# print(soltArr)
# print(soltArr['Defer'])

soltArr = [('muse',10),('defer',11),('shut',12)]
items1 = dict(soltArr)
print(items1)
print(items1['defer'])

soltArr2 = dict(name='pink',old=20)
print(soltArr2)
print(soltArr2['old'])

# 类似于HTML的渲染模板 format_map
testData = {'title':'一个标题','text':'Hello Python!!!','author':'Muse'}
template = '''
<html>
    <head>
        <title>{title}</title>
    </head>
    <body>
        <h1>{text}</h1>
        <small>{author}</small>
    <body>
</html>
'''
print(template.format_map(testData))

oked = testData.clear()
print(testData)
print(oked)


# copy 浅复制  deepcopy 深复制

#fromkeys 创建一个字典  包含指定的键 每个键的对应值都是none
print({}.fromkeys(['name','age']))
print({}.fromkeys(['name','age'],'default'))
print({}.fromkeys(['name','age'],["666","777"]))
print({}.fromkeys(['name','age'],("666","777")))

# get
dis = {'age':20}
# print(dis['name'])   error:(most recent call last):
print(dis.get('name'))  # None
print(dis.get('age'))
print(dis.get('name','defer'))  # 如果找不到匹配项返回的默认值

# items  映射
soltArr3 = {'name':'Muse','sex':'man','age':24}
it = soltArr3.items()
print(it)
print(len(it))
print(('age',24) in it)
print('age' in it) # False

# setdefault
soltArr4 = {'age':24}
print(soltArr4.setdefault('name','Muse'))
print(soltArr4.setdefault('name','Muse'))
print(soltArr4.setdefault('age',999))

# update 用一个字典更新另一个字典
soltArr5 = {
    'title':'Python aaaa',
    'created':'2019'
}
soltArr6 = {'created':'2020'}
soltArr5.update(soltArr6)
print(soltArr5)

print(soltArr5.keys())
print(soltArr5.values())

a,b,*solt = [1,2,3,4,5]
print(a,b,solt)

print(ord('😊'))

print('a'<'b') #字符串是根据字符的字母排列顺序做比较的

print('a'<'B')

print('A'<'B')

def runBth(a,b):
    if a.lower() < b.lower():
        print(1)
        return 'true'
    else:
        print(2)
        return 'false'

print(runBth('c','b'))

name = ['muse','defer','alex']
age = [10,11,12]
print(zip(name,age))
print(list(zip(name,age)))
```

#### 时间

```text
import os
import time

def main():
	content = '会挽雕弓如满月…………'
	while True:
		# 清理屏幕上的输出
		os.system('cls')  # os.system('clear')
		print(content)
		# 休眠200毫秒
		time.sleep(0.2)
		content = content[1:] + content[0]

if __name__ == '__main__':
	main()
```

#### 面向对象

```text
#类和类之间的关系有三种：is-a、has-a和use-a关系。
class Mode():
	#限定类可以扩展的属性
	#__slots__ = ('name','age')
	
	#定义类的方法
	@classmethod
	def init(cls):
		return cls("John","20")
		
	#静态方法
	def sum(a,b):
		return a+b	
	
	def __init__(self,name,age):
		self.name = name
		self.age = age
	def changeName(self,name):
		self.name = name
	def out(self):
		print(self.name+'今年'+self.age+'岁')

mode = Mode("BOB","12")
mode.out()
mode.changeName("Spider")
mode.out()
#mode.sex = "man"
#print(mode.sex)

mode1 = Mode.init()
mode1.out()

i = Mode.sum(2,3)
print(i)

class Person():
	def __init__(self,name):
		self.name = name
	def talk(slef):
		print('kkkkkkkkkkkkkkkkkkkkk')
#继承
class Student(Person):
	def __init__(self,name,book):
		super().__init__(name)
		self.book = book
	def study(self):
		print(self.name+'正在读'+self.book)

bob = Student("Pach", "History")
bob.study()
bob.talk()
```

#### File基本操作

```text
f = None
try:
	f = open('test.txt','r',encoding = 'utf-8')
	print(f.read())
except FileNotFoundError:
	print('==FileNotFoundError==')
finally:
	if f:
		f.close()
		
#print(f.read())
#f.close()
```

#### request

```text
import requests
#创建请求类  变量作用域   -》代码块
class Ajax():
	#构造类 为提高效率 初始化时定义好默认headers 避免重复设置
	def __init__(self,url,h={'passportId':'2f6174e21b4beb8b55afa12ee'}):
		self.headers = h
		self._url = url
		self.res = ''
	#get请求方法
	def get(self,url,data={}):
		#直接自动获取实例化类时传入的请求头
		_r = requests.get(self._url+url,headers = self.headers,params=data)
		_r.json()
		self.res = _r.text
#		return _r.text
	#post请求方法
	def post(self,url,data={}):
		_r = requests.post(self._url+url,headers = self.headers,json=data)
		_r.json()
		return _r.text

#实例化数据 可传headers 如果不传 则使用默认请求头
req = Ajax('http://39.107.87.000:20010/')
#发起get请求
#result1 = req.get("web/tenant-grant/details",{"tenantId":"d2fc4fe3ab9754a1f1fcf40a"})
req.get("web/tenant-grant/details",{"tenantId":"d2fc4fe3ab9754a1f1fcf40a"})
print(req.res)


```



