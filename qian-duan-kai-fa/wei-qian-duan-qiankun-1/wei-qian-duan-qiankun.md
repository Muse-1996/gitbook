# 子应用配置

#### 1. 新建项目

```text
vue create control-center-spa
```

#### 2. 在src下新建 `public-path.js` 

```javascript
if (window.__POWERED_BY_QIANKUN__) {
  __webpack_public_path__ = window.__INJECTED_PUBLIC_PATH_BY_QIANKUN__;
}
```

{% hint style="danger" %}
这里会报错，意思大概是\_\_**webpack\_public\_path\_\_**未定义
{% endhint %}

#### 3. 解决_`__webpack_public_path__`_作用域问题

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

#### 4. 修改`router/inde.js`

```javascript
let router = new VueRouter({
    base: window.__POWERED_BY_QIANKUN__ ? process.env.VUE_APP_QIANKUN_BASE : process.env.BASE_URL,
    mode: "history",
    routes
});
```

#### 5. 修改`main.js`

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

#### 6. 跨域配置`vue.config.js`

```javascript
const { name } = require("./package");
module.exports = {
    devServer: {
        https: false, //设置前端https进行访问
        headers: {
            "Access-Control-Allow-Origin": "*"
        }
    },
    configureWebpack: {
        output: {
            library: `${name}-[name]`,
            libraryTarget: "umd", // 把微应用打包成 umd 库格式
            jsonpFunction: `webpackJsonp_${name}`
        }
    },
    chainWebpack: config => {
        const imagesRule = config.module.rule('images');
        imagesRule.uses.clear()
        imagesRule.test(/\.(png|jpe?g|gif|webp)(\?.*)?$/)
        imagesRule.use('file-loader')
            .loader('url-loader')
            .options({
                //limit:10000,
                fallback: {
                    loader: 'file-loader',
                    options: {
                        name: 'img/[name].[hash:8].[ext]'
                    }
                }
            })
        const fontsRule = config.module.rule('fonts');
        fontsRule.uses.clear()
        fontsRule.test(/\.(eot|svg|ttf|TTF|woff|woff2?)$/)
        fontsRule.use('file-loader')
            .loader('url-loader')
            .options({
                fallback: {
                    loader: 'file-loader',
                    options: 'fonts/[name].[hash:8].[ext]'
                }
            })
    },
};
```

#### 7. 环境变量配置 避免资源404

```text
# .env.development
NODE_ENV = "development"
VUE_APP_PUBLIC_PATH = "./"
VUE_APP_QIANKUN_BASE = "/ctrl-vue"
```

