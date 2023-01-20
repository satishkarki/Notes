# JavaScript

## Web Console

- Open web developer tool of browser and go to console tab
- The console executes one code at a time
- To execute multiple code  press **SHIFT+ENTER**
- To execute multi-line code press **CTRL+B** in single line console and **CTRL+ENTER** to run it

## JavaScript can change

- HTML Content

  ```javascript
  document.getElementByID("demo").innerHTML="hello JavaScript";
  ```
  It accepts both double and single quotes

  ```javascript
  document.getElementByID('demo').innerHTML='hello JavaScript';
  ```

- It can change HTML Attribute Values

  ```html
  <img id="myImage" src="pic_bulboff.gif">
  <button onclick="document.getElementById('myImage').src='pic_bulbon.gif'">Turn on the light</button>
  ```

- It can change HTML Styles (CSS)

  ```html
  <p id="demo">JavaScript can change the style of an HTML element.</p>
  
  <button type="button" onclick="document.getElementById('demo').style.fontSize='35px'">Click Me!</button>
  ```

- It can hide/show HTML elements

  ```javascript
  document.getElementById("demo").style.display = "none"; 
  
  document.getElementById("demo").style.display = "block"; 
  ```

## Data Types 

- ```javascript
  String: let lastName = "Johnson";
  Number: let length = 16;
  Boolean: let x=True;
  Object : let x = {firstName:"John", lastName:"Doe"};
  ```

- typeof() command to check data type

- When adding a number and a string, JavaScript will treat the number as a  string

- JavaScript evaluates expressions from left to right. Different sequences can  produce different results

- JavaScript has dynamic types. This means that the same variable can be used  to hold  different data types

- JavaScript has only one type of numbers. Numbers can be written with, or without decimals

- JavaScript arrays are written with square brackets. Array indexes are zero-based, which means the first item is [0], second is  [1], and so on

- Empty Values: has nothing to do with `undefined`, an empty string has both a legal value and a type

  ```javascript
  //Example1
  let x = 16 + "Volvo"; 
  Result= 16Volvo
  
  //Example2
  let x = 16 + 4 + "Volvo";
  Result= 20Volvo
  
  let x;           // Now x is undefined
  x = 5;           // Now x is a Number
  x = "John";      // Now x is a String 
  
  let x1 = 34.00;     // Written with decimals
  let x2 = 34;        // Written without decimals
  
  const cars = ["Saab", "Volvo", "BMW"];
  
  let car = "";    // The value is "", the typeof is "string" 
  ```

## Variables

- There are 3 ways to declare a JavaScript variable:

  - var
  - let
  - const

- JavaScript variables are containers for storing data values

- All JavaScript **variables** must be **identified** with **unique names**

- These unique names are called **identifiers**

- You can declare many variables in one statement

  ```javascript
  //Example1
  var person = "John Doe", carName = "Volvo", price = 200;
  
  //Example2
  var person = "John Doe",
  carName = "Volvo",
  price = 200;
  ```

- If you re-declare a JavaScript variable, it will not lose its value

  ```javascript
  var carName = "Volvo";
  var carName;
  ```

- JavaScript let:
  - Variables defined with `let` cannot be Redeclared
  - Variables defined with `let` must be Declared before use
  - Variables defined with `let` have Block Scope
  - Block Scope: Before ES6 (2015), JavaScript had only **Global Scope** and **Function Scope**. ES6 introduced two important new JavaScript keywords: `let` and `const`. Variables declared inside a { } block cannot be accessed  from outside the block.

## Strings

- Length

  ```javascript
   let text = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  text.length;    // Will return 26 
  ```

- Escape Character

  ```javascript
  let text = "We are the so-called \"Vikings\" from the north."; 
  ```

- Slice() method

  This example slices out a portion of a string from position 7 to position 12 (13-1)

  ```javascript
  let str = "Apple, Banana, Kiwi";
  str.slice(7, 13)     // Returns Banana 
  ```

