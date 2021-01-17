---
description: 中间件是一种很灵活的写法，能适应很多业务场景的需要
---

# 中间件的基本使用

### 新建中间件

```javascript
//{app}/middleware
module.exports = (options, app) => {
    return async function forbidIp(ctx, next) {
        console.log(ctx.request.ip)
        if (ctx.request.ip == options.forbidip) {
            ctx.status = 403;
            ctx.body = "您的ip禁止访问"
        } else {
            await next()
        }
    }
}
```

### 挂载使用

```javascript
//{app}/config/config.default.js

  config.middleware = ['forbidip'];
  config.forbidip = {
    forbidip: ''   // forbidip: '127.0.0.1'
  }
```

