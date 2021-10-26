---
title: lib-state-recoil-faq
tags: [faq, react, recoil, state]
created: '1970-01-01T00:00:00.000Z'
modified: '2021-05-13T03:18:21.333Z'
---

# lib-state-recoil-faq

# faq-repeat

- recoil vs mobx
  - First of all, Recoil & MobX solve the same problem: efficient render widely shared state. 
    - This is a problem React (Context), Redux and most state management libs don't solve.
  - In that regard they are very similar. Hence terminology aligns: atoms, dep trees, derived data .
    - Roughly speaking Recoil offers observable.box + computed + useObserver from MobX. 
  - A difference is that Recoil builds on React primitives, the benefits are clear: Leaner, more easily compatible with concurrent mode, piggy back on React's batching. 
  - MobX in contrast is more general purpose and can be used in non-React projects and is even ported to different languages (eg Flutter) & doesn't need a React context to work or organize effects
  - MobX, like Recoil is build around atoms. But in MobX they are abstracted away in objects, maps, arrays, etc. 
    - More magic, but makes atoms easier composable/nestable. 
    - Concretely: no need to organize a separate atom for the collection (ids) & atoms for the individual objects
  - In MobX that is done under the hood for you by e.g. observable.array
  - More importantly, in MobX you always get an atom for each prop. 
  - That means that a component rendering one field, won't respond to updates in other fields in the same object. 
  - The same can be achieved in recoil, but you have to organize it yourself (either write a selector, or organize the state in smaller atoms). 
  - That brings us to the last important difference: In recoiljs you explicity specify what you consume. That is clearer, but also less optimal. 
  - Beyond being more course, due to the nature of react hooks, it has to be unconditional (or requires additional selectors). `<div>{user.loggedIn ? user.name : ""}</div>` will only subscribe to `user.name` as long as `user.loggedIn` is true in MobX. That is hard to achieve manually
  - To summarize: Recoil & MobX are similar: many, individual subscribable atoms (Redux has always one), enabling sideways comp updates + model that favors deriving & memoizing data. 
  - MobX offers higher level abstractions like maps and arrays based on atoms + transparent tracking
  - Recoil integrates much more closely with React and is purer. 
  - Disclaimer: above is based on just watching the talk, I haven't further used the project. Just want to elaborate on what looks similarly, and what differently to me. Definitely check it out!
  - May be a point worth clarifying: **Recoil is not concurrent mode compatible in its current form**.
  - Hopefully Recoil will soon integrate with the recent (still experimental) `useMutableSource` hook - at which point it will be concurrent mode compatible
  - ref
    - https://twitter.com/mweststrate/status/1261369872283467777

# faq

- Suggested folder structure for atoms and selectors
  - I think keeping state closer to where it is getting used is always more readable. 
  - And suppose if some new component is added which needs auth state then we can bring auth files file one level up.
  - Honestly, just put atoms and selectors in the same module as the components that use them. 
  - If they need to be used across multiple modules, only then put them in their own modules. 
  - Co-locate as closely as possible. Organize by feature. Just my two cents.
  - Also, a major aspect of Recoil as that atoms and selectors can be interchanged with each other. 
  - So I would not expose whether something is an atom or selector in its public interface. 
  - And a lot of the time you're going to be exporting hooks rather than the raw atom or selector.

