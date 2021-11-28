---
title: ES6
date: 2021-10-10 9:48:05
tags: ES6
categories: 面试
cover: https://z3.ax1x.com/2021/10/27/5TTOL8.jpg
---

# Class

ES6 的`class`可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

```javascript
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

// 用 ES6 的class改写
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

构造函数的`prototype`属性，在 ES6 的“类”上面继续存在。

事实上，**类的所有方法都定义在类的`prototype`属性上面**。

```javascript
class Point {
  constructor() {
    // ...
  }

  toString() {
    // ...
  }

  toValue() {
    // ...
  }
}

// 等同于
Point.prototype = {
  constructor() {},
  toString() {},
  toValue() {},
};
```

`Object.assign()`方法可以很方便地一次向类添加多个方法。

```javascript
class Point {
  constructor(){
    // ...
  }
}

Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
});
```

在类的实例上面调用方法，其实就是调用原型上的方法。

```javascript
class B {}
const b = new B();

b.constructor === B.prototype.constructor // true
```

# Hash表

**定义**：哈希表是一种根据关键码去寻找值得数据映射结构，该结构通过关键码映射的位置去寻找存放值得地方。

就像查字典一样，如果要获取“按”字详细信息，就会去根据拼音an查找 拼音索引

首先去查an在字典的位置，查了得到“安”。

这过程就是键码映射，在公式里，通过key去查找f(key)。其中就是关键字（key），f()就是字典索引，也就是哈希函数，查到的页码4就是哈希值。

![img](https://images2015.cnblogs.com/blog/799055/201612/799055-20161222093541698-299037518.png)

## 为什么要用Hash

我们通常使用数组或者链表来存储元素，一旦存储的内容数量特别多，需要占用很大的空间，而且在**查找某个元素**是否存在的过程中，数组和链表都需要挨个循环比较，而通过 哈希 计算，可以大大**减少比较次数**。

哈希 其实是随机存储的一种优化，先进行分类，然后查找时按照这个对象的分类去找。**通过一次计算大幅度缩小查找范围**，自然比从全部数据里查找速度要快。

## 哈希函数

是一种映射关系，根据数据的关键词 key ，通过一定的函数关系，计算出该元素存储位置的函数。

表示为：address = H [key]

## 实现哈希表

下面是通过构造函数得到一个哈希表，在使用时只需实例化即可，且下面的功能较为丰富，在实际问题中，我们可以选择性的使用 。

```js
// 创建构造函数HashTable
function HashTable() {
    // 初始化哈希表的记录条数size
    var size = 0;

    // 创建对象用于接受键值对
    var res = {};

    // 添加关键字，无返回值
    this.add = function (key, value) {

        //判断哈希表中是否存在key，若不存在，则size加1，且赋值 
        if (!this.containKey(key)) {
            size++;
        }

        // 如果之前不存在，赋值； 如果之前存在，覆盖。
        res[key] = value;
    };

    // 删除关键字, 如果哈希表中包含key，并且delete返回true则删除，并使得size减1
    this.remove = function (key) {
        if (this.containKey(key) && (delete res[key])) {
            size--;
        }
    };

    // 哈希表中是否包含key，返回一个布尔值
    this.containKey = function (key) {
        return (key in res);
    };

    // 哈希表中是否包含value，返回一个布尔值
    this.containValue = function (value) {

        // 遍历对象中的属性值，判断是否和给定value相等
        for (var prop in res) {
            if (res[prop] === value) {
                return true;
            }
        }
        return false;
    };

    // 根据键获取value,如果不存在就返回null
    this.getValue = function (key) {
        return this.containKey(key) ? res[key] : null;
    };

    // 获取哈希表中的所有value, 返回一个数组
    this.getAllValues = function () {
        var values = [];
        for (var prop in res) {
            values.push(res[prop]);
        }
        return values;
    };

    // 根据值获取哈希表中的key，如果不存在就返回null
    this.getKey = function (value) {
        for (var prop in res) {
            if (res[prop] === value) {
                return prop;
            }
        }

        // 遍历结束没有return，就返回null
        return null;
    };

    // 获取哈希表中所有的key,返回一个数组
    this.getAllKeys = function () {
        var keys = [];
        for (var prop in res) {
            keys.push(prop);
        }
        return keys;
    };

    // 获取哈希表中记录的条数，返回一个数值
    this.getSize = function () {
        return size;
    };

    // 清空哈希表，无返回值
    this.clear = function () {
        size = 0;
        res = {};
    };
}
```

# Map存键值对(key-value)

也就是说，Object 结构提供了“字符串—值”的对应，**Map 结构提供了“值—值”的对应**，是一种更完善的 Hash 结构实现。

- 在Object中，key必须是简单的数据类型，而在Map中则可以是JavaScript支持的所有的数据类型，也就是说可以用一个Object来当作一个Map元素的key。
- Map元素的顺序遵循插入的顺序，而Object则没有这一特性
- Map继承自Object对象
- JSON 直接支持 Object，但不支持 Map
- Map 在存储大量元素的时候性能表现更好，特别是在代码执行时不能确定 key 的类型的情况

## 新建实例

Object 支持以下几种方法来创建新的实例：

```js
var obj = {...};
var obj = new Object();
var obj = Object.create(null);
```

Map 仅支持下面这一种构建方法：

```js
var map = new Map([
    ['foo', 1],
    ['bar', 2]
 ]); // map = {'foo' => 1, 'bar' => 2}
