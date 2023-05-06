---
title: lib-fwk-solidjs-dev
tags: [dev, lib, solidjs]
created: 2020-12-05T07:10:10.426Z
modified: 2020-12-08T13:27:56.600Z
---

# lib-fwk-solidjs-dev

# guide

- https://github.com/ryansolid/solid
  - A reactive and declarative frontend library, inspired by React but working like Svelte (no VirtualDOM). 
  - Includes modern features like JSX, Fragments, Context, Portals, Suspense, SSR, Error Boundaries, and Asynchronous Rendering.
# discuss
- ## 

- ## I didn't invent Signals, but this is interesting to see.
- https://twitter.com/texastoland/status/1600827603664834560
- I think these are 2 conceptually different patterns. Rob's signals make the standard observer pattern less string-ly typed. TypeScript fixes that a different way. 
  - Ryan's signals automatically notify observers (reactive) when any signal in its call stack updates (recursive)

- ## When people say "reactivity"  they mean "observers" (e.g. React hooks/Solid signals).
- https://twitter.com/nomsternom/status/1600401447593517057
  - An observer-based UI has to manage a complex propagation graph to stay correct and performant.
  - React, Solid, Svelte... everyone uses the observer pattern as a central building block.
- The industry ditched view-models in favor of this at some point, and now working hard on "better" reactivity - in other words optimizing the observer pattern.
- I think the industry went towards observers and the frameworks are being innovative in trying to improve and optimize the way they work and that's great.
  - No, it's happened because many things in the UI are asynchronous, and it's just logical to handle them by observing the events.
- Observing changed values is different from listening to events and perhaps I could have clarified that better.

# ref
