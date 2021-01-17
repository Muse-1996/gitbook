# 组件概览

### MaterialApp 根

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :---: |
| home | Scaffold | appBar Body | 根 |
| theme | Theme | ThemeData | 设置文本样式 |

### Scaffold

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :---: |
| backgroundColor | Colors | color | 设置背景颜色 |

### ThemeData 主题样式

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :---: |
| primarySwatch | Color | color | 主色调 |
| hignlightColor | Color | color | 按钮按下的背景颜色 |
| splashColor | Color | color | 水波纹颜色 |
| theme | Theme | ThemeData | 设置文本样式 |

### Text 文本部件

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :---: |
| textDirection | TextDirection | ltr | 下划线 |
| style | TextStyle | fontSize fontWeight color | 设置文本样式 |
| style | Theme.of\(context\).textTheme | title subhead | 根据主题风格设置样式 |
| textAlign | TextAlign | ltrb | 文本对齐方式 |
| maxLines | num | num | 文本最大行数 |
| overflow | TextOverflow | ellipsis | 溢出处理方式 |

### RichText

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| text | TextSpan | text style | 富文本内容 |

#### TextSpan

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :---: |
| text | str | str | 文本内容 |
| style | TextStyle | fs | 文本样式 |
| children | TextSpan | textSpan | 子项 |

### Image 图像部件

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :--- |
| network | function | url | 加载远程网络图像 |
| fit | BoxFit | cover | 设置图像填充方式 |
| colorFilter | ColorFilter.mode | color BlendMode | 设置滤镜 |
| alignment | Alignment | topCenter | 设置位置 |
| repeat | ImageRepeat | repeatY | 重复 |

### Icon 图标部件

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :--- |
| Icons | Icon | 主题定义自带的图标 | 设置图标 |
| tooltip | String | 字符串 | 提示语 |
| onPressed | function | fun | 点击触发事件 |
| size | double | 浮点数 | 设置图标大小 |
| color | Color | color | 设置图标颜色 |

### Stack 内容叠加

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| alignment | Alignment | topRight | 设置对齐方式 |

#### Positioned 定位部件

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| child | widget | - | - |
| right/top/bottom/left | dob | 20.0 | - |

### SizedBox 占位块

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| width | SizedBox | double | 设置宽度 |
| height | SizedBox | double | 设置高度 |
| child | Widget | widget | 内容 |
| alignment | Alignment | \(0.0,1.0\) | 内容位置 |

### Center 布局居中部件

### AspectRatio 宽高比

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| child | widget | - | - |
| aspectRatio | 3.0/2.0 | - | 宽高比 |

### ConstrainedBox 限制子部件大小

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| child | widget | - | - |
| constraints | minHeight... | dob | 设置限制 |

### Column 纵向排列

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :--- |
| children | weights | 一个或多个部件 | 设置内容 |
| style | TextStyle | fontSize fontWeight color | 设置文本样式 |

### PageView 页面容器

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :--- |
| children | widget | - | - |
| pageSnapping | boolean | t f | 设置流畅切页 |
| reverse | boolean | t f | 倒序 |
| scrollDirection | Axis.vertical | - | 滑动方向 |
| onPageChange | fn | fn\(page\) | 切换页触发方法 |
| controller | PageController | - | - |

```text
PageController(
  initialPage:1, //初始页
  keepPage:false, //记住当前页
  viewportFraction:1.0 //单个页面屏幕占比
)
```

### AppBar 标题栏部件

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| title | Text | 继承Text | 导航标题 |
| elevation | Doubel | 浮点数 | 阴影效果 |
| leading | - | IconButton | 设置顶部左侧按钮 |
| actions | List | Button | 右侧工具按钮 |

### IconButton 图标按钮

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| title | Text | 继承Text | 导航标题 |
| elevation | Doubel | 浮点数 | 阴影效果 |
| leading | - | IconButton | 设置顶部左侧按钮 |

### ListView 列表布局

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| .builder | function | 继承Text | 创建列表 |
| elevation | Doubel | 浮点数 | 阴影效果 |

### builder - ListView构造方法

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | ---: | :--- |
| itemCount | function | int | 设置列表数量 |
| itemBuilder | function | fun | 构建方法 |