```

##  数据访问

Map 想要访问元素，可以使用 Map 本身的原生方法：

```js
map.get(1) // 2
```

Object 可以通过 . 和 [ ] 来访问

```js
obj.id;
obj['id'];
```

判断某个元素是否在 Map 中可以使用

```js
map.has(1);
```

判断某个元素是不是在 Object 中需要以下操作：

```js
obj.id === undefined;
// 或者
'id' in obj;
```

## 新增数据

Map 可以使用 set() 操作：

```js
map.set(key, value)  // 当传入的 key 已经存在的时候，Map 会覆盖之前的值
```

Object 新增一个属性可以使用：

```js
obj['key'] = value;
obj.key = value;    // object也会覆盖
```

## 删除数据

在 Object 中没有原生的删除方法，我们可以使用如下方式：

```js
delete obj.id;
// 下面这种做法效率更高
obj.id = undefined
// 需要注意的是，使用 delete 会真正的将属性从对象中删除，而使用赋值 undefined 的方式，仅仅是值变成了 undefined。属性仍然在对象上，也就意味着 在使用 for…in… 去遍历的时候，仍然会访问到该属性。
```

Map 有原生的 delete 方法来删除元素：

```js
var isDeleteSucceeded = map.delete(1);
console.log(isDeleteSucceeded ); // true
// 全部删除
map.clear();
```

## 获取size

Map 自身有 size 属性，可以自己维持 size 的变化。

Object 则需要借助 Object.keys() 来计算

```js
console.log(Object.keys(obj).length); 
```

# Array

## map()

- map()：通过指定函数处理数组的每个元素，并返回处理后的数组。
- map不会改变原数组，map不会检查空数组
- 传入的function可以有自己的三个形参，`currentValue`当前元素, `index`元素索引,`arr`元素所属数组对象，其中currentValue是必须的。

```javascript
 var numbers = [4, 9, 16, 25];
  
 function myFunction() {
     console.log(numbers.map(Math.sqrt)); // [2, 3, 4, 5]
 }
```

## some()

- some()：用于检测数组中的元素是否满足指定条件（函数提供)
- 如果有一个元素满足条件，则表达式返回true , 剩余的元素不会再执行检测
  如果没有满足条件的元素，则返回false
- some不会改变原数组，some不会检查空数组

```js
var ages = [3, 10, 18, 20];

function checkAdult(age) {
    return age >= 18;
}

function myFunction() {
    console.log(ages.some(checkAdult)); // true
}
```

## every()

- 用于检测数组所有元素是否都符合指定条件（通过函数提供）
- 数组中所有元素满足条件，则返回true；有一个元素不满足，则返回false
- some不会改变原数组，some不会检查空数组

```js
var ages = [32, 33, 16, 40];

function checkAdult(age) {
    return age >= 18;
}

function myFunction() {
    console.log(ages.every(checkAdult)); // false
}
```

## filter()

- 创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素
- filter会根据函数中的筛选条件将返回的结果组成一个新的数组并返回

```js
var ages = [32, 33, 16, 40];

