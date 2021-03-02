# 微前端QianKun

#### Vue子应用配置

1. 新建Vue项目

```text
vue create control-center-spa
```

2. 在src下新建 `public_path.js` 

```javascript
if (window.__POWERED_BY_QIANKUN__) {
  __webpack_public_path__ = window.__INJECTED_PUBLIC_PATH_BY_QIANKUN__;
}
```

{% hint style="danger" %}
这里会报错，意思大概是\_\_**webpack\_public\_path\_\_**未定义
{% endhint %}

3. 解决_`__webpack_public_path__`_作用域问题

```javascript
//根目录下新建 .eslintrc.js
module.exports = {
    root: true,
    env: {
        node: true
    },
    globals: {
        "__webpack_public_path__": "writable"
    },
}
```

4. 修改`router/inde.js`

```javascript
let router = new VueRouter({
    base: window.__POWERED_BY_QIANKUN__ ? process.env.VUE_APP_QIANKUN_BASE : process.env.BASE_URL,
    mode: "history",
    routes
});
```

5. 修改`main.js`

```javascript
require("./public-path")
import Vue from "vue";
import App from "./App.vue";
import router from "./router";
import store from "./store";
Vue.config.productionTip = false;

let instance = null;

function render(props = {}) {
    const { container } = props;
    instance = new Vue({
        router,
        store,
        render: h => h(App)
    }).$mount(container ? container.querySelector("#app") : "#app");
}
// 独立运行时
if (!window.__POWERED_BY_QIANKUN__) {
    render();
}
export async function bootstrap() {
    console.log("[vue] vue app bootstraped");
}
export async function mount(props) {
    console.log("[vue] props from main framework", props);
    render(props);
}
export async function unmount() {
    instance.$destroy();
    instance.$el.innerHTML = "";
    instance = null;
    // router = null;
}
```

