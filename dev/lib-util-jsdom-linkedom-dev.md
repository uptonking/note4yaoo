---
title: lib-util-jsdom-linkedom-dev
tags: [jsdom, lib, linkedom]
created: '2021-02-03T08:12:34.230Z'
modified: '2021-02-03T08:13:26.618Z'
---

# lib-util-jsdom-linkedom-dev

# guide

# pieces

# discuss

- ## I've made linkedom at pair, if not better, than basicHTML, with MutationObserver, Custom Elements, more tests for edge cases, etc.
- https://twitter.com/RyanCarniato/status/1356831335331979267
- This is game-changing. 
  - I've been doing a ton of benchmarking on SSR render times. 
  - I actually started with using basicHTML. 
  - I did a little back of the napkin math. 
  - I imagine this should outperform any VDOM SSR approach other than Inferno. 
  - And be faster than both Vue and Svelte.
  - Obviously need to test for real. But a general DOM capable approach. 3x gains over basicHTML would be enough to silence any contention over emulated DOM not being fast enough on the server.
- Impressive! I never thought about this way of representing trees, much less imagined that it would be this more efficient.
  - Do you think a flat array would be even better? This could reduce the amount of pointers in use and help the GC.
    - the array works if you keep updated end nodes indexes, and you need to relate start nodes indexes too, and as soon as you splice in between, you have much more to adjust than a ref by a property, 
    - so I think it'll fail at performance and RAM usage, instead of helping to simplify: using a flat array means updating all possible nodes indexes within surrounding nodes of a segment that got removed, and update all indexes in the segment itself.
    - linked lists don't need any of these operations, so I strongly doubt a flat array would be any faster!
  - Yeah that makes lots of sense. Splicing elements in and out would be horrible.
    - In the meantime I thought of a hybrid between linked list and array that could be better in this respect, and turns out it already exists.
    - Disadvantage would probably be JIT
- In the past I tried basicHTML as alternative to JSDOM for testing react components, although basicHTML wasn't meant for those cases. Is it still the case for LinkeDOM?
  - LinkeDOM is general purpose DOM, basicHTML was born to make viperHTML possible. I won’t use basicHTML anymore, as the “hyper” family is mostly maintained but not actively developed

# ref
