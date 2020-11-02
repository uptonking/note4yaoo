---
title: tmpl-redux
tags: [redux, template]
created: '2020-11-02T08:27:42.124Z'
modified: '2020-11-02T08:29:11.847Z'
---

# tmpl-redux

## demo

- ### [Getting Started with Redux](https://redux.js.org/introduction/getting-started)
- Following in the steps of Flux, CQRS, and Event Sourcing, 
  - Redux attempts to make state mutations predictable by imposing certain restrictions on how and when updates can happen.
- Redux can be described in [three fundamental principles](https://redux.js.org/understanding/thinking-in-redux/three-principles):
  - **单一数据源**
    - The global state of your application is stored in an object tree within a single store.
    - state可序列化、易调试、易实现redo/undo
  - **只读状态**
    - The only way to change the read-only state is to emit an action, an object describing what happened.
    - 视图交互和网络io的数据都只能发出更新状态的指令
    - Because all changes are centralized and happen one by one in a strict order, there are no subtle race conditions to watch out for.
  - **纯函数更新**
    - Changes are made with pure functions.
    - To specify how the state tree is transformed by actions, you write pure reducers.
    - reducer纯函数可拆分、可灵活控制计算逻辑

``` JS
import { createStore } from 'redux';

/**
 * reducer's function : (state, action) => 
 * 单一数据源、只读状态、纯函数更新
 */
function counterReducer(state = { value: 0 }, action) {
  switch (action.type) {
    case 'counter/incremented':
      return { value: state.value + 1 };
    case 'counter/decremented':
      return { value: state.value - 1 };
    default:
      return state
  }
}

// Its API is { subscribe, dispatch, getState }.
let store = createStore(counterReducer);

// use subscribe() to update the UI in response to state changes.
store.subscribe(() => console.log(store.getState()))

// The only way to mutate the internal state is to dispatch an action.
store.dispatch({ type: 'counter/incremented' })
```

- ### [Redux Toolkit Example](https://redux.js.org/introduction/getting-started)
  - redux-toolkit依赖redux, redux-thunk, immer, reselect
  - Redux Toolkit allows us to write shorter logic that's easier to read, while still following the same Redux behavior and data flow.

``` JS
import { createSlice, configureStore } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0
  },
  reducers: {
    incremented: state => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the Immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes
      state.value += 1
    },
    decremented: state => {
      state.value -= 1
    }
  }
});

export const { incremented, decremented } = counterSlice.actions;

const store = configureStore({
  reducer: counterSlice.reducer
});

store.subscribe(() => console.log(store.getState()));

// Still pass action objects to dispatch, but they're created for us
store.dispatch(incremented())
```
