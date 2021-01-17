# Cocos Creator远程图片加载

Cocos creator的资源是开发阶段就规定好的，没有远程载入图片的方法，但是当时开发业务有一个动态生成用户二维码的功能，写法如下：

```javascript
var img = new Image();
img.src = base; //base64格式为例
img.onload = function(){
  var texture = new cc.Texture2D();
  texture.initWithElement(img);
  texture.handleLoadedTexture();
  var newframe = new cc.SpriteFrame(texture);
  //插入sprite-frame
  _this.ewmimg.spriteFrame = newframe;
  //大小
  _this.ewmimg.node.setContentSize(300,300);
}
```

