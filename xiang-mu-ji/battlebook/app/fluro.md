---
description: 路由管理
---

# fluro

新建Routes目录，并新建三个文件

![](../../../.gitbook/assets/image%20%2811%29.png)

#### application.dart

```dart
import 'package:fluro/fluro.dart';

class Application {
  static FluroRouter router;
}

```

#### route\_handlers.dart

```dart
import 'package:flutter/material.dart';
import 'package:fluro/fluro.dart';
import "../pages/login.dart";

var rootHandler = Handler(
    handlerFunc: (BuildContext context, Map<String, List<String>> params) {
  return Login();
});

var loginRouteHandler = Handler(
  handlerFunc: (context, parameters) {
    return Login();
  },
);

```

#### routes.dart

```dart
import 'package:fluro/fluro.dart';
import 'package:flutter/material.dart';
import './route_handlers.dart';

class Routes {
  static void configureRoutes(FluroRouter router) {
    router.notFoundHandler = Handler(
      handlerFunc: (BuildContext context, Map<String, List<String>> params) {
        print("ROUTE WAS NOT FOUND !!!");
      },
    );
    router.define("/", handler: rootHandler);
    router.define(
      "/login",
      handler: loginRouteHandler,
      transitionType: TransitionType.inFromLeft,
    );
  }
}

```

#### 使用

```dart
import 'package:battle_book_app/pages/login.dart';
import 'package:battle_book_app/pages/single_login.dart';
import 'package:flutter/material.dart';
import 'uitl/main.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';
import 'package:fluro/fluro.dart';
import './routes/application.dart';
import './routes/routes.dart';

void main() {
  final router = FluroRouter();
  Routes.configureRoutes(router);
  Application.router = router;
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return ScreenUtilInit(
      designSize: Size(DEVICE_SCREEN_HEIGHT, DEVICE_SCREEN_HEIGHT),
      allowFontScaling: false,
      child: MaterialApp(
        debugShowCheckedModeBanner: false,
        title: 'Flutter Demo',
        theme: BASE_THEAM_DATA,
        onGenerateRoute: Application.router.generator,
      ),
    );
  }
}

```

