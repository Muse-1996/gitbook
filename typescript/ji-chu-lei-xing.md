# 基础类型

| 关键字 | 类型 |
| :--- | :--- |
| any | 任何类型 |
| number | 数字类型 |
| string | 字符串类型 |
| boolean | 布尔类型 |
| null | null |
| undefined | undefined |
| never | 其它类型（包括 null 和 undefined）的子类型，代表从不会出现的值 |

数组类型

```typescript
let arr: number[] = [1,2];
// or
let arr: Array<number> = [1,2];
```

元组

```typescript
let x: [string, number];
x = ['a', 1];    // 运行正常
x = [1, 'b'];    // 报错
```

枚举

```typescript
enum Color {Red, Green, Blue};
let c: Color = Color.Blue;
console.log(c);    // 输出 2
```

void

```typescript
//表示无返回值的方法
function hello(): void {
    alert("Hello Runoob");
}
```

