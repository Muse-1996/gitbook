# Swagger接口文档

### 安装依赖

```text
npm install --save @nestjs/swagger swagger-ui-express
```

### 使用

```typescript
// main.ts

import { NestFactory } from "@nestjs/core";
import { DocumentBuilder, SwaggerModule } from "@nestjs/swagger";
import { AppModule } from "./app.module";

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  //swagger
  const config = new DocumentBuilder()
    .setTitle("Nest GO API Doc")
    .setDescription("硬吃Nest.js")
    .setVersion("1.0")
    .addTag("Tag")
    .build();
  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup("doc", app, document);

  await app.listen(3000);
  console.log(`Application is running on: ${await app.getUrl()}`);
}
bootstrap();

```

这里访问[http://localhost:3000/doc](http://localhost:3000/doc)就可以请求到接口文档了

### 自定义配置

```typescript
// swagger自定义
const custom = {
  customCss: `.swagger-ui .topbar { display: none }
    .swagger-ui .opblock.opblock-get .opblock-summary-method { color: #61affe; background: transparent; } .swagger-ui table tbody tr td:first-of-type {
    min-width: 12em;}`,
  customSiteTitle: "BaseServer接口文档",
  swaggerOptions: {
    persistAuthorization: true,
  },
};
// ... 

//第四个参数传入自定义内容
SwaggerModule.setup("doc", app, document, custom);
```

{% hint style="info" %}
其实这里的document就是json文件
{% endhint %}

### 配置装饰器

swagger的配置装饰器都是以@api开头

1.ApiTags装饰器，让对应的模块分类到对应的标签当中

2. ApiQuery、ApiBody、ApiParam、ApiHeader、ApiHeaders

```text
name: string; // 该数据的名称，比如:id可以写用户id或者id
description?: string; // 简介
required?: boolean; // 是否是必须的
type?: any; // 类型
isArray?: boolean; // 是否是数组
enum?: SwaggerEnumType; // 枚举类型
collectionFormat?: "csv" | "ssv" | "tsv" | "pipes" | "multi";
```

3. ApiHeaders需要的对象只有三个参数

```text
name: string;
description?: string;
required?: boolean;
```

4. dto的参数配置ApiProperty

```typescript
@ApiProperty({
    description: "用户名",
    required: true,
    default: "13800000000",
})
username: string;
```

5. ApiResponse

```typescript
@ApiResponse({ status: 200, description: "状态码" })
```

6. 文件上传的文档

```typescript
@ApiBody({
  schema: {
    type: "object",
    properties: {
      file: {
        type: "string",
        format: "binary",
      },
    },
  },
})
```

