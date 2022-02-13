# JSX

- It is a syntax extension for JavaScript
- Syntax Extension: it means that JSX is not valid JavaScript, web browser cannot read it
- If a JavaScript file contains JSX it needs to be compiled first with  a JSX compiler to translate into regular JavaScript

```jsx
const h1=<h1>Hello World</h1>;
// The part that looks like HTML, <h1>Hello world</h1>, is something called JSX.
```

***

## JSX Element

A basic unit of JSX 

```jsx
<h1>Hello World</h1>
```

It is basically HTML code but written in JavaScript file.

### JSX Elements and their surrounding

- JSX elements are treated as expression
- JSX can be saved in a variable, passed to a function, stored inan object or array....you name it

```jsx
const userProfile={
name:<li> Satish karki</li>,
role:<li> Developer</li>,
position:<li>Intern</li>
};
```

***

### Attributes in JSX

Similar to HTML tags, JSX can have attributes with a format of `name=  'value'` pair. A single JSX element can have multiple attributes.

```JSX
const title=<h1 id='title'>Introduction to JSX</h1>;
```

We can also create our own custom attributes but make sure there is no white space in between the name.

***

### Nested JSX

We can use nested JSX just like in HTML but make sure you have your nested JSX within a parentheses if it is multi-line.

```jsx
 const theExample = (
   <a href="https://www.example.com">
     <h1>
       Click me!
     </h1>
   </a>
 );
```

***

### JSX Outer Elements

JSX elements must have exactly one outermost element.

```jsx
// This will work
const paragraphs = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph.</p>
    <p>I, too, am a paragraph.</p>
  </div>
);

//This will not work
const paragraphs = (
  <p>I am a paragraph.</p> 
  <p>I, too, am a paragraph.</p>
);
```

***

## Rendering JSX

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(<h1>Hello world</h1>, document.getElementById('app'));
```

- React is a JavaScript library for building UI and ReactDOM is the JavaScript library that allows React to interact with the DOM
- ReactDOM library contains several React-specific methods, all of which deals with [the DOM](http://www.w3schools.com/js/js_htmldom.asp) in some way or another

```jsx
ReactDOM.render(jsx expression, where to render it);

// The second argument acted as a container for jsx
```

Note: ReactDOM library is not included in the generic React library. And we can have multiple calls to ReactDOM.render() in a single JavaScript file.

***

### Passing a variable to ReactDOM.render()

```jsx
const toDoList = (
  <ol>
    <li>Learn React</li>
    <li>Become a Developer</li>
  </ol>
);
 
ReactDOM.render(
  toDoList, 
  document.getElementById('app')
);
```

- The first argument doesn't have to be  a JSX expression all the time, it could be a variable as well

***

## The Virtual DOM

- ReactDOM.render() only updates DOM elements that have been changed
- Only updating the necessary DOM elements is a large part of what makes React so successful
- By comparing the new virtual DOM with a pre-update version, React figures out *exactly which virtual DOM objects have changed.*  This process is called “diffing.”

### Summary

In summary, here’s what happens when you try to update the DOM in React:

- The entire virtual DOM gets updated.
- The virtual DOM gets compared to what it looked like before you updated it.  React figures out which objects have changed.
- The changed objects, and the changed objects only, get updated on the *real* DOM.
- Changes on the real DOM cause the screen to change. 

***

## References

https://www.codecademy.com

https://www.codecademy.com/articles/react-virtual-dom

