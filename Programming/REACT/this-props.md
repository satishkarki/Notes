# THIS.PROPS

A component’s `props` is an object.  It holds information about that component.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Greeting extends React.Component {
  render() {
    return <h1> Hi there, {this.props.firstName}!</h1>;
  }
}

ReactDOM.render(
  <Greeting firstName='Satish' />, 
  document.getElementById('app')
);
```

```JSX
import React from 'react';
import ReactDOM from 'react-dom';

class PropsDisplayer extends React.Component {
  render() {
  	const stringProps = JSON.stringify(this.props);

    return (
      <div>
        <h1>CHECK OUT MY PROPS OBJECT</h1>
        <h2>{stringProps}</h2>
      </div>
    );
  }
}

// ReactDOM.render goes here:
ReactDOM.render(<PropsDisplayer myProp='Hello'/>, document.getElementById('app'));
```

```jsx
// Output
CHECK OUT MY PROPS OBJECT
{"myProp":"Hello"}
```

**Refresher**: JSON.stringify

It is a method that converts JavaScript object into a string. One use of this method is to store the object as a sting in the database and then convert back to an object when obtaining

```jsx
JSON.stringify({ a: 1, b: 2 });
// "{"a": 1, "b": 2}"
```

**Question: Can we perform expressions with in curly braces?**

Ans: Yes, any valid JavaScript expression can be placed inside of the curly  braces. The curly braces are special characters that tell the parser  that there is JavaScript code inside, and to run it as such. As a  result, you can run any JavaScript expression inside of it, and it will  be evaluated before the resulting HTML is returned.

```jsx
return <h1>{ this.props.value * 10 }</h1>

```

***

## Pass props from component to component

```jsx
//Greeting.js
import React from 'react';

export class Greeting extends React.Component {
  render() {
    return <h1>Hi there, {this.props.name}!</h1>;
  }
}
```

```jsx
//App.js
import React from 'react';
import ReactDOM from 'react-dom';
import {Greeting} from './Greeting.js'
class App extends React.Component {
  render() {
    return (
      <div>
        <Greeting name="Satish"/>
        <article>
          How to pass props?
        </article>
      </div>
    );
  }
}
ReactDOM.render(
  <App />, 
  document.getElementById('app')
);

//Output
Hi there, Satish
How to p
```

***

## Render Different UI Based on props

```jsx
//Greeting.js
import React from 'react';
import ReactDOM from 'react-dom';

export class Greeting extends React.Component {
  render() {
  	if (this.props.signedIn === false) {
  	  return <h1>GO AWAY</h1>;
  	} else {
  	  return <h1>Hi there, {this.props.name}!</h1>;
  	}
  }
}
```

```jsx
// App.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Greeting } from './Greeting';

class App extends React.Component {
  render() {
    return (
      <div>
        <Greeting name="Satish" signedIn={true} />
        <article>
          Greeting.js is checking if I am signed in or not?
        </article>
      </div>
    );
  }
}

ReactDOM.render(
  <App />, 
  document.getElementById('app')
);
```

***

## Event Handler in a Component Class

```jsx
import React from 'react';

class Example extends React.Component {
  handleEvent() {
    alert(`I am an event handler.
      If you see this message,
      then I have been called.`);
  }

  render() {
    return (
      <h1 onClick={this.handleEvent}>
        Hello world
      </h1>
    );
  }
}
```

- You define an event handler as a method on the component class, just like the *render* method

### Pass/Receive an EventHandler as a prop

```jsx
//PASS
import React from 'react';
import ReactDOM from 'react-dom';
import { Button } from './Button';

class Talker extends React.Component {
  talk() {
    let speech = '';
    for (let i = 0; i < 10000; i++) {
      speech += 'blah ';
    }
    alert(speech);
  }
  
  render() {
    return <Button talk={this.talk} />;
  }
}

ReactDOM.render(
  <Talker />,
  document.getElementById('app')
);
```

```jsx
//Receive
import React from 'react';

