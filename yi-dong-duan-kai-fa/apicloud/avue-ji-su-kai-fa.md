---
description: 让我们一起用数据来驱动好伐？
---

# AVUE极速开发

> apicloud基于html,css,js进行开发，代码写法上跟web写法差不多，jQuery这种库也可以用，但是体积大，频繁操作dom，而且开发速度慢，也不便于维护，所以搞一个aVue来提高一下开发体验，毕竟任务完成快才有时间学习嘛。

### 起手式

> 首先要考虑的是移动端的点击300ms的延迟，直接先简单粗暴引入一个fastclick.js，因为整体是要基于Vue的，所以也来下载一个vue.min.js，放在目录备用，接下来起锅烧油。

ES6真香操作

```javascript
//使aVue继承Vue 以免对Vue源码直接扩展导致维护难度增大
class aVue extends Vue {}
```

把api方法拷贝到aVue上

```javascript
//对原型扩展api的相关方法 使语法风格一致
for(let _apiItem in api){
    aVue.prototype[_apiItem] = api[_apiItem]
}
```

扩展一些基本的方法备用

```javascript
//外部定义方法
const _avMethods = {
    //关闭窗口的方法
    _avCloseWin(winName){
        if(winName){
            this.closeWin();
        }else{
            this.closeWin({
                name: winName
            });
        }
    },

    //扩展options参数 --- listener
    _avEvent(item,fn){
        this.addEventListener({
            name: item
        }, function(ret, err){
            if( ret ){
                 fn(ret.value)
            }else{
                 api.toast( JSON.stringify( err ) );
            }
        });
    },

    _avSendEvent(item,data){
        this.sendEvent({
            name: item,
            extra: data
        });
    },

    //时间戳处理 yyyy-mm-dd hh:mm
    _avTimeEncode(time,type){
        let now = new Date(parseInt(time));
        let year = now.getFullYear();
        let month=now.getMonth()+1<10?'0'+(now.getMonth()+1):now.getMonth()+1;
        let day = now.getDate();
        let hour=now.getHours()<10?'0'+now.getHours():now.getHours();
        let minute=now.getMinutes()<10?'0'+now.getMinutes():now.getMinutes();
        return year+'-'+month+'-'+day+'  '+hour+':'+minute
    }

}
```

接下来做一下过滤器

```javascript
//鉴于常见的业务需求 时间戳设置为过滤器模式
aVue.filter('initTime', function (value) {
  return _avMethods._avTimeEncode(value)
})
```

进入正戏

```javascript
const apiPlus = {
    // 可以在install方法里做扩展
    install: function(Vue, options) {

        //自定义指令  关闭Win窗口
        Vue.directive('close',{
            bind(el){
                el.addEventListener('click',()=>{
                    _avMethods._avCloseWin(binding.value)
                })
            }
        })

        // 全局消息监听
        Vue.prototype.sendEvent = function(name,data){
            _avMethods._avSendEvent(name,data||{})
        }

        //时间戳格式化
        Vue.prototype.initTime = function(d){
            if(d){
                let _defineTime = _avMethods._avTimeEncode(d);
                return _defineTime;
            }else{
                return '时间戳格式不合法'
            }
        }

        //封装ajax Get方法
        Vue.prototype.$get = function(){
            var avHeaders;
            var avCallback;
            if(typeof arguments[1] == 'object'){
                avHeaders = arguments[1];
                avCallback = arguments[2];
            }else if(typeof arguments[1] == 'function'){
                avCallback = arguments[1];
            }
            api.ajax({
                url: this.indexUrl+arguments[0],
                method: 'get',
                headers:avHeaders
            }, function(ret,err){avCallback.call(Vue,ret,err)});
        };

        //封装ajax POST方法
        Vue.prototype.$post = function(){
            var postHeader = postData = {};
            var postCb;
            if(typeof arguments[1] == typeof arguments[2]){
                postHeader = arguments[1];
                postData = arguments[2];
                postCb = arguments[3];
            }else{
                postData = arguments[1];
                postCb = arguments[2];
            }
            api.ajax({
                url: this.indexUrl+arguments[0],
                method: 'post',
                data: {values: postData},
                headers:postHeader,
            },function(ret, err){
                postCb.call(Vue,ret,err)
            });
        }

        //显示loading...
        Vue.prototype.showLoading = function(stu){
            if(stu){
                api.showProgress({
                    title: '努力加载中...',
                    text: '请稍候...',
                    modal: true
                });
            }else{
                api.hideProgress();
            }
        }

        Vue.prototype.avStorage = function(){
            var isAndroid = (/android/gi).test(navigator.appVersion);
            var ls = window.localStorage;
            if(isAndroid){
               ls = os.localStorage();
            }
            return ls;
        };

        // 生命周期、公共数据可以在这里写
        Vue.mixin({
            data(){
                return{
                    //测试路由入口
                    indexUrl:'http://172.16.6.84:9949/',
                    //测试数据获取
                    avToken:9999999,
                    //自动获取窗口传参
                    Param:api.pageParam,
                    _avBase:{},
                    //自动获取窗口安全边距
                    safeArea:api.safeArea
                }
            },

            methods:{

                //Storage 存储数据
                setStorage(key,value){
                    if(arguments.length === 2){
                        var v = value;
                        if(typeof v == 'object'){
                            v = JSON.stringify(v);
                            v = 'obj-'+ v;
                        }else{
                            v = 'str-'+ v;
                        }
                        var ls = this.avStorage();
                        if(ls){
                            ls.setItem(key, v);
                        }
                    }
                },

                //Storage 获取数据
                getStorage(key){
                    var ls = this.avStorage();
                    if(ls){
                        var v = ls.getItem(key);
                        if(!v){return;}
                        if(v.indexOf('obj-') === 0){
                            v = v.slice(4);
                            return JSON.parse(v);
                        }else if(v.indexOf('str-') === 0){
                            return v.slice(4);
                        }
                    }
                },

                //Storage 移出数据
                rmStorage(key){
                    var ls = this.avStorage();
                    if(ls && key){
                        ls.removeItem(key);
                    }
                },

                //Storage 清空数据
                clrStorage(){
                    var ls = this.avStorage();
                    if(ls){
                        ls.clear();
                    }
                },
            },



            created: function () {
                //实例化的时候绑定监听
                var listener = this.$options.listener;
                for(item in listener){
                    if(typeof listener[item] !== 'function'){
                        console.error('the listener option is not a function!');
                        return;
                    }
                    _avMethods._avEvent(item,listener[item])
                }
            },
            
            mounted:function(){

                //移动端300ms延迟
                FastClick.attach(document.body)

            }
        })
    }
}


// 也可以使用Vue.use在Vue上直接扩展，看需要
aVue.use(apiPlus);
```

