# 环境变量配置

### 安装用于加载环境变量的依赖包

```bash
npm i --save @nestjs/config
```

### 修改入口文件

```typescript
// src/app.module.ts
import { Module } from "@nestjs/common";
import { AppController } from "./app.controller";
import { AppService } from "./app.service";
//环境变量读取
import { ConfigModule } from "@nestjs/config";

@Module({
  imports: [ConfigModule.forRoot()],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

上面的代码将从`.env`默认位置（项目根目录）加载并解析一个文件，将文件中的键/值对`.env`与分配给 的环境变量合并`process.env`，并将结果存储在一个私有结构中，您可以通过`ConfigService`. 该`forRoot()`方法注册`ConfigService`提供者，提供者提供`get()`读取这些解析/合并的配置变量的方法。

如果您不想加载`.env`文件，而只想从运行时环境访问环境变量（如 OS shell 导出，如`export DATABASE_USER=test`），请将选项对象的`ignoreEnvFile`属性设置为`true`

```typescript
// 这个配置的使用场景应该是在部署时使用，避免敏感信息暴露在代码包中
ConfigModule.forRoot({
  ignoreEnvFile: true,
});
```

当你想`ConfigModule`在其他模块中使用时，设置全局。

```typescript
// src/main.ts
ConfigModule.forRoot({
  // 一旦它被加载到根模块（例如，）中，您就不需要在其他模块中导入。
  isGlobal: true,
});
```

### 环境变量文件新建

根目录下新建 `.env` 文件

```text
# 运行端口
RUN_AT = 3333
```

### **自定义配置文件**

可以使用自定义配置文件来返回嵌套的配置对象**。**

```typescript
// src/conf/conf.ts
export default () => ({
  port: parseInt(process.env.RUN_AT, 10) || 3000,
  database: {
    host: process.env.MYSQL_HOST,
    port: parseInt(process.env.MYSQL_PORT, 10) || 5432,
  },
});
```

### 载入自定义配置文件

```typescript
// src/app.module.ts

// 自定义配置文件
import Conf from "./conf/conf";
// ...
ConfigModule.forRoot({
    //这个配置的使用场景应该是在部署时使用，避免敏感信息暴露在代码包中,这里先关掉
    ignoreEnvFile: false,
    //载入自定义配置文件 允许您加载多个配置文件
    load: [Conf],
}),
```

### 测试获取环境变量数据

使用vscode的nest插件生成User module目录，插件会自动组织依赖关系，结构如下

src  
--modules  
----user  
------user.controller.ts  
------user.service.ts  
------user.module.ts

```typescript
// user.controller.ts

import { Get } from "@nestjs/common";
import { Controller } from "@nestjs/common";
import { ConfigService } from "@nestjs/config";

@Controller("/user")
export class UserController {
  constructor(private configService: ConfigService) {}
  
  // 测试获取环境变量
  @Get("load_env")
  loadEnvData() {
    return {
      port: this.configService.get("port"),
      db: this.configService.get("database"),
    };
  }
}
```

### 测试结果

![](../../.gitbook/assets/image%20%2837%29.png)

