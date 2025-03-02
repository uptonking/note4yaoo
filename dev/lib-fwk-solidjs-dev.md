---
title: lib-fwk-solidjs-dev
tags: [dev, lib, solidjs]
created: 2020-12-05T07:10:10.426Z
modified: 2020-12-08T13:27:56.600Z
---

# lib-fwk-solidjs-dev

# guide

- https://github.com/solidjs/solid /ts/代码量不大
  - A reactive and declarative frontend library, inspired by React but working like Svelte (no VirtualDOM). 
  - 实现包括: reactive-core, render, server, store
  - Includes modern features like JSX, Fragments, Context, Portals, Suspense, SSR, Error Boundaries, and Asynchronous Rendering.

- https://github.com/fabiospampinato/flimsy
  - A single-file <1kb min+gzip simplified implementation of the reactive core of Solid, optimized for clean code.
  - Check out the annotated source, if you'd like to more in depth understand how Solid works
# discuss-author
- ## 

- ## 

- ## One design mistake in Solid 1.0 was supporting multiple ways to write props in JSX types. _202502
- https://x.com/RyanCarniato/status/1888008017171644777
  - I thought it good to do both lowercase and camelCase as HTML is case insensitive. 
  - This is bad for wrapping native elements because Component authors need to check multiple properties.
  - Solid types are not the same as React as we don't transform attributes. We have `aria-role` not `ariaRole` . Camelcasing is for things like `disableRemotePlayback` . This is important for performance and inlining stuff for templates and SSR. And we will not be adopting Reacts convention completely.

- Mostly camelCase because JS. If Solid have used templates I think otherwise. But JSX makes JS and the “X” blending in a way it’s hard to separate

- ## I often get asked about the difference between different reactive libraries and approaches
- https://twitter.com/RyanCarniato/status/1624105311425675264

- ## Having been given credit for things I didn't invent and seeing some being upset about not getting due credit
- https://twitter.com/RyanCarniato/status/1628123589898813442
  - Signals, Fine-grained rendering, Nested Routing, Compiled RPCs, Serializing Promises/Errors across the network, etc.. these are all obvious things in hindsight. And we would have arrived at them when focusing on the problem space long enough. Technology is inevitable

# discuss-roadmap
- ## 

- ## 

- ## [The Road to 2.0 · solidjs/solid _20250215](https://github.com/solidjs/solid/discussions/2425)
  - I'd like to officially announce the beginning of our journey to Solid 2.0. We've done a lot of prototyping over the last few months
  - Fine-grained non-nullable async
  - Derived signals
  - Automatic batching

- ## Solid 2.0 is gonna look a lot more like React, and at the same time a lot more like Rxjs in all the good ways
- https://x.com/devagrawal09/status/1885432475729453470
- Because of the "dependency function" in effects, dealing with stale data in effects, and having pending resources that throw?  Honestly I think we may be taking inspiration from the wrong parts of React

- ## has there been a decision yet whether Solid 2.0 reactivity will microtask batch signal writes/effects, or continue being fully synchronous?
- https://discord.com/channels/722131463138705510/780502110772658196/1138989102679736380
- As I understand it effects should be batched, and memos not refreshed until somebody calls them

- ## As for 2.0 we will start with the reactive system which is already underway._20230808
- https://discord.com/channels/722131463138705510/722131463889223772/1138208971426123896
  - We will be sharing our progress there in the next few weeks and people can start playing with that. And we can go from there. 
  - Right now we are sort of vetting the approach, so haven't wanted to put it out there yet. 
  - And because this is a **reactivity rewrite**, while the **API is basically unchanged**, it is basically a different version so it won't play with Solid's current reactivity. 

- ## So in summary, there are only really 2 things going on right now on R&D. Start and Solid 2.0._20230802
- https://discord.com/channels/722131463138705510/780502110772658196/1136004394899488941
  - For Start with the rebase (and merge of dev) we will be able to continue to move out of beta while keeping our experimental projects working in place.
  - For Start with the rebase (and merge of dev) we will be able to continue to move out of beta while keeping our experimental projects working in place.
  - There is also a reasonable likelihood of a Solid 1.8 release in the meanwhile to address some smaller unrelated things like Context lookup performance, root binding, etc.. but that will depend on time available

- ## [Proposal for easy Solid reactivity on server](https://github.com/solidjs/solid/discussions/1104)
  - When used outside the browser, Solid is currently "tuned" for SSR. If you want Solid reactivity in Node, for example, you need to declare a Node condition of "browser", which is potentially inaccurate

- ## [The ideal Solid? (v2, v3, v4, etc)](https://github.com/solidjs/solid/discussions/1804)
  - I feel like the current signals.ts file is doing too much. 
  - I believe the signals+effects reactive pattern, which is like a 100-200 LoC sort of deal, can be in its own file, with primitives exposed from it that allow making the other APIs on top.

- Have you thought about splitting/communicating the reactive system separately from the UI for v2?
  - Solid JS - The reactive system for JavaScript
  - Solid UI - The UI framework for SolidJS

- 1. Simplified project structure as close to vanilla ESM as possible.
  - With reactivity moving out of the core as well as store it really just a matter of `solid-js/web` can finally be pulled out I feel. 
  - This was something that I wasn't sure about at first but I think it makes sense.
  - There is also some thinking that `/h` or `/html` belongs core but these are just extensions of web. 
- 2. Stop custom building of dependencies into the main lib
- 3. Bring tools like dom-expressions into Solid proper.
- 4. Deferred effects by default (maybe even no synchronous effects).
- 5. As a consequence of the previous point, the batch API can be deleted
- 6. Highly-decoupled reactive system not coupled to all the component-specific features
- 7. Sell Solid's reactivity as a first-class library on its own
  - This effort has already started. We still need synchronous effects for rendering but yes queuedMicrotask, automated batching, an opt in flushSync are all already implemented. 
  - ie.. @solidjs/signals
# discuss
- ## 

- ## 

- ## I'm starting to see that Solid's lack of `isSignal` acknowledges React's goal of hiding reactivity and React's Component model is a concession(让步，允许) to the enormity(恶行) of reaching such a goal.
- https://twitter.com/dmitriid/status/1632096735475429378
- In Solid there is no `Reactive` type. We have an `Accessor` which is basically `MaybeReactive` , but it is because we treat everything as could be reactive. We don't want that decision to be part of your authoring.
  - However, we don't want the benefits of reactivity to be limited to a component model, given what that unlocks, which is hard to do with the tooling available. It is definitely a challenging set of decisions of where to draw lines or set arbitrary restrictions.
- It's not a dig against React, but fine-grained reactivity does seem to scale much better even for bad programmers than components-as-unit-of-work.

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

- ## The Ember example was important for understanding the impact design decisions like explicit setters. 
- https://twitter.com/RyanCarniato/status/1634256285402279936
  - Why providing mutable APIs that may not track can cause changes to be missed. 
  - I won't give Ember too hard of a time for having dependency arrays given where React ends up.
  - The Knockout section about source of truth, basically describes the issue of using `useEffect` to synchronize state. Combined with the lack of glitch-free execution at that time it could be a mess. I wonder if the patterns we use today couldn't have been applied there though. 

# ref
