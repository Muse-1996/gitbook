# Vue滚动轮播插件

vue-seamless-scroll插件实现滚动轮播，会造成页面整体抖动，使用css脱离文档流依然无法解决这个问题，遂采用另一个轮播库[seamscroll](https://github.com/chenxuan0000/seamless-scroll/blob/master/document/README.md)。

安装

```bash
cnpm install seamscroll --save
```

使用

```javascript
const seamless = require('seamscroll');

seamscroll.init({
     dom: document.getElementById('demo2'),
     step:1, //步长,越大越快
     hoverStop:true, //是否启用鼠标hover控制
     direction: 2, //方向 0 往下 1 往上 2向左 3向右
     singleHeight:0, //单步运动停止的高度(默认值0是无缝不停止的滚动) direction => 0/1
     singleWidth:0, //单步运动停止的宽度(默认值0是无缝不停止的滚动) direction => 2/3
     waitTime:1, //单步停止等待时间(default 1s)
});
```

