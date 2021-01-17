# 响应式

在初始化时，通过defineProperty进行绑定，设置通知机制

当编译生成的渲染函数被实际渲染的时候，会触发getter进行依赖收集，在数据变化时，通过setter进行更新。

### 响应式原理 defineProperty

示例

```markup
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <p id="name"></p>
    </div>
</body>
<script>
    var obj = {};
    Object.defineProperty(obj, 'name', {
        get() {
            return document.querySelector('#name').innerHTML;
        },
        set(newVal) {
            document.querySelector('#name').innerHTML = newVal;
        }
    });
    obj.name = "hello"
</script>

</html>
```

更像是一个对象管家的角色，主要进行数据劫持再处理。如果调用obj.name实际是调用了get函数，而obj.name="hello"实际是调用了set函数，能够对对象进行更好的数据管控。

