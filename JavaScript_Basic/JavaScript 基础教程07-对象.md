# JavaScript 基础教程07-对象

> JavaScript 的对象是一组由**键-值对**组成的无序集合。**对象的键都是字符串类型，值可以是任意数据类型**。

## 对象的创建

```JavaScript
var person = {
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    city: 'Beijing',
    hasCar: true,
    zipcode: null,
    'middle-school': 'No.1 Middle School' // 属性名包含特殊字符，就必须用''括起来
};
```

## 对象内属性的访问
> 要获取一个对象的属性，可以用**对象变量.属性名**（`object.prop`）的方式，也可以用**对象变量['属性名']**（`object['prop']`）的方式
 
在编写 JavaScript 代码的时候，属性名尽量使用标准的变量名，这样就可以直接通过object.prop的形式访问一个属性。

```JavaScript
person.name; // 'Bob'
person.zipcode; // null
person['middle-school']; // 'No.1 Middle School'，访问包含特殊字符的属性时无法使用.操作符，必须用['xxx']来访问
person.address; // 访问不存在的属性不报错，而是返回undefined
```

## 对象内属性的操作
> 由于 JavaScript 的对象是动态类型，你可以自由地给一个对象添加或删除属性

```JavaScript
var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
xiaoming.name; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
'name' in xiaoming; // false
'toString' in xiaoming; // true，用in判断一个属性存在时，需要注意这个属性可能是继承得到
xiaoming.hasOwnProperty('toString'); // false，判断一个属性是否是xiaoming自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法
```