-  Why do atom's and selector's have keys that are specified by the developer?
  - The main thing keys are used for is persistence
  - But, keys are intended to be used in a few use-cases where a persistent value is needed. For example, they are used to persist atom state in some way such as the URL, a backing store DB, etc. Another example is exposing the atom or selector in developer tools for debugging. (This hasn't been published yet)
  - We've discussed this internally. There were some proposals to add Recoil "zones/contexts", which would help solve the key namespace concern and help with composability. Though, this isn't the highest priority at the moment. In the meantime, we use conventions for namespacing keys, e.g. 'Module/Key'.
  - No current plans to allow non-opaque strings as atom/selector handles in the API. Generally we want to enforce that you're actually working with the same shared atom/selector, provide protection from string typos, etc. It has worked pretty well to export shared atoms/selectors from shared modules that can be imported from the components or selectors that need them.
  - ref
    - https://github.com/facebookexperimental/Recoil/issues/181
    - https://github.com/facebookexperimental/Recoil/issues/183
    - https://github.com/facebookexperimental/Recoil/issues/32

- atom vs selector
  - Atoms represent and maintain state while selectors represent functions. Use atoms when you need state and a selector when it is derived from other state or async requests.
  - In reality, atoms with asynchronous defaults are actually implemented by wrapping with a selector. It's provided as a convenience. 
  - So, to your original question, the atomFamily would actually construct selectors to get the async data as well as atoms with state that then go unused if you never set the atom.
  - If you want to pass a parameter to a selector then you might be looking for selectorFamily

- Is there a difference between atomFamily default and selectorFamily get?
  - One difference between `Atom::default` and `Selector::get` is that the `default` will only run once, but the Selector's `get` will run again if it accesses other RecoilValues. 
  - A difference in the behaviour for your code will be that `atomFamily` returns a ReadWrite RecoilValue, whereas the `selectorFamily` will return a read-only RecoilValue.
  - Another difference is that the current useTransactionObservation_UNSTABLE hook only provides access to atoms 
  - this may change in the future but it is an example of how Recoil could treat Atoms and Selectors differently. 
  - Over time more differences may appear between the two. 
  - For example a Recoil DevTools may display Atoms and Selectors differently.
  - https://github.com/facebookexperimental/Recoil/issues/230

-  I want it to re-render when a deep Node label changes
  - If you used an `atomFamily` per node, then your component rendering the tree would be subscribed to whatever nodes it used to render. 
  - To further limit that, you could have a component render the tree by rendering components for each node; those node components would then depend on the atom for that node. 
  - This way only the node with the label change would be re-rendered. 
  - Remember that values stored in atoms are immutable and frozen by default.
  - each component that is rendering a tree node should look it up by id
  - that would cause the component to only be subscribed to changes from that node.
  - https://github.com/facebookexperimental/Recoil/issues/316

``` JS
type ID = string;

type Node = {
  id: ID,
  label: string,
  children: $ReadOnlyArray < ID > ,
};

const treeState = atomFamily < ID,
  Node > ({
    key: 'Tree',
    default: id => ({ id, label: id, children: [] }),
  });
```

- If a selector can subscribe to an atom, but can also mutate that atom by being bi-directional using set. Why doesn't an infinite loop occur?
  - A selector depending on an atom value and setting an atom's value isn't sufficient to establish an infinite loop since there's no loop. 
  - If you set a selector that sets an atom which then causes the selector to reflect that value, then anyone else subscribing to the selector will now see the new value, but there's no loop there. 
  - A selector reflecting a new value from a change in its dependencies doesn't initiate the selector to "set" and change upstream. 
  - If you setup some component to subscribe to the selector changing values, and then immediately try to set or change the selector again, such as in an effect, then you would get a loop. 
  - But, that would be the same as if you just used an atom, React state, or anything else.

- In the spirit of a minimal api, why introduce `selectorFamily` ? why not use `selector(*args)` ?
  - Trying to keep the base core API minimal with selector. 
  - The selectorFamily is a helper that can be built on top of the core API as a convenience. 
  - But, it is not required to use nor part of the core API. 
  - We ended up including it in the primary package for convenience, but it's not required.

- I have a question about the best way (or even is it possible?) to change the state of atoms outside of the components.
  - **Recoil does not have global state**. 
  - Its store is coupled with the current React rendering tree. 
  - This will allow it to be compatible with the new Concurrent Mode with React. 
  - That does mean that we need to use hooks to access the state. That said, you can still use a hook to construct a callback that can allow you to update the state from an async action. 
  - Check out the the useRecoilCallback() hook. Perhaps this will work for your needs?
  - Atoms don't have a single value of truth—they reference the closest RecoilRoot, so what would accessing them globally mean?
  - A goal of Recoil is to support React Concurrent Mode, which means, unlike other state management libraries, it does not have a "global" state. 
  - Asynchronous rendering of components may occur concurrently with different "states". 
  - That is why it is important that all state access occur within the context of components or hooks, and their nearest encompassing `<RecoilRoot>` .
  - That said, we do understand the need for working and synchronizing with external state and events, and that it can be tedious to manage singleton components for these hooks. Therefore, we are working on an API to help with this pattern
  - ref
    - https://github.com/facebookexperimental/Recoil/issues/179
    - https://github.com/facebookexperimental/Recoil/issues/410

- How can i use atoms/selector from non-ui code ?
  - For proper support of React Concurrent Mode, Recoil does not have "global" state, unlike many other state management systems. 
  - With React CM, different parts of the tree may be asynchronously rendered with different versions of the state concurrently. 
  - So, all Recoil state is derived from hooks to obtain the "current" state for that rendering. 
  - That said, you can use those hooks, such as `useRecoilCallback()` to provide callbacks to access or set the state asynchronously.
  - ref
    - https://github.com/facebookexperimental/Recoil/issues/484

- Should we avoid keeping default values of atoms in memory?
  - Current behaviour is to store default value in memory for every atom once atomFamily called.
  - Suggestion: do not cache and do not store default value. Just call default() on demand on every render until another state is set.
  - I'm not sure if I should worry about having 1000 atoms filled with default values in the first place. Maybe it's fine as is?
  - If we already have 1000 atom objects in memory, having default values in isn't gonna add a lot to memory consumption. In your case, the default value is undefined, then it's even less a problem.
  - https://github.com/facebookexperimental/Recoil/issues/415

- What situations would it be more preferrable to use useContext over Recoil
  - I'm very biased ; ) , but I personally have found Recoil to be sufficient compared to using React context. Stylistic arguments could always be made, of course. 
  - Perhaps it might help in some cases where you want to share state without importing from a shared module.. 
  - Recoil doesn't require an all-or-nothing choice. The two systems can definitely co-exist; 
  - you don't need to choose and can use the one you prefer for a given situation, and we support some tools which do use both. One tool has a plug-in architecture and we have a mixture from that. 
  - Though, if you want to use Recoil for state persistence, then it helps to have all state you want to persist in that system.
  - If anyone has examples of situations where useContext enables something that doesn't work in Recoil it would be very interesting to see so that we can evaluate requirements.
  - https://github.com/facebookexperimental/Recoil/issues/177
  - Context remains useful for "infrastructure" components with parent-child relationships that are close together but not strictly direct descendants, especially as you get close to leaf nodes.
  - Examples that come to mind would be custom `<Menu>, <Tabs>, <CheckboxGroup>, <RadioGroup>` components, etc. I would 1000% use context for something like this
  - Note: the reason to use context instead of cloneElement in these components is so that your consumers can inject or escape the structure.

- Mobx-state-tree vs Recoil
  - First of all, Recoil & MobX solve the same problem: efficient render widely shared state.
  - This is a problem React (Context), Redux and most state management libs don't solve.
  - In that regard they are very similar. Hence terminology aligns: atoms, dep trees, derived data . Roughly speaking Recoil offers hobservable.box + computed + useObserver from MobX. 
  - A difference is that Recoil builds on React primitives, the benefits are clear:
    - Leaner, more easily compatible with concurrent mode, piggy back on React's batching. 
  - MobX in contrast is more general purpose and can be used in non-React projects and is even ported to different languages (eg Flutter) & doesn't need a React context to work or organize effects
  - MobX, like Recoil is build around atoms. But in MobX they are abstracted away in objects, maps, arrays, etc. More magic, but makes atoms easier composable / nestable. Concretely: no need to organize a separate atom for the collection (ids) & atoms for the individual objects
  - In MobX that is done under the hood for you by e.g. observable.array. More importantly, in MobX you always get an atom for each prop. That means that a component rendering one field, won't respond to updates in other fields in the same object. 
  - The same can be achieved in recoil, but you have to organize it yourself (either write a selector, or organize the state in smaller atoms). That brings us to the last important difference: 
  - In recoiljs you explicity specify what you consume. That is clearer, but also less optimal. 
  - Beyond being more course, due to the nature of react hooks, it has to be unconditional (or requires additional selectors). `<div>{user.loggedIn ? user.name : ""}</div>` will only subscribe to `user.name` as long `as user.loggedIn` is true in MobX. That is hard to achieve manually
  - To summarize: Recoil & MobX are similar: many, individual subscribable atoms (Redux has always one), enabling sideways comp updates + model that favors deriving & memoizing data. 
  - MobX offers higher level abstractions like maps and arrays based on atoms + transparent tracking
  - Recoil integrates much more closely with React and is purer. 
  - Disclaimer: above is based on just watching the talk, I haven't further used the project. Just want to elaborate on what looks similarly, and what differently to me. Definitely check it out!
  - One other big difference is that Recoil’s graph is async and async is handled in a quasi-functional manner. Not sure if MobX has an equivalent capability. Same API for state, sync derived, and async derived.
  - ref
    - https://twitter.com/mweststrate/status/1261369870152871937
    - https://www.youtube.com/watch?v=_ISAA_Jt9kI&list=PLCC436JpVnK0Q4WHoB85ZYBwcCyTaMgAl&index=1
