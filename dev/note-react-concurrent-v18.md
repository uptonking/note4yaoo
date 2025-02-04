---
title: note-react-concurrent-v18
tags: [concurrency, react]
created: 2021-08-14T07:07:50.968Z
modified: 2022-12-19T01:59:01.628Z
---

# note-react-concurrent-v18

# guide

# resources
- ## My “React Concurrency, Explained” talk from React Summit is now live_202306
- https://twitter.com/iamakulov/status/1675658158646128642
  - Explains and shows *how exactly* useTransition works under the hood
# discuss
- ## I had asked in the React 18 Working Group about the status of the "context selectors" PR
- https://github.com/reactwg/react-18/discussions/73
- Andrew just replied (paraphrased):
  - "Lazy propagation" showed mild perf+
  - API design is the blocker
  - Busy with React 18 release work now
  - Likely 18.x minor
- It's not an active area of research right now, unfortunately — we're too busy with other 18 stuff, for now.

- ## `unstable_useContextSelector`: What's the point if `useMutableSource` is available too? It's really easy to create a custom event emitter.
- https://twitter.com/sebastienlorber/status/1412852844437413902
- useMutableSource is "level 2". 
  - But context is "level 3" so it would be nice if we can get as many people as possible to use that.

- ### [Concurrent React for Library Maintainers](https://github.com/reactwg/react-18/discussions/70)
- What are the **different levels of Concurrent Rendering support**?
- Level 1: Make it work
  - minimum support is to just allow the UI to temporarily tear.
  - An example of this level is using the `useSubscription` hook which may tear during initial render but will trigger a synchronous update afterwards to “fix” the tear. 

- Level 2: Make it right
  - may currently be the best case for many libraries, is to not tear at all but occasionally take longer to render. 
  - An example of this is the proposed `useMutableSource` hook which will detect changes in external state during render and re-start rendering before showing the inconsistent UI to the user. 
  - The worst case here is that rendering takes a long time, but the user will always see a consistent UI.

- Level 3: Make it fast
  - The ideal level of support is to always show a consistent UI without de-opting .
  - Most libraries that only depend on React state have already met this level.
  - The example of this is to use React state, which does not tear or de-opt. 
  - Another example is to use a mutable store with immutable snapshots which do not change during render, but this strategy is still under research.

- Note: 
  - libraries that only depend on React state should already be level 3. 
  - Level 1 and 2 are for a small number of libraries that depend on external mutable state or on React state in atypical ways.

- discussion

- Yeah, _if_ the context selector API is finalized and is flexible enough, _and_ context itself is considerably sped up, we _might_ be able to consider a return to the architecture we had in React-Redux v6.
  - Until then, though, we gotta plan on `useMutableSource` + subscriptions.
- At some point, we have production codebases, if useMutableSource *seems* to offer a better API for the future, I'll go with that.
  - In any case you'd rather hide all this behind an abstraction to be able to switch implementation details
