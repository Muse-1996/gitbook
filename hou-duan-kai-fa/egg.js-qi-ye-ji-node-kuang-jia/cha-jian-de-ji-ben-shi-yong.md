# 插件的基本使用

### 基本的插件

1: 在app目录新建文件夹extend

2: 新建context.js文件

```javascript
module.exports = {
    get isIOS(){
        const iosReg = /iphone|ipad|ipod/i;
        return iosReg.test(this.get('user-agent'));
    }
}
```

step3: 在路由处理中使用-app/controller/home.js

```javascript
  async testPul(){
    const { ctx } = this;
    ctx.body = ctx.isIOS;
  }
```

### 插件自建

1: 新建目录 app-/lib/plugin/egg-ua/app/extend/context.js

```javascript
module.exports = {
    get isIOS(){
        const iosReg = /iphone|ipad|ipod/i;
        return iosReg.test(this.get('user-agent'));bb
    }
}
```

2.在lib/plugin/egg-ua/package声明插件

```javascript
{
  "eggPlugin":{
    "name":"ua"
  }
}
```

3.在config/plugin中通过path挂载插件

```javascript
const path  = require('path')
exports.ua = {
  enable:true,
  path:path.join(__dirname,'../lib/plugin/egg-ua')
}
```

