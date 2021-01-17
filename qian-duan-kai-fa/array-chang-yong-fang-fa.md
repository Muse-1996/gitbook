# Array常用方法

### shift\( \)

用于把数组的第一个元素从其中删除，并返回第一个元素的值,并且会改变原数组。

```text
 var arr = [1,2,3,4,5];
 var item = arr.shift();
 console.log(arr,item);   // [2, 3, 4, 5] 1
```

示例用法-递归执行

```text
var fileArr = ['file1','file2','file3'];

function parseFile(){
  if(fileArr.length == 0){
    return;
  };
  var file = file.shift();
  fs.readFile(file, function (err, data) {
    parseFile();
  });
};

parseFile();
```

### concat\( \)

用于连接两个或多个数组，该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本

```text
var arr1 = [1,2,3,4];
var arr2 = ['a','b','c','d'];
console.log(arr1.concat(arr2));  //[1, 2, 3, 4, "a", "b", "c", "d"]
```

### pop\( \)

删除并返回数组的最后一个元素 会改变原始数组

```text
var arr = [1,2,3,4];
console.log(arr.pop());    //4
```

### reverse\( \)

颠倒数组中元素的顺序 会改变原始数组

```text
var arr = [1,2,3,4];
var arr1 = arr.reverse();
console.log(arr1);           //[4, 3, 2, 1]
```

### unshift\(\)

向数组的开头添加一个或更多元素，并返回新的长度 会改变原数组

```text
var a = [1,2,3];
var b = a.unshift(4,5,6);
console.log(b);            //6
```