```dart
Widget _listItemBuilder(BuildContext context.index){
  return DataArr[index].key
}
```

### Container 容器

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | ---: | :--- |
| color | Container | color | 设置背景颜色 |
| margin | EdgeInsets | fun | 设置外边距 |
| padding | EdgeInsets | fun | 设置内边距 |
| child | weight | weight | 设置内容 |

### BoxDecoration

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :--- |
| color | Container | color | 设置背景颜色 |
| border | Border | ltrb | 设置边框 |
| borderRadius | BorderRadius | ltrb | Radius.circular（12.0） 圆角 |
| boxShadow | BoxShadow | Arr | 阴影 |
| shape | BoxShape | circle | 设置形状 设置圆形时父级不能设置圆角 |
| gradient | RadiaGradient | colors:\[\] | 径向渐变 |
| gradient | LinerGradient | colors:\[\]、---- | 线性渐变 |
| image | DecorationImage | image | 设置背景图像 |

```text
LinerGradient(
  begin:Alignment.topCenter,
  end:Alignment.bottomCenetr
)
```

#### BoxShadow

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :--- |
| offset | Offset | \(6.0,7.0\) | 阴影偏移 |
| color | color | color | 设置阴影的颜色 |
| blurRadius | dob | 1.0 | 模糊程度 |
| spreadRadius | dob | +-1.0 | 阴影扩散 |

#### Border

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :--- |
| color | color | color | 边框颜色 |
| width | dobb | dobb | 边框宽度 |
| style | BorderStyle | solid | 边框样式 |

### EdgeInsets 设置边距

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :---: |
| all | double | number | 设置四个边的外边距 |
| itemBuilder | function | fun | 构建方法 |

### TabBar tab切换器 【TabBar TabView TabController】

```dart
DefaultTabController(
  length:3,
  child:Scaffold(
    backgroundColor:Colors.grey[100],
    appBar:AppBar(
      title:Text('TEST'),
      bottom:TabBar(
        tabs:<widget>[
          tab(icon:Icon(Icons.menu)),
          tab(icon:Icon(Icons.menu)),
          tab(icon:Icon(Icons.menu))
        ]
      )
    ),
    body:TabBarView(
      children:<widget>[
        Icon(Icons.menu),
        Icon(Icons.menu),
        Icon(Icons.menu)
      ]
    )
  )
)
```

### TabBar tab切换导航

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :--- |
| tabs | Tab | list | 设置tab导航 |
| unselectedLabelColor | Color | color | 未被选择的标签颜色 |
| indicatorColor | Color | color | 指示器的颜色 |
| indicatorSize | ?? | TabBarIndicatorSize.label | 设置指示器宽度 |
| indicatorWeight | Doubel | 浮点数 | 设置指示器大小 |

### 部件溢出 越界

```dart
//滚动容器包裹
SingleChildScrollView{
  child:xxxxxxx;
}
```

### CircleAvatar 设置头像

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| backgroundImage | Image | img | 设置背景图像 |

### Drawer 抽屉 -》Drawer

可以直接跟部件 也可以使用Draw

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| child | widget | any | 内容 |

#### DrawerHeader

抽屉头部

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :--- | :--- |
| child | widget | any | 内容 |
| decoration | BoxDecoration | 样式 | style |

#### UserAccountDrawerHeader 用户相关头部

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :---: |
| accountEmail | Text | text | 用户邮箱 |
| accountName | Text | text | 用户名 |
| currentAccountPicture | CircleAvatar | img | 头像 |
| decoration | Boxdecation | color img | 背景图像//DecorationImage |

#### 打开 关闭 Drawer

```text
Navigator.pop(context);
```

### BottomNavigationBar 底部导航栏

与appbar同级 ! 如果子项大于四个 类型会发生变化 设置type

| 属性名 | 组件类型 | 值 | 作用 |
| :--- | :---: | :---: | :---: |
| bottomNavigationBar | BottomNavigationBar | items | 创建底部导航 |
| items | BootomNavigationBarItem | icon title | 导航子项 |
| type | BottomNavigationBarType | fixed | 设置类型 |
| fixedColor | Color | color | 子项激活状态的颜色 |
| currentIndex | num | index | 默认激活的子项索引 |
| onTap | fn | fn | 子项点击事件 接受一个index |

