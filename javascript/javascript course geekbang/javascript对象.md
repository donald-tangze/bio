##  对象基本概念

语言和宿主的基础设施由对象来提供，并且 JavaScript 程序即是一系列互相通讯的对象集合

Object（对象）在英文中，是一切事物的总称，这和面向对象编程的抽象思维有互通之处。中文的“对象”却没有这样的普适性，我们在学习编程的过程中，更多是把它当作一个专业名词来理解。

在不同的编程语言中，设计者也利用各种不同的语言特性来抽象描述对象，最为成功的流派是使用“类”的方式来描述对象，这诞生了诸如 C++、Java 等流行的编程语言。

而 JavaScript 早年却选择了一个更为冷门的方式：原型

### 原型

运行时的对象模型_prototype_

基于原型的面向对象系统通过“复制”的方式来创建新对象。一些语言的实现中，还允许复制一个空对象。这实际上就是创建一个全新的对象。

原型系统的“复制操作”有两种实现思路：一个是并不真的去复制一个原型对象，而是使得新对象持有一个原型的引用；另一个是切实地复制对象，从此两个对象再无关联。

#### js原型系统概括：

* 1.如果所有对象都有私有字段[[prototype]]，就是对象的原型；

* 2.读一个属性，如果对象本身没有，则会继续访问对象的原型，直到原型为空或者找到为止。

#### new 运算

接受一个构造器和一组调用参数，实际上做了几件事：

* 以构造器的 prototype 属性（注意与私有字段[[prototype]]的区分）为原型，创建新对象；
* 将 this 和调用参数传给构造器，执行；
* 如果构造器返回的是对象，则返回，否则返回第一步创建的对象

#### ES6 操纵原型内置函数

以便更为直接地访问。

三个方法分别为：Object.create 根据指定的原型创建新对象，原型可以是 null；Object.getPrototypeOf 获得一个对象的原型；Object.setPrototypeOf 设置一个对象的原型。

### 面向对象分析与设计

对象具有唯一标识性：即使完全相同的两个对象，也并非同一个对象。

对象有状态：对象具有状态，同一对象可能处于不同状态之下。

对象具有行为：即对象的状态，可能因为它的行为产生变迁。

结论：**JavaScript 对象的具体设计：具有高度动态性的属性集合。**

#### 1.数据属性。

它比较接近于其它语言的属性概念。数据属性具有四个特征。

value：就是属性的值。

writable：决定属性能否被赋值。

enumerable：决定 for in 能否枚举该属性。

configurable：决定该属性能否被删除或者改变特征值。

在大多数情况下，我们只关心数据属性的值即可。

#### 2.访问器（getter/setter）属性

有四个特征。

getter：函数或 undefined，在取属性值时被调用。

setter：函数或 undefined，在设置属性值时被调用。

enumerable：决定 for in 能否枚举该属性。

configurable：决定该属性能否被删除或者改变特征值。

## 具体对象

### 宿主对象（host Objects）

由 JavaScript 宿主环境提供的对象，它们的行为完全由宿主环境决定。

在浏览器环境中，我们都知道全局对象是 window，window 上又有很多属性，如 document。实际上，这个全局对象 window 上的属性，一部分来自 JavaScript 语言，一部分来自浏览器环境。

JavaScript 标准中规定了全局对象属性，W3C 的各种标准中规定了 Window 对象的其它属性。

### 内置对象（Built-in Objects）

由 JavaScript 语言提供的对象。

####  固有对象（Intrinsic Objects ）

[固有对象](https://www.ecma-international.org/ecma-262/9.0/index.html#sec-well-known-intrinsic-objects)

由标准规定，随着 JavaScript 运行时创建而自动创建的对象实例。

> 三个值：Infinity、NaN、undefined。
>
> 九个函数：eval
>
> isFinite
>
> isNaN
>
> parseFloat
>
> parseInt
>
> decodeURI
>
> decodeURIComponent
>
> encodeURI
>
> encodeURIComponent
>
> 一些构造器：Array、Date、RegExp、Promise、Proxy、Map、WeakMap、Set、WeakSet、Function、Boolean、String、Number、Symbol、Object、Error、EvalError、RangeError、ReferenceError、SyntaxError、TypeError、URIError、ArrayBuffer、SharedArrayBuffer、DataView、Typed Array、Float32Array、Float64Array、Int8Array、Int16Array、Int32Array、UInt8Array、UInt16Array、UInt32Array、UInt8ClampedArray。
>
> 四个用于当作命名空间的对象：AtomicsJSONMathReflect

#### 原生对象（Native Objects）

可以由用户通过 Array、RegExp 等**内置构造器或者特殊语法**创建的对象。

![img](https://static001.geekbang.org/resource/image/6c/d0/6cb1df319bbc7c7f948acfdb9ffd99d0.png)



#### 普通对象（Ordinary Objects）

由{}语法、Object 构造器或者 class 关键字定义类创建的对象，它能够被原型继承。

// 1. 利用字面量
var a = [], b = {}, c = /abc/g
// 2. 利用dom api
var d = document.createElement('p')
// 3. 利用JavaScript内置对象的api
var e = Object.create(null)
var f = Object.assign({k1:3, k2:8}, {k3: 9})
var g = JSON.parse('{}')
// 4.利用装箱转换
var h = Object(undefined), i = Object(null), k = Object(1), l = Object('abc'), m = Object(true)



### 用对象来模拟函数和构造器的机制

