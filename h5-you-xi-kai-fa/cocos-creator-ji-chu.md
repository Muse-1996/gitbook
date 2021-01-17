# Cocos Creator基础

#### 获取节点

1.通过节点绑定方式 2.通过代码获取

```javascript
var label = this.getComponent(cc.Label);

if (label) {
    label.string = "Hello";
}
else {
    cc.error("Something wrong?");
}
```

查找子节点

```javascript
var cannons = this.node.children;

this.node.getChildByName("Cannon 01");

cc.find("Cannon 01/Barrel/SFX", this.node);
```

全局名字查找

```javascript
this.backNode = cc.find("Canvas/Menu/Back");
```

节点状态和层级操作 通过 this.node 访问当前脚本所在节点

激活/关闭节点

```javascript
this.node.active = true;
```

更改节点的父节点

```javascript
this.node.parent = parentNode;
||
this.node.removeFromParent(false);
parentNode.addChild(this.node);
```

更改节点位置

```javascript
this.node.x = 100;
this.node.y = 50;

this.node.setPosition(100, 50);
this.node.setPosition(cc.v2(100, 50));

this.node.position = cc.v2(100, 50);
```

加载和切换场景

```javascript
cc.director.loadScene("MyScene");
```

常驻内存

```javascript
cc.game.addPersistRootNode(myNode);
```

场景加载回调

```javascript
cc.director.loadScene("MyScene", onSceneLaunched);
```

预加载场景

```javascript
cc.director.preloadScene("table", function () {
    cc.log("Next scene preloaded");
});

cc.director.loadScene("table");
```

