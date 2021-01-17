---
description: 前端开发常用的代码片段
---

# 代码片段

### 时间格式化

```text
Date.prototype.format = function (fmt) {
    var o = {
        "M+": this.getMonth() + 1, //月份
        "d+": this.getDate(), //日
        "h+": this.getHours(), //小时
        "m+": this.getMinutes(), //分
        "s+": this.getSeconds(), //秒
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度
        "S": this.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o)
        if (new RegExp("(" + k + ")").test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    return fmt;
}

//to use
new Date(timer).format("yyyy-MM-dd hh:mm:ss")
```

### 手机号码验证

```text
var checkPhone = function(phone){  
    var reg = /^1[3|4|5|7|8][0-9]{9}$/; //验证规则,第一位是【1】开头，第二位有【3,4,5,7,8】，第三位及以后可以是【0-9】  
//  var reg = /^1[0-9]{10}$/;//不验证第二位，防止几年后新增号码段  
    if(!reg.test(phone)){  
        return false;  
    }  
    return true;  
} 
```

### 身份证验证

```text
var checkIdCard = function(idCard) {  
    var aCity={11:"北京",12:"天津",13:"河北",14:"山西",15:"内蒙古",21:"辽宁",22:"吉林",23:"黑龙江",31:"上海",32:"江苏",33:"浙江",34:"安徽",35:"福建",36:"江西",37:"山东",41:"河南",42:"湖北",43:"湖南",44:"广东",45:"广西",46:"海南",50:"重庆",51:"四川",52:"贵州",53:"云南",54:"西藏",61:"陕西",62:"甘肃",63:"青海",64:"宁夏",65:"新疆",71:"台湾",81:"香港",82:"澳门",91:"国外"}  
    var iSum = 0;  
    var info = "";  
    if (!/^\d{17}(\d|x)$/i.test(idCard)){  
        return false;//身份证长度或格式错误  
    }  
    idCard = idCard.replace(/x$/i, "a");  
    if (aCity[parseInt(idCard.substr(0, 2))] == null){  
        return false;//身份证地区非法;  
    }  
    var sBirthday = idCard.substr(6, 4) + "-" + Number(idCard.substr(10, 2)) + "-" + Number(idCard.substr(12, 2));  
    var d = new Date(sBirthday.replace(/-/g, "/"));  
    if (sBirthday != (d.getFullYear() + "-" + (d.getMonth() + 1) + "-" + d.getDate())){  
        return false;//身份证上的出生日期非法;  
    }  
    for (var i = 17; i >= 0; i--){  
        iSum += (Math.pow(2, i) % 11) * parseInt(idCard.charAt(17 - i), 11);  
    }  
    if (iSum % 11 != 1){  
        return false;//身份证号非法;   
    }  
    return true;  
}
```

### 获取URL中的参数

```text
function findDataInUrl(name,url) {
var reg = new RegExp("(^|\\?|&)" + name + "=([^&]*)(\\s|&|$)", "i"); 
if (reg.test(url)) 
    return decodeURIComponent(RegExp.$2.replace(/\+/g, " ")); 
}
```

### 随机数生成

```text
var getRandom = function(min, max){
    return min + (Math.random() * (max-min +1));
}
```

### 对象深拷贝

```text
function cloneObj(obj) {
    var o = obj.constructor == Object ? new obj.constructor() : new obj.constructor(obj.valueOf());
    for(var key in obj){
        if(o[key] != obj[key] ){
            if(typeof(obj[key]) == 'object' ){
                o[key] = mods.cloneObj(obj[key]);
            }else{
                o[key] = obj[key];
            }
        }
    }
    return o;
}
```

### 清除对象中值为空的属性

```text
function filterParams(obj){
    let _newPar = {};
    for (let key in obj) {
        if ((obj[key] !== 0 && obj[key]) && obj[key].toString().replace(/(^\s*)|(\s*$)/g, '') !== '') {
            _newPar[key] = obj[key];
        }
    }
    return _newPar;
}

filterParams({a:0, b:1, c:"010", d:null, e:undefined,f:false}) 
// 当值等于0,null,undefined的时候，就会被过滤
```

### 获取文件名后缀

```text
function getSuffix(file_name) {
    var result = /[^\.]+$/.exec(file_name);
    return result;
}
```

