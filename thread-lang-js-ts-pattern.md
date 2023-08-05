---
title: thread-lang-js-ts-pattern
tags: [js, pattern, architecture]
created: 2023-08-04T18:28:05.397Z
modified: 2023-08-04T18:28:26.530Z
---

# thread-lang-js-ts-pattern

# guide

# discuss
- ## 

- ## 

- ## I think I have a nice pattern for being able to add extensions without an JS, 
- https://twitter.com/justinfagnani/status/1687512185201893376
  - which should make this pretty unique in the ability to drop into plain HTML contexts
  - https://github.com/justinfagnani/codemirror-elements
  - A set of CodeMirror custom HTML elements

- This is amazing! Very unique way of packing extensions using declarative syntax, and lets you circumvent needing to load all extensions then enable / disable them ... I may need to steal this for Rhino!!

- I am curious how you worked around the getSelection API not working if you're rendering the editor in the shadow DOM, I faced it with ProseMirror / TipTap.
  - Does CodeMirror use getSelection()?
  - I imagine it would for highlighting and transforming

- ## JS challenge: async task with concurrency limit
- https://twitter.com/thdxr/status/1686856181745111040
  - you have an async function `process(item)` , like `await new Promise(r => setTimeout(r, 1000))` .
  - you need to process all items
  - it needs to be done concurrently, but not more than 25 at a time
  - collect items with errors

- 参考方案
  - https://twitter.com/justinfagnani/status/1687568232872566784
  - https://twitter.com/jviide/status/1687451964437622784
    - Turns out that with a couple of modifications it can support async iterables too

- https://github.com/sindresorhus/p-queue
  - Promise queue with concurrency control

- https://github.com/tannerlinsley/swimmer /js
  - async task pooling and throttling utility for JS

- Let's not forget about good old async semaphore primitive, a simple and effective way to limit concurrency. Plenty of implementation out there

- isn't this literally the @milliondotjs demo?
  - yes. the bottleneck here is the concurrent thing tho, million would only help with dom stuff.

- 
- 

## 💡 [Which has better performance in JavaScript: a switch or a lookup table?](https://twitter.com/kadikraman/status/1680886385010528256)

- 待确认: You can speed up the lookup access, by checking if it's a property first by using `name in obj`

- I would hope the switch stmt given the compiler knows the choices will never change. Even if you moved the object creation out of the loop.

- The magic of JS, they probably optimize for switch because of the high usage compare to lookup. Note that a lookup has an upfront init cost which makes it useless on small datasets. Bottom line, a constant (0(1)) vs O(n) is a no-brainer.

- ## Goal: Allow the user to select items in a list.
- https://twitter.com/housecor/status/1668946224198680578
  - Three state approaches, from worst, to best:
  - 1. list and selectedList 👎
  - 2. list and selectedIds 👎
  - 3. list with a selected property 👍
  - Principle: Store related data in one array. This simplifies and avoids out-of-sync bugs.
  - I should have added a 4th option: Store the selected ids in an "map" object. This is a fine option too. The map makes it efficient to check if a given record is selected.

- Adding a "selected" field to the User model kind of breaks seperation of concerns. Like beeing selected is not an attribute of a User but knowing which items are selected is an attribute of the list.
So IMO option two is the cleanest - but as alwas there is no right or wrong here

- i have a strong preference for lookup maps
