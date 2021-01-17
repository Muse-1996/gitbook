# 作死秀

### Mac 安装Flutter IOS相关内容权限问题

作死详情：设置根目录全部文件权限为777

作死结果：管理员账号无权操作硬盘，应用程序异常，获取不到管理员的权限

解决：

```text
// Mac恢复默认权限

chflags -R nouchg ~
diskutil resetUserPermissions / `id -u`
```