function checkAdult(age) {
    return age >= 18;
}

function myFunction() {
    console.log(ages.filter(checkAdult)); // [32,33,40]
}
```

## from()

将伪数组或者可迭代对象转换成数组

```js
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

# Set

Set构造函数能创建Set对象，其可以存储任意类型的唯一值

```js
let mySet = new Set()

mySet.add(1)           // Set [ 1 ]
mySet.add(5)           // Set [ 1, 5 ]
mySet.add(5)           // Set [ 1, 5 ]
mySet.add('some text') // Set [ 1, 5, 'some text' ]
let o = {a: 1, b: 2}
mySet.add(o)           // Set [ 1, 5, 'some text', { a: 1, b: 2 } ]
```

在Set加入值得时候，不会发生类型转换，所以5和”5“是两个不同的值

向Set加入值时，认为NaN等于NaN，而===认为NaN不等于NaN，所以在加入Set时被视为一个值

两个空对象不相等的，所以在加入Set时被视为两个值

# 数组去重

```js
[...new Set(array)]
```

# 字符串去重

```js
[...new Set('ababbc')].join('')  // "abc"
```

# let/const

在 ES6 之前，是没有块级作用域的概念的。

**let 声明的变量只在 let 命令所在的代码块内有效。**

**const 声明一个只读的常量，一旦声明，常量的值就不能改变。**

1. let 声明的变量只在 let 命令所在的代码块 **{}** 内有效，在 **{}** 之外不能访问。

2. 使用 **let** 关键字声明的全局作用域变量不属于 window 对象（var属于）

   不能使用 window.carName 访问变量

3. 在相同的作用域或块级作用域中，不能使用var和let来重置 **let** 关键字声明的变量

**const**声明一个或多个常量，声明时必须进行初始化，且初始化后值不可修改

`const`定义常量与使用`let` 定义的变量相似：

- 二者都是块级作用域
- 都不能和它所在作用域内的其他变量或函数拥有相同的名称

两者还有以下两点区别：

- `const`声明的常量必须初始化，而`let`声明的变量不用
- const 定义常量的值不能通过再赋值修改，也不能再次声明。而 let 定义的变量值可以修改。



## 暂时性死区

进入当前作用域，在变量声明之前访问变量，是无法访问到的

**这是由于let/const没有变量提升**

- 我们平常所说的“变量提升“其实是指将「创建」和「初始化」这2个步骤都提升了

但是为什么报错信息是“Cannot access 'value' before initialization”，而不是我们常见的“value is not defined”呢，这2者有啥区别？

**因为变量被创建，但是还没有执行初始化，就开始执行代码了**

我们可以把 JS 变量分为「创建create、初始化initialize 和赋值assign」3个步骤

- 我们平常所说的“变量提升“其实是指将「创建」和「初始化」这2个步骤都提升了
- var存在变量提升，因为其同时提升了「创建」和「初始化」
- let/const不存在变量提升，实际上是因为let/const只提升了「创建」，而没有提升「初始化」。

同时，上面的报错也很好理解了：

- “value is not defined”是因为变量没有「创建」
- “Cannot access 'value' before initialization”是「创建」了变量，但没「初始化」

因此，**所谓暂时性死区，就是不能在初始化之前使用变量。**

# Object.create()

语法：

`Object.create(proto, [propertiesObject])`
方法创建一个新对象，使用现有的对象来提供新创建的对象的**__proto__**。

参数：

proto：必须，表示新建对象的原型对象。该参数可以是`null`， `对象`， 函数的`prototype属性` （创建空的对象时需传null , 否则会抛出`TypeError`异常）。

propertiesObject：可选，需要传入一个对象。对象中存在的属性描述符主要有两种：数据描述符和访问器描述符

```js
o = {};
// 以字面量方式创建的空对象就相当于:
o = Object.create(Object.prototype);

o = Object.create(Object.prototype, {
  // foo会成为所创建对象的数据属性
  foo: {
    writable:true,
    configurable:true,
    value: "hello"
  },
  // bar会成为所创建对象的访问器属性
  bar: {
    configurable: false,
    get: function() { return 10 },
    set: function(value) {
      console.log("Setting `o.bar` to", value);
    }
  }
});
```

