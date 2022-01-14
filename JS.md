---
title: JS
date: 2021-10-09 9:48:05
tags: JS面试题
categories: 面试
cover: https://s3.ax1x.com/2020/12/19/rNJiZD.png
---

# 闭包

一个函数以及创建该函数的词法环境组合而成。这个环境包含了闭包创建时所能访问的所有局部变量。

其实闭包是可以重用一个对象，又保护对象不被篡改的一种机制

**当某个函数的作用域链还引用着其他函数的活动对象时，就会形成闭包**

## 闭包产生的原因

当某个函数的作用域链还引用着其他函数的活动对象时，其他函数一直没有被释放，导致闭包产生

**闭包**让内部函数总是可以访问其所在的外部函数中声明的参数和变量，即使在其外部函数被返回（寿命终结）了之后。

- 局部变量会常驻在内存中；
- 可以避免使用全局变量，防止全局变量污染；
- 会造成内存泄漏（有一块内存空间被长期占用，而不被释放）

**通过闭包，我们可以在其他的执行上下文中，访问到函数的内部变量**

```javascript
function foo() {
  var a = 20;
  var b = 30;
  function bar() {
    return a + b;
  }
  return bar;
}
var bar = foo();
bar();
```

上面的例子，首先有执行上下文foo，在foo中定义了函数bar，而通过对外返回bar的方式让bar得以执行。当bar执行时，访问了foo内部的变量a，b。因此这个时候闭包产生。

## 闭包的应用 

1、原生的**setTimeout**传递的第一个函数不能带参数，通过闭包可以实现传参效果

```js
function f1(a) {
    function f2() {
        console.log(a)
    }
    return f2
}
setTimeout(f1(1), 1000)
```

2、**回调**，定义行为，然后把它关联到某个用户事件上。代码会作为一个回调绑定到事件

我们想在页面上添加一些可以调整字号的按钮：

```js
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);
```

`size12`，`size14` 和 `size16` 三个函数将分别把 `body` 文本调整为 12，14，16 像素。我们可以将它们分别添加到按钮的点击事件上。如下所示：

```js
document.getElementById('size-12').onclick = size12;
document.getElementById('size-14').onclick = size14;
document.getElementById('size-16').onclick = size16;
```

3、**封装私有变量**

如下面代码：用js创建一个计数器，在返回的对象中，实现了一个闭包，该闭包携带了局部变量sum，并且从外部代码无法访问到变量sum

```js
function f1() {
    var sum = 0;
    var obj = {
       inc:function () {
           sum++;
           return sum;
       }
    };
    return obj;
}
let result = f1();
console.log(result.inc());//1
console.log(result.inc());//2
console.log(result.inc());//3
```



# 原型

JavaScript规定，每一个构造函数都有一个`prototype`属性，指向另一个对象。这个对象的所有属性和方法，都会被构造函数所拥有。

这也就意味着，我们可以把所有对象实例需要共享的属性和方法直接定义在 `prototype` 对象上。

![alt](data:image/png;base64,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)

构造函数的 `prototype` 对象默认都有一个 `constructor` 属性，指向 `prototype` 对象所在函数。

```js
console.log(F.prototype.constructor === F) // => true
```

通过构造函数得到的实例对象内部会包含一个指向构造函数的 `prototype` 对象的指针 `__proto__`。

```js
var instance = new F()
console.log(instance.__proto__ === F.prototype) // => true
```

`__proto__` 是非标准属性。  

## 原型链

- 当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，就会去它的原型对象里找这个属性
- 这个原型对象又会有自己的原型，于是这样一直找下去，这就是原型链的概念
- 原型链的尽头一般都是`Object.prototype`，这就是为什么新建的对象可以使用`toString()`等方法的原因

## 更简单的原型语法

我们注意到，前面例子中每添加一个属性和方法就要敲一遍 `Person.prototype` 。
为减少不必要的输入，更常见的做法是用一个包含所有属性和方法的对象字面量来重写整个原型对象

这样做的好处就是为 `Person.prototype` 添加成员简单了，但是也会带来一个问题，那就是原型对象丢失了 `constructor` 成员。

所以，我们为了保持 `constructor` 的指向正确，建议的写法是：

```js
function Person (name, age) {
  this.name = name
  this.age = age
}

Person.prototype = {
  constructor: Person, // => 手动将 constructor 指向正确的构造函数
  type: 'human',
  sayHello: function () {
    console.log('我叫' + this.name + '，我今年' + this.age + '岁了')
  }
}
```

# 作用域

