# 主应用配置

#### 1. 创建项目

```text
vue create main-spa
```

#### 2. 安装乾坤依赖

```text
cnpm i qiankun -S
```

#### 3. 在src下新建目录apps用于项目的管理调度

#### 4. 在apps下创建子应用配置文件`microApps.js`

```javascript
const microApps = [{
    name: "control-center-spa", //微应用的名称，微应用之间必须确保唯一
    entry: "//localhost:9002", //微应用的入口
    container: "#control-center-viewport", //微应用的容器节点的选择器或者 Element 实例
    activeRule: "/ctrl-vue", //微应用的激活规则
    props: {
        routerBase: "/ctrl-vue"
    }
}];

export default microApps;
```

#### 5. 在apps下创建乾坤主逻辑文件`index.js`

```javascript
import {
    registerMicroApps, //注册子应用
    setDefaultMountApp, //设置默认启动的自应用
    runAfterFirstMounted, //第一个微应用 mount 后需要调用的方法，比如开启一些监控或者埋点脚本
    addGlobalUncaughtErrorHandler, //添加全局的未捕获异常处理器
    start //启动乾坤
    // initGlobalState,         //设置全局变量
    // MicroAppStateActions,  //
} from "qiankun";

import MicroApps from "./microApps";

let QK_START = async function() {
    //注册自应用并绑定生命周期监听
    registerMicroApps(MicroApps, {
        beforeLoad: app => {
            console.log("beforeLoad:" + app.name);
        },
        beforeMount: app => {
            console.log("beforeMount:" + app.name);
        },
        afterMount: app => {
            console.log("afterMount:" + app.name);
        },
        beforeUnmount: app => {
            console.log("beforeUnmount:" + app.name);
        },
        afterUnmount: app => {
            console.log("afterUnmount:" + app.name);
        }
    });

    //设置默认进入的项目
    setDefaultMountApp("/");

    //启动
    start({
        /*
         * 配置为 true 则会在第一个微应用 mount 完成后开始预加载其他微应用的静态资源
         * 配置为 'all' 则主应用 start 后即开始预加载所有微应用静态资源
         * 配置为 string[] 则会在第一个微应用 mounted 后开始加载数组内的微应用资源
         * 配置为 function 则可完全自定义应用的资源加载时机 (首屏应用及次屏应用)
         */
        prefetch: true, //是否开启预加载
        sandbox: true, //是否开启沙箱 确保单实例场景子应用之间的样式隔离，但是无法确保主应用跟子应用、或者多实例场景的子应用样式隔离。
        singular: true //是否为单实例场景，单实例指的是同一时间只会渲染一个微应用
    });

    runAfterFirstMounted(() => {
        console.log("the first app was mounted!");
    });

    addGlobalUncaughtErrorHandler(event => console.log(event));
}

export default QK_START
```

#### 6. 启动微前端

```javascript
//main.js

import Vue from "vue";
import App from "./App.vue";
import router from "./router";
import store from "./store";

import QK_START from "./apps/index"

Vue.config.productionTip = false;

new Vue({
    router,
    store,
    render: h => h(App)
}).$mount("#app");

QK_START()
```

#### 7. 根据第4步的container配置新建dom容器用于挂载子应用

```text
# app.vue

<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/ctrl-vue/">SubVue</router-link>
    </div>
    <router-view />
    <div id="controller-center-viewport"></div>
  </div>
</template>
```

