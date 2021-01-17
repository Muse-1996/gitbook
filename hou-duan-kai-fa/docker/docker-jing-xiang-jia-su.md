# Docker镜像加速

查看docker信息

```text
docker info
```

![](../../.gitbook/assets/image%20%2810%29.png)

```text
{
  "debug": true,
  "experimental": false,
  "registry-mirrors": [
    "https://reg-mirror.qiniu.com/"
  ]
}
```

执行docker info

```text
#出现该属性则配置成功
Registry Mirrors:
  https://reg-mirror.qiniu.com/
```

