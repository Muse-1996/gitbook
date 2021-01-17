# 安装RabbitMQ

镜像搜索

```text
docker search rabbitmq:management
```

镜像拉取

```text
docker pull rabbitmq:management
```

启动

```text
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 docker.io/rabbitmq:management
```

访问

```text
http://localhost:15672/
```

账号密码都为guest

