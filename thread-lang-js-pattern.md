---
title: thread-lang-js-pattern
tags: [architecture, js, pattern]
created: 2023-08-04T18:28:05.397Z
modified: 2023-11-10T08:05:12.852Z
---

# thread-lang-js-pattern

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-dynamic-import
- ## 

- ## 

- ## 

- ## in ESM, imports had too much boilerplate, so now I await d
- https://x.com/nullvoxpopuli/status/1802011355534274803
- it removes the type information 
  - The types for fastify seems goofy(愚蠢的；傻的；疯的) to begin with so I'm ignoring them
- I think the issue is more bundling than goofy typings. Anyway, for me the types of Fastify works good for most plugins

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Btw the takeaway here isn't "never use objects rather than N args" but to profile. 
- https://twitter.com/Jack_Franklin/status/1764245242079834142
  - Yes objects tend to be slower, but the vast majority of the time it won't matter. 
  - We had to optimise in canvas rendering code that gets run rapidly over and over again as users scroll/zoom etc.
  - As always, the answer is to be aware of this fact and profile your application if you think it might be problematic. In this particular case look for lots of Garbage Collection (this shows up in the Perf panel of DevTools).

- ## Has anyone heard of a technique where you cache a value only until the current event loop tasks finish?
- https://twitter.com/SCooperDev/status/1737200221459734681
  - So the first time a value is read, cache the result and set up a micro task to clear the cache value. Then all reads during the current execution share that value.
  - Seems to be an effective way to avoid layout thrashing without having to refactor code so that the read of a Dom value is only performed once. 
  - So even within a loop, which modifies a Dom element, we don't cause the browser to relayout. 
  - Assumes read value is independent though.

- I've done this a fair bit on different projects. It's effective but can bite you in the ass if you assume that there will be a reset for every loop. Loop -> loop -> reset -> reset will happen to you sooner or later.

- Yeah, I  think that's my main concern. The browser will be recalculating for a reason and at some point the cache might be outdated even within a single task execution. Refactoring is probably the right choice...

- ## [No love for boolean parameters | TkDodo's blog](https://tkdodo.eu/blog/no-love-for-boolean-parameters)

- ## if you are a TS fan, how would you describe something like JSON.parse where a string input goes in and literally anything could go out!
- https://twitter.com/WebReflection/status/1729799525290668518
- I think many people leave the problem to zod and other runtime checkers since TS itself doesn't cover the problem by design.
- Use a schema validation lib like zod/valibot, or a user defined type guard (a very manual process but saves the heavy dependency).
- you use any. Or a generic

- ## Did you know there's a way to execute code in a function *after* the return?
- https://twitter.com/daniguardio_la/status/1729573561524711543
  - "Try, return, finally: a curious JavaScript pattern"
  - [Try, return, finally: a curious JavaScript pattern | dio.la - Dani Guardiola's blog](https://dio.la/article/try-return-finally)

- ## Did you know that JS modules are the fastest way to create a singleton in JavaScript?
- https://twitter.com/browsermage/status/1718374661585547579
- I alway create db.js/log.js and import to module i wanted to use. I dont create instance, just use module as singleton. I know not good for unit testing but dont forget you can mock modules too.

- ## I think I have a nice pattern for being able to add extensions without an JS, 
- https://twitter.com/justinfagnani/status/1687512185201893376
  - which should make this pretty unique in the ability to drop into plain HTML contexts
- https://github.com/justinfagnani/codemirror-elements
  - A set of CodeMirror custom HTML elements

- This is amazing! Very unique way of packing extensions using declarative syntax, and lets you circumvent needing to load all extensions then enable/disable them ... I may need to steal this for Rhino!!

- I am curious how you worked around the getSelection API not working if you're rendering the editor in the shadow DOM, I faced it with ProseMirror/TipTap.
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

## 💡 [Which has better performance in JavaScript: a switch or a lookup table?](https://twitter.com/kadikraman/status/1680886385010528256)

- 待确认: You can speed up the lookup access, by checking if it's a property first by using `name in obj`

- I would hope the switch stmt given the compiler knows the choices will never change. Even if you moved the object creation out of the loop.

- The magic of JS, they probably optimize for switch because of the high usage compare to lookup. Note that a lookup has an upfront init cost which makes it useless on small datasets. Bottom line, a constant (0(1)) vs O(n) is a no-brainer.

- ## The goal is to have an ordered list of unique items or in other words, a sorted map.
- https://automerge.slack.com/archives/C61RJCM9S/p1692837509469869
  - There are three approaches so far

```JS
// s1
list = ["alice", "bob", "marta", "stephen"]

// s2
names = {
  "alice": { order: "938fcn389" },
  "bob": { order: "fn38fk309" },
  "marta": { order: "b38v03mdo" },
  "stephen": { order: "sl3uvmt03" }
}

order = ["fn38fk309", "b38v03mdo", "sl3uvmt03", "938fcn389"]

// s3
names = {
  "alice": { order: "1" },
  "bob": { order: "3" },
  "marta": { order: "4" },
  "stephen": { order: "2" }
}
```

- s1
  - In this approach we have a normal array. 
  - Everytime we synchronize / merge changes into the array we check if there are duplicates and then we remove the duplicates starting at the end so only the first unique entry is left in the array.
- s2
  - Here we use a names mapping where the keys are the names itself and the values are objects with an order field. The order field contains a random id.
  - Everytime a name is added we do the following steps to validate
  - Now if n peers do these steps at the same time with the same name and then merge their changes they will end up with a unique name in the mapping and an order list with n - 1 unused order ids.
- s3
  - Here we use an increasing order number to determine the order of the names.
  - If we see duplicated order numbers we sort the names according to the alphabet and then we update the order numbers accordingly
- As all of these solutions are not really perfect
- [Realtime Editing of Ordered Sequences | Figma Blog_201703](https://www.figma.com/blog/realtime-editing-of-ordered-sequences/)

- ## Goal: Allow the user to select items in a list.
- https://twitter.com/housecor/status/1668946224198680578
  - Three state approaches, from worst, to best:
  - 1. list and selectedList 👎
  - 2. list and selectedIds 👎
  - 3. list with a selected property 👍
  - Principle: Store related data in one array. This simplifies and avoids out-of-sync bugs.
  - I should have added a 4th option: Store the selected ids in an "map" object. This is a fine option too. The map makes it efficient to check if a given record is selected.

- Adding a "selected" field to the User model kind of breaks seperation of concerns. Like beeing selected is not an attribute of a User but knowing which items are selected is an attribute of the list.
So IMO option two is the cleanest - but as always there is no right or wrong here

- i have a strong preference for lookup maps
