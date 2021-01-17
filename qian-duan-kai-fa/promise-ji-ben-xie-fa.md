---
description: 摆脱大箭头Callback Hell写法
---

# Promise基本写法

### 常规写法

```text
function loadImg(src,callback,fail){
  var img = document.createElement('img');
  img.onload = function(){
    callback(img);
  };
  img.onerror = function(){
    fail();
  };
  img.src = src;
};


var src = 'https://www.baidu.com/img/baidu_jgylogo3.gif';

loadImg(src,function(img){
  console.log(img.width);
},function(){
  console.log('failed');
});
```

### Promise写法

```text
function loadImg(src){
  const promise = new Promise(function(resolve,reject){
    var img = document.createElement('img');
    img.onload = function(){
      resolve(img);
    };
    img.onerror = function(){
      reject();
    };
    img.src = src;
  });
  return promise;
};


var src = 'https://www.baidu.com/img/baidu_jgylogo3.gif';
var result = loadImg(src);

result.then(function(img){
  console.log(img.width);
},function(){
  console.log('failed');
});

result.then(function(img){
  console.log(img.height);
});
```

### 基本结构

```text
new Promise(function(resolve,reject){
  resolve() //继续执行 =》1
  //reject() //放弃执行 =》2
}).then(function(){
  alert(1)
},function(){
  alert(2)
})
```