省略了的属性特性默认为false,所以属性p是不可写,不可枚举,不可配置的

```js
// 创建一个以另一个空对象为原型,且拥有一个属性p的对象
o = Object.create({}, { p: { value: 42 } })
o.p = 24 // 不可写
o.q = 12 
for (var prop in o) { // 不可枚举
   console.log(prop)
}
//"q"

delete o.p // 不可配置的
//false
```

创建一个可写的,可枚举的,可配置的属性p

```js
o2 = Object.create({}, {
  p: {
    value: 42,
    writable: true,
    enumerable: true,
    configurable: true
  }
});
```

# Proxy

用于修改某些操作的默认行为，在语言层面做出修改，即**对编程语言进行编程**

Proxy可以理解成，在目标对象之前架设一层”拦截“，外界对该对象的访问都必须先通过这层拦截，因此可以**对外界的访问进行过滤和改写**。

```js
var proxy = new Proxy(target, handler);
```

Proxy对象的所有用法，都是上面这种形式，不同的只是handler参数的写法。

`new Proxy()`表示生成一个Proxy实例，`target`表示要拦截的对象，`handler`对象用来定制拦截行为。

```js
var handler = {
  get: function(target, name) {
    if (name === 'prototype') {
      return Object.prototype;
    }
    return 'Hello, ' + name;
  },

  apply: function(target, thisBinding, args) {
    return args[0];
  },

  construct: function(target, args) {
    return {value: args[1]};
  }
};

var fproxy = new Proxy(function(x, y) {
  return x + y;
}, handler);

fproxy(1, 2) // 1
new fproxy(1, 2) // {value: 2}
fproxy.prototype === Object.prototype // true
fproxy.foo === "Hello, foo" // true
```

下面是 Proxy 支持的拦截操作一览，一共 13 种。

- **get(target, propKey, receiver)**：拦截对象属性的读取，比如`proxy.foo`和`proxy['foo']`，三个参数依次是：目标对象、属性名和 proxy 实例本身（可选）。
- **set(target, propKey, value, receiver)**：拦截对象属性的设置，比如`proxy.foo = v`或`proxy['foo'] = v`，返回一个布尔值。
- **apply(target, object, args)**：拦截 Proxy 实例作为函数调用的操作，比如`proxy(...args)`、`proxy.call(object, ...args)`、`proxy.apply(...)`，三个参数依次是：目标对象、目标对象的上下文对象（`this`）和目标对象的参数数组。
- **construct(target, args)**：拦截 Proxy 实例作为构造函数调用的操作，比如`new proxy(...args)`。
- **has(target, propKey)**：拦截`propKey in proxy`的操作，返回一个布尔值。
- **deleteProperty(target, propKey)**：拦截`delete proxy[propKey]`的操作，返回一个布尔值。
- **ownKeys(target)**：拦截`Object.getOwnPropertyNames(proxy)`、`Object.getOwnPropertySymbols(proxy)`、`Object.keys(proxy)`、`for...in`循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而`Object.keys()`的返回结果仅包括目标对象自身的可遍历属性。
- **getOwnPropertyDescriptor(target, propKey)**：拦截`Object.getOwnPropertyDescriptor(proxy, propKey)`，返回属性的描述对象。
- **defineProperty(target, propKey, propDesc)**：拦截`Object.defineProperty(proxy, propKey, propDesc）`、`Object.defineProperties(proxy, propDescs)`，返回一个布尔值。
- **preventExtensions(target)**：拦截`Object.preventExtensions(proxy)`，返回一个布尔值。
- **getPrototypeOf(target)**：拦截`Object.getPrototypeOf(proxy)`，返回一个对象。
- **isExtensible(target)**：拦截`Object.isExtensible(proxy)`，返回一个布尔值。
- **setPrototypeOf(target, proto)**：拦截`Object.setPrototypeOf(proxy, proto)`，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。

# Promise

有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。

Promise对象特点：

