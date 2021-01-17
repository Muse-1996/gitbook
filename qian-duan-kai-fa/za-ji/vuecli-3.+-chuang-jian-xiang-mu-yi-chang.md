# Vue-cli 3.+创建项目异常

最开始以为是国内局域网的问题，后来设置了 .vuerc 的"useTaobaoRegistry":true还是没什么用，科学上网创建项目还是报错

```bash
Unhandled rejection Error: EACCES: permission denied, open '/Users/muser/.npm/_cacache/index-v5/6c/78/0a091ae17635a89c46898ebbfa32872fd8a3aaf189472db67e92bcb7d8e4'

Unhandled rejection Error: EACCES: permission denied, open '/Users/muser/.npm/_cacache/index-v5/b4/9d/5a271b1898a503a6f8a6b2361235fd7539e9ae1aa5622d3e78124d1a0c34'

Unhandled rejection Error: EACCES: permission denied, open '/Users/muser/.npm/_cacache/index-v5/b0/9b/5d6c7d98f25da0e346068f68aa5a6644d5cdc04e020512064a38102875d5'

Unhandled rejection Error: EACCES: permission denied, open '/Users/muser/.npm/_cacache/index-v5/9f/1e/6ed93cb42527eaea422beae9e75ae26fb9bbd4ebdcf2e6b57efc73e49401'
```

解决办法

```bash
sudo chown -R ${用户名} ~/.npm
```

我擦，竟然是个权限问题

