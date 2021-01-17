# Express Node框架

### 安装Express生成器

```bash
 npm install express-generator -g
```

### 生成项目

```bash
 express myappName #创建项目

 cd myappName  #进入项目目录

 npm install  #安装依赖

 npm start  #启动服务
```

### nodemon express的热重启

安装nodemon

```bash
npm install -g nodemon
```

配置文件

```javascript
//项目目录下创建nodemon.json
{    
    "restartable": "rs",    
    "ignore": [        
        ".git",        
        ".svn",        
        "node_modules/**/node_modules"    
    ],    
    "verbose": true,    
    "execMap": {        
        "js": "node --harmony"    
    },    
    "watch": [     ],
    "env": {        
        "NODE_ENV": "development"    
    },    
    "ext": "js json"
}
```

注释app.js最后一行

启动 nodemon app.js

