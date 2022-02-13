# Function Components

## Stateless Functional Components

```jsx
/ A component class written in the usual way:
export class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}

// The same component class, written as a stateless functional component:
export const MyComponentClass = () => {
  return <h1>Hello world</h1>;
}

// Works the same either way:
ReactDOM.render(
	<MyComponentClass />,
	document.getElementById('app')
);
```

In React, we can also define components as JavaScript functions — we call them *function components* to differentiate them from *class components*. 

**Question: Is a stateless functional component the same as a stateless component?**

**Ans: [Find Out](https://discuss.codecademy.com/t/is-a-stateless-functional-component-the-same-as-a-stateless-component/398723)**

***

## Function Components and Props

- To access these `props`, give your function component a parameter named `props`
- Within the function body, you can access the props using this pattern: `props.propertyName`. You don’t need to use the `this` keyword

```jsx
export function YesNoQuestion (props) {
  return (
    <div>
      <p>{props.prompt}</p>
      <input value="Yes" />
      <input value="No" />
    </div>
  );
}
 
ReactDOM.render(
  <YesNoQuestion prompt="Have you eaten an apple today?" />,
  document.getElementById('app');
);
```

**Question: Can a stateless functional component have more parameters?**

**Ans: [Find Out](https://discuss.codecademy.com/t/can-a-stateless-functional-component-have-more-parameters/398724)**

***

## Review

- *Function components* are React components defined as JavaScript functions
- Function components must return JSX
- Function components may accept a `props` parameter. Expect it to be a JavaScript object

***

