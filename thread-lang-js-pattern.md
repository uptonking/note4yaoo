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

- ## 💡 In TypeScript, there are at least 4 ways to implement immutability.
- https://x.com/housecor/status/1902378789859885550
- how would you choose between the typescript versions? Mainly when to use `as const` vs `readonly/ReadOnly` .
  - readonly is the only granular option. 
  - Otherwise I generally prefer “as const”
- Only in JavaScript, we declare something as const but then add an `as const` at the end of it to say, please remain immutable.

- ## [The handleEvent() method is the absolute best way to handle events in Web Components | Go Make Things](https://gomakethings.com/the-handleevent-method-is-the-absolute-best-way-to-handle-events-in-web-components/)
- https://x.com/WebReflection/status/1866817584039071759
- I like it. It’s quite clean to forward like `this[“on”+ev.type]?.(ev)` when you use prefixed handler names, and overall intercepting all events has a lot of other advantages, too

# discuss-dynamic-import
- ## 

- ## 

- ## 

- ## in ESM, imports had too much boilerplate, so now I await d
- https://x.com/nullvoxpopuli/status/1802011355534274803
- it removes the type information 
  - The types for fastify seems goofy(愚蠢的；傻的；疯的) to begin with so I'm ignoring them
- I think the issue is more bundling than goofy typings. Anyway, for me the types of Fastify works good for most plugins

# discuss-fp-functional-programming
- ## 

- ## 

- ## 

- ## People say FP style is slow because you do filter, map, map, filter, reduce, etc, doing a million passes through an array and creating intermediate arrays.
- https://x.com/wollantine/status/1826903703753793699
  - If you have small arrays, that is no problem. If they are enormous, or streams that you can't know when they end, what?

- Notice that maps and filters can be implemented as reducers, reduce allows "everything".

- You can't compose a filter with a reduce.
  - A filter is of type a -> Bool, a reducer is b -> a -> b. They don't compose because they have different arity. If you make them able to compose, good job, you are implementing transducers.

- This a limitation of how FP is often done in JS. e.g. append(arr, el) creates a whole new array. If it were a linked list, it would just return an object containing el and a pointer to the existing array.

- laziness solves this (also if you work in a real FP language with a decent compiler it’ll do optimizations like stream fusion that eliminate many redundant operations)

- You can compose folds; see Haskell’s FoldL library or streamly. Or recursion-schemes for folding on arbitrary, recursive ADTs.

- fusion (haskell) or transducers (clojure), problem solved
# discuss
- ## 

- ## Destructuring is still the nicest way to remove an object property. I always name it 'removed' for clarity.
- https://x.com/toddmotto/status/1902791574129414248
  - TypeScript doesn't like unused variables, comment added to keep the compiler happy.

- `{ [0]: removed, [1]: removed_2, [2]: removed_final, ...rest }`

- `Object.assign({...form.state}, {[field]: undefined}) as Omit<T, field>?`

- Todd please try to rename it to `_removed` . prefixing an unused variable with _ (e.g. _removed) is supposed to suspend the "unused variable" error.

- ## would people use AsyncLocalStorage more if we called it React Context for javascript functions
- https://x.com/threepointone/status/1894224170570911939
- AsyncContext is kind of a better name

- I really like AsyncLocalStorage but it can be kind of hard to reason about if you're not in a purely Request/Response domain. Great for APIs though

- ## the cloneable class pattern in TypeScript 
- https://x.com/colinhacks/status/1889617191231713568
- Is it more performant than just creating a new one?

- ## JavaScript's most important feature is that "errors" don't crash the program.
- https://x.com/cpojer/status/1880728065703366840
  - Imagine if your browser crashed for every JS error, or if developers had to handle every error before being able to ship. The web would basically not exist as a platform without this.

- that's not a feature of javascript, it's the feature of the browser
  - that's not a feature of javascript, it's the feature of the browser

- https://x.com/aboodman/status/1880848014740443480
  - it’s actually deeper than this. The existence of this feature is dependent on web browsers being structured as an event loop. This separation between the main loop of the program being in the platform and app code being expressed as handlers is what enables the web to limp on after an error and mostly sorta work.
  - In a hypothetical alternate design where web apps just got to run a main loop this couldn’t work.

- ## Why use: `const x = JSON.parse('{"foo":42}')` ?
- https://x.com/DanShappir/status/1874909922313596990
  - When you can: `const x = await import('data:application/json,{"foo":42}', {type:'json'})`

- Easy CORS

- its matter if your using on Lambda or function or serverless, if your normal controller based app its fine to use import example.
  1. Memory Usage ( import ) 
  2. Compute Cost
  3. Scalability
  4. Asynchronous

- ## TIL, you cant catch errors thrown in setTimeout and requestIdleCallback from outside the setTimeout
- https://x.com/okikio_dev/status/1834663298173702518
- Add process.nextTick and queueMicrotask to the list.

- ## People hate reducers because they get convoluted code that is hard to decompose. Transducers also solve this
- https://x.com/wollantine/status/1826903720698769453
- this ancient knowledge will disappear into the past along with the release of Iterator helpers
- I’m one of the few who wrote about the memory issues of chaining multiple JS native functions on arrays.

- ## Symbols is a neat way to have internals that can only be accessed if you have access to the symbol. 
- https://x.com/kettanaito/status/1824021118354702836
  - "private" is sugar, those properties aren't really private. 
  - "#" has some issues as well. 
  - Symbols are battle-proof for actually private properties.
  - The only struggle I have with symbols is typing them. Naturally, TS wouldn't know about your custom symbols, you have to tell it. But once you do, it keeps showing them in the thing's type definition, which defies the whole purpose of them being internal.
- Symbols are public, because of `Object.getOwnPropertySymbols` . Only # fields are truly private.
  - Yup, they do get used and are public API points for runtimes like Node or JS itself meant to be able to be modified and as DI. Closures / private are what you want if you don't want people to modify/accidentally copy stuff.

- ## how to catch error when using fetch
- https://x.com/WarrenInTheBuff/status/1815440867936948371
- You mean where you have a try/catch and all the catch does is throw the error? Yeah, that's useless
  - Not to mention that there is no response.ok check

- Needs a `.catch(e => throw e)` on fetch and json() to make sure all the errors get handled
- You don't like the "rethrow with vigor" pattern?

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
