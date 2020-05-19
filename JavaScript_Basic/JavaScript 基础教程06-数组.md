# JavaScript 基础教程06-数组

## 数组的基础
### 数组的简介
> 数组是一组按顺序排列的集合，集合中的每个值称为元素。JavaScript的数组可以包括任意数据类型。

数组用 `[]` 表示，元素之间用 `,` 分隔
```JavaScript
[1, 2, 3.14, 'Hello', null, true];
```

### 数组的创建
+ 直接使用 `[]` 进行创建；
+ 通过 `Array()` 函数实现；

```JavaScript
[1, 2, 3]; // 创建了数组[1, 2, 3]
new Array(1, 2, 3); // 创建了数组[1, 2, 3]
```

### 数组中元素的访问
> 数组的元素可以通过索引（索引的**起始值为0**）来访问

```JavaScript
var arr = [1, 2, 3.14, 'Hello', null, true];
arr[0]; // 返回索引为0的元素，即1
arr[5]; // 返回索引为5的元素，即true
arr[6]; // 索引超出了范围，返回undefined
```

## 数组的操作
### 属性
#### length属性
> `length` 属性用于获取数组的长度

**直接给数组的length属性赋一个新的值会导致数组产生变化**

```JavaScript
var arr = [1, 2, 3];
arr.length; // 3
arr.length = 6;
arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
arr.length = 2;
arr; // arr变为[1, 2]
```

数组可以通过索引把对应的元素修改为新的值，如果通过索引赋值时，索引超过了范围，同样会导致数组产生变化

```JavaScript
var arr = ['A', 'B', 'C'];
arr[1] = 99;
arr; // arr现在变为['A', 99, 'C']
arr[5] = 'x';
arr; // arr变为['A', 99, 'C', undefined, undefined, 'x']
```

注意：**强烈建议，不要（修改数组的length属性或为超过范围的索引赋值）直接修改数组的大小，在访问索引时要确保索引不会越界。**

### 方法

#### indexOf
> `indexOf()` 用于搜索一个指定元素的位置，与字符串中的 `indexOf()` 方法类似

```JavaScript
var arr = [10, 20, '30', 'xyz'];
arr.indexOf(30); // 元素30没有找到，返回-1
arr.indexOf('30'); // 元素'30'的索引为2
```

#### slice
> `slice()` 用于截取数组的部分元素，然后返回一个新的数组，类似于String的 `substring()` 方法

+ slice() 的起止参数包括开始索引，不包括结束索引
+ 如果不给 slice() 传递任何参数，它就会从头到尾截取所有元素--相当于复制

```JavaScript
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']

var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
```

#### push 和 pop
> + `push()` 向Array的末尾添加若干元素，返回数组新的长度
> + `pop()` 则把Array的最后一个元素删除掉，返回删除的那个元素值

```JavaScript
var arr = [1, 2]; 
arr.push('A', 'B'); // 返回数组新的长度: 4 
arr; // [1, 2, 'A', 'B'] 
arr.pop(); // pop()返回'B' 
arr; // [1, 2, 'A'] 
arr.pop(); 
arr.pop(); 
arr.pop(); // 连续pop 3次 
arr; // [] 
arr.pop(); // 空数组继续pop不会报错，而是返回undefined 
arr; // []
```

#### unshift 和 shift
> + `unshift()` 向Array的头部添加若干元素，返回数组新的长度
> + `shift()` 则把Array的第一个元素删掉，返回删除的那个元素值

```JavaScript
var arr = [1, 2];
arr.unshift('A', 'B'); // 返回Array新的长度: 4
arr; // ['A', 'B', 1, 2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
arr; // []
arr.shift(); // 空数组继续shift不会报错，而是返回undefined
arr; // []
```

#### sort
> `sort()` 可以对当前Array进行排序，它会**直接修改当前Array的元素位置**，返回排序后的数组

直接调用时，按照默认顺序排序

```JavaScript
var arr = ['B', 'C', 'A']; 
arr.sort(); // ['A', 'B', 'C'] 
arr; // ['A', 'B', 'C']
```

#### reverse
> `reverse()` 将反转整个数组，返回反转后的数组

```JavaScript
var arr = ['one', 'two', 'three']; 
arr.reverse();  // ['three', 'two', 'one'] 
arr; // ['three', 'two', 'one']
```

#### splice
> splice() 可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素，返回删除的元素组成的数组

```JavaScript
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再从该位置添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```

#### concat
> concat() 把当前的Array和另一个Array连接起来，返回一个新的Array
> 
> concat() 方法并没有修改当前Array
> 
> concat()方法可以接收任意个元素和Array，并且自动把Array拆开，然后全部添加到新的Array里

```JavaScript
var arr = ['A', 'B', 'C'];
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
arr; // ['A', 'B', 'C']
```

#### join
> join() 把当前Array的每个元素都用指定的字符串连接起来，返回连接后的字符串

如果Array的元素不是字符串，将自动转换为字符串后再连接

```JavaScript
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'
```

## 多维数组

> 数组的某个元素又是一个Array，则可以形成多维数组（锯齿形）

```JavaScript
var arr = [[1, 2, 3], [400, 500, 600], '-'];
```
