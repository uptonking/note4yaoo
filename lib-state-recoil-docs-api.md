---
title: lib-state-recoil-docs-api
tags: [api, docs, react, recoil, state]
created: '1970-01-01T00:00:00.000Z'
modified: '2020-12-08T13:27:07.981Z'
---

# lib-state-recoil-docs-api

# `<RecoilRoot ...props />`

- Provides the context in which atoms have values. 
- Must be an ancestor of any component that uses any Recoil hooks. 
- Multiple roots may co-exist; atoms will have distinct values within each root. 
- If they are nested, the innermost root will completely mask any outer roots.

# `atom(options)`

- An atom represents state in Recoil. 
- The `atom()` function returns a writeable `RecoilState` object.
- You can initialize an atom either with a static value or with a `Promise` or a `RecoilValue` representing a value of the same type. 
- Because the `Promise` may be pending or the default selector may be asynchronous it means that the atom value may also be pending or throw an error when reading. 
- Note that you cannot currently assign a Promise when setting an atom. 
- Please use selectors for async functions.
- Atoms cannot be used to store `Promise` s or `RecoilValue` s directly, 
  - but they may be wrapped in an object. 
  - Note that `Promise` s may be mutable.

# `selector(options)`

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

# `useRecoilState(state)`

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

# `useRecoilValue(state)`

- Returns the value of the given Recoil state.
- This hook will implicitly subscribe the component to the given state.
- This is the recommended hook to use when a component intends to read state without writing to it, as this hook works with both read-only state and writeable state. 
- Atoms are writeable state while selectors may be either read-only or writeable
- Using this hook in a React component will subscribe the component to re-render when the state is updated

# `useRecoilStateLoadable(state)`

- This hook is intended to be used for reading the value of asynchronous selectors. 
- This hook will implicitly subscribe the component to the given state.
- Unlike `useRecoilState()` , this hook will not throw an Error or Promise when reading from an asynchronous selector (for the purpose of working alongside React Suspense).
- Instead, this hook returns a `Loadable` object for the value along with the setter callback.

# `atomFamily(options)`

- Returns a function that returns a writeable RecoilState atom.
- An atom represents a piece of state with Recoil.
- An atom is created and registered per `<RecoilRoot>` by your app.
- What if your state is associated with a particular instance of a control, or with a particular element? 
  - For example, maybe your app is a UI prototyping tool where the user can dynamically add elements and each element has state, such as its position. 
  - Ideally, each element would get its own atom of state. 
  - You could implement this yourself via a memoization pattern. 
  - But, Recoil provides this pattern for you with the `atomFamily` utility. 
- An Atom Family represents a collection of atoms.
- When you call `atomFamily` , it will return a function which provides the `RecoilState` atom based on the parameters you pass in.
- The `atomFamily` essentially provides a map from the parameter to a atom. 
- You only need to provide a single `key` for the `atomFamily` and it will generate a unique key for each underlying atom. 
- These atom keys can be used for persistence, and so must be stable across application executions. 
- The parameters may also be generated at different callsites and we want equivalent parameters to use the same underlying atom. 
- Therefore, value-equality is used instead of reference-equality for atomFamily parameters. 
- This imposes restrictions on the types which can be used for the parameter. 
- `atomFamily` accepts primitive types, or arrays or objects which can contain arrays, objects, or primitive types.

``` JS
const elementPositionStateFamily = atomFamily({
  key: 'ElementPosition',
  default: [0, 0],
});

function ElementListItem({ elementID }) {
  const position = useRecoilValue(elementPositionStateFamily(elementID));
  return (
    <div>
      Element: {elementID}
      Position: {position}
    </div>
  );
}
```

- One advantage of using this pattern for separate atoms for each element over trying to store a single atom with a map of state for all elements is that they all maintain their own individual subscriptions.
- So, updating the value for one element will only cause React components that have subscribed to just that atom to update.
- Persistence observers will persist the state for each parameter value as a distinct atom with a unique key based on serialization of the parameter value used. 
  - Therefore, it is important to only use parameters which are primitives or simple compound objects containing primitives. 
  - Custom classes or functions are not allowed.
- It is allowed to “upgrade” a simple atom to be an atomFamily in a newer version of your app based on the same key. 
- If you do this, then any persisted values with the old simple key can still be read and all parameter values of the new `atomFamily` will default to the persisted state of the simple atom. 
- If you change the format of the parameter in an `atomFamily` , however, it will not automatically read the previous values that were persisted before the change. 
- However, you can add logic in a default selector or validator to lookup values based on previous parameter formats. 
- We hope to help automate this pattern in the future.

# `selectorFamily(options)`

