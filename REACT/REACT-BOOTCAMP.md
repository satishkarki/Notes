# REACT

## Introduction to JSX and Babel

```jsx
// ReactDOM.render(What to render, where to render)

ReactDOM.render(<h1>Hello World</h1>, documentgetElementById('root'));
```

***

**Babel**: Inside the React module, there is babel which is a JavaScript Compiler. It compiles next-gen javascript to plain old JavaScript.

[Link](https://babeljs.io/)

| REACT                                                        | JavaScript                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `ReactDOM.render(<h1>Hello World</h1>, documentgetElementById('root'));` | `ReactDOM.render( /*#__PURE__*/React.createElement("h1", null, "Hello World"), documentgetElementById('root'));` |

Online IDE to test code: [codesand](https://codesandbox.io)

**Note**; You can write JS expression within JSX but not the JS statement.

***

[**Tempelate Literals**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals): IN ES6 we have this feature.

```jsx
// normal expression
let a = 5;
let b = 10;
console.log('Fifteen is ' + (a + b) + ' and\nnot ' + (2 * a + b) + '.');
//Output
// "Fifteen is 15 and not 20."

//Using tempelate literals
let a = 5;
let b = 10;
console.log(`Fifteen is ${a + b} and
not ${2 * a + b}.`);
// Output
// "Fifteen is 15 and not 20.
```

***

## JSX Attribute and Styling React Element

- Attributes are `camelCased`
- Self closing tags

```jsx
<h1 class="heading"> My first heading</h1>

//In JS, the property to access all the class element is `Element.className`
<<h1 className="heading"> My first heading</h1>
```

```jsx
<script src='../src/index.js' type='text/javascript'></script>

<script src='../src/index.js' type='text/jsx'></script>
```

### Inline Styling for React

```jsx
const customStyle={
	color:'red',
	fontSize:'20px',
	border:'1px solid black'
}
ReactDOM.render(
	<h1 style={customStyle}>Hello World</h1>,
	document.getElementById('root')
);
```

**Example:**

```jsx
import React from "react";
import ReactDOM from "react-dom";

const date = new Date();
const currentTime = date.getHours();

let greeting;

const customStyle = {
  color: ""
};

if (currentTime < 12) {
  greeting = "Good Morning";
  customStyle.color = "red";
} else if (currentTime < 18) {
  greeting = "Good Afternoon";
  customStyle.color = "green";
} else {
  greeting = "Good Night";
  customStyle.color = "blue";
}

ReactDOM.render(
  <h1 className="heading" style={customStyle}>
    {greeting}
  </h1>,
  document.getElementById("root")
);
```

***

## React Component

```jsx
//Heading.jsx
import React from "react";

function Heading() {
  const date = new Date();
  const currentTime = date.getHours();

  let greeting;

  const customStyle = {
    color: ""
  };

  if (currentTime < 12) {
    greeting = "Good Morning";
    customStyle.color = "red";
  } else if (currentTime < 18) {
    greeting = "Good Afternoon";
    customStyle.color = "green";
  } else {
    greeting = "Good Night";
    customStyle.color = "blue";
  }

  return (
    <h1 className="heading" style={customStyle}>
      {greeting}
    </h1>
  );
}

export default Heading;


// App.jsx
import React from "react";
import Heading from "./Heading";

function App() {
  return (
    <div>
      <Heading />
    </div>
  );
}
export default App;

// index.js
import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App";

ReactDOM.render(<App />, document.getElementById("root"));
```

****

## JavaScript ES6 -Import, Export and Modules

```jsx
// math.js

const pi = 3.1415962;

function doublePi() {
  return pi * 2;
}

function triplePi() {
  return pi * 3;
}

export default pi;
export { doublePi, triplePi };


//index.js
import React from "react";
import ReactDOM from "react-dom";
import pi, { doublePi, triplePi } from "./math.js";

ReactDOM.render(
  <ul>
    <li>{pi}</li>
    <li>{doublePi()}</li>
    <li>{triplePi()}</li>
  </ul>,
  document.getElementById("root")
);
```

***

## Local Environment Setup for React Development

```bash
npx create-react-app my-app
cd my-app
npm start

```

***

## React Props

## Mapping Data to Components

## Map/Filter/Reduce

## JavaScript Arrow Function

## Conditional Rendering with Ternary Operator and &&

```jsx
// && in JS
(Expression && Expression)
(x>3 && x<7)

// && in React
Condition && Exxpression
true && Expression
false && noExpression
```

## State

- Declarative Programming
- Imperative Programming

## React Hook

useState()

## JavaScript ES6 Object and Array Destructuring

## Event  Handling in React

## React Form

Controlled Component

## Class Components vs  Functional Components

## ES6 Spread Operator

## Managing a Comonent Tree





