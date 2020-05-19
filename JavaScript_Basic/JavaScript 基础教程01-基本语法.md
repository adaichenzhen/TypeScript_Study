# JavaScript 基础教程01-基本语法

## 语句
> 每个语句以 `;` 结束（`JavaScript` 并不强制要求在每个语句的结尾加 `;` ，因为浏览器中负责执行 `JavaScript` 代码的引擎会自动在每个语句的结尾补上 ;）

```JavaScript
var x = 1; // 赋值语句
'Hello, world'; // 一个字符串，但仍然可以视为一个完整的语句
var x = 1; var y = 2; // 不建议一行写多个语句!!!

function foo() {
    // 由于JavaScript引擎在行末自动添加分号的机制，下面一条语句相当于 return;  
    return 
        {name: 'foo'}; 
}  
foo(); // undefined

function foo1() {
    return {name: 'foo'}; 
}  
foo1(); // {name: 'foo' }
```

## 语句块
> 语句块用 `{...}` ，`{...}` 还可以嵌套，形成层级结构

```JavaScript
if (2 > 1) {
    x = 1;
    y = 2;
    z = 3;
}
```

## 注释

> + 以 // 开头直到行末的字符被视为行注释
> + 用 /*...*/ 把多行字符包裹起来被视为块注释

## 注意事项：

+ 花括号 `{...}` 内的语句具有缩进，通常是4个空格。
+ `JavaScript` 严格区分大小写