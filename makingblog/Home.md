# Creating my Portfolio

 ***Part 2***

## 1. Typed.js

**References**

 [Typing Effect in React](https://dev.to/shareef/typing-effect-in-react-with-typed-js-and-hooks-5bl2)

[The Complete Guide to useRef() and Refs](https://dmitripavlutin.com/react-useref-guide/) 



```bash
npm install typed.js
```

```jsx
import Typed from "typed.js";
import { useEffect, useRef } from "react";

function ScrollInfo() {
  // Create Ref element.
  const el = useRef(null);

  useEffect(() => {
    const typed = new Typed(el.current, {
      strings: ["Caffeinated", "Curious", "Persistence","Motivated"], 
      startDelay: 3000,
      typeSpeed: 100,
      backSpeed: 100,
      backDelay: 500,
      smartBackspace:true,
      showCursor:false,
      loop: false
      
    });

    // Destropying
    return () => {
      typed.destroy();
    };
  }, []);

  return (
    <div>
      <h1>Hi there! I am always</h1>
      {/* Element to display typing strings */}
      <span ref={el}></span>
    </div>
  );
}
export default ScrollInfo;
```

