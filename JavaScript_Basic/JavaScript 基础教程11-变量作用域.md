# JavaScript 基础教程11-变量作用域

## 函数的变量作用域
> JavaScript 的函数在查找变量时从自身函数定义开始，从“内”向“外”查找。如果内部函数定义了与外部函数重名的变量，则内部函数的变量将“屏蔽”外部函数的变量。

+ 一个变量在函数体内部申明，则该变量的作用域为整个函数体，在函数体外不可引用该变量；
+ 不同函数内部的同名变量互相独立，互不影响；
+ 在嵌套的函数中，内部函数可以访问外部函数定义的变量，反过来则不行；

```JavaScript
function foo() {
    var x = 1;
    function bar() {
        var x = 'A';
        console.log('x in bar() = ' + x); // 'A'
    }
    console.log('x in foo() = ' + x); // 1
    bar();
}
```
 
## 函数的变量提升
> JavaScript 的函数定义，会先扫描整个函数体的语句，把**所有声明的变量“提升”到函数顶部**：JavaScript 引擎自动提升了变量的声明，但不会提升变量的赋值。

```JavaScript
function foo() {    
     var x = 'Hello, ' + y; // 提升变量y的声明，此时y为undefined
     console.log(x);
     y = 'Bob';
 }
```

## 全局作用域
> + 不在任何函数内定义的变量就具有全局作用域；
> + JavaScript 默认有一个全局对象 `window`，全局作用域的变量实际上被绑定到 `window` 的一个属性；
> + 由于函数可以通过函数名这个变量调用，因此顶层函数的定义也被视为一个全局变量，并绑定到 `window` 对象；

JavaScript 实际上只有一个全局作用域。任何变量（函数也视为变量），如果没有在当前函数作用域中找到，就会继续往上查找，最后如果在全局作用域中也没有找到，则报 ReferenceError 错误。

```JavaScript
var course = 'Learn JavaScript';
alert(course); // 'Learn JavaScript'
alert(window.course); // 'Learn JavaScript'

function foo() {
    alert('foo');
}

foo(); // 直接调用foo()
window.foo(); // 通过window.foo()调用
```

## 名称空间
> 全局变量会绑定到 window 上，不同的 JavaScript 文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，就会造成命名冲突。为减少全局变量冲突的可能，可以把自己的所有变量和函数全部绑定到一个全局变量。
著名的 jQuery 库就是这么干的。

```JavaScript
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;

// 其他函数:
MYAPP.foo = function () {
    return 'foo';
};
```

## 局部作用域
> `var` 声明的变量没有块级作用域，为了解决块级作用域，ES6 引入了新的关键字 `let`，用 `let` 替代 `var` 可以声明一个块级作用域的变量；

```JavaScript
function foo() {
    for (var i=0; i<100; i++) {
        //
    }
    i += 100; // 仍然可以引用变量i
}

function foo() {
    var sum = 0;
    for (let i=0; i<100; i++) {
        sum += i;
    }
    // SyntaxError:
    i += 1;
}
```

在 ES6 之前无法声明明一个常量，ES6 标准引入了新的关键字 `const` 来定义常量，`const` 与 `let` 都具有块级作用域；

```JavaScript
const PI = 3.14;
PI = 3; // 某些浏览器不报错，但是无效果！
PI; // 3.14
```
