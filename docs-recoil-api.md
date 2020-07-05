---
tags: [react, state]
title: docs-recoil-api
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-05T18:49:36.325Z'
---

# docs-recoil-api

## `<RecoilRoot ...props />`

- Provides the context in which atoms have values. 
- Must be an ancestor of any component that uses any Recoil hooks. 
- Multiple roots may co-exist; atoms will have distinct values within each root. 
- If they are nested, the innermost root will completely mask any outer roots.

## `atom(options)`

- An atom represents state in Recoil. 
- The `atom()` function returns a writeable `RecoilState` object.
- You can initialize an atom either with a static value or with a `Promise` or a `RecoilValue` representing a value of the same type. 
- Because the `Promise` may be pending or the default selector may be asynchronous it means that the atom value may also be pending or throw an error when reading. 
- Note that you cannot currently assign a Promise when setting an atom. 
- Please use selectors for async functions.
- Atoms cannot be used to store `Promise` s or `RecoilValue` s directly, 
  - but they may be wrapped in an object. 
  - Note that `Promise` s may be mutable.

## `selector(options)`

- Selectors represent a function, or derived state in Recoil. 
- You can think of them as a "pure function" without side-effects that always returns the same value for a given set of dependency values. 
- If only a `get` function is provided, the selector is read-only and returns a `RecoilValueReadOnly` object.
- If a `set` is also provided, it returns a writeable `RecoilState` object.
- A read-only selector has a `get` method which evaluates the value of the selector based on dependencies. 
  - If any of those dependencies are updated, then the selector will re-evaluate. 
  - The dependencies are dynamically determined based on the atoms or selectors you actually use when evaluating the selector. 
  - Depending on the values of the previous dependencies, you may dynamically use different additional dependencies.
  - Recoil will automatically update the current data-flow graph so that the selector is only subscribed to updates from the current set of dependencies
- A bi-directional selector receives the incoming value as a parameter and can use that to propagate the changes back upstream along the data-flow graph. 
  - Because the user may either set the selector with a new value or reset the selector, the incoming value is either of the same type that the selector represents or a `DefaultValue` object which represents a reset action.
- Selectors may also have asynchronous evaluation functions and return a Promise to the output value.

## `useRecoilState(state)`

- Returns a tuple where the first element is the value of state 
  - and the second element is a setter function that will update the value of the given state when called.
- This hook will implicitly subscribe the component to the given state.
- `state` parameter is an atom or a writeable selector.
  - Writeable selectors are selectors that have both a `get` and `set` in their definition 
  - while read-only selectors only have a `get` .
- This API is similar to the `useState()` hook 
  - except it takes a Recoil state instead of a default value as an argument. 
- It returns a tuple of the current value of the state and a setter function. 
  - The setter function may either take a new value as an argument or an updater function which receives the previous value as a parameter.
- This is the recommended hook to use when a component intends to read and write state.
- Using this hook in a React component will subscribe the component to re-render when the state is updated. 
- This hook may throw if the state has an error or is pending asynchronous resolution.

## `useRecoilValue(state)`

- Returns the value of the given Recoil state.
- This hook will implicitly subscribe the component to the given state.
- This is the recommended hook to use when a component intends to read state without writing to it, as this hook works with both read-only state and writeable state. 
- Atoms are writeable state while selectors may be either read-only or writeable
- Using this hook in a React component will subscribe the component to re-render when the state is updated

## `Loadable` class

- A `Loadable` object represents the current state of a Recoil atom or selector. 
- This state may either have a value available, may be in an error state, or may still be pending asynchronous resolution.
- A Loadable has the following interface:
- `state`
  - The current state of the atom or selector. 
  - Possible values are 'hasValue', 'hasError', or 'loading'.
- `contents`
  - The value represented by this Loadable.
  - If the state is hasValue, it is the actual value, if the state is hasError it is the Error object that was thrown, and if the state is loading, then it is a Promise of the value.
- Loadables also contain helper methods for accessing the current state. 
