# Node.js开发杂记

#### 最简单创建node服务的写法

```javascript
var http = require('http')
http.createServer(function(req,res){
  res.writeHead(200,{'Content-Type':'text/plain'})
  res.end('hello')
}).listen(1337,'127.0.0.1')
```

#### \_\_diename是使用该全局变量的绝对路径，而process.cwd是运行脚本进程的绝对路径。

#### path.join\(\)可以生成带有有效斜线语法的路径

```javascript
require(path.join(__dirname,,"routes","messages"))
```



