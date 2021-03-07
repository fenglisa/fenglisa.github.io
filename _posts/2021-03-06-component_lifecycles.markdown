---
layout: post
title:      "Component Lifecycles"
date:       2021-03-07 02:57:35 +0000
permalink:  component_lifecycles
---


Last week I talked about the state hook (`useState`) for React's functional components. This week I'll be diving into the effect hook: [`useEffect`](https://reactjs.org/docs/hooks-effect.html).

## Class vs. Functional
Traditionally, only class components were able to take advantage of methods designated to the three phases of a component's lifecycle: mounting, updating, and unmounting (the corresponding methods are: `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`). Now, we have `useEffect` for functional components, which essentially combines all three of those methods into one hook.

### Mounting and Updating
A class component with a `count` key in its state object would utilize the mounting and updating lifecycle methods like this:
```
componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }
  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }
```
Because we frequently want the same thing to happen whether the component has just been mounted or updated, there is identical code in both these methods. 

The equivalent effect in a functional component would look like this:
```
useEffect(() => {
    document.title = `You clicked ${count} times`;
  })
```
Because `useEffect` runs after every render *and* update, there's no need to separate the "mount" and "update". Effects will simply happen "after render".

### Unmounting
A class component with an `isOnline` key in its state object would utilize the mounting and unmounting lifecycle methods like this:
```
componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }
```
You'll notice that `componentDidMount()` and `componentWillUnmount()` have duplicate code (once again). Even though they are both related to the same effect, lifecycle methods have to split this into two different methods. 

The equivalent effect in a functional component would look like this:
```
useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Cleaning up after this effect:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  })
```
Every effect has the option to return a function that cleans up after it (the "unmounting" counterpart). 

### More Thoughts
Effects are scheduled everytime we re-render, replacing the previous effect. We can think of each effect being tied to a particular render. Apps built with `useEffect` will feel more responsive since it doesn't block the browser from updating the screen, like `componentDidMount` and `componentDidUpdate` will do. 

I'll admit, after looking more into these React hooks, I am eager for my next React app to utilize the full power of functional components.




