---
description: Nestjs内置了文件上传的方法，Nestjs中通过file-upload可以实现单文件上传，多文件上传
---

# 文件上传

### common模块创建

创建目录

src  
----modules  
--------common  
------------common.controller.ts  
------------common.service.ts  
------------common.module.ts

```typescript
// common.controller.ts
import {
  Body,
  Controller,
  Post,
  UploadedFile,
  UseInterceptors,
} from "@nestjs/common";
import { FileInterceptor } from "@nestjs/platform-express";
import { ApiTags, ApiConsumes, ApiBody, ApiOperation } from "@nestjs/swagger";

@Controller("common")
export class CommonController {
  @ApiTags("common")
  @ApiOperation({ summary: "文件上传" })
  @ApiConsumes("multipart/form-data")
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
  @Post("upload")
  @UseInterceptors(FileInterceptor("file"))
  upload(@UploadedFile() file, @Body() body) {
    console.log(file);
    // TO_DO: upload file to CDN server
    return "上传成功";
  }
}
```

