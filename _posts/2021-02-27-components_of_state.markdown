---
layout: post
title:      "Components of State"
date:       2021-02-27 23:00:09 -0500
permalink:  components_of_state
---

## Functional vs. Class
In the past, only class components had the capability of keeping track of state; functional components just accepted data to to display and were purely presentational. In fact, functional components used to be called "stateless components".

Now we have [`useState`](https://reactjs.org/docs/hooks-state.html). This is a hook (a special function that lets you “hook into” React features) that takes in an initial state as an argument and returns two values: the current state and the function that updates it. 

```
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
[(source)](https://reactjs.org/docs/hooks-state.html)

An equivalent class component would look like this:
```
import React, { Component } from 'react';

class Example extends Component {
 constructor(props) {
   super(props);
   this.state = {
     count: 0
   };

 render() {
   return (
     <div>
       <p>You clicked {this.state.count} times</p>
       <button onClick={() => this.setState({ count: this.state.count + 1 })}>
         Click me
       </button>
     </div>
   );
 }
}
```

In this case, `count` would be equivalent to `this.state.count` and `setCount` would equal `this.setState` if we were to implement this example as a class component. It should be noted that, unlike `this.setState`, updating a state variable declared using `useState` will always replace the current state instead of merging it.


### Thoughts
It appears that the fortification of functional components is making it the more popular component of the two. Functional components also have hooks that can replace the lifecycle methods which also used to be something exclusive to class components.
Not only are functional components lightweight and have a performance boost over class components, they are easier to read and test because they are plain JavaScript functions. Even though class components aren't quite on their way out, it seems that functional components are the way to go when building a new project in React.
