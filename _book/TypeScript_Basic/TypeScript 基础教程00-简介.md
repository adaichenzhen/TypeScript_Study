## TypeScript 是什么
> TypeScript 是 JavaScript 的类型的超集，它可以编译成纯 JavaScript。编译出来的 JavaScript 可以运行在任何浏览器上。TypeScript 编译工具可以运行在任何服务器和任何系统上。TypeScript 是开源的。

+ TypeScript 是 JavaScript 的超集，所以 JS 代码完全可以在 TS 文件中使用，.js 文件可以直接将其后缀名改为 .ts 使用。 
+ TS 代码编译后会转为 JS 代码，即使 TS 代码有语法错误也会成功编译。
+ 提供了类型系统
+ 提供了对 ES6 的支持

## TypeScript 的安装
TypeScript 的命令行工具安装方法如下：
```
npm install -g typescript
```
以上命令会在全局环境下安装 `tsc` 命令，安装完成之后，我们就可以在任何地方执行 `tsc` 命令了，例如编译一个 TypeScript 文件：
``` 
tsc hello.ts
```

## TypeScript 的入门示例
新建 hello.ts 文件，加入如下代码：
``` typescript
function sayHello(person: string) {
    return 'Hello, ' + person;
}

let user = [0, 1, 2]; 
console.log(sayHello(user));
```
然后执行编译命令（`tsc hello.ts`），将在同目录下生成一个编译好的文件 hello.js：
``` typescript
function sayHello(person) {
    return 'Hello, ' + person;
}
var user = [0, 1, 2];
console.log(sayHello(user));

error TS2345: Argument of type 'number[]' is not assignable to parameter of type 'string'.
```
1. 变量类型：将形参变量 `person` 定义为 `string` 类型；
2. 编译报错：由于实参变量 `user` 初始化为一个数组类型（编译器会进行类型推断），所以实参和形参类型的不匹配；
3. 即使编译时报错，`.ts` 文件还是会成功编译为 `.js` 文件，这是因为 TypeScript 只会进行静态检查，如果发现有错误，编译的时候会报错但不会阻止编译过程。如果想要在报错的时候终止 `.js` 文件的生成，可以在 `tsconfig.json` 中配置 `noEmitOnError` 即可（参阅[官方手册](http://www.typescriptlang.org/docs/handbook/tsconfig-json.html)（[中文版](https://zhongsp.gitbooks.io/typescript-handbook/content/doc/handbook/tsconfig.json.html)））。