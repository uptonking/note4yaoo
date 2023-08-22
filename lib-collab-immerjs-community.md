---
title: lib-collab-immerjs-community
tags: [collaboration, community, immerjs]
created: 2023-06-04T21:26:40.284Z
modified: 2023-06-04T21:27:01.100Z
---

# lib-collab-immerjs-community

# guide

- who is using #immer-patches
  - webstudio
  - luckysheet

- resources
  - [Distributing state changes using snapshots, patches and actions — Part 1 | by Michel Weststrate | Medium](https://medium.com/@mweststrate/distributing-state-changes-using-snapshots-patches-and-actions-part-1-2811a2fcd65f)
  - [Distributing state changes using snapshots, patches and actions — Part 2 | by Michel Weststrate | Medium](https://medium.com/@mweststrate/distributing-state-changes-using-snapshots-patches-and-actions-part-2-2f50d8363988)
  - [Using Immer to compress Immer patches](https://medium.com/@dedels/using-immer-to-compress-immer-patches-f382835b6c69)
# dev

# discuss-collaboration
- ## 

- ## [add immer-yjs to built-with.md](https://github.com/immerjs/immer/pull/915)
- immer-yjs allows manipulating y.js data types with the api provided by immer.
- Two-way binding between y.js and plain (nested) json object/array.

- ## [Maintaining invariants with non-Immer managed derived state through applyPatches](https://github.com/immerjs/immer/issues/940)
  - Does Immer have any recommended "best practices" for this sort of thing?

- ## [Rebasing patches in collaborative editing](https://github.com/immerjs/immer/issues/410)
  - Implement a `rebase` function that transforms patches so that they can be applied to the state created by another array of patches.
  - Inspired by ProseMirror rebasing logic
- I've wrote about it a while ago
  - Beyond that, there are many ways in which one can reason about patches, but doing such things is not the goal of this library and can be implemented just as well in user-land / another library. 
  - Immer provides the raw patches, but any post processing as normalizing, minimising, compressing and rebasing go beyond the scope of this package.
- I didn't find the answer there unfortunately. It seems like replaying pending actions doesn't always preserve the right intent. Any tips on that? How do you deal with collab conflicts at Mendix?
  - That is because there is no generic solution to the problem, as it depends on the semantics.
- So telling how we solved it at Mendix is kind of irrelevant, because we are not operating in the same domain. 
  - But what we do is have meta information on every property and collection, that allows us to set conflict resolutions, e.g; is last winner ok, or should it cause conflict? 
  - And for collections: is ordering important, or not? As with non-important ordering concurrent adds are fine, just apply them in any order. Etc. etc. For further research, I suggest to google on "Operational Transformation", its a more advanced solution that might take you further.

# discuss
- ## 

- ## 

- ## [Introducing Immer: Immutability the easy way_201801](https://medium.com/hackernoon/introducing-immer-immutability-the-easy-way-9d73d8f71cb3)
- Immutable, structurally shared data structures are a great paradigm for storing state. 
  - Especially when combined with an event-sourcing architecture. 
  - However, there is a cost to pay. 
- In a language like JavaScript where immutability is not built into the language, producing a new state from the previous one is a boring, boiler-platy task. 
  - To prove the point: The Redux-ecosystem-links page alone lists 67(!) packages to help
- And still; most of them don’t solve the root problem: lack of language support. 
  - For example, where update-in is an elegant concept in a language like ClojureScript, any JavaScript counterparts will basically rely on ugly string paths.
- Immer works by writing producers
  - The produce function takes two arguments. The currentState and a producer function.
  - The producer function receives one argument, the draft, which is a proxy to the current state you passed in. Any modification you make to the draft will be recorded and used to produce nextState. The currentState will be untouched during this process.
- Because immer uses **structural sharing**, and our example producer above didn’t modify anything, the next state above is simply the state we started with.
  - that the parts of the state that were modified in the draft have resulted in new objects. However, unchanged parts are structurally shared with the previous state.
- The idea to produce the next immutable state by modifying a temporarily draft isn’t new. 
  - For example immutableJS provides a similar mechanism: withMutations. 
  - The big advantage of Immer however, is that you don’t have to learn (nor load) an entire new library for your data structures. Immer operates on normal JavaScript objects and arrays.

- ### How does Immer work?
  - 1) Copy-on-write. 
  - 2) Proxies
- Initially, when the producer starts, there is only one such proxy. 
  - It is the draft object that get’s passed into your function. 
  - Whenever you read any non-primitive value from that first proxy, it will in turn create a Proxy for that value. 
  - So that means that you end up with a proxy tree, that kind of overlays (or shadows) the original base tree. 
  - Yet, only the parts you have visited in the producer so far.
- Now, as soon as you try to change something on a proxy (directly or through any API), it will immediately create a shallow copy of the node in the source tree it is related to, and sets a flag “modified”.
  - From now on, any future read and write to that proxy will not end up in the source tree, but in the copy.

- ## [In Javascript, is there a way to create a copy-on-write clone of an object?](https://stackoverflow.com/questions/60242768/in-javascript-is-there-a-way-to-create-a-copy-on-write-clone-of-an-object)
- The immer library doing exactly what you describe - implementing COW using JavaScript proxies
