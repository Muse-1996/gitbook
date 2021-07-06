# 身份验证

### 创建authModule

src  
----modules  
--------auth  
------------auth.controller.ts  
------------auth.service.ts  
------------auth.module.ts

> 确保app.module.ts已挂载authModule，且userModel应暴露userService

### 在auth.service.ts中新增用户名和密码验证方法

```typescript
// auth.service.ts
import { Injectable } from "@nestjs/common";
import { UserService } from "../user/user.service";

@Injectable()
export class AuthService {
  constructor(private userService: UserService) {}
  async validateUser(username: string, pass: string): Promise<any> {
    const user = await this.userService.findUserByUserName(username);
    if (user && user.password === pass) {
      const { password, ...result } = user;
      return result;
    }
    return null;
  }
}
```

这里需要实现userService的findUserByUserName方法

```typescript
// user.service.ts
import { Injectable } from "@nestjs/common";

@Injectable()
export class UserService {
  // 通过用户名查找用户
  findUserByUserName(name: string) {
    // 先随便定义一个假数据返回
    return { id: 6, name, password: "12345" };
  }
}
```



