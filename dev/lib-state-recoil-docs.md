---
title: lib-state-recoil-docs
tags: [docs, react, recoil, state]
created: 2024-05-28T12:37:59.456Z
modified: 2020-12-08T13:27:02.442Z
---

# lib-state-recoil-docs

- A state management library for React
- Recoil is an experimental set of utilities for state management with React.

- **features**
  - Minimal and Reactish
    - Recoil works and thinks like React. 
    - Add some to your app and get fast and flexible shared state.
  - Data-Flow Graph
    - Derived data and asynchronous queries are tamed with pure functions and efficient subscriptions.
  - Cross-App Observation
    - persistence
    - routing
    - time-travel debugging
    - undo 
    - implemented by observing all state changes across your app, without impairing code-splitting.

# resources

- https://recoiljs.org/docs/introduction/getting-started
- https://github.com/facebookexperimental/Recoil

# Getting Started

- Components that use recoil state need `RecoilRoot` to appear somewhere in the parent tree. 
  - A good place to put this is in your root component
- An **atom** represents a piece of **state**.
  - Atoms can be read from and written to from any component. 
  - Components that read the value of an atom are implicitly subscribed to that atom, 
  - so any atom updates will result in a re-render of all components subscribed to that atom
- Components that need to read from and write to an atom should use `useRecoilState()`
- A **selector** represents a piece of **derived state**. 
  - Derived state is a transformation of state.
  - You can think of derived state as the output of passing state to a pure function that modifies the given state in some way

``` typescript
import React from 'react';
import {
  RecoilRoot,
  atom,
  selector,
  useRecoilState,
  useRecoilValue,
} from 'recoil';

function App() {
  return (
    <RecoilRoot>
      <CharacterCounter />
    </RecoilRoot>
  );
}

function CharacterCounter() {
  return (
    <div>
      <TextInput />
      <CharacterCount />
    </div>
  );
}

const textState = atom({
  key: 'textState', // unique ID (with respect to other atoms/selectors)
  default: '', // default value (aka initial value)
});

function TextInput() {
  const [text, setText] = useRecoilState(textState);

  const onChange = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <input type="text" value={text} onChange={onChange} />
      <br />
      Echo: {text}
    </div>
  );
}

const charCountState = selector({
  key: 'charCountState', // unique ID (with respect to other atoms/selectors)
  get: ({ get }) => {
    const text = get(textState);

    return text.length;
  },
});

function CharacterCount() {
  const count = useRecoilValue(charCountState);

  return <> Character Count: { count } </>;
}
```

# Motivation

- For reasons of compatibility and simplicity, it's best to use React's built-in state management capabilities rather than external global state. 
- But React has certain limitations:
  - Component state can only be shared by lifting it up to the common ancestor, but this might include a huge tree that then needs to re-render.
  - Context can only store a single value, not an indefinite set of values each with its own consumers.
  - Both of these make it difficult to code-split the top of the tree (where the state has to live) from the leaves of the tree (where the state is used).
- Recoil defines a directed graph orthogonal to but also intrinsic and attached to your React tree. 
- State changes flow from the roots of this graph (which we call atoms) through pure functions (which we call selectors) and into components. With this approach:
  - We get a boilerplate-free API where shared state has the same simple get/set interface as React local state (yet can be encapsulated with reducers etc. if needed).
  - We have the possibility of compatibility with Concurrent Mode and other new React features as they become available.
  - The state definition is incremental and distributed, making code-splitting possible.
  - State can be replaced with derived data without modifying the components that use it.
  - Derived data can move between being synchronous and asynchronous without modifying the components that use it.
  - We can treat navigation as a first-class concept, even encoding state transitions in links.
  - It's easy to persist the entire application state in a way that is backwards-compatible, so persisted states can survive application changes.

# Core Concepts

- Recoil lets you create a data-flow graph that flows from atoms (shared state) through selectors (pure functions) and down into your React components. 
- Atoms are units of state that components can subscribe to. 
- Selectors transform this state either synchronously or asynchronously.

