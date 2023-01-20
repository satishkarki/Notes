# Hooks

React Hooks, plainly put, are functions that let us manage the internal  state of components and handle post-rendering side effects directly from our function components. 

React offers a number of built-in Hooks. A few of these include `useState()`, `useEffect()`, `useContext()`, `useReducer()`, and `useRef()`. See [the full list in the docs](https://reactjs.org/docs/hooks-reference.html). 

***

## Update Function Component State

### State Hook

```jsx
import React, { useState } from 'react';
```

`useState()` is a JavaScript function defined in the React library. When we call this function, it returns an array with two values:

- *current state* - the current value of this state
- *state setter* - a function that we can use to update the value of this state

Because React returns these two values in an array, we can assign them  to local variables, naming them whatever we like. For example: 

```jsx
const [toggle, setToggle] = useState();
```

***

### Example

```jsx
// import the default export and the named export `useState` from the 'react' library
import React,{useState} from "react";

export default function ColorPicker() {
  // call useState and assign its return values to `color` and `setColor`
const [color, setColor] = useState();
 const divStyle = {backgroundColor: color};

  return (
    <div style={divStyle}>
      <p>The color is {color}</p>
      <button onClick={() => setColor("Aquamarine")}>
        Aquamarine
      </button>
      <button onClick={() => setColor("BlueViolet")}>
        BlueViolet
      </button>
      <button onClick={() => setColor("Chartreuse")}>
        Chartreuse
      </button>
      <button onClick={() => setColor("CornflowerBlue")}>
        CornflowerBlue
      </button>
    </div>
  );
}

```

***

### Initialize State

