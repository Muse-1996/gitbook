# v-sheel 选择器

### 下拉选择器

```markup
<div 
 v-err-btn
 @change="selectCb" 
 v-sheel="listData">
 123
</div>

...

data:{
 listData:[{id:1,name:123},{id:2,name:234},{id:3,name:345}]
},
methods:{
 selectCb(data,index){
  //data {id:1,name:123}
  //index 0
 }
}
```

![](../../../.gitbook/assets/image%20%2813%29.png)

