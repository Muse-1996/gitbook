# MongoDB数据库

{% hint style="danger" %}
疑似superagent模块阻塞mongoose
{% endhint %}

### 安装Mongoose

```bash
cnpm install egg-mongoose -S
```

### 挂载

```javascript
//{app}/config/plugin.js
exports.mongoose = {
  enable: true,
  package: 'egg-mongoose',
};
```

### 配置

```javascript
config.mongoose = {
    client: {
      //mongodb://username:password@api.yunsinek.cn/service
      url: 'mongodb://db.yunsinek.cn/service',
      options: {}
    },
};
```

### 开发

```javascript
//在{app}新建目录model chart.js
module.exports = app => {
    const mongoose = app.mongoose;
    const Schema = mongoose.Schema;
    const ChartSchema = new Schema({
        //发送者
        from: {
            type: String,
            default: '-'
        },
        //接收者
        to: {
            type: String,
            default: '-'
        },
        //文本内容
        text: {
            type: String,
            default: '-'
        },
        //发送时间
        send_time: {
            type: Number,
            default: 0
        }
    })

    return mongoose.model('Chart', ChartSchema, 'chart');
} 
```

### 使用

```javascript
this.ctx.model.Chart.Chart.create(ajaxData.result.data)
```

操作数据库的方法可参考mongoose。



