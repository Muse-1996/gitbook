---
description: 能看懂就知道可以用在哪里
---

# 扩展的基本使用

### 目录新建

```javascript
{app}/extend/helper.js
```

### 扩展编写

```javascript
//日期格式化
const sd = require('silly-datetime');

module.exports = {
    //时间格式化
    async formatTime(param, format) {
        return await sd.format(new Date(param), format || 'YYYY-MM-DD HH:mm')
    },

    //获取随机数
    async getRandom(min, max) {
        return parseInt(min + (Math.random() * (max - min + 1)));
    },
}
```

### 使用方法

```javascript
this.ctx.helper.formatTime(Date.now())
```

