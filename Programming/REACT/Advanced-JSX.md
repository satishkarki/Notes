# Advanced JSX

## class VS className

In JSX you can't use the word `class`. You have to use `className` instead. JSX gets translated into JavaScript and `class` is a reserved word in JavaScript.

```jsx
// In HTML
<h1 class="big">Hey</h1>

// In JSX
<h1 className="big">Hey</h1>
```

**Note:*

- `class` - which will be `className` in JSX
- `for` - which will be `htmlFor` in JSX

To read about more HTML attributes that use different names in JSX, check the React documentation for *Tags and Attributes*.

***

## Self Closing Tags

Some tags in HTML like `<br>` `<img>`and `<input>` only uses one tag but in JSX we need to include slash.

```jsx
const profile = (
  <div>
    <h1>I AM JENKINS</h1>
    <img src="images/jenkins.png" />
    <article>
      I LIKE TO SIT
      <br/>
      JENKINS IS MY NAME
      <br/>
      THANKS HA LOT
    </article>
  </div>
);
```

***

## JavaScript written inside JSX expression

- If we want any expression to be treated as JavaScript inside of a JSX  element we need to wrap it in curly braces.  

- The curly braces themselves won’t be treated as JSX nor as JavaScript.  They are *markers* that signal the beginning and end of a JavaScript injection into JSX,  similar to the quotation marks that signal the boundaries of a string.

```jsx
ReactDOM.render(
  <h1>2 + 3</h1>,
  document.getElementById('app')
);
//Output
2+3

//Curly Braces in JSX
ReactDOM.render(
  <h1>{2 + 3}</h1>,
  document.getElementById('app')
);
//Output
5
```

```jsx
const math=(
  <h1>2+3={2+3}</h1>
)
ReactDOM.render(math,document.getElementById('app'));
//output
2+3=5
```

- Even when we assign a  JavaScript expression to a variable and want to use that variable inside JSX, the variable name needs to be wrapped in curly braces.

```jsx
 // `myVar` without curly braces will render as `myVar` in the browser, while `{myVar}` will render as `hello!` in the browser 

import React from 'react';
import ReactDOM from 'react-dom';

let myVar = 'hello!';

const myJsxElement = <h1>myVar value is {myVar}</h1>;

ReactDOM.render(
        myJsxElement,
        document.getElementById('app')
);
```

***

## Variables in JSX

Here, we assign a function to the variable `myFunc` then call the myFunc fuction from inside our JSX - this is especially useful if the logic inside myFunc would be difficult to read and understand from inside a JSX expression

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const myFunc  = (a, b) => {
  //do some logic or calculations with parameters here
}
ReactDOM.render(<h1>{myFunc(3,4)}</h1>, document.getElementById('app'));
```

***

## Variable Attributes in JSX

```jsx
const sideLength = "200px";
 
const panda = (
  <img 
    src="images/panda.jpg" 
    alt="panda" 
    height={sideLength} 
    width={sideLength} />
);
```

***

## Event Listners in JSX

- An event listener attribute’s *name* should be something like `onClick` or `onMouseOver`: the word `on`, plus the type of event that you’re listening for.  You can see a list of valid event names [here](http://facebook.github.io/react/docs/events.html#supported-events).
- An event listener attribute’s *value* should be a function.  
- In HTML event listner's name is written in lowercase where as in JSX it is written in camelCase.

```jsx
<img onClick={myFunc}/>
```

***

## JSX Conditionals

### If Statements that don't work

```jsx
//This code will break
(
  <h1>
    {
      if (purchase.complete) {
        'Thank you for placing an order!'
      }
    }
  </h1>
)
```

### If Statements that do work

**Refresher**: Conditional(ternary) operators

```javascript
condition ? exprIfTrue : exprIfFalse

var age = 26;
var beverage = (age >= 21) ? "Beer" : "Juice";
console.log(beverage); // "Beer"
```

```JSX
import ReactDOM from 'react-dom';

function coinToss() {
  // This function will randomly return either 'heads' or 'tails'.
  return Math.random() < 0.5 ? 'heads' : 'tails';
}

const pics = {
  kitty: 'https://content.codecademy.com/courses/React/react_photo-kitty.jpg',
  doggy: 'https://content.codecademy.com/courses/React/react_photo-puppy.jpeg'
};
let img;

// if/else statement begins here:
if (coinToss()==='heads'){
  img=(<img src={pics.kitty}/>
  );
} else {
   img=(
    <img src={pics.doggy}/>
  );
}
ReactDOM.render(img, document.getElementById('app'));

// Second Method
const img=<img src={pics[coinToss()==='heads'?'kitty':'doggy']}/>;

```

### JSX  Conditionals: &&

If the expression on the left of the `&&` evaluates as true, then the JSX on the right of the `&&` will be rendered. If the first expression is false, however, then the JSX to the right of the `&&` will be ignored and not rendered.

```jsx
const tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```

***

## .map in JSX

Array method `.map`

```jsx
// This is fine in JSX, not in an explicit array:
 
<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>
 
// This is also fine!
 
const liArray = [
  <li>item 1</li>, 
  <li>item 2</li>, 
  <li>item 3</li>
];
 
<ul>{liArray}</ul>
```

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const people = ['Rowe', 'Prevost', 'Gare'];

const peopleLis = people.map(person =>
  // expression goes here:
<li>{person}</li>
);

// ReactDOM.render goes here:
ReactDOM.render(<ul>{peopleLis}</ul>, document.getElementById('app'));
```

***

## Keys

- It is a JSX attribute.
- The attribute’s *name* is `key`.  The attribute’s *value* should be something unique, similar to an `id` attribute.
- `keys` don’t do anything that you can see!  React uses them internally to keep track of lists.  
- A list needs `keys` if either of the following are true:
  - The list-items have *memory* from one render to the next.  For instance, when a to-do list renders,  each item must “remember” whether it was checked off.  The items  shouldn’t get amnesia when they render.
  - A list’s order might be shuffled.  For instance, a list of search results might be shuffled from one render to the next.
- Each `key` must be a unique string that React can use to correctly pair each rendered element with its corresponding item in the array. 

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const people = ['Rowe', 'Prevost', 'Gare'];

const peopleLis = people.map((person, i) =>
  // expression goes here:
  <li key={'person_' + i}>{person}</li>
);

// ReactDOM.render goes here:
ReactDOM.render(<ul>{peopleLis}</ul>, document.getElementById('app'));
```

***

## React.createElement

- It is possible to write React code without JSX.
- Every JSX element is secretly a call to `React.createElement()`.

```jsx
// JSX expression
const h1 = <h1>Hello world</h1>;

// Without JSX expression
const h1 = React.createElement(
  "h1",
  null,
  "Hello, world"
);

```

***

## References

https://www.codecademy.com

https://www.codecademy.com/learn/react-101/modules/react-101-jsx-u/cheatsheet