### 冒泡排序

```text
function bubbleSort(arr) {
    var len = arr.length;
    for (var i = 0; i < len; i++) {
        for (var j = 0; j < len - 1 - i; j++) {
            if (arr[j] > arr[j+1]) {        //相邻元素两两对比
                var temp = arr[j+1];        //元素交换
                arr[j+1] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr;
}

var arr=[3,44,38,5,47,15,36,26,27,2,46,4,19,50,48];
bubbleSort(arr);//[2, 3, 4, 5, 15, 19, 26, 27, 36, 38, 44, 46, 47, 48, 50];
```

### 最简单的模板引擎

```text
var render = function(tpl,data){
    return tpl.replace(/\{\{(.+?)\}\}/g,function(m,m1){
        return data[m1]
    })
}

render('我是{{name}}，年龄{{age}}，性别{{sex}}',{
    name:'姓名',
    age:18,sex:'女',
})
```

### 去除空格

```text
//去除空格  type 1-所有空格  2-前后空格  3-前空格 4-后空格
function trim(str,type){
    switch (type){
        case 1:return str.replace(/\s+/g,"");
        case 2:return str.replace(/(^\s*)|(\s*$)/g, "");
        case 3:return str.replace(/(^\s*)/g, "");
        case 4:return str.replace(/(\s*$)/g, "");
        default:return str;
    }
}

trim('a   a   dd ',1); // "aadd"
trim('a   a   dd ',2); // "a   a   dd"
trim('a   a   dd ',3); // "a   a   dd "
trim(' a   a   dd ',4); // " a   a   dd"
```

### 字符串替换

```text
//字符串替换(字符串,要替换的字符,替换成什么)
function replaceAll(str,AFindText,ARepText){
　　　raRegExp = new RegExp(AFindText,"g");
　　　return str.replace(raRegExp,ARepText);
}
replaceAll('abcd','bc','111') // "a111d"
```

### Base64转图片

```text
function dataURLtoFile(dataurl, filename) {
    var arr = dataurl.split(','), mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
    while(n--){
        u8arr[n] = bstr.charCodeAt(n);
    }
    return new File([u8arr], filename, {type:mime});
}
```

### 文本溢出显示省略号

```text
.elipText{
    display: inline-block;
    max-width: 60%;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

### JS去除空格

```javascript
String.prototype.Trim = function(){ 
    return this.replace(/(^\s*)|(\s*$)/g, ""); 
}
```

### 清除对象中值为空的属性

```javascript
function filterParams(obj){
    let _newPar = {};
    for (let key in obj) {
        if ((obj[key] !== 0 && obj[key]) && obj[key].toString().replace(/(^\s*)|(\s*$)/g, '') !== '') {
            _newPar[key] = obj[key];
        }
    }
    return _newPar;
}

filterParams({a:0, b:1, c:"010", d:null, e:undefined,f:false})
```

### 获取文件后缀名

```javascript
function getSuffix(file_name) {
    var result = /[^\.]+$/.exec(file_name);
    return result;
}
getSuffix('1234.png') // ["png", index: 5, input: "1234.png"]
```

### 去除字符串中的空格

```javascript
//去除空格  type 1-所有空格  2-前后空格  3-前空格 4-后空格
function trim(str,type){
    switch (type){
        case 1:return str.replace(/\s+/g,"");
        case 2:return str.replace(/(^\s*)|(\s*$)/g, "");
        case 3:return str.replace(/(^\s*)/g, "");
        case 4:return str.replace(/(\s*$)/g, "");
        default:return str;
    }
}

trim('a   a   dd ',1); // "aadd"
trim('a   a   dd ',2); // "a   a   dd"
trim('a   a   dd ',3); // "a   a   dd "
trim(' a   a   dd ',4); // " a   a   dd"
```

### 转xml

```javascript
/**
  * 转成XML对象
  * 
  * @param {String} str 一个xml格式的串
  * @returns 
  */
function createXml(str) {
  if (document.all) {
    var xmlDom = new ActiveXObject("Microsoft.XMLDOM")
    xmlDom.loadXML(str)
    return xmlDom
  }
  else
    return new DOMParser().parseFromString(str, "text/xml")
}
```

>

