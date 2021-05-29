# 起步

总感觉Go的实例有些晦涩，所以在研究过程中会先揣摩一下`node.js`的用法，然后融会贯通到Go上。

### 安装

```bash
# golang
go get github.com/casbin/casbin/v2

# node.js
npm install casbin --save
```

### 实例化

根据文档来看，要实例化一个Casbin实例，需要两个文件，分别是Model和Adapter，然后会给你一个模板。

```go
// go
import "github.com/casbin/casbin/v2"
e, err := casbin.NewEnforcer("path/to/model.conf", "path/to/policy.csv")
```

```javascript
// node.js
import { newEnforcer } from 'casbin';
const e = await newEnforcer('path/to/model.conf', 'path/to/policy.csv');
```

## 支持的Models <a id="__docusaurus"></a>

1. [**ACL \(Access Control List, 访问控制列表\)**](https://en.wikipedia.org/wiki/Access_control_list)
2. **具有** [**超级用户**](https://en.wikipedia.org/wiki/Superuser) **的 ACL**
3. **没有用户的 ACL**: 对于没有身份验证或用户登录的系统尤其有用。
4. **没有资源的 ACL**: 某些场景可能只针对资源的类型, 而不是单个资源, 诸如 `write-article`, `read-log`等权限。 它不控制对特定文章或日志的访问。
5. [**RBAC \(基于角色的访问控制\)**](https://en.wikipedia.org/wiki/Role-based_access_control)
6. **支持资源角色的RBAC**: 用户和资源可以同时具有角色 \(或组\)。
7. **支持域/租户的RBAC**: 用户可以为不同的域/租户设置不同的角色集。
8. [**ABAC \(基于属性的访问控制\)**](https://en.wikipedia.org/wiki/Attribute-Based_Access_Control): 支持利用`resource.Owner`这种语法糖获取元素的属性。
9. [**RESTful**](https://en.wikipedia.org/wiki/Representational_state_transfer): 支持路径, 如 `/res/*`, `/res/: id` 和 HTTP 方法, 如 `GET`, `POST`, `PUT`, `DELETE`。
10. **拒绝优先**: 支持允许和拒绝授权, 拒绝优先于允许。
11. **优先级**: 策略规则按照先后次序确定优先级，类似于防火墙规则。

开篇跪了啊，这看起来十分晦涩啊，心中不由升起了一丝忌惮。看来不能直接起步了，先补一下基础概念。