压缩

将vue.js fastclick.js avue.js进行es5编译打包，生成avue.js 文件

使用方法

```markup
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="maximum-scale=1.0,minimum-scale=1.0,user-scalable=0,initial-scale=1.0,width=device-width" />
    <meta name="format-detection" content="telephone=no,email=no,date=no,address=no">
    <title>Hello APP</title>
    <link rel="stylesheet" type="text/css" href="../css/api.css" />
    <link rel="stylesheet" href="../css/animate.css">
</head>

<body class="wrap">
    <div id="main">
        <v-header :title="'AVue 示例'" @top-click="headerClick()"></v-header>
        <div v-close>关闭窗口</div>
    </div>
</body>
<link rel="stylesheet" href="../css/main.css">
  <!-- 组件适合抽离一些很常用的部分 -->
<script type="text/javascript" src="../template/tmp_header.js"></script>
<script type="text/javascript" src="../script/avue.min.js"></script>
<script type="text/javascript">
    apiready = function() {
        new aVue({
            el:'#main',
            data:{
                titleArr:[
                    'Hello Avue?',
                    'Hello Avue.',
                    'Hello Avue!'
                ],
                title:'APICloud和Vue结合会发生什么',
                vindex:0
            },
            //监听消息广播的写法
            listener:{
                keyback:function(){
                    this.closeWidget()
                }
            },
            methods:{
                saveDate(){
                    this.setStorage('key','123456')
                },
                headerClick(data){
                    //data 666
                }
            },
            created(){
                //显示加载中
                this.showLoading(true)
                //关闭加载中
                setTimeout(function(){
                    this.showLoading(false)
                }.bind(this),2000)
            }
        })
    };

</script>

</html>

```

组件

```javascript
//tmp_header.js
var tmpStr = `
    <header id="head" :style="{paddingTop:paddingTop}" style="width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background: #565bff;
    color: #fff;
    text-align: center;
    display: flex;
    line-height: 48px;
    text-align: center;">
        <span @click="closeWin()" style="width: 40px;
        font-size: 14px;">返回</span>
        <p v-text="title" @click="clickHeader()" style="flex:1"></p>
        <span @click="closeWin()" style="width: 40px;
        font-size: 14px;">跳过</span>
    </header>
`
Vue.component("v-header",{
    props:{
        title:{
            type:String,
            default:'default'
        },
    },
    data(){
        return{
            paddingTop:0
        }
    },
    template:tmpStr,
    methods:{
        clickHeader(index){
            this.$emit("topClick",666);
        },
        closeWin(){
            this.closeWin()
        }
    },
    created(){
        this.paddingTop = this.safeArea.top+'px'
    }
});

```

这里只做了一个雏形，还有很多地方需要完善和优化，但是鉴于公司原来的写法写了太多东西，不会采用这种方式开发，所以这个也没继续更新了，就一般自己使，有时间的话再回头重新完善一下。

