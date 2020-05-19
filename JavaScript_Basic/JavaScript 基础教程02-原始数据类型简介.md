# JavaScript 基础教程02-原始数据类型简介

> JavaScript 的类型分为两种：原始数据类型（Primitive data types）和对象类型（Object types）。
> 
> 原始数据类型包括：布尔值、数值、字符串、null、undefined 以及 ES6 中的新类型 Symbol。
> 
> 本文主要介绍前五种原始数据类型。

## 布尔值
> 一个布尔值只有 `true` 、`false` 两种值，要么是 `true` ，要么是 `false` ，可以直接用 `true`、`false` 表示布尔值，也可以通过布尔运算计算出来

```JavaScript
true; // 这是一个true值
2 >= 3; // 这是一个false值
```

## 数值
> `JavaScript` **不区分整数和浮点数**，统一用数值（`Number`）表示。数值包括：整数、浮点数、`NaN`、`Infinity`，后面两种可能不太好理解。
> + `NaN` 表示 Not a Number，当无法计算结果时用NaN表示
> + `Infinity` 表示无限大，当数值超过了 `JavaScript` 的 `Number` 所能表示的最大值时，就表示为 `Infinity`

```JavaScript
123; // 十进制整数123
-99; // 负数
0xff00; // 十六进制表示的整数

0.456; // 浮点数0.456
1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5

NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
1/0; // Infinity
```

## 字符串
> 字符串是以单引号 `'` 或双引号 `"` 括起来的任意文本，比如 `'abc'`，`"xyz"` 等等。请注意，`''` 或 `""` 本身只是一种表示方式，不是字符串的一部分，因此，字符串 `'abc'` 只有 `a`，`b`，`c` 这3个字符。

## null
> `null` 表示一个“空”的值，例如Java（或C#）也用 `null`，Python用 `None` 表示

## undefined 
> `undefined` 表示值未定义

## 注意
JavaScript的设计者希望用 `null` 表示一个空的值，而 `undefined` 表示值未定义。事实证明，这并没有什么卵用，区分两者的意义不大。大多数情况下，我们都应该用 `null` 。`undefined` 仅仅在判断函数参数是否传递的情况下有用。