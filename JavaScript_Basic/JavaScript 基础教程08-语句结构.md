# JavaScript 基础教程08-语句结构

## 条件判断
> JavaScript 使用 `if () { ... } else if () { ... } else { ... }` 来进行条件判断，其中 `else if` 和` else` 是可选项。

如果语句块只包含一条语句，那么可以省略 `{}`，但建议永远都要写上 `{}`。

```JavaScript
if(){
    ...
}else if(){
    ...
}else{
    ...
}
```

如果条件判断语句结果不是布尔值，而是其他的数据类型，**JavaScript把 `null`、`undefined` 、`0`、`NaN` 和空字符串 `''` 视为 `false`**，其他值一概视为 `true`。

## 循环
### for循环
> 通过初始条件、结束条件和递增条件来循环执行语句块

```JavaScript
var x = 0;
var i;
for (i=1; i<=10000; i++) {
    x = x + i;
}
```

### for ... in循环
> 可以把一个对象（Array 也是对象，元素索引被视为对象属性）的所有属性名依次循环出来

`for ... in` 对Array的循环得到的索引（属性名）是 `String` 而不是 `Number`
```JavaScript
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    console.log(key); // 'name', 'age', 'city'
}
var a = ['A', 'B', 'C'];
for (var i in a) {
    console.log(i); // '0', '1', '2'
    console.log(a[i]); // 'A', 'B', 'C'
} 
```

### while循环
> 判断条件满足，就不断循环，条件不满足时则退出循环

```JavaScript
var x = 0;
var n = 99;
while (n > 0) {
    x = x + n;
    n = n - 2;
}
x; // 2500
```

### do ... while循环
> 与while循环类似，区别在于，不是在每次循环开始的时候判断条件，而是在每次循环完成的时候判断条件，所以至少执行循环体一次

```JavaScript
var n = 0;
do {
    n = n + 1;
} while (n < 100);
n; // 100
```

