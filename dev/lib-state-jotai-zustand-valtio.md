---
title: lib-state-jotai-zustand-valtio
tags: [jotai, valtio, zustand]
created: 2022-01-05T14:25:43.576Z
modified: 2022-01-05T14:36:28.057Z
---

# lib-state-jotai-zustand-valtio

# guide

- ref
  - [npm trends: jotai vs recoil vs valtio vs zustand](https://www.npmtrends.com/jotai-vs-recoil-vs-valtio-vs-zustand)

- zustand  /12.6kStar/MIT/202201/ts/NoDeps/Flux
  - https://github.com/pmndrs/zustand
  - https://zustand.surge.sh/
  - A small, fast and scalable bearbones state-management solution using simplified flux principles.
  - Why zustand over redux?
    - Simple and un-opinionated
    - Makes hooks the primary means of consuming state
    - Doesn't wrap your app in context providers
    - Can inform components transiently (without causing render)
  - Why zustand over context?
    - Less boilerplate
    - Renders components only on changes
    - Centralized, action-based state management
  - deal with common pitfalls, like the dreaded zombie child problem, react concurrency, and context loss between mixed renderers
  - Zustand's core(`zustand/vanilla`) can be imported and used without the React dependency. 

- jotai  /6.7kStar/MIT/202201/ts/Atoms
  - https://github.com/pmndrs/jotai
  - https://jotai.org/
  - Primitive and flexible state management for React
  - How does Jotai differ from Recoil?
    - Minimalistic API
    - No string keys
    - TypeScript oriented

- valtio  /3.5kStar/MIT/202112/ts
  - https://github.com/pmndrs/valtio
  - http://valtio-demo.pmnd.rs/
  - Valtio makes proxy-state simple for React and Vanilla
  - Rule of thumb: read from snapshots, mutate the source.
  - 依赖 proxy-compare
# comparison

## [When I Use Valtio and When I Use Jotai ?](https://blog.axlight.com/posts/when-i-use-valtio-and-when-i-use-jotai/)

- My answer is I would use valtio for data-centric apps and jotai for component-centric apps.

- In the past, I had this tweet, mentioning “React Centric” and “Data Centric”. React component centric approach is an internal store, where as data centric approach is an external store.
- Here’s another tweet with the same idea. It’s “state resides at component level (inside react)” vs. “state resides at module level (outside react)”.
- The data-centric approach is you have data first regardless of React components. React components are used to represent those data. For example, in game development, it’s likely that you may have game state in advance to design components. You don’t want these data to be controlled by React lifecycle.
- On the other hand, with the component-centric approach, you would design components first. Some states can be locally defined in components with useState. Other states will be shared across components. For example, in a GUI intensive app, you want to control UI parts in sync, but they are far away in the component tree.
- https://github.com/dai-shi/remote-faces
  - it uses valtio. It’s an app to share your face image with your colleagues to show presense in a remote-work environment.
  - It has data to be shared with other users. The latest version uses valtio-yjs to sync data with others.
- https://github.com/dai-shi/katachidraw
  - it uses jotai. This is an SVG-based drawing app.
  - It’s actually developed to demonstrate how jotai can extensively used.

- Another suggestion is, if you really like the syntax of valtio, pick valtio, otherwise pick jotai. 
  - If you are even unsure about it, just pick jotai which has less gotchas.

## [How is Jotai different from Zustand?](https://github.com/pmndrs/jotai/blob/main/docs/basics/comparison.mdx)

- Jotai is close to Recoil. 
  - Zustand is close to Redux.
- Jotai state is within React component tree. 
  - Zustand state is in the store outside React.
- Jotai state consists of atoms (i.e. bottom-up). 
  - Zustand state is one object (i.e. top-down).
- Technical difference
  - The major difference is the state model.
    - Jotai is primitive atoms and composing them. 
    - Zustand is basically a single store (you could create multiple stores, but they are separated.) 
    - In this sense, it's the matter of programming mental model.
  - Jotai can be seen as a replacement for useState+useContext. Instead of creating multiple contexts, atoms share one big context.
  - Zustand is an external store and the hook is to connect the external world to the React world.

- zustand的源码复杂度不高，支持middleware
  - jotai core的源码复杂度也很低，提供了很多主流库的集成

- [How is Jotai different from Recoil?](https://github.com/pmndrs/jotai/blob/main/docs/basics/comparison.mdx)
  - Jotai depends on atom object referential identities.
  - Recoil depends on atom string keys.

## [Difference between zustand and valtio](https://github.com/pmndrs/zustand/wiki/Difference-between-zustand-and-valtio)

- The major difference is:
  - zustand is immutable state model, whereas valtio is mutable state model.
- Another difference is render optimization.

- It's about mental model.
  - Immer is mutation style. If I were to use mutation style, I'd use valtio.
  - So, that means, in zustand, I prefer immutable style, like rambda.

### [What's the difference between zustand and valtio? ](https://github.com/pmndrs/zustand/issues/483)

- If someone comes from redux or likes react's natural immutable updates, zustand would fit well.
- If someone is from vue/svelte/mobx, or new to JS and/or react, valtio's mutable model would fit well.
- zustand is a very thin library and never behaves unexpectedly. 
  - valtio comes with proxy magic.
- One thing I suggest most of the time: if someone use zustand + immer, my recommendation is to try valtio instead.
  - I suggest considering valtio if they haven't, for people who consider zustand with immer middleware. 
  - If people prefer the mutable state model, it's a built-in feature in valtio, whereas zustand is basically on the immutable state model. 
# discuss
- ## 

- ## 

- ## 🔡🎯 Want to read the entire code of Zustand v5-alpha? Here you go!
- https://twitter.com/dai_shi/status/1748635607402967154
  - One file

- ## We have three state management libraries at Poimandres. What's in common is they prefer simpler APIs
- https://twitter.com/dai_shi/status/1681514924173037569