- Returns a function that returns a read-only `RecoilValueReadOnly` or writeable `RecoilState` selector.
- A `selectorFamily` is a powerful pattern that is similar to a selector, but allows you to pass parameters to the get and set callbacks of a selector. 
- The `selectorFamily()` utility returns a function which can be called with user-defined parameters and returns a selector. 
- Each unique parameter value will return the same memoized selector instance.
- The `selectorFamily` essentially provides a map from the parameter to a selector. 
- Because the parameters are often generated at the callsites using the family, and we want equivalent parameters to re-use the same underlying selector, it uses value-equality by default instead of reference-equality. (There is an unstable cacheImplementationForParams API to adjust this behavior). 
- This imposes restrictions on the types which can be used for the parameter. 
- Please use a primitive type or an object that can be serialized. 
- Recoil uses a custom serializer that can support objects and arrays, some containers (such as ES6 Sets and Maps), is invariant of object key ordering, supports Symbols, Iterables, and uses toJSON properties for custom serialization (such as provided with libraries like Immutable containers). 
- Using functions or mutable objects, such as Promises, in parameters is problematic.

# class `Loadable`

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

# class `Snapshot`

- A Snapshot object represents an immutable snapshot of the state of Recoil atoms. 
- It is intended to standardize the API for observing, inspecting, and managing global Recoil state. 
- It is mostly useful for dev tools, global state synchronization, history navigation, &c.
- Snapshots are read-only with respect to atom state. 
  - They can be used to read atom state and evaluate selectors' derived state.
  - The getPromise() method can be used to wait for the evaluated value of asynchronous selectors, so you can see what the value would be based on the static atom state.
- While snapshots are immutable, they have methods to map themselves with a set of transformations to a new immutable snapshot. 
  - The map methods take a callback that is passed a MutableSnapshot, which is mutated throughout the callback and will ultimately become the new snapshot returned by the mapping operation.
- The `<RecoilRoot>` component takes an `initializeState` prop for initializing the global state via a `MutableSnapshot` . 
  - This can be helpful for loading persisted state when you know all atoms in advance and is compatible with server-side rendering where the state should be setup synchronously with the initial render. 
  - For most state initialization and persistence, though, consider Atom Effects.

# `useRecoilCallback(callback, deps)`

- This hook is similar to `useCallback()` , but will also provide an API for your callbacks to work with Recoil state. 
- This hook can be used to construct a callback that has access to a read-only `Snapshot` of Recoil state and the ability to asynchronously update current Recoil state.
- Some motivations for using this hook may include:
  - Asynchronously read Recoil state without subscribing a React component to re-render if the atom or selector is updated.
  - Deferring expensive lookups to an async action that you don't want to do at render-time.
  - Performing side-effects where you would like to also read or write to Recoil state.
  - Dynamically updating an atom or selector where we may not know at render-time which atom or selector we will want to update, so we can't use `useSetRecoilState()` .
  - Pre-fetching data before rendering.
- ref
  - https://recoiljs.org/docs/api-reference/core/useRecoilCallback

# `waitForAll(dependencies)`

- A concurrency helper which allows us to concurrently evaluate multiple asynchronous dependencies.
- The dependencies may either be provided as a tuple array or as named dependencies in an object.
- Because the concurrency helper is provided as a selector, it may be used by Recoil hooks in a React component, as a dependency in a Recoil selector, or anywhere a Recoil state is used.

# `waitForAny(dependencies)`

- A concurrency helper that returns a set of `Loadable` s for the current state of the requested dependencies. 
- It waits until at least one of the dependencies are available.
- `waitForAny()` is similar to `waitForNone()` , except that it waits until at least one dependency has a value available instead of returning immediately.

# `waitForNone(dependencies)`

- A concurrency helper that returns a set of `Loadable` s for the current state of the requested dependencies.
- `waitForNone()` is similar to `waitForAll()` , except that it returns immediately and returns a Loadable for each dependency instead of the values directly. 
- It is similar to `noWait()` , except that it allows requesting multiple dependencies at once.
- This helper is useful for working with partial data or incrementally updating the UI as different data becomes available.

# `noWait(state)`

- A selector helper that will return a `Loadable` for the current state of the provided `atom` or `selector` .
- This helper can be used to obtain the current state of a potentially asynchronous dependency without throwing if there is an error or the dependency is still pending. 
- It is similar to `useRecoilValueLoadable(` ) except that it is a selector instead of a hook. 
- Because `noWait()` returns a selector, it can in turn be used by other Recoil selectors as well as hooks.

# `constSelector(constant)`

- A selector which always provides a constant value.
- A `constSelector` may be useful if you have an interface that uses a type such as `RecoilValue<T>` or `RecoilValueReadOnly<T>` that may be provided by different selector implementations.
- These selectors will memoize based on reference value equality. 
- So, `constSelector()` can be called multiple times with the same value and the same selector will be provided. 
- Because of this, the value used as a constant is restricted to types that may be serialized using the Recoil serialization. 
- Please see documentation in selectorFamily describing the limitations.

# `errorSelector(message)`

- A selector which always throws the provided error
