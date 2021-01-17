# ListView Builder

### ListView Builder 循环

```dart
import 'package:flutter/material.dart';
import 'res/listData.dart';

void main(List<String> args) {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Flutter Demo List')),
        body: HomeContent(),
      ),
    );
  }
}

class HomeContent extends StatelessWidget {
  //创建HomeContent的构造函数
  List list = new List();
  HomeContent() {
    for (var i = 0; i < 20; i++) {
      list.add('我是第${i}个数据');
    }
  }

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return ListView.builder(
      itemCount: this.list.length,
      itemBuilder: (context, index) {
        return ListTile(
          title: Text(this.list[index]),
        );
      },
    );
  }
}
```

