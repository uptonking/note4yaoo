---
title: lib-state-redux-rewrite
tags: [react, redux, rewrite]
created: 1970-01-01T00:00:00.000Z
modified: 2021-05-13T03:44:33.382Z
---

# lib-state-redux-rewrite

# State Management with React Hooks and Context in 10 lines of code

- ref
  - [State Management with React Hooks and Context API in 10 lines of code](https://medium.com/simply/state-management-with-react-hooks-and-context-api-at-10-lines-of-code-baf6be8302c)

- useContext+useReducer
  - The only limitation is that this `useStateValue` function must be called inside functional component. Because it calls a useContext hook inside.

``` JS
import React, { createContext, useContext, useReducer } from 'react';
export const StateContext = createContext();
export const StateProvider = ({ reducer, initialState, children }) => (
  <StateContext.Provider value={useReducer(reducer, initialState)}>
    {children}
  </StateContext.Provider>
);
// a custom hook. It returns exactly the same [state, dispatch]
export const useStateValue = () => useContext(StateContext);
```

# Use Hooks + Context, not React + Redux

- ref
  - [Use Hooks + Context, not React + Redux](https://blog.logrocket.com/use-hooks-and-context-not-react-and-redux/)
- To a good extent, Redux works for state management in React applications and has a few advantages, but its verbosity makes it really difficult to pick up, and the ton of extra code needed to get it working in our application introduces a lot of unnecessary complexity.
- On the other hand, with the useContext API and React Hooks, there is no need to install external libraries or add a bunch of files and folders in order to get our app working. This makes it a much simpler, more straightforward way to handle global state management in React applications.

``` JS
// store.js
import React, { createContext, useReducer } from 'react';
const initialState = {};
const store = createContext(initialState);
const { Provider } = store;
const StateProvider = ({ children }) => {
  const [state, dispatch] = useReducer((state, action) => {
    switch (action.type) {
      case 'action description':
        const newState = // do something with the action
          return newState;
      default:
        throw new Error();
    };
  }, initialState);

  return <Provider value={{ state, dispatch }}>{children}</Provider>;
};
export { store, StateProvider }

// exampleComponent.js
import React, { useContext } from 'react';
import { store } from './store.js';

const ExampleComponent = () => {
  const globalState = useContext(store);
  console.log(globalState); // this will return { color: red }
};
```
