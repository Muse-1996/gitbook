# 路由

#### /routes/router.go

```go
//引入控制器 使注释路由生效
beego.Include(&BaseController{})
//....
//默认是get请求 会调用对应控制器的Get方法
beego.Router("/", &controllers.MainController{})
//post:PostFn 指定post请求 并指定控制器PostFn方法
beego.Router("/post",&controllers.ResController{},"post:PostFn")
```

#### 通过注释自动生成路由

```go
//在Controller中 使用注释来声明路由 以下注释声明了路径及请求方式

// @router /test [get]
func (c *BaseController) Get() {
	c.Ctx.WriteString("Test API")
}
```

