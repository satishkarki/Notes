# LifeCycle Methods

The component lifecycle has three high-level parts:

1. *Mounting*, when the component is being initialized and put into the DOM for the first time
2. *Updating*, when the component updates as a result of changed state or changed props
3. *Unmounting*, when the component is being removed from the DOM

***

- React components have several methods, called *lifecycle methods*, that are called at different parts of a component’s lifecycle.
- We have already used two must common lifecycle methods: constructor() and render()
- `constructor()` is the first method called during the mounting phase. `render()` is called later during the mounting phase, to render the component for  the first time, and during the updating phase, to re-render the  component.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Clock extends React.Component {
  // Add your methods in here.
  constructor(props){
    super(props);
    this.state={date:new Date()};
  }
  render(){
    return(
    <div>{this.state.date.toLocaleTimeString()}</div>
    )
  }
}

ReactDOM.render(<Clock />, document.getElementById('app'));
```

**Question: Do the mounting lifecycle methods run more than once in a components's life?**

**Ans:** No, the mounting lifecycle methods (excluding `render`) are only run once in the entire life of a component.

This is because a component instance can only be mounted once and can never be mounted a second time. It is not possible to unmount and then  “remount” a component, because once the component is unmounted it is  permanently “destroyed” and cannot be mounted again.

***

## componentDidMount

`componentDidMount()` is the final method called during the mounting phase. The order is:

1. The constructor
2. `render()`
3. `componentDidMount()`

***

## componentWillUnmount

*In general, when a component produces a side-effect, you should remember to clean it up.*

```jsx
import React from 'react';

export class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }
  render() {
    return <div>{this.state.date.toLocaleTimeString()}</div>;
  }
  componentDidMount() {
    const oneSecond = 1000;
    this.intervalID=setInterval(() => {
      this.setState({ date: new Date() });
    }, oneSecond);
  }
  componentWillUnmount(){
    clearInterval(this.intervalID);
  }
}
```



