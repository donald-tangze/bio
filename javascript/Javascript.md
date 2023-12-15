Code Exercise:  [Learn JavaScript](https://www.codecademy.com/learn/introduction-to-javascript/modules/learn-javascript-scope/cheatsheet)

Coursera Video: [Welcome to Module 4: Introduction to Javascript](https://www.coursera.org/learn/html-css-javascript-for-web-developers/lecture/qVueq/welcome-to-module-4-introduction-to-javascript)

### JavaScript

JavaScript is a programming language that powers the dynamic behavior on most websites. Alongside HTML and CSS, it is a core technology that makes the web run.

Where to put Javascript

```html
<html>
  <head>
  </head>
  <body>
    <script src= "../hello.js"> </script>
    <script>console.out("Hello World!") </script>
  </body>
</html>
```

## 1.Variable

```

```



### 1.1Undefined & NULL

`undefined` is a primitive JavaScript value that represents lack of defined value. Variables that are declared but not initialized to a value will have the value `undefined`.

### 1.2.Declaring Variable

- `var` is used in pre-ES6 versions of JavaScript.

- `let` is the preferred way to declare a variable when it can be reassigned.

- `const` is the preferred way to declare a variable with a constant value.

  ```javascript
  let variable = 1 //  no need semicolon in the end
  const constant = 'Hello World' //String
  let array = [1,3,5]
  let array 2 = ['Apple', 'Twitter', 'IBM', 'Microsoft']
  let isQualified = true 
  // object is key-value pairs
  let employee = {
    name : 'donald',
    age : 33,
    work: function makeMoney(){
      
    }
  }
  ```

  

### 1.3.Javascript Data Type

String, Number(float and integer), boolean, Object(include Array, Object literal), Special Values(Undefined and Null)



### 1.3.1.Boolean: Truthy and Falsy

In JavaScript, values evaluate to `true` or `false` when evaluated as Booleans.

- Values that evaluate to `true` are known as *truthy*
- Values that evaluate to `false` are known as *falsy*

Falsy values include `false`, `0`, empty strings, `null` `undefined`, and `NaN`. All other values are truthy.

## 2.Scope

Various scopes include:

- *Global* scope (a value/function in the global scope can be used anywhere in the entire program)
- *File* or *module* scope (the value/function can only be accessed from within the file)
- *Function* scope (only visible within the function),
- *Code block* scope (only visible within a `{ ... }` codeblock)

## 3.Function

Define a function is by using the keyword function followed by function name and followed parentheses then curly braces.

Function is a object.

```javascript
// Defining the function:
function sum(num1, num2) {
  return num1 + num2;
}
```

### 1.Annoymous Functions

```
// Notation
public function doSomething(){  
}

let fahrenheitToCelsius = function(fahrenheit) {
  return (fahrenheit - 32) * (5/9);
};
```

### 2.Arrow Functions

```javascript
let fahrenheitToCelsius = (fahrenheit) => {} {
  return (fahrenheit - 32) * (5/9);
};
```

### 

## 4.Javascript Object

An *object* is a built-in data type for storing key-value pairs. Data inside objects are unordered, and the values can be of any type.

### Properties and values of a JavaScript object

A JavaScript object literal is enclosed with curly braces `{}`. Values are mapped to keys in the object with a colon (`:`), and the key-value pairs are separated by commas. All the keys are unique, but values are not.

Key-value pairs of an object are also referred to as *properties*.

### 4.1.Dot Notation for Accessing Object Properties

### 4.2. Notation

### 4.3.javascript passing objects as arguments

When JavaScript objects are passed as arguments to functions or methods, they are passed by *reference*, not by value. This means that the object itself (not a copy) is accessible and mutab

### 4.4.`this` Keyword



## 5.Asynchronous Programming

Even though JavaScript is a single-threaded language, it can still execute asynchronous code using the **event loop**.

It's for **time-consuming** operations, like http request.

```javascript
//callback function
setTimeout(() => {
  console.log('Delay the printing of this string, please.');
}, 1000);

```

### 5.1. Understand the Components of the Event Loop

The *event loop* is made up of these parts:

- Memory Heap
- Call Stack
- Event Queue
- Event Loop
- Node or Web APIs

### 5.2. Understand [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

Chained Promise could replace `nested callback function` to make `asynchronous` task clearer.

Promise states: Pending, Settled (fulfilled) , Rejected

Promise is a object with value produced in the future.

#### 5.2.1.Promise Constructor

Constructor has only one arguments called executor function, parmeter are handlers for success and failure outcome.  

be sure to always call `resove` and `reject` in executer function body.

```new Promise((resolve, reject) => { if(){resolve(value)} else {reject(reason)}  })```

**Immediately Settled Promises**: 

static `Promise.resolve(value)`  return a promise that is fullfilled with the given value.

#### 5.2.2.Promise chaining Pipline: 

`then()`  `catch()`  only accept function arguments, like array function, return a Promise

`then()`  syntax

```javascript
then(onFulfilled, onRejected)
// value: The value that the promise was fulfilled with.
// reason: The value that the promise was rejected with.
then(value => {}, 
     reason => {})
```

### 5.3.Use async/ await

async/ await is simplified syntax for native `promise`.

*  `async` keyword is used to write functions that handle asynchronous actions

  ```javascript
      const putImage = async function (url, element) {
        const img = await loadImage(url) // resolved(result)
        element.appendChild(img)
      }
      
  Equivalent to pipeline then
      const putImage = (url, element) => {
          // Promise pipeline
          loadImage(url)
          .then(img => element.appendChild(img))
      }
          
  ```

* `async` functions always return a promise. An `async` function will return in one of three ways:

  - If there’s nothing returned from the function, it will return a promise with a resolved value of `undefined`.

  - If there’s a non-promise value returned from the function, it will return a promise resolved to that value.

  - If a promise is returned from the function, it will simply return that promise



The `await` keyword can only be used inside an `async` function. `await` is an operator: it returns the resolved value of a promise. 

```javascript
async function noAwait() {
 let value = myPromise();
 console.log(value);
}

async function yesAwait() {
 let value = await myPromise();
 console.log(value);
}

noAwait(); // Prints: Promise { <pending> }
yesAwait(); // Prints: Yay, I resolved!
```



![](https://static-assets.codecademy.com/Courses/Learn-JavaScript/Event-Loop-and-Concurrency/JavaScript-Engine-Diagram.png)https://static-assets.codecademy.com/Courses/Learn-JavaScript/Event-Loop-and-Concurrency/JavaScript-Engine-Diagram.png?_gl=1

# 6.Modules

## 6.1.Implementations of Modules in JavaScript: Node.js vs ES6

Before we dive in, it should be noted that there are multiple ways of implementing modules depending on the *runtime environment* in which your code is executed. In JavaScript, there are two runtime environments and each has a preferred module implementation:

1. The [Node](https://nodejs.org/en/about/) runtime environment and the `module.exports` and `require()` syntax.
2. The browser’s runtime environment and the [ES6](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) `import`/`export` syntax.

## 6.2. [ES6](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) `import`/`export` syntax

A module must be entirely contained within a file. 

* declaration

```javascript
// export any functions, variables, objects, Class(syntax sugar of Object constructor and prototype )
export { resourceToExportA, resourceToExportB, ...}

/* dom-functions.js */
export const toggleHiddenElement = (domElement) => {
  // logic omitted...
}

export const changeToFunkyColor = (domElement) => {
  // logic omitted...
}

import { exportedResourceA, exportedResourceB } from '/path/to/module.js';
```

* The addition of the attribute `type='module'` to the `<script>` element

```html
<!-- secret-messages.html --> 
<html>
  <head>
    <title>Secret Messages</title>
  </head>
  <body>
    <button id="secret-button"> Press me... if you dare </button>
    <p id="secret-p" style="display: none"> Modules are fancy! </p>
    <script type="module" src="./secret-messages.js"> </script>
  </body>
</html>
```

* Renaming Imports to Avoid Naming Collisions

```
import { exportedResource as newlyNamedResource } from '/path/to/module'
```

* Default Exports and Imports

  ```
  export { resources as default };
  import { default as importedResources } from 'module.js 
  
  Equivalent to 
  export default resources;
  import importedResources from 'module.js';
  
  const resources = { 
    toggleHiddenElement, 
    changeToFunkyColor
  }
  export default resources;
  
  import domFunctions from '../modules/dom-functions.js';
  const { toggleHiddenElement, changeToFunkyColor } = domFunctions;
  ```

  

## 6.3.Modules in JavaScript: Node.js

Every JavaScript file that runs in a Node environment is treated as a distinct module. 

*  add them as properties to the built-in module.exports object:
* require()  The `require()` function accepts a string as an argument. That string provides the [file path](https://www.freecodecamp.org/news/requiring-modules-in-node-js-everything-you-need-to-know-e7fbd119be8/) to the module you would like to import.
* Using Object Destructuring to be more Selective With `require()`

```javascript
/* converters.js */
function celsiusToFahrenheit(celsius) {
  return celsius * (9/5) + 32;
}
// add them as properties to the built-in module.exports object:
module.exports.celsiusToFahrenheit = celsiusToFahrenheit;

// annoymous function
module.exports.fahrenheitToCelsius = function(fahrenheit) {
  return (fahrenheit - 32) * (5/9);
};


// Using Object Destructuring to be more Selective With `require()`
/* celsius-to-fahrenheit.js */
const { celsiusToFahrenheit } = require('./converters.js');
```