``` JS
const fontSizeState = atom({
  key: 'fontSizeState',
  default: 14,
});
```

- **Atoms** are units of state. 
  - They're updateable and subscribable: when an atom is updated, each subscribed component is re-rendered with the new value. 
  - They can be created at runtime, too.
  - Atoms can be used in place of React local component state. 
  - If the same atom is used from multiple components, all those components share their state.
- Atoms need a globally unique key, which is used for debugging, persistence, and for certain advanced APIs that let you see a map of all atoms.
- To read and write an atom from a component, we use a hook called `useRecoilState` . 
  - It's just like React's `useState` , but now the state can be shared between components

``` JS
const fontSizeLabelState = selector({
  key: 'fontSizeLabelState',
  get: ({ get }) => {
    const fontSize = get(fontSizeState);
    const unit = 'px';

    return `${fontSize}${unit}` ;
  },
});
```

- A **selector** is a pure function that accepts atoms or other selectors as input. 
  - When these upstream atoms or selectors are updated, the selector function will be re-evaluated. 
  - Components can subscribe to selectors just like atoms, and will then be re-rendered when the selectors change.
- Selectors are used to calculate derived data that is based on state. 
  - This lets us avoid redundant state, usually obviating the need for reducers to keep state in sync and valid. 
  - Instead, a minimal set of state is stored in atoms, while everything else is efficiently computed as a function of that minimal state. 
  - Since selectors keep track of what components need them and what state they depend on, they make this functional approach more efficient.
  - From the point of view of components, selectors and atoms have the same interface and can therefore be substituted for one another.
- The `get` property is the function that is to be computed. 
  - It can access the value of atoms and other selectors using the `get` argument passed to it. 
  - Whenever it accesses another atom or selector, a dependency relationship is created such that updating the other atom or selector will cause this one to be recomputed.
- Selectors can be read using `useRecoilValue()` , which takes an atom or selector as an argument and returns the corresponding value. 
- A **Snapshot** is an immutable snapshot of the state of Recoil atoms.
  - This is intended to standardize the API for observing, inspecting, and managing global Recoil state and derived state. 
  - It’s useful for dev tools, global state synchronization, history, and navigation.

# Tutorial

- Atoms contain the source of truth for our application state. 
- In our todo-list, the source of truth will be an array of objects, with each object representing a todo item.
- A selector represents a piece of derived state.
- You can think of derived state as the output of passing state to a pure function that modifies the given state in some way.
- Derived state is a powerful concept because it lets us build dynamic data that depends on other data. 
- In the context of our todo list application, the following are considered derived state: 
  - Filtered todo list
  - Todo list statistics
- From a component's point of view, selectors can be read using the same hooks that are used to read atoms.
  - However it's important to note that certain hooks only work with writable state (i.e useRecoilState()).
  - All atoms are writable state, but only some selectors are considered writable state (selectors that have both a `get` and `set` property)

# Asynchronous Data Queries

- Recoil provides a way to map state and derived state to React components via a data-flow graph. 
  - What's really powerful is that the functions in the graph can also be asynchronous. 
  - This makes it easy to use asynchronous functions in synchronous React component render functions. 
  - Recoil allows you to seamlessly mix synchronous and asynchronous functions in your data-flow graph of selectors. 
  - Simply return a Promise to a value instead of the value itself from a selector get callback, the interface remains exactly the same.
  - Because these are just selectors, other selectors can also depend on them to further transform the data.
- Selectors can be used as one way to incorporate asynchronous data into the Recoil data-flow graph.
  - Please keep in mind that selectors represent pure functions: For a given set of inputs they should always produce the same results (at least for the lifetime of the application).
  - This is important as selector evaluations may execute one or more times, may be restarted, and may be cached. 
  - Because of this, selectors are a good way to model read-only DB queries where repeating a query provides consistent data. 
  - If you are looking to synchronize local and server state, then please see Asynchronous State Sync or State Persistence.