- **对象的状态不受外界影响**。Promise对象代表一个异步操作，有三种状态：**`pending`（进行中）、`fulfilled`（已成功）和`rejected`（已失败）**。只有异步操作的结果，可以决定当前是哪一种状态。这也是`Promise`这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。
- **一旦状态改变，就不会再变**。Promise对象的状态改变，只有两种可能：从`pending`变为`fulfilled`和从`pending`变为`rejected`。只要这两种情况发生，就会一直保持这个结果，这时就成为resolved。
- 如果改变已经发生了，你再对`Promise`对象添加回调函数`.then()`，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

```javascript
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(100).then((value) => {
  console.log(value);
});
```

上面代码中，`timeout`方法返回一个`Promise`实例，表示一段时间以后才会发生的结果。过了指定的时间（`ms`参数）以后，`Promise`实例的状态变为`resolved`，就会触发`then`方法绑定的回调函数。

## Promise.prototype.then()

`then`方法是定义在原型对象`Promise.prototype`上的

为Promise实例添加状态改变时的回调函数

第一个参数是`resolved`状态的回调函数，第二个参数是`rejected`状态的回调函数，它们都是可选的。

`then`方法返回的是一个新的`Promise`实例（注意，不是原来那个`Promise`实例）。因此可以采用链式写法，即`then`方法后面再调用另一个`then`方法。

```javascript
getJSON("/post/1.json").then(function(post) {
  return getJSON(post.commentURL);
}).then(function (comments) {
  console.log("resolved: ", comments);
}, function (err){
  console.log("rejected: ", err);
});
```

上面代码中，第一个then方法指定的回调函数，返回的时另一个Promise对象。这时，第二个then方法指定的回调函数，就会等待这个新的Promsie对象状态发生变化。如果变为resolved，就调用第一个回调函数，；如果变为reject，就调用第二个回调函数。

## Promise.prototype.catch()

是.then(null, rejection) 或 .then(undefined, rejection) 的别名，用于指定发生错误的回调函数

一般来说，不要在`then()`方法里面定义 Reject 状态的回调函数（即`then`的第二个参数）

```js
// bad
promise
  .then(function(data) {
    // success
  }, function(err) {
    // error
  });

// good
promise
  .then(function(data) { //cb
    // success
  })
  .catch(function(err) {
    // error
  });
```

理由是第二种写法可以捕获前面`then`方法执行中的错误，也更接近同步的写法（`try/catch`）。

跟传统的`try/catch`代码块不同的是，如果没有使用`catch()`方法指定错误处理的回调函数，Promise 对象抛出的错误不会传递到外层代码，即不会有任何反应。

这就是说，Promise内部的错误不会影响到Promise外部的代码，通俗的说法就是”Promise会吃掉错误“

## Promise.prototype.finally()

不管Promise对象最后状态如何，都会执行的操作。该方法时ES2018引入标准的。

```js
promise
.then(res => {...})
.catch(err => {...})
.finally(() => {...})
```

finally方法里的操作，是与状态无关的，不依赖于Promise的执行结果

`finally`本质上是`then`方法的特例

```js
promise
.finally(() => {
    // 语句
})

// 等同于
promise
.then(
	res => {
        // 语句
        return res;
    },
    error => {
        throw error;
    }
)
```

## Promise.all()

用于将多个Promise实例，包装成一个新的Promise实例

```js
const p = Promise.all([p1, p2, p3]);
```

`p`的状态由`p1`、`p2`、`p3`决定，分成两种情况。

（1）只有`p1`、`p2`、`p3`的状态都变成`fulfilled`，`p`的状态才会变成`fulfilled`，此时`p1`、`p2`、`p3`的返回值组成一个数组，传递给`p`的回调函数。

（2）只要`p1`、`p2`、`p3`之中有一个被`rejected`，`p`的状态就变成`rejected`，此时第一个被`reject`的实例的返回值，会传递给`p`的回调函数。

**注意**，作为参数的Promise实例，自己定义了catch方法，那么它被rejected，也不会触发Promise.all()的catch方法。

```js
const p1 = new Promise((resolve, reject) => {
    resolve('hello');
})
.then(res => res)
.catch(err => err)

const p2 = new Promise((resolve, reject) => {
    throw new Error("报错了")；
})
.then(res => res)
.catch(err => err)

Promise.all([p1, p2])
.then(res => console.log(res))
.catch(err => console.log(err));
// ["hello", Error: 报错了]
```