export class Button extends React.Component {
  render() {
    return (
      <button onClick={this.props.talk}>
        Click me!
      </button>
    );
  }
}
```

***

Above code can be written with proper naming conventions as following:

```jsx
//PASS
import React from 'react';
import ReactDOM from 'react-dom';
import { Button } from './Button';

class Talker extends React.Component {
  handleClick() {
    let speech = '';
    for (let i = 0; i < 10000; i++) {
      speech += 'blah ';
    }
    alert(speech);
  }
  
  render() {
    return <Button onClick={this.handleClick} />;
  }
}

ReactDOM.render(
  <Talker />,
  document.getElementById('app')
);
```

```jsx
//RECEIVE
import React from 'react';

export class Button extends React.Component {
  render() {
    return (
      <button onClick={this.props.onClick}>
        Click me!
      </button>
    );
  }
}
```

***

**Question: What happens if we pass the function with parentheses?**

**Ans:** [Find Out](https://discuss.codecademy.com/t/what-happens-if-we-pass-the-function-with-parentheses/398582)

**Question: Can we pass multiple event handlers as props and choose a specific one to attach to a child component?**

**Ans:** [Find Out](https://discuss.codecademy.com/t/can-we-pass-multiple-event-handlers-as-props-and-choose-a-specific-one-to-attach-to-a-child-component/398578)

***

## this.props.children

- Every component’s `props` object has a property named `children`
- `this.props.children` will return everything in between a component’s opening and closing JSX tags
- So far, all of the components that we have seen have been *self-closing tags*, such as `<MyComponentClass />`.  They don’t have to be!  We could write `<MyComponentClass></MyComponentClass>`, and it would still work.
- `this.props.children` would return everything in between `<MyComponentClass>` and `</MyComponentClass>`. 

```jsx
// Example 1
<BigButton>
  I am a child of BigButton.
</BigButton>
// this.props.children would equal the text, “I am a child of BigButton.”

// Example 2
<BigButton>
  <LilButton />
</BigButton>
//this.props.children would equal a <LilButton /> 

// Example 3
<BigButton />
// this.props.children would equal undefined
```

- If a component has more than one child between its JSX tags, then `this.props.children` will return those children in an array.  
- However, if a component has only one child, then `this.props.children` will return the single child, *not* wrapped in an array.

```jsx
// App.js
//PASS
import React from 'react';
import ReactDOM from 'react-dom';
import { List } from './List';

class App extends React.Component {
  render() {
    return (
      <div>
        <List type='Living Musician'>
          <li>Sachiko M</li>
          <li>Harvey Sid Fisher</li>
        </List>
        <List type='Living Cat Musician'>
          <li>Nora the Piano Cat</li>
        </List>
      </div>
    );
  }
}

ReactDOM.render(
  <App />, 
  document.getElementById('app')
);
```

```jsx
//List.js
//RECEIVE
import React from 'react';

export class List extends React.Component {
  render() {
    let titleText = `Favorite ${this.props.type}`;
    if (this.props.children instanceof Array) {
    	titleText += 's';
    }
    return (
      <div>
        <h1>{titleText}</h1>
        <ul>{this.props.children}</ul>
      </div>
    );
  }
}
```

```jsx
//OutPut
Favorite Living Musicians

    Sachiko M
    Harvey Sid Fisher

Favorite Living Cat Musician

    Nora the Piano Cat
    Dora the Piano Cat
```

***

## defaultProps

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Button extends React.Component {
  render() {
    return (
      <button>
        {this.props.text}
      </button>
    );
  }
}

// defaultProps goes here:
Button.defaultProps={
  text:'I am a button'
};

ReactDOM.render(
  <Button text="Click Me" />, 
  document.getElementById('app')
);

//Output
In ReactDOM if we delete text="Click Me", then the button will display "I am a button"
```

***

## References

https://www.codecademy.com

https://www.codecademy.com/learn/react-101/modules/learn-react-components-interacting/cheatsheet

