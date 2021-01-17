---
description: 设计模式存在的根本原因是为了代码复用，增加可维护性
---

# 浅聊设计模式

### 设计模式的原则

1. 【开闭原则】对扩展开放 对修改关闭
2. 【里氏转换原则】子类继承父类 可单独运行
3. 【依赖倒转原则】引用一个对象，如果这个对象有底层类型，直接引用底层
4. 【接口隔离原则】每一个接口应该是一种角色
5. 【合成/聚合复用原则】新的对象应使用一些已有的对象，使之成为新对象的一部分
6. 【迪米特原则】一个对象应对其他对象有尽可能少的了解

### 单例模式

> 单例就是保证一个类只有一个实例，实现的方法一般是先判断实例存在与否，如果存在直接返回，如果不存在就创建了再返回，这就确保了一个类只有一个实例对象。在JavaScript中，单例作为一个命名空间提供者，从全局命名空间里提供一个唯一的访问点来访问该对象。

作用

1. 模块间通信 
2. 系统中某个类的对象只能存在一个 
3. 保护自己的属性和方法

示例

```text
var a = (function(){
  var a = function(msg){
    this.ding = msg;
  };
  var door;
  var info = {
    sendMsg:function(msg){
      if(!door){
        door = new a(msg);
      }
      return door;
    };
  }
  return info;
})()

var b = {
  callA:function(msg){
    var _xw = a.sendMsg(msg);
    console.log(_xw);
    //清理 等待垃圾回收
    _xw = null;
  };
};

b.callA('ling。。。');
```

{% hint style="warning" %}
注意

1. 注意this的使用 
2. 闭包容易造成内存泄漏 
3. 注意new的成本
{% endhint %}

### 构造函数模式

> 构造函数用于创建特定类型的对象——不仅声明了使用的对象，构造函数还可以接受参数以便第一次创建对象的时候设置成对象的成员值。你可以自定义自己的构造函数，然后在里面声明自定义类型对象的属性或方法。

作用

1. 用于创建特定类型的对象 
2. 第一次声明的时候给对象赋值 
3. 自己声明构造函数，赋予属性和方法

示例

```text
function zaomen(){
  if(!(this instanceof zaomen)){
     return new zaomen();
  };
  this.suo = "普通";
  this.huawen = "普通";
  this.create = function(){
    return "[suo]"+this.suo+"[huawen]"+this.huawen;
  };
}
var xiaozhang = new zaomen();
xiaozhang.create();
```

{% hint style="warning" %}
注意

1. 声明函数的时候处理业务逻辑 
2. 区分和单例的区别，配合单例实现初始化 
3. 构造函数建议大写字母开头 
4. 注意new的成本（继承）
{% endhint %}

### 建造者模式

> 建造者模式可以将一个复杂对象的构建与其表示相分离，使得同样的构建过程可以创建不同的表示。也就是说如果我们用了建造者模式，那么用户就需要指定需要建造的类型就可以得到它们，而具体建造的过程和细节就不需要知道了。建造者模式实际，就是一个指挥者，一个建造者，一个使用指挥者调用具体建造者工作得出结果的客户。主要用于分步构建一个复杂的对象，分步骤是一个稳定的算法，而复杂对象的各个部分则经常变化。

作用

1. 可以分步创建一个复杂的对象 
2. 解耦封装过程和具体创建的组件 
3. 无需关心组件如何组装

### 工厂模式

> 工厂模式定义一个用于创建对象的接口，这个接口由子类决定实例化那一个类。该模式使一个类的实例化延迟到了子类。而子类可以重写接口方法以便创建的时候指定自己的对象类型（抽象工厂）

示例

```text
var gongchang = {}
gongchang.chanyifu = function(){
  this.gongren = 50
  alert("我们有"+this.gongren)
}
gongchang.chanxie = function(){
  alert("产鞋子")
}
gongchang.yunshu = function(){
  alert("运输")
}
gongchang.changzhang = function(para){
  return new gongchang[para]()
}

var me = gongchang.changzhang("chanyifu")
alert(this.gongren)
```

### 外观模式

> 外观模式为子系统中的一组接口提供了一个一致的界面，此模块定义了一个高层接口，这个接口使得这一子系统更加容易使用。
>
> 外观模式不仅简化类中的接口，而且对接口与调用者也进行了解耦。外观模式经常被认为开发者必备，它可以将一些复杂操作封装起来，并创建一个见得接口用于调用。

作用

1. 在设计初期，应该有意识地将不同的两个层分离，比如经典的三层结构。 
2. 在开发阶段，子系统往往因为不断地重构演化而变得越来越复杂，增加外观F可以提供一个简单的接口，减少他们之间的依赖。 
3. 在维护一个遗留的大型系统时，为系统开发一个外观Facade类，为实际粗糙和高度复杂的遗留代码提供比较清晰地接口，让新系统和Facade对象交互。

示例

```text
var fuhao = {
  
}
fuhao.huofang = function(){
  return "馒头"
}
fuhao.chuliliangshi = function(){
  return "面粉"
}
fuhao.mantou = function(){
  this.chuliliangshi();
  this.huofang();
}
fuhao.men = function(){
  return this.mantou()
}
```

{% hint style="danger" %}
外观模式被开发者连续使用会产生一定的性能问题，因为在每次调用时都要检测功能的可用性。
{% endhint %}

### 代理模式

> （Proxy）为其他对象提供一种代理以控制对这个对象的访问。
>
> 代理模式使得代理对象控制具体对象的引用，代理几乎可以使任何对象：文件，资源，内存中的对象，或者是一些难以复制的东西。

示例

```text
function maijia(){
  this.name = "小明"
}
function zhongjie(){
  
}
zhongjie.prototype.maifang = function(){
  new fangdong(new maijia()).maifang("20w")
}
function fangdong(maijia){
  this.maijia_name = maijia.name
  this.maifang = function(money){
    alert("收到了【"+this.maijia_name+"]"+money+"rmb")
  }
}
(new zhongjie).maifang()
```