上面代码中，p1会resolve，p2首先会rejected，但是p2有自己的catch方法，该方法返回的是一个新的Promise实例，p2实际指向的是这个实例，该实例执行完之后也会变成resolve，所以两个参数的实例都会说resolved，因此会调用then

如果p2没有自己的catch方法，就会调用Promise.all()的catch方法，输出Error：报错了

## Promise.race()

同样用于将多个Promise实例，包装成一个新的Promise实例

```js
const p = Promise.race([p1, p2, p3]);
```

只要p1、p2、p3之中有一个实例率先改变，p的状态就跟着改变。那个率先改变的Promise实例的返回值，就传递给p的回调函数。

## Promise.resolve()

将现有对象转为Promise对象

```javascript
Promise.resolve('foo')
// 等价于
new Promise(resolve => resolve('foo'))
```

（1）参数是一个Promise实例，原封不动地返回这个实例

（2）参数是一个thenable对象

thenable对象指的是具有then方法的对象

```js
let thenable = {
    then: function(resolve, reject) {
        resolve(42)
    }
}

let p1 = Promise.resolve(thenable);
p1.then(function (value) {
  console.log(value);  // 42
});
```

Promise.resolve()方法会将这个对象转为Promise对象，然后就立即执行thenable对象的then()

（3）参数不是具有`then()`方法的对象，或根本就不是对象，则`Promise.resolve()`方法返回一个新的 Promise 对象，状态为`resolved`。

```js
const p = Promise.resolve('Hello');

p.then(function (s) {
  console.log(s)
});
// Hello
```

（4）不带有任何参数，直接返回一个`resolved`状态的 Promise 对象。

所以，如果希望得到一个 Promise 对象，比较方便的方法就是直接调用`Promise.resolve()`方法。

```javascript
const p = Promise.resolve();

p.then(function () {
  // ...
});
```

上面代码的变量`p`就是一个 Promise 对象。

## Promise.reject()

返回一个新的 Promise 实例，该实例的状态为`rejected`

```javascript
const p = Promise.reject('出错了');
// 等同于
const p = new Promise((resolve, reject) => reject('出错了'))

p.then(null, function (s) {
  console.log(s)
});
// 出错了
```

# 箭头函数

1. `this`是静态的，始终指向函数声明时所在的作用域下的`this`的值
2. 不能作为构造函数去实例化对象
3. 不能使用`arguments`变量

适合与`this`无关的回调，定时器、数组的方法回调

不适合与`this`有关的回调，事件回调、对象的方法

# this绑定问题

## 隐式绑定

```js
function foo() { 
    console.log(this.bar); 
} 
var bar = "bar1"; 
var o2 = {bar: "bar2", foo: foo}; 
var o3 = {bar: "bar3", foo: foo}; 
foo();            // "bar1" – 默认绑定
o2.foo();          // "bar2" – 隐式绑定
o3.foo();          // "bar3" – 隐式绑定
```

## 显示绑定

```js
function foo() { 
console.log(this.bar); 
} 
var bar = "bar1"; 
var obj = {bar: "bar2"}; 

foo();          // "bar1"   默认绑定
foo.call(obj);     // "bar2"  显式绑定，使用obj作为"this" 
```

## new绑定

```js
function foo() { 
    this.baz = "baz"; 
    console.log(this.abc + " " + baz); 
} 
var abc = "bar"; 
var baz = new foo();  // undefined undefined
```

## 箭头函数

箭头函数会无视以上所有的规则，this始终指向**函数声明时所在的作用域**下的`this`的值

```js
function Person(){
  this.age = 0;
  setTimeout(function () {
    console.log(this.age);     // 输出undefined
  }, 1000);
}
var p = new Person();
```

使用了箭头函数，this就会使用Person中的this，因此输出10。

```js
function Person(){
  this.age = 10;
  setTimeout(()=> {
    console.log(this.age);     // 输出10
  }, 1000);
}
var p = new Person();
```

## 绑定优先级

如果多重绑定规格都适用，那么绑定规则的优先级顺序是这样的：

1. 箭头函数
2. 关键字new调
3. 显式绑定
4. 隐式绑定
5. 默认绑定

# rest参数

ES6引入`rest`参数，用于获取函数的实参，用来代替arguments

ES5获取实参的方式

