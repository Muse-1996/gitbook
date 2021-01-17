# Dio AJAX

### DIO AJAX

```text
dio: ^2.1.1
```

> 使用 Get

```dart
get(String url) async {
    try {
      var data = {"name": "test"};
      Response response =
          await Dio().get("${this._url}${url}", {queryParameters: data});
      return response.data;
    } catch (e) {
      print(e);
    }
  }
```

> 使用 Post

```dart
post() async {
    var data = {"name": "test"};
    try {
      Response response =
          await Dio().post("${this._url}${url}", {queryParameters: data});
      return data;
    } catch (e) {
      print(e);
    }
  }
```

> 请求头设置

```dart
Dio dio = new Dio();
dio.options.headers = this.headers;
```

> 请求

```dart
Ajax().get('/test').then((data) {
   //
});
```

