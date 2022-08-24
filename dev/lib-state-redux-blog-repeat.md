---
title: lib-state-redux-blog-repeat
tags: [blog, redux, repeat, state]
created: 2020-11-06T18:08:44.624Z
modified: 2021-05-13T03:20:00.313Z
---

# lib-state-redux-blog-repeat

# guide

- 基于hooks模仿redux的api
  - [State Management with React Hooks and Context API](https://devsmitra.medium.com/state-management-with-react-hooks-and-context-api-2968a5cf5c83)
  - [React doesn't need state management tool, I said](https://dev.to/tolgee_i18n/react-doesnt-need-state-management-tool-i-said-31l4)
    - https://github.com/tolgee/tolgee-platform/blob/main/webapp/src/fixtures/createProvider.tsx
# [You Might Not Need Redux_2016](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)
- Redux offers a tradeoff. It asks you to:
  - Describe application state as plain objects and arrays.[state]
  - Describe changes in the system as plain objects.[action]
  - Describe the logic for handling changes as pure functions.[reducer]
- None of these limitations are required to build an app, with or without React. In fact these are pretty strong constraints, and you should think carefully before adopting them even in parts of your app.
- These limitations are appealing to me because they help to
  - Persist state to a local storage 
  - Pre-fill state on the server, send it to the client in HTML 
  - Serialize user actions and attach them, together with a state snapshot, to automated bug reports, so that the product developers can replay them to reproduce the errors.
  - Pass action objects over the network to implement collaborative environments without dramatic changes to how the code is written.
  - Maintain an undo history or implement optimistic mutations without dramatic changes to how the code is written.
  - Travel between the state history in development, and re-evaluate the current state from the action history when the code changes, a la TDD.
  - Provide full inspection and control capabilities to the development tooling so that product developers can build custom tools for their apps.
  - Provide alternative UIs while reusing most of the business logic.
- However, if you’re just learning React, don’t make Redux your first choice. 
  - Instead learn to think in React. 
  - Come back to Redux if you find a real need for it, or if you want to try something new.
- Finally, don’t forget that you can apply ideas from Redux without using Redux.

```typescript
import React, { Component } from 'react';

class Counter extends Component {
  state = { value: 0 };

  increment = () => {
    this.setState(prevState => ({
      value: prevState.value + 1
    }));
  };

  decrement = () => {
    this.setState(prevState => ({
      value: prevState.value - 1
    }));
  };

  render() {
    return (
      <div>
        {this.state.value}
        <button onClick={this.increment}>+</button>
        <button onClick={this.decrement}>-</button>
      </div>
    )
  }
}
```

- The tradeoff that Redux offers is to add indirection to decouple “what happened” from “how things change”.
  - Is it always a good thing to do? No. It’s a tradeoff.

```typescript
import React, { Component } from 'react';

const counter = (state = { value: 0 }, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { value: state.value + 1 };
    case 'DECREMENT':
      return { value: state.value - 1 };
    default:
      return state;
  }
}

class Counter extends Component {
  state = counter(undefined, {});
  
  dispatch(action) {
    this.setState(prevState => counter(prevState, action));
  }

  increment = () => {
    this.dispatch({ type: 'INCREMENT' });
  };

  decrement = () => {
    this.dispatch({ type: 'DECREMENT' });
  };
  
  render() {
    return (
      <div>
        {this.state.value}
        <button onClick={this.increment}>+</button>
        <button onClick={this.decrement}>-</button>
      </div>
    )
  }
}
```

- we can extract a reducer from our component
- Redux library itself is only a set of helpers to “mount” reducers to a single global store object. 
  - You can use as little, or as much of Redux, as you like.
  - But if you trade something off, make sure you get something in return.