```javascript
function data() {
    console.log(arguments);
}
data('a','b','c') 
```

rest参数

```js
function data(...args) {
    console.log(args)
}
data('a','b','c') // ['a','b','c'] Array
```

rest参数必须放到参数最后

```js
function fn(a, b, ...args) {
    console.log(a);
    console.log(b);
    console.log(args);
}
fn(1,2,3,4,5,6) 
// 1
// 2
// [3, 4, 5, 6]
```

## 扩展运算符 `...`

`...`扩展运算符能将【数组】转换为都好分隔的 【参数列表】

```js
const tfboys = ['a', 'b', 'c']

function fn() {
    console.log(argument)
}

fn(...tfboys);  // fn('a', 'b', 'c')
fn(tfboys); // fn(['a', 'b', 'c'])
```

## 数组的合并

```js
const arr1 = ['a', 'b']
const arr2 = ['c', 'd']

const arr3 = arr1.concat(arr2)  // ES5
const arr3 = [...arr1, ...arr2] // ES6的扩展运算符

console.log(arr3) // ['a', 'b', 'c', 'd']
```

## 数组的克隆

```js
const arr1 = ['a', 'b']
const arr2 = [...arr1]
console.log(arr2) // ['a', 'b']
```

## 将伪数组转为真正的数组

```js
const divs = document.querySelectorAll('div');
const divArr = [...divs]
console.log(divs) // Object
console.log(divArr) // Array
```

# 生成器

```js
function * gen() {
    console.log(111)
    yield '123'; // yield 函数代码的分隔符
    console.log(222)
    yield '456';
    console.log(333)
    yield '789';
    console.log(444)
}

let iterator = gen() // 执行获取迭代器对象
iterator.next() // 111
iterator.next() // 222
iterator.next() // 333
iterator.next() // 444

for (let v of gen()) {
    console.log(v)
    // 111
    // 123
    // 222
    // 456
    // 333
    // 789
    // 444
}

```

# async 函数

返回的结果是一个Promise类型的对象

对象的状态由函数内部的return决定

- return 成功的Promise 则async 函数就是一个成功的Promise
- throw 抛出错误 则async 函数就是一个失败的Promise
- return 非Promise类型的数据 则async 函数就是一个成功的Promise

```js
async function fn() {
    // 返回一个字符串
    // return 'gwl'
    
    // 返回的结果不是一个Promise类型的对象，async函数返回的记过就是成功的Promise对象
    // return
    
    // 抛出错误，返回的结果是一个失败的Promise
    // throw new Error('出错啦！')
    
    // 返回的结果如果是一个Promise对象
    return new Promise((resolve, reject) => {
        resolve('成功')
        // reject('失败')
    })
}

const result = fn()
result.then(value => {
    console.log(value); // 成功
}, reason => {
    console.warn(reason)
})
```

# await表达式

await必须写在async函数中

await右侧的表达式一般为promise对象

await返回的是一个promise成功的值

await的promise失败了,就会抛出异常,需要通过try...catch捕获处理

```js
const p = new Promise((resolve, reject) => {
    // resolve("用户数据")
    reject("失败啦!")
})

async function main() {
    try {
        let result = await p
        console.log(result) //用户数据
    } catch(e) {
        console.log(e) //失败啦!
    }
}
```

如果它等到的不是一个 Promise 对象，那 await 表达式的运算结果就是它等到的东西。

如果它等到的是一个 Promise 对象，await 就忙起来了，它会阻塞后面的代码，等着 Promise 对象 resolve，然后得到 resolve 的值，作为 await 表达式的运算结果。

看到上面的阻塞一词，心慌了吧……放心，**这就是 await 必须用在 async 函数中的原因**

async 函数调用不会造成阻塞，它内部所有的阻塞都被封装在一个 Promise 对象中异步执行。

# async/await 帮了啥

async 会将其后的函数（函数表达式或 Lambda）的返回值封装成一个 Promise 对象，而 await 会等待这个 Promise 完成，并将其 resolve 的结果返回出来。

现在举例，用 `setTimeout` 模拟耗时的异步操作，先来看看不用 async/await 会怎么写

