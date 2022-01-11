---
title: lib-state-jotai-community
tags: [community, jotai, state]
created: '2022-01-05T14:25:11.950Z'
modified: '2022-01-05T14:25:35.961Z'
---

# lib-state-jotai-community

# guide

# discuss
- ## Jotai https://jotai.org atoms are primarily for bottom-up approach, but it can do top-down approach like zustand. 
- https://twitter.com/dai_shi/status/1477593623156105217  /20220102
  - So, I created a ToDo app with a single store with jotai. 
  - As a bonus, it uses `atomWithHash` , so the state is persisted in the URL.
  - https://codesandbox.io/s/jotai-single-store-pmi40
  - Does zustand have something like atomWithHash?
    - no, not handy like atomWithaHash.

- I made another variant of the demo. 
  - https://twitter.com/dai_shi/status/1477796451900358657  /20220103
  - It's single state and top-down approach, but yet somewhat atomic. Thanks to focusAtom and splitAtom. And, persisted with atomWithHash. Jotai is very flexible!
  - https://codesandbox.io/s/jotai-todos-focus-atom-ledxb


- ## i was initially hesitant to use valtio with its proxy-based APIs 
- https://twitter.com/_paulshen/status/1478792368274821122
  - but i've now replaced all jotai usage with valtio and may do the same with zustand
  - most of my usage are single-value atoms. i use an object with a single key `value` so valtio can observe changes (downside of proxy APIs).
  - valtio watches for all updates via proxies by default so i wrap objects with valtio's `ref` function to bypass the nested proxy.
- jotai is a great library but you're exposed to the complexity of react context. you can't read/write to atoms anywhere like you can with zustand and valtio.
  - Yeah, the fact that jotai is based on context is essential and that's why we created a new library even if we already had zustand.
  - The demand on reading/writing anywhere is high, and we are planning to expose a new experimental api
