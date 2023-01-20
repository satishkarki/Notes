# Component Interact

- Render methods can also return another kind of JSX:  *component instances.*
- When a component renders another component, what happens is very similar to what happens when `ReactDOM.render()` renders a component.

```jsx
class OMG extends React.Component {
  render() {
    return <h1>Whooaa!</h1>;
  }
}
 
class Crazy extends React.Component {
  render() {
    return <OMG />;
  }
}
```

**Question: Why don't I need a ReactDOM.render() for each component?**

**Ans:** Imagine your app.js as a root component just like the trunk of a tree. And your components like the branches. And there are other sub branches that makes up the branches. Each component might look insignificant alone but together they from the structure of the app like a tree.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import SmallerBranch from '../SmallerBranch/SmallerBranch';

class Branch extends React.Component {
  
  render() {
    return(
      <div>
        <SmallerBranch/>
        <SmallerBranch/>
        <SmallerBranch/>
      </div>
    )
  }
}

export default Branch;
```

 ```jsx
 import React from 'react';
 import ReactDOM from 'react-dom';
 import Branch from '../Branch/Branch';
 
 class Trunk extends React.Component {
   
   render() {
     return(
       <div>
         <Branch/>
         <Branch/>
         <Branch/>
       </div>
     )
   }
 }
 
 ReactDOM.render(<Trunk/>, document.getElementById('root'));
 ```

***

## Require a File

- If you use an `import` statement, and the string at the end begins with either a dot or a slash, then `import` will treat that string as a *filepath*. 
- If your filepath doesn’t have a file extension, then “.js” is assumed.

> "Write code that is easy to delete, not easy to extend." 

```jsx

// NavBar.js
import React from 'react';

class NavBar extends React.Component {
  render() {
    const pages = ['home', 'blog', 'pics', 'bio', 'art', 'shop', 'about', 'contact'];
    const navLinks = pages.map(page => {
      return (
        <a href={'/' + page}>
          {page}
        </a>
      )
    });

    return <nav>{navLinks}</nav>;
  }
}
export default NavBar;
```

```jsx
// ProfilePage.js
import React from 'react';
import ReactDOM from 'react-dom';
import {NavBar} from './NavBar'

class ProfilePage extends React.Component {
  render() {
    return (
      <div>
        <NavBar/>
        <h1>All About Me!</h1>
        <p>I like movies and blah blah blah blah blah</p>
        <img src="some http link" />
      </div>
    );
  }
}
```

**Question: Why sometimes import has {} and sometimes doesn't?**

**Ans:** [Find Out](https://discuss.codecademy.com/t/why-sometimes-import-has-and-sometimes-doesnt/384837)

***

## Export

**Named Export**

```jsx
// Manifestos.js:
 
export const faveManifestos = {
  futurist: 'http://www.artype.de/Sammlung/pdf/russolo_noise.pdf',
  agile: 'https://agilemanifesto.org/iso/en/manifesto.html',
  cyborg:   'http://faculty.georgetown.edu/irvinem/theory/Haraway-CyborgManifesto-1.pdf'
};
```

```jsx
// Import faveManifestos and alsoRan from ./Manifestos.js:
import { faveManifestos, alsoRan } from './Manifestos';
 
// Use faveManifestos:
console.log(`A Cyborg Manifesto:  ${faveManifestos.cyborg}`); 
```

**Question: What would be the advantages of named exports over other exports?**

**Ans:** [Find Out](https://discuss.codecademy.com/t/what-would-be-the-advantage-of-named-exports-over-other-exports/385635)

***

## Reference

https://www.codecademy.com

