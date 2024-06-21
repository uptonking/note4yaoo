---
title: lib-state-recoil-dev
tags: [dev, react, recoil, state]
created: 2024-05-28T12:37:59.455Z
modified: 2021-05-13T03:18:13.613Z
---

# lib-state-recoil-dev

- recoil git repo is open sourced at 2020-05-04

# pieces

- It's not an error to store an atom in an atom. 
  - It doesn't do anything special, though.
  - We are adding a feature soon where atoms will be deleted when no longer used, together with another hook that lets a component retain an atom without subscribing to it. 
  - These could be combined into a utility that gives you a list of IDs with automatic deletion of the individual atoms when they are removed from the list.
  - Currently you have to use the `useResetRecoilState` hook to delete atoms.

- `atomFamily` is a Map of the params passed to the function and the created atom. i.e. `Map<params, Atom>` .
- `atomFamily` is a factory pattern which will dynamically generate an atom based on the serialization of the parameters. 
  - You only need to provide a single key for the atomFamily, it will generate a key for each individual atom based on serializing the parameters. 
  - You can "add" an atom to an atomFamily simply by calling it with a new parameter value. 
  - The state for an atom in the family can be removed via useResetRecoilState() hook, though the key currently remains registered. 
  - We have plans to look at automatic memory management of unused atoms.

- State sharing in different RecoilRoot components
  - Since Recoil relies on the context to propagate and store its state, it would be nice to have the ability to bridge this context, if it isn't propagated to all nodes in the tree.
  - Unfortunately, this is the case with ReactART (and friends) and the only proposed solution (for now) is to bridge the context using a "Consumer" with another "Provider" directly below it.
  - ref
    - https://github.com/facebookexperimental/Recoil/issues/140

- middleware
  - Have you tried using a read/write selector? 
  - It would essentially "wrap" the atom and you would then not call the atom directly where you want the middleware functionality
  - `useRecoilCallback` can work with multiple atoms
  - https://github.com/facebookexperimental/Recoil/issues/236

- Subscriptions are currently done at the granularity of atoms and selectors, when one is updated then all downstream components will re-render. 
  - We do plan to allow nodes to customize when they may propagate updates, so they could implement a diff or other equivalence check. 
  - Likely this can default to reference-quality for a good optimization.
- why do I need to define a unique `key` in atom
  - Having a string key is necessary to provide a fixture for state which survives past the lifetime of the app -- it enables scenarios such as debugging for dev tools, and stable persistence
- Right now Atoms are never removed from Recoil, so if you over the lifetime of an App you keep creating new Atoms/Selectors then you might end up with a memory leak. Though this may change in the future.
- We are adding a feature soon where atoms will be deleted when no longer used, together with another hook that lets a component retain an atom without subscribing to it. 
  - These could be combined into a utility that gives you a list of IDs with automatic deletion of the individual atoms when they are removed from the list.
  - Currently you have to use the useResetRecoilState hook to delete atoms.
  - https://github.com/facebookexperimental/Recoil/issues/30
  - To make a family of atoms, just create a memoized function that returns a distinct atom for each state
  - We are going to open-source a utility called `atomFamily` / `selectorFamily` that does this for you in the near future.
  - https://github.com/facebookexperimental/Recoil/issues/327
  - You don't want to randomly generate keys as discussed here. What you're probably looking for is the atomFamily.
- An atom should never be defined in a render function.   
  - They need to persist across renders to refer to the same state. 
  - Creating an atom is really a side-effect that is forbidden in React render functions.

- Multi-context is exactly the word I've been using to describe Recoil. 
  - You can think of an atomFamily as Recoil giving you a separate context `<Provider />` for each item, 
  - and you can subscribe to each one individually. I think of it as "multi-context".
- It's worth mentioning that, unlike Redux, Recoil state is not stored globally anywhere, but is specific to a particular React context. 
  - Not only that, but it's specific to a particular rendered tree (for concurrent mode, coming soon). 
  - So there is no "current state", just "the last committed state as seen by this particular component".
  - https://github.com/facebookexperimental/Recoil/issues/5
- In Recoil, state seems React based.
- The only thing to be aware of is that Recoil is bound to a particular React root and hence a particular renderer.   
  - You can use Recoil transaction observation to pass state changes between roots. 
  - React does not schedule changes across roots and I am told never plans to.

- Warning: Cannot update a component ( `Batcher` ) while rendering a different component ( `CharacterCount` ). To locate the bad `setState()` call inside `CharacterCount` , follow the stack trace as described in in CharacterCount (at RecoilApp.tsx:16)
  - I have this issue and I'm not using react hot module loading.
  - The Batcher's component's setState is the state setter that is being called, and the main cause is because replaceState from RecoilRoot is called when rendering subscribed components.
  - I understand that the main goal of the Batcher is to catch as many setState calls from subscribers as possible and delegate to react batching to gather queuedComponentCallbacks and optimize the count of re-renders.
  - I think to solve the problem without dropping the `Batcher` , a work loop that schedules when to flush the subscriptions is mandatory (may have its own problems though).
  - I'm working on a big refactor where dependencies will not go through React state at all. That will fix this (and make it a lot more efficient, and is needed for CM). In the meantime I don't see a an obvious workaround unfortunately.
  - Confirming Recoil breaking hmr/fast refresh.
  - ref
    - https://github.com/facebookexperimental/Recoil/issues/12

# guide

- ref
  - It appears recoil project has reinvented an idea that has existed for five years in a ClojureScript framework called re-frame. 
    - My guess is that some of the other ideas in that framework might also be of interest
    - https://github.com/facebookexperimental/Recoil/issues/46
    - https://github.com/day8/re-frame/blob/master/README.md
