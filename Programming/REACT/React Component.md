# REACT COMPONENT

A component is a small reusable chunk of code that is responsible for one job, that job is often to render some HTML.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
 
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
};
 
ReactDOM.render(
  <MyComponentClass />,
  document.getElementById('app')
);
```

***

## Import React

```jsx
import React from'react';
```

This creates an object named React which contains methods necessary to use the React library.

```jsx
import { functionA, functionB, functionC } from 'library';

import { Router, Switch } from 'react-router';
```

We can import multiple objects from a library at once.

***

## Import ReactDOM

```jsx
import ReactDOM from 'react-dom';
```

The methods imported from `react` don't deal with the DOM.

Note: ReactDOM method is not same as the component render() method.

***

## Component Class

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
 
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
 
ReactDOM.render(
    <MyComponentClass />, 
    document.getElementById('app')
);
```

- `React.Component` is a JavaScript *class*. To create your own component class, you must *subclass* `React.Component`.

- Component class variable names must begin with capital letters!

- Component Class is not a component!  A component class is more like a factory that produces components. 

- The body of component class must contain `render method`

  - render method is a property whose naem is `render` and value is a function
  - render method must contain a return statement
  - return statement usually returns a JSX expression

- Component Instances:

  ```jsx
  <MyDocumentClass/>
  ```

  Learn about [classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

***

## Logic in a Render Function

```jsx
class Random extends React.Component {
  render() {
    // First, some logic that must happen
    // before rendering:
    const n = Math.floor(Math.random() * 10 + 1);
    // Next, a return statement
    // using that logic:
    return <h1>The number is {n}!</h1>;
  }
}
```

***

## Condiional in a Render Function

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const fiftyFifty = Math.random() < 0.5;

// New component class starts here:
class TonightsPlan extends React.Component {
  render() {
    if (fiftyFifty) {
      return <h1>Tonight I'm going out WOOO</h1>;
    } else {
      return <h1>Tonight I'm going to bed WOOO</h1>;
    }
  }
}

ReactDOM.render(
	<TonightsPlan />,
	document.getElementById('app')
);
```

***

## Use `this` in a component

```jsx
class IceCreamGuy extends React.Component {
  get food() {
    return 'ice cream';
  }
 
  render() {
    return <h1>I like {this.food}.</h1>;
  }
}
```

- IceCreamGuy` has two methods:  `.food` and `.render()
- `this` refers to an instance of `IceCreamGuy`

**Q. Why don’t you need parentheses after `this.food`?  Shouldn’t it be `this.food()`?**

```jsx
 return <h1>I like {this.food}.</h1>;

 return <h1>I like {this.food()}.</h1>;
```

Ans: You don’t need those parentheses because `.food` is a *getter* method. You can tell this from the `get` in the above class declaration body.

Learn more about [this](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/)

Learn More about [getter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)

**Q: What happens if we don't use `this` when referencing a method from inside a class?**

Ans: [Find Out](https://discuss.codecademy.com/t/what-happens-if-i-dont-use-this-when-referencing-a-method-from-inside-a-class/408751)

***

## Event Listner in a Component

```jsx
class MyClass extends React.Component {
  myFunc() {
    alert('Stop it.  Stop hovering.');
  }
 
  render() {
    return (
      <div onHover={this.myFunc}>
      </div>
    );
  }
}
```

- Recall that an event *handler* is a function that gets called in response to an event.  In the above example, the event handler is `myFunc()`.
- In React, you define event handlers as *methods* on a component class.

**Question: Can I call multiple event handlers in response to a single event?**

Ans: [Find Out](https://discuss.codecademy.com/t/can-i-call-multiple-event-handlers-in-response-to-a-single-event/407324)

***

## Reference

https://www.codecademy.com

https://www.codecademy.com/learn/react-101/modules/learn-react-components/cheatsheet

