# Dart基础

### 基本写法

```dart
//void 没有返回值
void main() {
  print('Hello Dart & World');

  var Str = 'type String defined';
  String str = 'type strong defined';

  print(Str);
  print(str);
}
```

### 数据类型

```dart
main(List<String> args) {
  //字符串

  var str = 'this is a str';
  String str1 = 'this was a str';

  print(str);
  print(str1);

  var str3 = '''
    1
    2
    3
    4
    5
  ''';
  print(str3);

  print("$str $str1");

  print(str + str1);

  //int double
  int a = 123;
  double b = 12.99;
  double c = 10;
  print(a);
  print(b);
  print(c);
  print(a + b);

  //bool
  var d = true;
  bool e = false;
  print(d);
  print(e);

  //条件
  if (d) {
    print('✔️');
  }

  //list
  var f = ['aaa', 'bbb', 'ccc'];
  print(f);
  print(f[0]);
  print(f.length);

  var f1 = new List();
  f1.add('ppp');
  f1.add('ggg');
  print(f1);

  //list指定类型
  var f2 = new List<String>();

  f2.add('fffff');

  print(f2);

  //Maps {}
  var g = {"name": "Muse", "age": 12};
  print(g);
  print(g["name"]);

  var g1 = new Map();
  g1["name"] = "Defer";
  print(g1);

  print(g1 is String);
  print(g1 is Map);
}
```

### 运算符、类型转换

```dart
main(List<String> args) {
  var a = 123.123;
  var b = 4;
  print(a ~/ b);

  //??= 如果没有值就赋值
  var c = '18';
  c ??= '12';
  print(c);

  var d = 123;
  d.toString();
  print(d);

  var e = '123';
  int.parse(e);
  print(e);

  //判断字符串是否为空
  print(e.isEmpty);
}
```

### List/set/map

```dart
main(List<String> args) {
  var a = new List();
  List b = ['a', 'b', 'c'];

  print(b.length);

  //判断为空或者不为空
  print(a.isEmpty);
  print(a.isNotEmpty);

  //翻转倒序排序
  print(b.reversed);
  print(b.reversed.toList());

  // 方法
  a.add('123');
  print(a);
  a.addAll(['aaa', 'bbb']);
  print(a);
  print(a.indexOf('aaa'));
  print(a.indexOf('vvv'));
  a.remove('bbb');
  print(a);

  a.addAll(['fff', 'ggg', 'hhh']);
  print(a);
  a.removeAt(1);
  print(a);

  a.fillRange(0, 2, 'aaa');
  print(a);

  a.insert(1, 'nnnnn');
  print(a);

  var f = 'aaaaa';
  print(f.split(''));
  print(a.join('-'));

  //不能添加重复的数据
  var c = new Set();
  c.add('a');
  c.add('a');
  c.add('b');
  print(c);

  //去重操作
  c.addAll(a);
  print(c);

  var r = {"name": 'Muse', "age": 12, "sex": "nan"};
  print(r.keys);
  print(r.values.toList());

  //查看映射Map里的值  返回true false
  print(r.containsValue(12));
  print(r.containsKey("age"));

  var list = [1, 2, 3, 4, 5];
  list.forEach((value) {
    print(value);
  });

  // var list2 = new List();
  var list2 = list.map((value) {
    return value * 2;
  });
  print(list2);

  var list3 = list.where((value) {
    return value > 2;
  });
  print(list3);

  var list4 = list.any((value) {
    return value > 4;
  });
  print(list4);
}
```

### Function

```dart
main(List<String> args) {
  printTest();

  var a = testFun2();
  print(a);

  var b = testNum();
  print(b);
}

void printTest() {
  print('Im a test func');
}

testFun2() {
  return '99999';
}

int testNum() {
  return 111;
}

```

### 对象、类

```dart
main(List<String> args) {
  Person a = new Person.now();
  a.talk();
  print(a.age);
  var b = new DateTime.now();
  print(b);
}

class Person {
  String name = "aaa";
  int age = 12;
  void talk() {
    print('hello ' + this.name);
  }

  //构造函数
  Person() {
    print('类实例化自动触发');
  }

  Person.now() {
    print(new DateTime.now());
  }
}
```

### 抽象类

```dart
main(List<String> args) {
  Dog pop = new Dog();
  pop.eat();
}

//抽象类
abstract class Animal {
  eat(); //抽象方法  约束子类必须有这个方法
}

class Dog extends Animal {
  @override
  eat() {
    // TODO: implement eat
    print('this dog eatting role');
    return null;
  }
}

```

