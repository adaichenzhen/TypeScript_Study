# JavaScript 基础教程09-Map和Set

## Map
> 为了解决 JavaScript 的对象的键必须是字符串的问题，ES6 规范引入了新的数据类型 `Map`。
> 
> `Map` 是一组键值对的结构，且键唯一（如果多次对一个 key 放入 value，后面的值会把前面的值冲掉）。

初始化 Map 需要一个二维数组（相当于 key-value 的一维数组），或者直接初始化一个空 Map。

```JavaScript
var m1 = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]); 
m1.get('Michael'); // 95

var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined
```

## Set
> `Set` 也是 ES6 标准新增的数据类型。`Set` 和 `Map` 类似，也是一组 `key` 的集合（key 不能重复，重复元素在 `Set` 中自动被过滤），但不存储 `value`。

初始化 `Set` 需要一个一维数组（相当于 key 的一维数组），或者直接初始化一个空 Set。

```JavaScript
var s2 = new Set([1, 2, 3]); // 含1, 2, 3

var s = new Set([1, 2, 3, 3, '3']);
s; // Set {1, 2, 3, "3"}

s.add(4); // 添加元素 
s; // Set {1, 2, 3, 4} 
s.add(4); // 添加重复元素 
s; // 仍然是 Set {1, 2, 3, 4}

s.delete(3); // 删除元素
s; // Set {1, 2, 4}
```

## iterable
> 遍历 Array 可以采用下标循环，遍历 Map 和 Set 就无法使用下标。为了统一集合类型，ES6 标准引入了新的 iterable 类型，Array、Map 和 Set 都属于 iterable 类型。 

具有 iterable 类型的集合可以通过新的 `for ... of` 循环来遍历。（`for ... of` 循环也是 ES6 引入的新的语法）

### for ... in 

> `for ... in` 循环由于历史遗留问题，遍历的实际上是对象的属性名称（Array 也是对象）

 `for ... in` 循环将把 name 包括在内，但 Array 的 length 属性却不包括在内 

```JavaScript
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x in a) {
    console.log(x); // '0', '1', '2', 'name'
}
```
 
### for ... of 

> `for ... of` 循环只循环集合本身的元素

```JavaScript
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x of a) {
    console.log(x); // 'A', 'B', 'C'
}
```

### forEach 

> `forEach()` 方法接收一个函数，每次迭代就自动回调该函数

```JavaScript
a.forEach(function (element, index, array) {
    console.log(element + ', index = ' + index);
});

// 如果 a 是一个 Array：element 指向当前元素的值，index 指向当前索引，array 指向 Array 对象本身
// 如果 a 是一个 Set：element 指向当前元素的值，index 也指向当前元素的值，array 指向 Set 对象本身
// 如果 a 是一个 Map：element 指向当前元素的 value，index 指向当前元素的 key，array 指向 Map 对象本身
```
