# Flutter表单

Flutter表单提交demo

```text
## Form表单处理数据

```Dart

final testKey = GlobalKey<FormState>();
String tel = '';
String pwd = '';



//部件部分
Form(
  key:testKey,
  child:Column(
    children:[
      TextFormField(
        onSaved(value){
          tel = value
        }
      ),
      TextFormField(
        onSaved(value){
          pwd = value
        }
      ),
    ]
  )
)

RaisedButton(
  child:Text('Login'),
  onPressed(){
    testKey.currentState.save();
    print(tel+pwd)
  }
)



```
```

