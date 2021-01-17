# brew & Nginx

### Nginx

1.检测brew升级

```text
brew update
```

2.查询nginx是否存在

```text
brew search nginx
```

3.安装nginx

```text
brew install nginx
```

4.查看nginx目录

```text
open /usr/local/etc/nginx/
```

5.查看nginx安装目录

```text
open /usr/local/Cellar/nginx
```

6.启动nginx

```text
nginx
```

7.访问验证

```text
localhost:8080
```

8.nginx配置文件

```text
cat /usr/local/etc/nginx/nginx.conf
```

9.关闭nginx

```text
nginx -s quit/stop
```

10.nginx重启

```text
nginx -s reload
```

