# v-open 打开新窗口

### 简化打开窗口的操作

```markup
<div v-open="{to:'./demo',param:{code:1}}">打开新窗口</div>
```

| 属性 | 说明 |
| :--- | :--- |
| to | 跳转的文件路径，不需写.html后缀 |
| param | 传递参数至目标页面，在目标页面可通过this.$param获取参数 |



