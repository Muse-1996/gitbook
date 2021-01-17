---
description: 人艰不拆的class
---

# class的基本使用

### class和普通构造函数的区别

1. class在语法上更加贴合面向对象的写法
2. class实现继承更加易读、易理解
3. 易于后端开发人员使用
4. 本质还是语法糖，使用的还是prototype继承方式

### 基本语法

```text
class MathHandle{
  //构造器
  constructor(x,y){
    this.x = x;
    this.y = y;
  }
  
  add(){
    return this.x+this.y
  }
}

const m = new MathHandle(1,2)
console.log(m.add())
```

### 语法糖

转化为另一种形式

```text
class MathHandle{
  //...
}

typeof MathHandle //function
MathHandle == MathHandle.prototype.constructor //true
```

