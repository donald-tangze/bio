<[Modern JavaScript From The Beginning](https://learning-oreilly-com.ezproxy.hkpl.gov.hk/videos/modern-javascript-from/9781789539509/)>        [Brad Traversy](https://learning.oreilly.com/search/?query=author%3A"Brad Traversy"&sort=relevance&highlight=true)

javascript   jQuery

> Basic & fundamendals:  variable, data type, loop, Function, arrays, 
>
> error handling
>
> async    promise, await/async,fetch,  ajax, callback 
>
> Modules
>
> es5 Prototype, es6 classes   :  object-oriented programming
>
> Dom

bootstrap

Skelton css

# Js Core Concepts

## 0. Overview

* Javascript language = Valina Javascript,  
* ECMAScript = browser Specification  of Javascript, how the language should be interpreted by browser, defined by Europe Asscosiation

/ ES 2015/ ES 2019/ ES 2011/ 

* Typescript, Coffescript:   dialect of javascript

  strong type

  IFFE  = Immediately Invoked Function Expression

## 1. Data Type

 6  type:  String, Boolean, Number, Null, Undefined, Object

###  Reference type: 

对象定义（类）通过构造函数，对象是对象定义的一个实现。

Object = built-in Object + self-created Object.

**built-in Object**: Array, Date, Regular Expression, Global, Math. 

1.Object creation:  literal, constructor function, shortcut for building objects.

2.prototypre, Object has properties and methods

Object

**Comparision of Constructor vs Prototype vs Class** 

Constructor function can have properties and methods. its properties can be Reference Object or simple Object, or even a Object with method.

**Advantage** of constructor function over literal:  reduce duplicate code, easy to  reuse.

**Advantage** of prototype over constructor function: abstract same properties and methods of different constructor, to reduce memory footprint and duplicate code.   **Disadvantage** of prototype's property is common and shared, so would mess when used by different sub-object,  while consturctor's property is seperated and customed by each object that it creates.

 **Advantage** of Class over prototype and constructor: easy to map out its prototype chain exactly.   **Disadvantage**  of class is not hoisting, whereas constructor  function is hoisting.  



## 2. Js prototype

Every function has prototype. as well as constructor function.  object has prototype.

Mechanism: object or function would obtain its prototype's all properties and methods.

**prototype chain/inheritance**:   Modify an object's prototype

``` java
//set prototype's property
Construtor.prototype.property = 180;
object.prototype = Constructor.prototype

// Modify an object's prototype
obj.prototype = new Constructor();
```

**apply prototypal chain/inheritance**,  base of class **inheritance**.

Only change once to make all constructor function  inherited the root prototype  and their object automately update the property.



## 3. Class

new syntax in ES6, Js is not class-based language like java, **syntactic sugar** for **constructors and prototypes**. Compiler like Babel will transfer into old-style constructors and prototypes automately. backward compatiable

**Extends** keyword clearer to do prototypal chain/inheritance.  **Advantage** to code organisation.

it's similar with class and object in java to implement prototype in js.

```javascript
class Item extends Something{
  // below is constructor function, only when constructor has arguments. if without arguments, it's part of prototype.
	constructor(arguments){
    super();
		this.property = arguments;
    this.property2 = "constant"; //prototype propertiers
	}
	
	//below is prototype methods. 方法函数无状态stateless，应该都是原型prototype, 
	function(){
	
	}
}
```

class is constructor function, but not hoisting.  function is hoisting.  Function始终在执行顺序上优先，而不是看代码的位置先后



## 4.Flow and Control

if, else, loop, switch, for, 

Operator: add,multi, divide, boolean&& || !;  bit operator, >>有符号右移   <<左移  ~Not按位非  &AND按位与  |OR按位或  ^XOR按位异或

## 5.Function

arguments参数是pass copied value， 传值。arguments是一个数组array.

没有重载， 有重写覆盖Override.

## 6. Js Syntax

### 6.1 Scope, Closure 

Let 是有闭包Closure, 只在声明的函数范围有效， var永远是全局范围，尽量避免使用var.

### 6.2 module

###  6.3 XMLHttpRequest vs Fetch

Fetch: new api to implment streamlined XMLHttpRequest, optimized nested function callback, Fetch use **promise** and  **then**.

```javascript
// XMLHttpRequest

// Fetch
fetch(url)
	.then((response) => handleErrors())
	.then((data) => updateUISucess(data))
	.catch((error) => updateUIError(error));
```

Https://caniuse.com



## 7.DOM Extension





# Reference Online Course

[ JavaScript Essential Training ](https://www.linkedin.com/learning/paths/become-a-javascript-developer?leis=LTI&u=2058332)

[JavaScript: Prototypes](https://www.linkedin.com/learning/javascript-prototypes?contextUrn=urn%3Ali%3AlyndaLearningPath%3A5f6b7ff5498e706fb4dda1f1&leis=LTI&u=2058332)

[ JavaScript: Classes ](https://www.linkedin.com/learning/javascript-classes-2018/next-steps?autoSkip=true&autoplay=true&leis=LTI&resume=false&u=2058332)

# Reference Book

## 1. <JavaScript: The Definitive Guide>

![image-20220328151827788](https://tva1.sinaimg.cn/large/e6c9d24egy1h0pme4pznaj20b00egmyg.jpg)

## 2. Professional JavaScript for Web Developers, 4th Edition

![image-20220328151924450](https://tva1.sinaimg.cn/large/e6c9d24egy1h0pmf2phfbj20b10dugms.jpg)





# NEXT STEP

#### Framework

Angular vs React       js based framework

####  Tool

Babel,  WebPack, npm, Gulp

#### Server Language

Node.js

![image-20220326214128777](https://tva1.sinaimg.cn/large/e6c9d24egy1h0nm81wwiqj20py0h1q45.jpg)












