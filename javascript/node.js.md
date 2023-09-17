## Javascript Engine

Chrome/Edge: V8. Convert javascript code into Machine language

Netscape: SpiderMonkey

IE: Chakara

Could be run on Browser, Mobile and Server.

## Definition:

Runtime environmet on Server which use V8 javascript engine.

NPM: Node.js package manager, similar to Maven, Jar package management

## Developement Suits

### 1.MERN

MongoDB + Express.js(framework) + React.js(language) + node.js(runtime)

### 2.MEAN

MongoDB + Express.js(framework) + React.js(language) + node.js(runtime)

Similar with:  Mysql + Spring + Java + JVM

​                                       django + Pyton



###  2.iTerm2与远程服务器进行文件上传、下载

```shell
scp '/Users/don2021/Documents/online course/Javascript/jsFromBeginning/bookcode/codacademy/learn_js/http.zip' root@39.108.160.59:/var/www/html/game/http.zip
```

###  3.[Deploying Node.js Apps on Heroku](https://devcenter.heroku.com/articles/deploying-nodejs)



## 4. Node.js Module

Npm has a lot of package, which are shared freely and could imported into our own node.js project. The most popular package manager is **N**ode **P**ackage **M**anager which is the default package manager for Node.js. Its command-line tool, `npm`, is even included in the Node.js installation process. This tool enables developers to download and manage packages via the terminal.

[Codecademy course](https://www.codecademy.com/journeys/back-end-engineer/paths/becj-22-back-end-development/tracks/becp-22-basics-of-back-end-development/modules/wdcp-22-modular-development-with-node-js-93219e8d-d0b1-4700-b089-3b003e19abc7/articles/node-package-manager)

#### Kick Off:  Add Module dependencies

```
npm init -y // generate package.json dependencies
npm install express // add and import dependencies package

node app.js  // run application
```



#### Package Scope

local project or Global Packages

```
npm install http-server -g

npm i == npm install
```



#### Use Imported Module

Every JavaScript file that runs in a Node environment is treated as a distinct module. 

*  add them as properties to the built-in module.exports object:
*  require()  The `require()` function accepts a string as an argument. That string provides the [file path](https://www.freecodecamp.org/news/requiring-modules-in-node-js-everything-you-need-to-know-e7fbd119be8/) to the module you would like to import.
*  Using Object Destructuring to be more Selective With `require()`

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



## 5.How to write Node.js and Express.js

[Introduction to Server-Side Frameworks with Express.js](https://www.codecademy.com/journeys/back-end-engineer/paths/becj-22-back-end-development/tracks/becp-22-build-a-back-end-with-express-js/modules/wdcp-22-introduction-to-express-js-29c19102-ea29-4723-bf5c-0a4e02b2c9ab/articles/introduction-to-server-side-frameworks-with-express-js)

```javascript
import express from "express";
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("<h1>Hello</h1>");
});

app.get("/about", (req, res) => {
  res.send("<h1>About Me</h1><p>My name is Angela</p>");
});

app.get("/contact", (req, res) => {
  res.send("<h1>Contact Me</h1><p>Phone: +44123456789</p>");
});

app.listen(port, () => {
  console.log(`Server started on port ${port}`);
});
```