- toUpperCase() method

  ```javascript
   let text1 = "Hello World!";       // String
  let text2 = text1.toUpperCase();  // text2 is text1 converted to upper 
  
   let text1 = "Hello World!";       // String
  let text2 = text1.toLowerCase();  // text2 is text1 converted to lower 
  ```

  [More about String Methods](https://www.w3schools.com/js/js_string_methods.asp)

## Numbers

- JavaScript numbers are always stored as double precision floating point  numbers, following the international IEEE 754 standard

- This format  stores numbers in 64 bits, where the number (the fraction) is stored in bits 0  to 51, the exponent in bits 52 to 62, and the sign in bit 63

- `NaN` is a JavaScript reserved word indicating that a number is not a legal number

  ```javascript
  let x = 100 / "Apple";  // x will be NaN (Not a Number)
  ```

- JavaScript interprets numeric constants as hexadecimal if they are preceded by  0x

  ```javascript
   let x = 0xFF;        // x will be 255 
  ```

## Functions

- Creating a function

  ```javascript
  function myFunction(p1, p2) {
    return p1 * p2;   // The function returns the product of p1 and p2
  }
  
  // Calling a function
  myFunction(2,3);
  ```

- A Function is much the same as a Procedure or a Subroutine, in other programming languages
- Accessing a function without () will return the function object instead of  the function result
- Variables declared within a JavaScript function, become  **LOCAL** to  the function

# Intermediate JavaScript

## JavaScript Random 

```javascript
Math.random();
```

- `Math.random()` returns a random number between 0 (inclusive), and 1  (exclusive)

- `Math.random()` used with `Math.floor()` can be used to return random integers

- A proper random function:

  ```javascript
  //This JavaScript function always returns a random number between min (included) and max (excluded)
  function getRndInteger(min, max) {
    return Math.floor(Math.random() * (max - min) ) + min;
  }
  
  //This JavaScript function always returns a random number between min and max (both included)
  function getRndInteger(min, max) {
    return Math.floor(Math.random() * (max - min + 1) ) + min;
  }
  ```

## Control Statement

- If Else Statement

  ```javascript
  if (condition1) {
    //  block of code to be executed if condition1 is true
  } else if (condition2) {
    //  block of code to be executed if the condition1 is false and condition2 is true
  } else {
    //  block of code to be executed if the condition1 is false and condition2 is false
  }
  ```

- [Comparison Operators](https://www.w3schools.com/js/js_comparisons.asp)

- Conditional(Ternary) operator

  ```javascript
  // variablename = (condition) ? value1:value2 
  
  let voteable = (age < 18) ? "Too young":"Old enough"; 
  ```

- While Loop

  ```javascript
  while (condition) {
    // code block to be executed
  }
  ```

  If you forget to increase the variable used in the condition, the loop will never end. This will crash your browser.

- Do While Loop

  ```javascript
  do {
    // code block to be executed
  }
  while (condition);
  ```

  This loop will  execute the code block once, before checking if the condition is true, then it will repeat the loop as long as the condition is true.

- For Loop

  ```javascript
  for (statement 1; statement 2; statement 3) {
    // code block to be executed
  }
  ```

  

## [Arrays](https://www.w3schools.com/js/js_arrays.asp)

```javascript
const cars = ["Saab", "Volvo", "BMW"];

//Using keyword
const cars = new Array("Saab", "Volvo", "BMW");
```

- JavaScript arrays are used to store multiple values in a single  variable
- It is a common practice to declare arrays with the const keyword
- Arrays are a special type of objects. The `typeof` operator in JavaScript returns "object" for  arrays
- Arrays use **numbers** to access its "elements"
- Objects use **names** to access its "members"
- [Array Methods](https://www.w3schools.com/js/js_array_methods.asp)

***

#  Advanced JavaScript 

## Hoisting

JavaScript **Hoisting** refers to the process whereby the  interpreter allocates memory for variable and function declarations  prior to execution of the code. Declarations that are made using `var` are initialized with a default value of `undefined`. Declarations made using `let` and `const` are not initialized as part of hoisting.

[Learn More](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

***

## getter method

The **`get`** syntax binds an object property to a function  that will be called when that property is looked up.

```javascript
const obj = {
  log: ['a', 'b', 'c'],
  get latest() {
    if (this.log.length === 0) {
      return undefined;
    }
    return this.log[this.log.length - 1];
  }
};

console.log(obj.latest);
// expected output: "c"
```

[Learn More](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)

***

## this

A property of an execution context (global, function or eval) that, in non–strict mode,  is always a reference to an object and in strict mode can be any value.

```javascript
const test = {
  prop: 42,
  func: function() {
    return this.prop;
  },
};

console.log(test.func());
// expected output: 42
```

[Learn More](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

***

