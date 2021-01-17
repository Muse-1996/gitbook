# Vue工作机制

### new Vue\(\) 发生了什么

> Vue初始化

生命周期、事件、props、methods、data、computed、watch...

{% hint style="info" %}
通过Object.defineProperty设置setter和getter，用来实现响应式及依赖收集。
{% endhint %}

> 调用$mount挂载组件

类似于指定Vue在DOM的作用节点

> compile\(\)

生成vdom虚拟节点树

> render fn\(\)

用js执行时间换取dom的时间

> 依赖收集

当数据更新时，寻找对应的dom节点

> watcher 观察者

收集数据变化，并更新dom



