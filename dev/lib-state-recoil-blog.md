---
title: lib-state-recoil-blog
tags: [blog, recoil]
created: '2020-07-24T10:10:30.576Z'
modified: '2021-05-13T03:18:02.387Z'
---

# lib-state-recoil-blog

# Recoil - Ideal React State Management Library

- [Recoil - Ideal React State Management Library](https://dev.to/alexandrzavalii/recoil-ideal-react-state-management-library-1203)

- redux drawbacks
  - Ridiculous learning curve.
  - Boilerplate – reducers, actions, connectors.
  - Restructuring of Business logic
  - No “concurrent mode” support YET.
    - Concurrent mode is fixing fundamental limitation by making rendering interruptible.
    - As of now, React-Redux does not support it, but it is planning to introduce `useMutableSource` hook, that will make it compatible with "Concurrent Mode".
- context api drawbacks
  - Unpredictable and not performant updates.
    - context is designed for solving the prop drilling problem.
    - it is good to be used for low-frequency updates, such as theme or locale. 
    - If you move your global store in the value of the Provider, you will be losing out on performance. 
    - When a React `<Context.Provider>` gets a new value, all the components that consume that value are updated and have to render, even if a component only cares about part of the state.
  - No way of creating context dynamically.
    - Introducing another item would require placing another Context Provider at the top of the tree, which would cause the whole tree to unmount and mount again.
  - Context Wrapper Hell
  - No code split support
    - Because Context API introduces coupling between the roots of the tree and leaves of the tree, code splitting becomes nontrivial.
- recoil features
  - Very easy to learn, simple API.
  - Minimal boilerplate and reactish approach.
  - Performant granular updates.
  - Dynamically created state
  - Async Support.
  - No impact on code-splitting.
  - **Concurrent mode support**.

- Mark Erikson notes
  - To my knowledge, Recoil is not currently Concurrent Mode compatible. 
    - David McCabe made a couple comments on Reddit about investigating options like the upcoming `useMutableSource` hook, but I don't have a link to that discussion atm.
  - React-Redux will also eventually be using that `useMutableSource` hook when it's out, likely in a React-Redux v8 release. 
    - This won't make it "fully CM compatible", but it will likely be sufficient to allow React-Redux to work in a CM-configured React app
  - The Redux code splitting recipe you pointed to basically boils down to re-generating the root reducer by calling combineReducers again, and then passing that to store.replaceReducer()
  - I'm currently working on a major set of updates to the Redux core docs, including new tutorials and reorganized content. 
    - That said, you mentioned things like "where does my business logic go?", and we specifically already answer questions like that in the Redux FAQ. 
    - The new Redux Style Guide page also gives specific guidance on recommended patterns and best practices.
  - Finally, please check out our official Redux Toolkit package, which is specifically designed to simplify most common Redux use cases.
