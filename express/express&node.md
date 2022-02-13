# Express and Node

### What is Node?

[Node](https://nodejs.org/) (or more formally *Node.js*) is an open-source, cross-platform runtime environment that allows  developers to create all kinds of server-side tools and applications in [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript). 

### Callback Functions

You can't know when a user is going to click a button, so what you do is, you define an event handler for the click event. This event handler accepts a function, which will be called when the event is triggered:

```javascript
document.getElementById('button').addEventListener('click', () => {
//item clicked
})
```

This is the so-called callback.
A callback is a simple function that's passed as a value to another function, and will only be executed when the event happens. We can do this because JavaScript has first-class functions, which can be assigned to variables and passed around to other functions (called higher-order functions).

### Higher Order Function

Let's first understand this function before we jump into node. It is a function that either takes a function as an argument or returns a function.

```javascript
function add(num1,num2){
  return num1+num2;
}
function multiply(num1,num2){
  return num1*num2;
}
function calculator(num1,num2,operator){
  return operator(num1,num2);
}
console.log(calculator(4,5,add));
console.log(calculator(4,5,multiply));
```

```javascript
function multiplyBy(multiplier) {
    return function result(num) {
        return num * multiplier
    }
}multiplyByThree = multiplyBy(3)
multiplyByThree(4)------------
Output
------------
12
```

### [Introduction to CommonJS](https://flaviocopes.com/commonjs/)

The CommonJS module specification is the standard used in Node.js for working with modules. The huge [npm](https://flaviocopes.com/npm/) ecosystem is built upon this CommonJS format.

**Note:** Client-side JavaScript that runs in the browser uses another standard, called **ES Modules**

```javascript
//The syntax to import a module
const package = require('module-name')

```

Modules are loaded synchronously, and processed in the order the JavaScript runtime finds them. A JavaScript file is a module when it exports one or more of the symbols it defines, being them variables, functions, objects:

**uppercase.js**

```javascript
export.uppercase=(str)=>str.toUpperCase()
```

Any JavaScript file can import and use this module:

```javascript
const uppercaseModule = require('uppercase.js')
uppercaseModule.uppercase('test')

```

Learn more about Module system [here](https://blog.risingstack.com/node-js-at-scale-module-system-commonjs-require/)

### Build an HTTP Server

```javascript
const http = require('http')
const port = 3000
const server = http.createServer((req, res) => {
res.statusCode = 200
res.setHeader('Content-Type', 'text/plain')
res.end('Hello World\n')
})
server.listen(port, () => {
console.log(`Server running at http://${hostname}:${port}/`)
})
```

### Hello World

```javascript
const express = require('express')
const app = express()
app.get('/', (req, res) => res.send('Hello World!'))
app.listen(3000, () => console.log('Server ready'))
```

### Routing

Routing is the process of determining what should happen when a URL is called, or also which parts of the application should handle a specific incoming request.

```javascript
app.get('/', (req, res) => { /* */ })

// options 2
ap.get("/category/:<paramName". function(req.res){
       //Access req.params.paramName
       })
```

This creates a route that maps accessing the root domain URL / using the HTTP GET method to the response we want to provide.

### Templating

Express is capable of handling server-side template engines. Template engines allow us to add data to a view, and generate HTML dynamically.

Template engines (referred to as "view engines" by *Express*) allow you to specify the *structure* of an output document in a template, using placeholders for data that  will be filled in when a page is generated. Templates are often used to  create HTML, but can also create other types of documents. Express has  support for [a number of template engines](https://github.com/expressjs/express/wiki#template-engines), and there is a useful comparison of the more popular engines here: [Comparing JavaScript Templating Engines: Jade, Mustache, Dust and More](https://strongloop.com/strongblog/compare-javascript-templates-jade-mustache-dust/).

```javascript
app.set('view engine', 'ejs');
```

For more information see [Using template engines with Express](https://expressjs.com/en/guide/using-template-engines.html) (Express docs).

### Scope

**Local variables**

```javascript
function a{
var x=2;
console.log(x);
}
// x is not accessible in function b
function b{
console.log(x);
}
```

**Global Variables**

```javascript
var x=2;
function a {
console.log(x);
}
function b{
console.log(x);
}
```

[More on JS Scope](https://www.w3schools.com/js/js_scope.asp)

Variables declared with the `var` keyword can NOT have block scope. So try to avoid using var as much as possible. Instead use **let** and **const**.

Learn more about **var** [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)

Learn more about **let** [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) 

Learn more about **const** [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

### Creating our own Module

Example: First create a file date.js. Code below have two functions getDate which will give us a full date (Sunday September,19) and getDay which gives us a day(Sunday).

```javascript
// In date.js
module.exports.getDate=getDate;
function getDate(){
    
    let today=new Date();
    let options={
    weekday:"long",
    day:"numeric",
    month:"long"
};
let day=today.toLocaleDateString("en-US",options);
return day;
};

module.exports.getDay=getDay;
function getDay(){
    
    let today=new Date();
    let options={
    weekday:"long",
   
};
let day=today.toLocaleDateString("en-US",options);
return day;
};
```

```javascript
// In main app
......
const date = require(__dirname+"/date.js");
......
......
let day=date.getDate();
let day=date.getDay();

```

Refactoring our date.js module

```javascript
exports.getDate=function(){ 
    const today=new Date();
    const options={
    weekday:"long",
    day:"numeric",
    month:"long"
};
return today.toLocaleDateString("en-US",options);
};
exports.getDay=function(){
    
    const today=new Date();
    const options={
    weekday:"long", 
};
return today.toLocaleDateString("en-US",options);
};
```



### Reference

https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction

https://towardsdatascience.com/what-is-a-higher-order-function-12f5fd671e97

https://flaviocopes.com/commonjs/

https://flaviocopes.com/

https://www.w3schools.com/js/js_scope.asp