```javascript
function takeLongTime() {
    return new Promise(resolve => {
        setTimeout(() => resolve("long_time_value"), 1000);
    });
}

takeLongTime().then(v => {
    console.log("got", v);
});
```

如果改用 async/await 呢，会是这样

```javascript
function takeLongTime() {
    return new Promise(resolve => {
        setTimeout(() => resolve("long_time_value"), 1000);
    });
}

async function test() {
    const v = await takeLongTime();
    console.log(v);
}

test();
```

眼尖的同学已经发现 `takeLongTime()` 没有申明为 `async`。实际上，`takeLongTime()` 本身就是返回的 Promise 对象，加不加 `async` 结果都一样

# async与await封装AJAX请求

```js
function sendAJAX(url) {
      return new Promise((resolve, reject) => {
        const x = new XMLHttpRequest()
        x.open('GET', url)
        x.send() 
        x.onreadystatechange = function () {
          if (x.readyState === 4) {
            if (x.status >= 200 && x.status < 300) {
              // 成功啦
              resolve(x.response)
            } else {
              reject(x.status)
            }
          }
        }
      })
    }

    // promise then 方法测试
    sendAJAX("https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata").then(value => {
      console.log(value);
    }, reason => {})

    // async 与 await 测试
    async function main() {
      let res = await sendAJAX("https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata")
      console.log(res);
    } 
    main()
```

# Reflect

Reflect是一个内置的对象，它提供拦截 JavaScript 操作的方法。

与大多数全局对象不同，Reflect没有构造函数，不能与一个new运算符一起使用。

Reflect的所有属性和方法都是静态的（就像Math对象）。

## apply

[`Reflect.apply(target, thisArgument, argumentsList)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/apply)

对一个函数进行调用操作，同时可以传入一个数组作为调用参数。和 [`Function.prototype.apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) 功能类似。

## construct

[`Reflect.construct(target, argumentsList[, newTarget\])`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/construct)

对构造函数进行 [`new` ](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)操作，相当于执行 `new target(...args)`。

## defineProperty

[`Reflect.defineProperty(target, propertyKey, attributes)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/defineProperty)

和 [`Object.defineProperty()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 类似。如果设置成功就会返回 `true`

## deleteProperty

[`Reflect.deleteProperty(target, propertyKey)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/deleteProperty)

作为函数的[`delete`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/delete)操作符，相当于执行 `delete target[name]`。

## enumerate

`Reflect.enumerate()`该方法会返回一个包含有目标对象身上所有可枚举的自身字符串属性以及继承字符串属性的迭代器，`for...in`操作遍历到的正是这些属性。

## get

[`Reflect.get(target, propertyKey[, receiver\])`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/get)

获取对象身上某个属性的值，类似于 `target[name]。`

## getOwnPropertyDescriptor

[`Reflect.getOwnPropertyDescriptor(target, propertyKey)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/getOwnPropertyDescriptor)

类似于 [`Object.getOwnPropertyDescriptor()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor)。如果对象中存在该属性，则返回对应的属性描述符, 否则返回 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined).

## getPrototypeOf

[`Reflect.getPrototypeOf(target)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/getPrototypeOf)

类似于 [`Object.getPrototypeOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/GetPrototypeOf)。

## has

[`Reflect.has(target, propertyKey)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/has)

判断一个对象是否存在某个属性，和 [`in` 运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/in) 的功能完全相同。

## isExtensible

[`Reflect.isExtensible(target)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/isExtensible)

类似于 [`Object.isExtensible()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/isExtensible).

## ownKeys

[`Reflect.ownKeys(target)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/ownKeys)

返回一个包含所有自身属性（不包含继承属性）的数组。(类似于 [`Object.keys()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys), 但不会受`enumerable影响`).

## preventExtensions

[`Reflect.preventExtensions(target)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/preventExtensions)

类似于 [`Object.preventExtensions()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)。返回一个[`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Boolean)。

## set

[`Reflect.set(target, propertyKey, value[, receiver\])`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/set)

将值分配给属性的函数。返回一个[`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Boolean)，如果更新成功，则返回`true`。

## setPrototypeOf

[`Reflect.setPrototypeOf(target, prototype)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/setPrototypeOf)

设置对象原型的函数. 返回一个 [`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Boolean)， 如果更新成功，则返回`true。`