- The interface of the selector is the same, so the component using this selector doesn't need to care if it was backed with synchronous atom state, derived selector state, or asynchronous queries!
- But, since React render functions are synchronous, what will it render before the promise resolves? 
  - Recoil is designed to work with React `Suspense` to handle pending data. 
  - Wrapping your component with a Suspense boundary will catch any descendants that are still pending and render a fallback UI
- Recoil selectors can also throw errors which will then be thrown if a component tries to use that value. 
  - This can be caught with a React `<ErrorBoundary>` .
- Sometimes you want to be able to query based on parameters that aren't just based on derived state, but also on props
  - You can do that using the `selectorFamily`
  - pass props as query parameters
- Remember, by modeling queries as selectors, we can build a data-flow graph mixing state, derived state, and queries! 
  - This graph will automatically update and re-render React components as state is updated.
- You can use a concurrency helper such as `waitForAll` to run queries in parallel. This helper accepts both arrays and named objects of dependencies.
- You can use `waitForNone` to handle incremental updates to the UI with partial data
- For performance reasons you may wish to **kick off fetching before rendering**. 
  - That way the query can be going while we start rendering. 
  - The React docs give some examples. This pattern works with Recoil as well.
- It is not necessary to use React `Suspense` for handling pending asynchronous selectors. You can also use the `useRecoilValueLoadable()` hook to determine the status during rendering

# Asynchronous State Sync

- Recoil atoms represent local application state.
- Your application may have remote or server-side state as well, such as via a RESTful API. 
- Consider synchronizing the remote state with Recoil atoms. 
- Doing this allows you to easily access or write to the state from React components using the `useRecoilState()` hook, or use that state as input to the Recoil data-flow graph for other derived state selectors.
- If you're looking to query a database or server for read-only data, consider using asynchronous selectors.
- An advantage of using atoms to represent remote state is that you can use it as input for other derived state. 

# State Persistence

- Recoil allows you to persist application state using atoms.
- To save state, subscribe to atom changes and record the new state. 
- You could use React effects to subscribe to individual atoms (See Asynchronous State Sync). 
- However, Recoil provides a hook to allow you to subscribe to state changes for all atoms using `useTransactionObservation_UNSTABLE()` .
- The subscription callback provides all of the atom state and tells you which atoms changed. From this you can save the changes with the storage and serialization of your preference. 

``` JS
function PersistenceObserver() {
  useTransactionObservation_UNSTABLE(({ atomValues, atomInfo, modifiedAtoms }) => {
    for (const modifiedAtom of modifiedAtoms) {
      Storage.setItem(
        modifiedAtom,
        JSON.stringify({ value: atomValues.get(modifiedAtom) }),
      );
    }
  });
}
```

- `Storage` could be the browser URL history, LocalStorage, AsyncStorage or whichever storage you like.
  - atomValues - A Map of the atom keys and values.
  - modifiedAtoms - Gives you a map containing the modified atoms.
  - atomInfo - Atom metadata.
- You may not wish to persist all atoms, or some atoms may have different persistence behaviors. You can read metadata (NOTE: new API coming soon) to get options from each atom.
- Note that the current hook was designed for persistence and only reports atoms with special option 
  - property `persistence_UNSTABLE` which is an object with a non-null type property
- Restoring State can be done using the `initializeState` prop on the `<RecoilRoot>` component. 
  - `initializeState` is a function that provides a `set` method to provide the initial atom value for an atom key. 
  - Pass the key for the atom and the stored value to this callback and it will initialize the atom to the restored state.
  - Note that it is important to use this prop instead of just manually setting atom values in an effect.
  - Otherwise there will be an initial render without the restored state which can cause flicker or be invalid.
- You may also wish for asynchronous updates of the storage, such as the user pressing the browser back button with URL persistence, to sync with the current app state. 
- You can use a React effect to subscribe to these changes and update the value of any modified atoms directly.
