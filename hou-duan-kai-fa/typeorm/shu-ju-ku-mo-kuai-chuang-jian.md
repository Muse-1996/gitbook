# 数据库模块创建

{% tabs %}
{% tab title="src/database/database.module.ts" %}
```typescript
import { Module } from "@nestjs/common";
import { MySqlProviders } from "./mysql.providers";

@Module({
  imports: [],
  controllers: [],
  providers: [...MySqlProviders],
  exports: [...MySqlProviders],
})
export class DatabaseModule {}
```
{% endtab %}
{% endtabs %}

