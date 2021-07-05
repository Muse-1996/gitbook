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

