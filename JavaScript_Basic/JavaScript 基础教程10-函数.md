# JavaScript 基础教程10-函数

## 函数的定义
> 函数的定义包括函数声明和函数表达式两种方式。

```JavaScript
// 函数声明（Function Declaration）
function sum(x, y) {
    return x + y;
}


// 函数表达式（Function Expression）
let mySum = function (x, y) {
    return x + y;
};
```
+ 关键字 `function` 表示这是一个函数定义；
+ `sum` 和 `mySum` 是函数的名称，由于函数也是一个对象，因此函数名可以视为指向该函数的变量；
+ `(x)` 括号内列出函数的参数，多个参数以 `,` 分隔；
+ `{ ... }` 之间的代码是函数体，可以包含若干语句，甚至可以没有任何语句；
+ 函数体内一旦执行到 return 语句时，函数就执行完毕，并将结果返回；
+ **如果没有 return 语句，函数执行完毕后会返回 undefined**。    

## 函数的调用
> 调用函数时，按顺序传入参数即可。不过 JavaScript 允许传入任意个参数而不影响调用。

```JavaScript
var abs = function (x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
};

abs(10); // 返回10--正常调用
abs(10, 'blablabla'); // 返回10--传入的参数比定义的参数多
abs(); // 返回NaN--传入的参数比定义的少，此时参数 x 将收到 undefined
```

### arguments 参数
> arguments 只在在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。
> 
> arguments 类似 Array 但它不是一个Array。
> 
> arguments 常用于判断传入参数的个数 。

```JavaScript
function abs() {
    if (arguments.length === 0) {
        return 0;
    }
    var x = arguments[0];
    return x >= 0 ? x : -x;
}

abs(); // 0
abs(10); // 10
abs(-9); // 9
```

### rest 参数
> 为获取任意参数，ES6 标准引入了 `rest` 参数。
> 
> rest 参数只能写在最后，前面用 `...` 标识，多余的参数以数组形式交给变量 rest，如果传入的参数连正常定义的参数都没填满，rest 参数会接收一个空数组。

```JavaScript
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

foo(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]

foo(1);
// 结果:
// a = 1
// b = undefined
// Array []
```
