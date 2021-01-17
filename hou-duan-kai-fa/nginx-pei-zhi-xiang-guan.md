# Nginx 配置相关

#### Nginx启动

```text
[root@LinuxServer sbin]# /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

#### 从容停止

```text
//查看进程号(master)
[root@LinuxServer ~]# ps -ef|grep nginx
//杀死进程
[root@LinuxServer ~]# kill -QUIT 2072
```

#### 验证nginx配置文件是否正确

```text
//进入nginx安装目录sbin下，输入命令

./nginx -t
```

#### 重启

```text
//进入nginx可执行目录sbin下，输入命令

./nginx -s reload
```



