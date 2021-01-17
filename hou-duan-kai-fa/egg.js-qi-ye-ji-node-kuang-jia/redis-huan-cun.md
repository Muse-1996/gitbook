# Redis缓存

1.插件安装

```text
cnpm install egg-redis --save
```

2. 启用插件

```text
# plugin.js

redis : {
    enable: true,
    package: 'egg-redis',
}
```

3.连接库

```text
# config.default.js

config.redis = {
    client: {
        port: 6379, // Redis port
        host: 'xxx.xxx.xxx.xxx', // Redis host
        password: '********',
        db: 0,
    },
}
```