![ä½ç¨å](https://images0.cnblogs.com/blog/138012/201409/241708372951952.png)

作用域有上下级关系，上下级关系的确定就看函数是在那个作用域下创建的。

如上，fn作用域下创建了bar作用域，那么fn作用域就是bar作用域的上级。

## 作用域链

如果当前作用域中没有查到值，就会向上级作用域去查，直到查到全局作用域，这个查找的过程形成的链。

变量取值：**到创建 这个变量 的函数的作用域中取值**

```js
var x = 10;

function fn(){
    console.log(x);
}

function show(f){
    var x = 20;
    (function(){
       f();    // 10
    })()  
}

show(fn);
```

# 继承

## 原型链继承

让新实例的原型等于父类的实例

```js
function Person(){
    this.name = 'Hello world';
}

Person.prototype.getName = function(){
    console.log(this.name);
}

function Child(){

}

Child.prototype = new Person();
var child1 = new Child();
child1.getName();  // Hello World
```

缺点：

1. 新实例无法向父类构造函数传参。
2. 继承单一。
3. 所有新实例都会共享父类实例的属性。（原型上的属性是共 享的，一个实例修改了原型属性，另一个实例的原型属性 也会被修改！）

## 构造函数继承

用.call()和.apply()将父类构造函数引入子类函数（在子类 函数中做了父类函数的自执行（复制））

```js
function Person(){
    this.name = 'xiaoming';
    this.colors = ['red', 'blue', 'green'];
}

Person.prototype.getName = function(){
    console.log(this.name);
}

function Child(age) {
    Person.call(this);
    this.age = age
}

var child1 = new Child(23);
var child2 = new Child(12);
child1.colors.push('yellow');

console.log(child1.name);  // xiaoming
console.log(child1.colors); // ["red", "blue", "green", "yellow"]
console.log(child2.colors); // ["red", "blue", "green"]
```

缺点：

1. 只能继承父类构造函数的属性。
2. 无法实现构造函数的复用。（每次用每次都要重新调用）
3. 每个新实例都有父类构造函数的副本，臃肿。

## 组合继承（组合原型链继承和借用构造函数继承）

结合了两种模式的优点，传参和复用

```js
function Parent(name){
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
}

Parent.prototype.getName = function(){
    console.log(this.name);
}

function Child(name,age){
    Parent.call(this,name);// 第二次调用 Parent()
    this.age = age;
}

Child.prototype = new Parent(); // 第一次调用 Parent()

var child1 = new Child('xiaopao',18);
var child2 = new Child('lulu',19);
```

缺点：

调用了两次父类构造函数（耗内存），子类的构造函数会代替原型上的那个父类构造函数。

## 原型式继承

用一个函数包装一个对象，然后返回这个函数的调用，这个函数就变成了个可以随意增添属性的实例或对象。object.create()就是这个原理。

```js
function CreateObj(o) {
    function F(){}
    F.prototype = o
    console.log(F.prototype.constructor === Object); // true
    return new F()
}

var person = {
    name: 'xiaopao',
    friend: ['daisy','kelly']
}

var person1 = CreateObj(person)
var person2 = CreateObj(person)

person1.name = 'person1'
console.log(person2.name); // xiaopao

person1.friend.push('taylor')
console.log(person2.friend); // ["daisy", "kelly", "taylor"]
console.log(person); // {name: "xiaopao", friend: Array(3)}

person1.friend = ['lulu']
console.log(person1.friend); // ["lulu"]
console.log(person2.friend); //  ["daisy", "kelly", "taylor"]
// 注意： 这里修改了person1.name的值，person2.name的值并未改变，并不是因为person1和person2有独立的name值
// 而是person1.name='person1'是给person1添加了name值，并非修改了原型上的name值
// 因为找对象上的属性时，总是先找实例上对象，没有找到的话再去原型对象上的属性。实例对象和原型对象上如果有同名属性，总是先取实例对象上的值
```

缺点：

1. 所有实例都会继承原型上的属性。
2. 无法实现复用。（新实例属性都是后面添加的）

## 寄生式继承

就是给原型式继承外面套了个壳子

```js
function CreateObj(o){
    function F(){};  // 创建一个构造函数F
    F.prototype = o;
    return new F();
}

var ob = {
    name: 'xiaopao',
    friends: ['lulu','huahua']
}

function CreateChild(o){
    var newob = CreateObj(o); 
    // 创建对象 或者用 var newob = Object.create(o)
    newob.sayName = function(){ // 增强对象
        console.log(this.name);
    }
    return newob; // 指定对象
}

var p1 = CreateChild(ob);
p1.sayName(); // xiaopao 
```

缺点：没用到原型，无法复用

## 寄生组合式继承

修复了组合继承的问题

```js
function Parent(name){
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
}

Parent.prototype.sayName = function(){
    console.log(this.name);
}

function Child(name,age){
    Parent.call(this,name); 
    this.age = age;
}

function CreateObj(o){
    function F(){};
    F.prototype = o;
    return new F();
}

// 组合继承中 Child.prototype = new Parent(); 这里换成下面
function prototype(child, parent) {
    var prototype = CreateObj(parent.prototype);
    prototype.constructor = child;
    child.prototype = prototype;
}
prototype(Child, Parent)

var child1 = new Child('xiaopao', 18);
console.log(child1)
```

## class继承

Class 可以通过`extends`关键字实现继承

```javascript
class Point {
}

class ColorPoint extends Point {
}
```

上面代码定义了一个`ColorPoint`类，该类通过`extends`关键字，继承了`Point`类的所有属性和方法。但是由于没有部署任何代码，所以**这两个类完全一样**，等于复制了一个`Point`类。

```js
class ColorPoint extends Point {
    constructor(x, y, color) {
        super(x, y);
        this.color = color;
    }
    toString() {
        return this.color + ' ' + super.toString // 调用父类的toString()
    }
}
```

子类必须在`constructor`方法中调用`super`方法，否则新建实例时会报错。

这是因为子类自己的`this`对象，必须先通过父类的构造函数完成塑造，得到与父类同样的实例属性和方法，然后再对其进行加工，加上子类自己的实例属性和方法。**如果不调用`super`方法，子类就得不到`this`对象。**

```javascript
// 如果子类没有定义`constructor`方法，这个方法会被默认添加，代码如下。也就是说，不管有没有显式定义，任何一个子类都有`constructor`方法。
class ColorPoint extends Point {
}

// 等同于
class ColorPoint extends Point {
  constructor(...args) {
    super(...args);
  }
}
```

ES5的继承，实质是先创造子类的实例对象`this`，然后再将父类的方法添加到`this`上面（`Parent.apply(this)`）。

ES6的继承机制完全不同，实质是先将父类实例对象的属性和方法，加到`this`上面（所以必须先调用`super`方法），然后再用子类构造函数修改`this`。

# JS语言特点

1. 是一种解释型的脚本语言，在程序的运行过程中逐行进行解释。
2. 是一种基于对象的脚本语言，它不仅可以创建对象，也能使用现有的对象。
3. 采用的是弱类型的变量类型，对使用的数据未做出严格的要求。
4. 是一种事件驱动的脚本语言，它不需要经过Web服务器就可以对用户的输入做出响应。
5. 具有跨平台性，不依赖于操作系统，仅需浏览器的支持

# JS基础数据类型

ES5：Number、String、Boolean、undefined、object、Null

ES6 中新增了一种 Symbol。这种类型的对象永不相等，即始创建的时候传入相同的值，可以解决属性名冲突的问题，做为标记。

ES11 新增 bigInt。是指安全存储、操作任意长的整数。

Object 中包含了Data、function、Array

NaN是Number中的一种，用 isNaN（） 检测是否是非数值型。

Number(‘as’) 输出 NaN ？NaN == NaN 为什么是 false。其实 js 规定的NaN 不等于NaN。

# typeof和instanceof

**typeof**运算符返回一个用来表示表达式的数据类型的字符串，值包括如下几种：

1. 'undefined'       --未定义的变量或值

2. 'boolean'         --布尔类型的变量或值

3. 'string'           --字符串类型的变量或值

4. 'number'         --数字类型的变量或值

5. 'object'          --对象类型的变量或值，或者null(这个是js历史遗留问题，将null作为object类型处理)

6. 'function'         --函数类型的变量或值

**typeof`在判断`null`、`array`、`object`以及函数实例`（new + 函数）`时，得到的都是`object**

有时我们需要判断该实例是否为某个对象的实例，那么这个时候需要用到instanceof运算符。

**instanceof用来检测某个对象是不是另一个对象的实例。**

官方的话：该运算符用来测试一个对象在其原型链中是否存在一个构造函数prototype属性

# 检测数组类型的方法 

instanceof 操作符

```js
arr instanceof Array  // true/false
```

对象的constructor属性

```js
arr.constructor === Array  // true/false
```

Array.isArray()检验值是否为数组

```js
Array.isArray(arr)  // true/false
```

# Object.prototype.toString.call()

调用Object**原型上的toString方法（返回对象的具体类型）**

typeof`在判断`null`、`array`、`object`以及函数实例`（new + 函数）`时，得到的都是`object

使用typeof 无法准确判断一个对象变量

```js
console.log(Object.prototype.toString.call("jerry"));//[object String]
console.log(Object.prototype.toString.call(12));//[object Number]
console.log(Object.prototype.toString.call(true));//[object Boolean]
console.log(Object.prototype.toString.call(undefined));//[object Undefined]
console.log(Object.prototype.toString.call(null));//[object Null]
console.log(Object.prototype.toString.call({name: "jerry"}));//[object Object]
console.log(Object.prototype.toString.call(function(){}));//[object Function]
console.log(Object.prototype.toString.call([]));//[object Array]
console.log(Object.prototype.toString.call(new Date));//[object Date]
console.log(Object.prototype.toString.call(/\d/));//[object RegExp]
function Person(){};
console.log(Object.prototype.toString.call(new Person));//[object Object]
```

toString方法返回反映这个对象的字符串

```js
console.log("jerry".toString());//jerry
console.log((1).toString());//1
console.log([1,2].toString());//1,2
console.log(new Date().toString());//Wed Dec 21 2016 20:35:48 GMT+0800 (中国标准时间)
console.log(function(){}.toString());//function (){}
console.log(null.toString());//error
console.log(undefined.toString());//error
```

obj.toString()的结果和Object.prototype.toString.call(obj)的结果不一样，这是为什么？

- 因为toString为Object的原型方法，而Array、Function等类型作为Object的实例，都重写了toString方法。
- 根据原型链的知识，不同对象类型调用toString方法时，调用的是重写后的toString方法（Function类型返回内容为函数体的字符串，Array类型返回元素组成的字符串.....），而不会去调用Object**原型上的toString方法（返回对象的具体类型）**
- 因此想要得到对象的具体类型，应该调用Object上原型toString方法。

验证：

如果将数组的toString方法删除

```js
var arr=[1,2,3];
console.log(Array.prototype.hasOwnProperty("toString"));//true
console.log(arr.toString());//1,2,3
delete Array.prototype.toString;//delete操作符可以删除实例属性
console.log(Array.prototype.hasOwnProperty("toString"));//false
console.log(arr.toString());//"[object Array]"
```

删除了后，因为Array没有了toString方法，则需要沿着原型链，调用Object的toString方法。

# DOM事件模型

DOM事件模型分为捕获和冒泡。一个事件发生后，会在子元素和父元素之间传播（propagation）。这种传播分成三个阶段。

1. 捕获阶段：事件从window对象自上而下向目标节点传播的阶段；
2. 目标阶段：真正的目标节点正在处理事件的阶段；
3. 冒泡阶段：事件从目标节点自下而上向window对象传播的阶段。

![img](https://images2015.cnblogs.com/blog/740839/201609/740839-20160910153551644-925968915.jpg)

## 事件冒泡

而事件冒泡的流程刚好是事件捕获的逆过程。

指在一个对象上触发某类事件，如果此对象绑定了事件，就会触发事件。如果没有，就会像这个对象的父级对象传播，最终父级对象触发了事件。

### 阻止冒泡

```js
evt.stopPropagation()    // 无法阻止 IE 低版本事件冒泡；
evt.cancelBubble = true  // 兼容 IE 低版本冒泡；
```



## 事件捕获(委托)

本质上是利用了浏览器事件冒泡的机制。

1. 事件先从window对象
2. 然后再到document（对象），
3. 然后是html标签（通过document.documentElement获取html标签）
4. 然后是body标签（通过document.body获取body标签）
5. 然后按照普通的html结构一层一层往下传，最后到达目标元素

### 事件委托的应用

在有很多子节点需要绑定事件，性能会很差。这时候就需要使用冒泡，在父节点绑定事件，通过事件委托机制，在点击子节点时，通过冒泡去获取。

例如，有一个列表需要绑定点击事件，每一个列表项点击都需要返回不同的结果。

传统写法会利用for循环遍历列表，为每一个列表元素绑定点击事件，这样会性能不好

改用事件委托：

```html
<ul id="color-list">
  <li>red</li>
  <li>yellow</li>
  <li>blue</li>
  <li>green</li>
  <li>black</li>
  <li>white</li>
</ul>
<script>
(function () {
  var color_list = document.getElementByid('color-list');
  color_list.addEventListener('click', showColor, true); // 事件句柄在捕获阶段执行
  function showColor(e) {
    var x = e.target;
    if (x.nodeName.toLowerCase() === 'li') {
      alert(x.innerHTML);
    }
  }
})();
</script>
```

## Event对象的应用

1. event存在的环境是绑定事件中；
2. event是一个对象，代表事件的状态；


### event. preventDefault()

如果调用这个方法，默认事件行为将不再触发。

很多时候我们使用a标签仅仅是想当做一个普通的按钮，点击实现一个功能，不想页面跳转，也不想瞄点定位。

```html
//方法一：
<a href="javascript:;">链接</a>
```

也可以通过JS方法来阻止，给其click事件绑定方法，当我们点击A标签的时候，先触发click事件，其次才会执行自己的默认行为

```html
//方法二:
<a id="test" href="http://www.cnblogs.com">链接</a>
<script>
test. = function(e){
    e = e || window.event;
    return false;
}
</script>

//方法三：
<a id="test" href="http://www.cnblogs.com">链接</a>
<script>
test. = function(e){
    e = e || window.event;
    e.preventDefault();
}
</script>
```

输入框最多只能输入六个字符，如何实现？

```html
// 例5
 <input type="text" id='tempInp'>
 <script>
    tempInp.onkeydown = function(ev) {
        ev = ev || window.event;
        let val = this.value.trim() //trim去除字符串首位空格（不兼容）
        // this.value=this.value.replace(/^ +| +$/g,'') 兼容写法
        let len = val.length
        if (len >= 6) {
            this.value = val.substr(0, 6);
            //阻止默认行为去除特殊按键（DELETE\BACK-SPACE\方向键...）
            let code = ev.which || ev.keyCode;
            if (!/^(46|8|37|38|39|40)$/.test(code)) {
                ev.preventDefault()
            }
        }
    }
 </script>
```

### event.stopPropagation()

event.stopPropagation() 方法阻止事件冒泡到父元素，阻止任何父事件处理程序被执行。

stopImmediatePropagation 既能阻止事件向父元素冒泡，也能阻止元素同事件类型的其它监听器被触发。

### event.target()

`event.target`指向引起触发事件的元素，而`event.currentTarget`则是事件绑定的元素

只有被点击的那个目标元素的`event.target`才会等于`event.currentTarget`

`event.currentTarget`始终是监听事件者，而`event.target`是事件的真正发出者。

### 鼠标在可视窗口的位置

- `clientX`  鼠标在x轴的位置 
- `clientY`  鼠标在y轴的位置

```html
<body>
    <p></p>
    <p></p>
</body>
<script type="text/javascript">
    var obody=document.getElementsByTagName('body')[0];
    var op1=document.getElementsByTagName('p')[0];
    var op2=document.getElementsByTagName('p')[1];
    obody.οnmοusemοve=function(evt){
        var e=evt||window.event;
        alert(e.clientX)//获取鼠标的x坐标值
        alert(e.clientY)//获取鼠标的y坐标值
        op1.innerHTML=e.clientX+'px';
        op2.innerHTML=e.clientY+'px';
    }
</script>

```

### 鼠标在页面的坐标位置

- `pageX`	鼠标在页面x轴的位置
- `pageY`	鼠标在页面y轴的位置

### 鼠标在屏幕坐标位置

- `screenX` 鼠标在屏幕的x轴的位置
- `screenY` 鼠标在屏幕的y轴的位置

## DOM0级事件

1：简单来说就是所有的事件叫DOM0事件。

举例：`onclick,onmouseover,onmouseout....`

2：DOM就是文档对象模型，0是指这个事件的最初版本

## DOM2级事件

1. `addEventListener(事件，函数，布尔值) `	绑定事件方法   IE不支持

2. 第三个参数是 true 的话是捕获事件，是 false 的话是冒泡事件

3. `removeEventListener()`	删除事件方法	IE不支持

4. IE的DOM2事件

   attachEvent('事件'，函数)

   detachEvent('事件'，函数)

## DOM3级事件

在DOM 2级事件的基础上添加了更多的事件类型。

- UI事件，当用户与页面上的元素交互时触发，如：load、scroll
- 焦点事件，当元素获得或失去焦点时触发，如：blur、focus
- 鼠标事件，当用户通过鼠标在页面执行操作时触发如：dblclick、mouseup
- 滚轮事件，当使用鼠标滚轮或类似设备时触发，如：mousewheel
- 文本事件，当在文档中输入文本时触发，如：textInput
- 键盘事件，当用户通过键盘在页面上执行操作时触发，如：keydown、keypress
- 合成事件，当为IME（输入法编辑器）输入字符时触发，如：compositionstart
- 变动事件，当底层DOM结构发生变化时触发，如：DOMsubtreeModified
- 同时DOM3级事件也允许使用者自定义一些事件。

# new的实现

```js
function myNew(fn, ...arguments) {
// 创建一个新的对象
const obj = {}
// 将obj的原型指向构造函数的原型对象，这样obj就可以访问构造函数原型上的属性
obj.__proto__ = fn.prototype 
// 将构造函数的this指向obj，这样obj就可以访问到构造函数中的属性
const res = fn.apply(obj, arguments)
// 如果是引用类型，就返回这个引用类型的对象；如果是值类型，返回创建的对象
return res instanceof Object ? res : obj
}
```

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

# Event Loop事件循环

JavaScript 是一门 **单线程** 语言，即同一时间只能执行一个任务，即代码执行是同步并且阻塞的。

Event Loop 就是为了确保 异步代码 可以在 同步代码 执行后继续执行的

它一直在查找新的事件并且执行。一次循环的执行称之为 tick， 在这个循环里执行的代码称作 task

- 执行栈选择最先进入队列的宏任务（一般都是script），**执行其同步代码**直至结束；
- 检查是否存在微任务，有则会**执行至微任务队列为空**；
- 如果宿主为浏览器，可能会渲染页面；
- 开始下一轮tick，**执行宏任务中的异步代码**（setTimeout等回调）。

![image-20210913233240162](https://z3.ax1x.com/2021/10/15/581E34.png)

1. Promise构造函数入栈，输出4，resolve(5)，Promise出栈
2. func2入栈，setTimeout入栈，log(2)入消息队列，setTimeout出栈
3. func1入栈，输出1，func1出栈
4. 输出3
5. p.then入栈，log(resolve)入微任务队列，log(6)入微任务队列，p.then出栈，func2出栈
6. 栈空，先执行微任务队列，log(resolve)输出5，log(6)输出6
7. 最后执行消息队列，log(2)输出2

# 宏任务和微任务

**宏任务**，由宿主（Node、浏览器）发起，会触发新一轮Tick

1. script（可以理解为外层同步代码）
2. setTimeout/setInterval
3. UI rendering/UI事件
4. postMessage，MessageChannel
5. setImmediate

**微任务**，由JS引擎发起，不会触发新一轮Tick

1. Promise
2. MutationObserver
3. Object.observe（已废弃，Proxy对象替代）
4. process.nextTick（Node.js)

## 执行顺序

1. 首先在宏任务队列中取出第一个任务
2. 执行完毕后取出微任务队列中所有任务顺序执行
3. 然后进行浏览器渲染
4. 之后再取宏任务，周而复始，直至两个队列的任务都取完

**微任务** 先于 **DOM渲染** 先于 **宏任务**

![img](https://pic2.zhimg.com/80/v2-e6dd78c74cb671dd9408c2273308a265_720w.jpg)

```js
setTimeout(() => {
    //执行后 回调一个宏事件
    console.log('内层宏事件3')
}, 0)
console.log('外层宏事件1');

new Promise((resolve) => {
    console.log('外层宏事件2');
    resolve()
}).then(() => {
    console.log('微事件1');
}).then(()=>{
    console.log('微事件2')
})
// 外层宏事件1
// 外层宏事件2
// 微事件1
// 微事件2
// 内层宏事件3
```

1. 首先浏览器执行第一个宏任务进入主线程，遇到setTimeout分发的 宏任务队列 中
2. 遇到console.log()直接执行 输出 外层宏事件1
3. 遇到Promise，new Promise直接执行 输出 外层宏事件2
4. 执行then，被分到 微任务队列 中
5. 第一轮宏任务执行结束，开始执行所有的微任务，输出 微事件1 微事件2
6. 第一轮微任务执行结束，执行第二轮宏任务，输出setTimeout里的 内层宏事件3

# setTimeout运行机制

- setTimeout和setInterval的运行机制是，将指定的代码移出本次执行，等到下一轮Event Loop时，再检查是否到了指定时间。
- 如果到了，就执行对应的代码；如果不到，就等到再下一轮Event Loop时重新判断。
- 这意味着，setTimeout指定的代码，必须等到本次执行的所有代码都执行完，才会执行。
- 每一轮Event Loop时，都会将“任务队列”中需要执行的任务，一次执行完。
- setTimeout和setInterval都是把任务添加到“任务队列”的尾部。
- 因此，它们实际上要等到当前脚本的所有同步任务执行完，然后再等到本次Event Loop的“任务队列”的所有任务执行完，才会开始执行。

# **AJAX**

**Ajax** 的全称是**Asynchronous JavaScript and XML**（异步的JavaScript 和 XML）

**Ajax的原理简单来说通过XmlHttpRequest对象来向服务器发送异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。**

```js
//创建 XMLHttpRequest 对象
var xmlhttp = new XMLHttpRequest();
//规定请求的类型、URL 以及是否异步处理请求。
xmlhttp.open('GET', url, true); // true（异步）或 false（同步）
//发送信息至服务器时内容编码类型
xmlhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded"); 
//发送请求
xmlhttp.send(null); // string：仅用于 POST 请求
//接受服务器响应数据
xmlhttp.onreadystatechange = function() {
    if (xmlhttp.readyState == 4 && (xmlhttp.status == 200 || xmlhttp.status == 304)) {
        console.log(xmlhttp.responseText)
    }
}
```

| 属性               | 描述                                                         |
| :----------------- | :----------------------------------------------------------- |
| onreadystatechange | 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 |
| readyState         | 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。0: 请求未初始化1: 服务器连接已建立2: 请求已接收3: 请求处理中4: 请求已完成，且响应已就绪 |
| status             | 200: "OK" 404: 未找到页面                                    |

- AJAX最大优点就是能在不刷新整个页面的前提下与服务器通信维护数据。
- AJAX使用异步方式与服务器通信，不需要打断用户的操作，响应能力更迅速。
- AJAX可以把以前一些服务器负担的工作转嫁到客户端，利用客户端闲置的能力来处理，减轻服务器和带宽的负担，节约空间和宽带租用成本。

# for循环

## 普通for循环

普通for循环可用于遍历数组

## for(.. in ..)循环

可遍历`Array`,`Object`对象
可以结合`break` `continue` `return`, 随时退出循环

遍历返回的值都是数据结构的**键名**:

- 遍历对象返回的对象的key值
- 遍历数组返回的数组的下标(key)

```js
const arr = ["A","B","C","D"]
for(let i in arr){
    console.log(i) // 都是string
    // 0
    // 1
    // 2
    // 3
}
```

```js
const obj = {
    a:1,
    b:2,
    c:3
}
for(let i in obj){
    console.log(i)
    // a
    // b
    // c
}
```

主要是为遍历对象而设计的，**不适用于遍历数组，遍历出来的索引值是字符串类型。**

## for(..of..)循环

可遍历`iterable`可被迭代的对象（不包括Object）

- 因为能够被for...of正常遍历的，都需要实现一个遍历器Iterator。而数组、字符串、Set、Map结构，早就内置好了Iterator（迭代器），它们的原型中都有一个Symbol.iterator方法，而Object对象并没有实现这个接口，使得它无法被for...of遍历。

`Array`(数组) `Map`(映射) `Set`(集合) `String`(字符串) `arguments对象`(传递给函数的参数的类数组对象) `Nodelist对象`(获取的dom列表集合)

凡是部署了 `iterator` 接口的数据结构也都可以使用数组的 `扩展运算符(...)`、和`解构赋值`等操作

```js
const arr = ["A","B","C","D"]
for(let i of arr){
    console.log(i)
    // A
    // B
    // C
    // D
}
```

```js
const obj = {
    a:1,
    b:2,
    c:3
}
for(let i of obj){
    console.log(i)  // 报错：obj is not iterable
}
```

for...of遍历对象需要通过和Object.keys()搭配使用

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
}
console.log(Object.keys(obj)) // [ 'a', 'b', 'c' ]
for (let i of Object.keys(obj)) {
    console.log(i)
    // a
    // b
    // c
}
```

## forEach循环

```js
arr.forEach(function(value,key,iterable){
    console.log(key, value, iterable)
})
// 0 'A' [ 'A', 'B', 'C', 'D' ]
// 1 'B' [ 'A', 'B', 'C', 'D' ]
// 2 'C' [ 'A', 'B', 'C', 'D' ]
// 3 'D' [ 'A', 'B', 'C', 'D' ]
```

| 参数           | 描述                           |
| :------------- | :----------------------------- |
| *currentValue* | 必需。当前元素                 |
| *index*        | 可选。当前元素的索引值。       |
| *arr*          | 可选。当前元素所属的数组对象。 |

## 总结

- `forEach`更多的用来遍历数组，不能使用`break` `continue` `return`退出循环
- `for...in`一般用来遍历对象或json
- `for...of`用来遍历数组非常方便且比较安全
- `for...in`循环出的是key, `for...of`循环出的是value

# 获取网页的URL

## Window Location

**window.location** 对象在编写时可不使用 window 这个前缀。 一些例子：

一些实例:

- location.href 属性返回当前页面的整个 URL
- location.hostname 返回 web 主机的域名
- location.pathname 返回当前页面的路径和文件名
- location.port 返回 web 主机的端口 （80 或 443）
- location.protocol 返回所使用的 web 协议（http: 或 https:）
- location.assign() 方法加载新的文档

# 无限循环动画

## setInterval

```html
<div id="e"></div>
<script>
    var e = document.getElementById("e");
    var flag = true;
    var left = 0;

    function render() {
      if (flag == true) {
        if (left >= 100) {
          flag = false
        }
        e.style.left = ` ${left++}px`
      } else {
        if (left <= 0) {
          flag = true
        }
        e.style.left = ` ${left--}px`
      }
    }
    setInterval(function () {
      render()
    }, 1000 / 60)
</script>
```

## requestAnimationFrame

1. 它会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率，一般来说，这个频率为每秒60帧。
2. 在隐藏或不可见的元素中，requestAnimationFrame将不会进行重绘或回流，这当然就意味着更少的的cpu，gpu和内存使用量。

```html
<div id="e"></div>
<script>
    var e = document.getElementById("e");
    var flag = true;
    var left = 0;
    var rafId = null

    function render() {
      if (flag == true) {
        if (left >= 100) {
          flag = false
        }
        e.style.left = ` ${left++}px`
      } else {
        if (left <= 0) {
          flag = true
        }
        e.style.left = ` ${left--}px`
      }
    }
    //requestAnimationFrame效果
    (function animloop() {
        render();
        rafId = requestAnimationFrame(animloop);
        //如果left等于50 停止动画
        if(left == 50){
            cancelAnimationFrame(rafId)
        }
    })();
</script>
```

如果我们想每50ms执行一次怎么办呢？

`requestAnimationFrame` 执行条件类似递归调用，能否自定一个时间间隔再执行呢？

```html
<div id="e"></div>
<script>
    var e = document.getElementById("e
    var flag = true;
    var left = 0;
    //当前执行时间
    var nowTime = 0;
    //记录每次动画执行结束的时间
    var lastTime = Date.now();
    //我们自己定义的动画时间差值
    var diffTime = 40;

    //requestAnimationFrame效果
    (function animloop() {
        //记录当前时间
        nowTime = Date.now()
        // 当前时间-上次执行时间如果大于diffTime，那么执行动画，并更新上次执行时间
        if(nowTime-lastTime > diffTime){
            lastTime = nowTime
            render();
        }
        requestAnimationFrame(animloop);
    })()
    
    function render() {
        if(flag == true){
            if(left>=100){
                flag = false
            }
            e.style.left = ` ${left++}px`
        }else{
            if(left<=0){
                flag = true
            }
            e.style.left = ` ${left--}px`
        }
    }
</script>
```



## 服务端推送消息不给时间戳

和服务器通信时，记录下时间差（服务端时间 - 本地时间）不管正负，这样每当接收到消息或者发送消息的时候，**就拿本地时间和时间差相加**。这样就保证了和服务端时间一致。

# attribute和property的区别

写HTML源代码时，可以在HTML元素上定义属性(attribute) 。

 然后，一旦浏览器解析了您的代码，就会创建一个对应的DOM节点。 该节点是一个对象，因此具有属性 (property)。

最后总的来讲就是 **HTML属性** (attribute)和 **DOM属性**(property)，是相互关联的。多数情况`attribute`值仅用作初始DOM节点对象使用，而`property`更多用于页面交互，很多框架都是在与元素和指令的 `property`和事件打交道。

# 数组的拷贝

- 浅拷贝：如果数组元素是基本类型，就会拷贝一份，互不影响，而如果是对象或者数组，就会只拷贝对象和数组的引用，无论对新旧数组的哪一个进行了修改，两者都会发生变化。
- 深拷贝：完全的拷贝一个对象，即使嵌套了对象，两者也相互分离，修改一个对象的属性，也不会影响另一个。

```js
var arr = [{name: 'wens'},{age: '26'}];           //原数组 
var newArr1 = arr;                                //浅拷贝
// 缺点：由于数组是引用类型，修改了arr或者newArr中的一个会影响全部
var newArr2 = arr.slice();                        //浅拷贝
var newArr3 = arr.concat();                       //浅拷贝
// 数组中的值如果是引用类型，对其进行增删改，会影响拷贝的数组，但是如果数组中的值是基本类型，就不会影响
var newArr4 = JSON.parse(JSON.stringify(arr));    //深拷贝
// JSON.stringify()有一些局限，比如对于RegExp类型和Function类型则无法完全满足，而且不支持有循环引用的对象。
arr[0].name = 'leon';  
arr[1].age = '27';  
console.log(arr);
console.log(newArr1);
console.log(newArr2);
console.log(newArr3);
console.log(newArr4);
```

运行结果：

![img](https://img-blog.csdnimg.cn/20191203204501210.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc2MjA4OQ==,size_16,color_FFFFFF,t_70)

# Array

## split（不改变字串，返回数组）

split() 方法用于把一个字符串分割成字符串数组。

**注意：** split() 方法不改变原始字符串。

```js
var str = "How are you doing today?"
var n = str.split(" ")
console.log(n);
// ["How", "are", "you", "doing", "today?"]
```

## join（不改变数组）

方法将数组作为字符串返回。

元素将由指定的分隔符分隔。默认分隔符是逗号 (,)

**注意：**join() 方法不会改变原始数组。

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];
var energy = fruits.join('');
// BananaOrangeAppleMango
```

## reduce（不改变）

reduce()方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。

**reduce 为数组中的每一个元素依次执行回调函数**

```js
array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
```

`function`必需，用于执行每个数组元素的函数

| 参数           | 描述                                     |
| :------------- | :--------------------------------------- |
| *total*        | 必需。*初始值*, 或者计算结束后的返回值。 |
| *currentValue* | 必需。当前元素                           |
| *currentIndex* | 可选。当前元素的索引                     |
| *arr*          | 可选。当前元素所属的数组对象。           |

`initialValue`  可选。传递给函数的初始值

**注意:** reduce() 对于空数组是不会执行回调函数的。

### 数组中每个元素出现的次数

```jsx
let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

let nameNum = names.reduce((pre,cur)=>{
  if(cur in pre){
    pre[cur]++
  }else{
    pre[cur] = 1 
  }
  return pre
},{})
console.log(nameNum); //{Alice: 2, Bob: 1, Tiff: 1, Bruce: 1}
```

### 数组去重

```jsx
let arr = [1,2,3,4,4,1]
let newArr = arr.reduce((pre,cur)=>{
    if(!pre.includes(cur)){
      return pre.concat(cur)
    }else{
      return pre
    }
},[])
console.log(newArr);// [1, 2, 3, 4]
```

### 将二维数组转化为一维

```jsx
let arr = [[0, 1], [2, 3], [4, 5]]
let newArr = arr.reduce((pre,cur)=>{
    return pre.concat(cur)
},[])
console.log(newArr); // [0, 1, 2, 3, 4, 5]
```

### 将多维数组转化为一维

```jsx
let arr = [[0, 1], [2, 3], [4,[5,6,7]]]
const newArr = function(arr){
   return arr.reduce((pre,cur)=>pre.concat(Array.isArray(cur)?newArr(cur):cur),[])
}
console.log(newArr(arr)); //[0, 1, 2, 3, 4, 5, 6, 7]
```

### 对象里的属性求和

```js
var result = [
    {
        subject: 'math',
        score: 10
    },
    {
        subject: 'chinese',
        score: 20
    },
    {
        subject: 'english',
        score: 30
    }
];

var sum = result.reduce(function(prev, cur) {
    return cur.score + prev;
}, 0);
console.log(sum) //60
```

## map（不改变）

map() 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。

map() 方法按照原始数组元素顺序依次处理元素。

**注意：** map() 不会对空数组进行检测。

**注意：** map() 不会改变原始数组。

```js
var numbers = [4, 9, 16, 25];
var x = numbers.map(Math.sqrt);

console.log(x);
// [2, 3, 4, 5]
```

**注意：**map()方法创建一个新数组，但新数组并不是再遍历完array1后才被赋值，而是遍历一次就得到一个值，相当于满足条件的就返回处理后的值，没满足的就是undefined。

```js
var array1 = [1, 4, 9, 16];
const map1 = array1.map(x => {
    if (x == 4) {
        return x * 2;
    }
    // return x  // 加上这个就可以打印出 [1, 8, 9, 16]
});
console.log(map1); // [undefined, 8, undefined, undefined]
```

## concat（不改变）

concat() 方法用于连接两个或多个数组。

**注意：**该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

```js
var hege = ["Cecilie", "Lone"];
var stale = ["Emil", "Tobias", "Linus"];
var kai = ["Robin"];
var children = hege.concat(stale,kai);

console.log(children);
// ["Cecilie","Lone","Emil","Tobias","Linus","Robin"]
```

## slice（不改变）

slice()方法可提取字符串的某个部分，并以新的字符串**返回被提取的部分**。

**注意：** slice() 方法不会改变原始数组。

```js
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1,3);

console.log(citrus);
// ["Orange","Lemon"]
```

## filter（不改变）

过滤器

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

返回值：**满足过滤器回调函数的新数组**

**注意：** filter() 不会对空数组进行检测。

**注意：** filter() 不会改变原始数组。

`array.filter(function(currentValue,index,arr), thisValue)`

| 参数           | 描述                         |
| :------------- | :--------------------------- |
| *currentValue* | 必须。当前元素的值           |
| *index*        | 可选。当前元素的索引值       |
| *arr*          | 可选。当前元素属于的数组对象 |

| thisValue | 可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。 如果省略了 thisValue ，"this" 的值为 "undefined" |      |      |      |      |
| --------- | ------------------------------------------------------------ | ---- | ---- | ---- | ---- |

```js
// 计数，数组arr中出现item的次数
function count(arr, item) {
    let res = arr.filter(function (cur) { // res是满足过滤器回调函数的新数组
        return cur === item
    })
    return res.length
}
```



## fill（改变）

fill() 方法用于将一个固定值替换数组的元素。

**注意：** map() 会改变原始数组。

填充 "Runoob" 到数组的最后两个元素：

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"]; fruits.fill("Runoob", 2, 4);

console.log(fruits)
// Banana,Orange,Runoob,Runoob
```

## splice（改变）

splice() 方法用于添加或删除数组中的元素。

`array.splice(index,howmany,item1,.....,itemX)`

| 参数                  | 描述                                                         |
| :-------------------- | :----------------------------------------------------------- |
| *index*               | 必需。规定从何处添加/删除元素。 该参数是开始插入和（或）删除的数组元素的下标，必须是数字。 |
| *howmany*             | 可选。规定应该删除多少元素。必须是数字，但可以是 "0"。 如果未规定此参数，则删除从 index 开始到原数组结尾的所有元素。 |
| *item1*, ..., *itemX* | 可选。要添加到数组的新元素                                   |

输出返回值，即删除的元素数组

**注意：**这种方法会改变原始数组。

```js
var vegetables = ['Cabbage', 'Turnip', 'Radish', 'Carrot'];
console.log(vegetables);
// ["Cabbage", "Turnip", "Radish", "Carrot"]

var pos = 1, n = 2;

var removedItems = vegetables.splice(pos, n);
// 从索引为pos的元素开始，删除n个

// 输出被改变的原数组
console.log(vegetables);
// ["Cabbage", "Carrot"] (the original array is changed)

// 输出返回值，即删除的元素数组
console.log(removedItems);
// ["Turnip", "Radish"]
```

## shift（改变）

shift() 方法用于把数组的第一个元素从其中删除，并返回第一个元素的值。

**注意：** 此方法改变数组的长度！

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];
var delell = fruits.shift()

console.log(fruits);
// ["Orange", "Apple", "Mango"]

console.log(detell)
// ["Banana"]
```

## pop（改变）

pop() 方法用于删除数组的最后一个元素并返回删除的元素。

**注意：**此方法改变数组的长度！

## unshift（改变）

unshift() 方法可向数组的开头添加一个或更多元素，并返回新的长度。

**注意：** 该方法将改变数组的数目。

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];
var newlength = fruits.unshift("Lemon","Pineapple");

console.log(fruits);
// ["Lemon","Pineapple","Banana", "Orange", "Apple", "Mango"]

console.log(newlength);
// 6
```

## push（改变）

push() 方法可向数组的末尾添加一个或多个元素，并返回新的长度。

**注意：** 新元素将添加在数组的末尾。

**注意：** 此方法改变数组的长度。

## sort（改变）

默认排序顺序为按字母升序。

**注意：** 这种方法会改变原始数组！

```js
var points = [40,100,1,5,25,10];
points.sort(function(a,b){return a-b});
//a-b：升序     b-a：降序
console.log(points);
// [1,5,10,25,40,100]
```

# String

## trim（不改变）

用于删除字符串的头尾空白符

空白符包括：空格、制表符tab、换行符等

**注意：**方法不会改变原始字符串。 方法不适用于 null, undefined, Number 类型。

```js
var str = "    trim    ";
console.log(str.trim());
// trim
```



# Date

Date对象是在JavaScript内置的对象存储日期和时间。

```js
let now = new Date();    // 设置变量为当前日期和时间
// Fri Nov 05 2021 17:32:08 GMT+0800 (中国标准时间)
```

**Date对象的方法**：

| 方法                                                         | 描述                                        |
| :----------------------------------------------------------- | :------------------------------------------ |
| [getDate()](https://www.runoob.com/jsref/jsref-getdate.html) | 从 Date 对象返回一个月中的某一天 (1 ~ 31)。 |
| [getDay()](https://www.runoob.com/jsref/jsref-getday.html)   | 从 Date 对象返回一周中的某一天 (0 ~ 6)。    |
| [getFullYear()](https://www.runoob.com/jsref/jsref-getfullyear.html) | 从 Date 对象以四位数字返回年份。            |
| [getHours()](https://www.runoob.com/jsref/jsref-gethours.html) | 返回 Date 对象的小时 (0 ~ 23)。             |
| [getMilliseconds()](https://www.runoob.com/jsref/jsref-getmilliseconds.html) | 返回 Date 对象的毫秒(0 ~ 999)。             |
| [getMinutes()](https://www.runoob.com/jsref/jsref-getminutes.html) | 返回 Date 对象的分钟 (0 ~ 59)。             |
| [getMonth()](https://www.runoob.com/jsref/jsref-getmonth.html) | 从 Date 对象返回月份 (0 ~ 11)。             |
| [getSeconds()](https://www.runoob.com/jsref/jsref-getseconds.html) | 返回 Date 对象的秒数 (0 ~ 59)。             |
| [getTime()](https://www.runoob.com/jsref/jsref-gettime.html) | 返回 1970 年 1 月 1 日至今的毫秒数。        |

| [toLocaleDateString()](https://www.runoob.com/jsref/jsref-tolocaledatestring.html) | 根据本地时间格式，把 Date 对象的日期部分转换为字符串。 |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [toLocaleTimeString()](https://www.runoob.com/jsref/jsref-tolocaletimestring.html) | 根据本地时间格式，把 Date 对象的时间部分转换为字符串。 |
| [toLocaleString()](https://www.runoob.com/jsref/jsref-tolocalestring.html) | 根据本地时间格式，把 Date 对象转换为字符串。           |

# iframe

通常我们使用iframe直接直接在页面嵌套iframe标签指定src就可以了。

```html
<iframe src="demo_iframe_sandbox.htm"></iframe>
```

## iframe常用属性

1. frameborder: 是否显示边框，1(yes),0(no)
2. height: 框架作为一个普通元素的高度，建议在使用css设置。
3. width: 框架作为一个普通元素的宽度，建议使用css设置。
4. name: 框架的名称，window.frames[name]时专用的属性。
5. scrolling: 框架的是否滚动。yes,no,auto。
6. src：内框架的地址，可以使页面地址，也可以是图片的地址。
7. srcdoc: 用来替代原来HTML body里面的内容。但是IE不支持, 不过也没什么卵用
8. sandbox: 对iframe进行一些列限制，IE10+支持

```html
A:<iframe id="mainIframe" name="mainIframe" src="/main.html" frameborder="0" scrolling="auto" ></iframe>
B:<iframe id="mainIframe" name="mainIframe" src="http://www.baidu.com" frameborder="0" scrolling="auto" ></iframe>
```

使用A时，因为同域，父页面可以对子页面进行改写,反之亦然。
使用B时，不同域，父页面没有权限改动子页面,但可以实现页面的跳转

## 获取iframe里的内容

`iframe.contentWindow`：获取iframe的window对象
`iframe.contentDocument`： 获取iframe的document对象

```js
var iframe = document.getElementById("iframe1");
var iwindow = iframe.contentWindow;
var idoc = iwindow.document;
console.log("window",iwindow);//获取iframe的window对象
console.log("document",idoc);  //获取iframe的document
console.log("html",idoc.documentElement);//获取iframe的html
console.log("head",idoc.head);  //获取head
console.log("body",idoc.body);  //获取body
```

获取iframe的window对象更简单的方式是，结合Name属性，通过window提供的frames获取.

```html
<iframe src ="/index.html" id="ifr1" name="ifr1" scrolling="yes">
    <p>Your browser does not support iframes.</p>
</iframe>
<script type="text/javascript">
    console.log(window.frames['ifr1'].window);
</script>
```

## iframe中获取父级内容

同理，**在同域下**，父页面可以获取子iframe的内容，那么子iframe同样也能操作父页面内容。

在iframe中，可以通过在window上挂载的几个API进行获取：

- window.parent：获取上一级的window对象，如果还是iframe则是该iframe的window对象
- window.top：获取最顶级容器的window对象，即，就是你打开页面的文档
- window.self：返回自身window的引用。可以理解 window===window.self(脑残)

