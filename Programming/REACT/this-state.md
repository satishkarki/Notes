# State

There are two ways for a component to get dynamic information:  `props` and `state`.  Besides `props` and `state`, every value used in a component should always stay exactly the same.

***

## Setting Initial State

Unlike `props`, a component’s `state` is *not* passed in from the outside.  A component decides its own `state`. 

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
	// constructor method begins here:
constructor(props){
  super(props);
  this.state={title:'Best App'}
}
	
  render() {
    return (
      <h1>
        Wow this entire app is just an h1.
      </h1>
    );
  }
}
```

- To make a component have `state`, give the component a `state` property.  This property should be declared inside of a constructor method
- `this.state` should be  equal to an object, like in the example above.  This object represents  the initial “state” of any component instance
-  `constructor` and `super` are both features of ES6, not unique to React
- It is important to note that React components *always* have to call `super` in their constructors to be set up properly
- Make sure *not* to separate `constructor` and `render` with a comma! Methods should never be comma-separated, if inside of a class body.

**Question: What values can you store in state?**

**Ans:** A React component’s state is a plain JavaScript object, so it can store  any valid value that is storable within a JavaScript object. This  includes booleans, strings, numbers, and even other objects which you  can nest within the state.

***

## Access a component's state

To *read* a component’s `state`, use the expression `this.state.name-of-property`

```jsx
class TodayImFeeling extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: 'decent' };
  }
 
  render() {
    return (
      <h1>
        I'm feeling {this.state.mood}!
      </h1>
    );
  }
}
```

**Question: Can  we access state properties using a bracket notation?**

**Ans:** Yes, component state is essentially a JavaScript object, so you can  access the properties using dot notation as well as bracket notation.

```jsx
this.state = {
  "key 1": value
}

/* Not valid */
this.state.key 1;

/* Valid */
this.state["key 1"];
```

Using bracket notation allows us to select property names that have  special characters or spaces that we otherwise could not select using  dot notation. 

***

## Update state with this.setState

- A component changes its state by calling the function `this.setState()`
- `this.setState()` takes two arguments:  an *object* that will update the component’s state, and a callback.  You basically never need the callback
- `this.setState()` takes an object, and *merges* that object with the component’s current state

```jsx
// Initial State
{
  mood:   'great',
  hungry: false
}

// update
this.setState({ hungry: true });

// Changed State
{
  mood:   'great',
  hungry: true
}
```

***

## Call this.setState from Another Function

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { weather: 'sunny' };
    this.makeSomeFog = this.makeSomeFog.bind(this);
  }
 
  makeSomeFog() {
    this.setState({
      weather: 'foggy'
    });
  }
}
```

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Mood extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: 'good' };
    this.toggleMood = this.toggleMood.bind(this);
  }

  toggleMood() {
    const newMood = this.state.mood == 'good' ? 'bad' : 'good';
    this.setState({ mood: newMood });
  }

  render() {
    return (
      <div>
            <h1>I'm feeling {this.state.mood}!</h1>
        <button onClick={this.toggleMood}> 
          Click Me
        </button>
      </div>
    );
  }
}

ReactDOM.render(<Mood />, document.getElementById('app'));
```

**Question: Can `this.setState` change multiple properties at once?**

**Ans:** Yes, you can use `this.setState` to change single,  multiple, or even all properties of state at a time. When setting state  for multiple properties, only the properties passed in will be updated.

For example, the following shows how the properties `key1` and `key3` of a state could be updated.

```jsx
/* Given this state */
this.state = {
  key1: value1,
  key2: value2,
  key3: value3
}

/* We could use code like the following to update specific properties */
this.setState({ key1: newValue1, key3: newValue3 });
```

***

Note: *Any time that you call this.setState(), this.setState() AUTOMATICALLY calls .render() as soon as the state has changed.*

- Think of `this.setState()` as actually being two things:  `this.setState()`, immediately followed by `.render()`
- *That* is why you can’t call `this.setState()` from inside of the `.render()` method!  `this.setState()` *automatically* calls `.render()`.  If `.render()` calls `this.setState()`, then an infinite loop is created

***

## References

https://www.codecademy.com/courses/react-101/lessons/this-state/exercises/this-state-intro

https://reactjs.org/docs/handling-events.html



