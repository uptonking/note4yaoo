---
title: lang-js-base-generator-iterator
tags: [ECMAScript, generator, iterator, js, lang]
created: 2022-11-23T17:40:38.765Z
modified: 2022-11-23T17:41:19.245Z
---

# lang-js-base-generator-iterator

# guide

# examples

# blogs

## more-generator

- [Feature: Implement iterator into LexicalNode to allow simple tree traversal · facebook/lexical](https://github.com/facebook/lexical/issues/3419)
  - We have an issue open to refactor getChildren to use a linked list. 
  - This would probably be more useful for your usecase, as it will necessarily introduce some methods which are similar to the iterable protocol implemented by generators, so developers could call next or previous on the list of child nodes.

- [Using Generators to Create Powerful Iterators in JavaScript and Typescript - DEV Community](https://dev.to/kalashin1/using-generators-to-create-powerful-iterators-in-javascript-and-typescript-3kb5)

- [Binary Tree iterator with ES6 generators](https://blog.mgechev.com/2014/09/12/binary-tree-iterator-with-es6-generators/)
  - https://github.com/mgechev/blog.mgechev.com/blob/master/content/post/2014-09-12-binary-tree-iterator-with-es6-generators.md
# discuss
- ## 

- ## 

- ## 

- ## I will absolutely not go back to using Generators. 
- https://twitter.com/TkDodo/status/1693592744835301656
- Not even with the new helpers?  tc39/proposal-iterator-helpers
  - I agree that they are pretty difficult to work with now, but being able to use things like .take and .filter seems like it would be pretty natural.

- People don't like generators but use async/await without knowing that it is the same thing, async/await should have never been added to js

- why such a strong hate? if you squeeze your eyes then the syntax is basically the same as the one you have with async/await
- generators are so much more flexible than async/await, I don't understand why they get such a bad rep
  - yep, this flexibility comes at a cost but it's usually at the author of a library built around them - users can enjoy writing synch-like code (just like async/await one) without really thinking about those things that much

- What’s the reason? I have been using generators a lot while processing big csv and excel files and it worked pretty well. Do you see them difficult to use?

- ## Has anyone ever use a pattern of hybrid sync/async iterables in JS?
- https://twitter.com/justinfagnani/status/1372579326953103364
  - I have a case where I want the highest throughput and all-async is just slower than sync. But a couple of features require async. 
  - I'm thinking about a sync iterable that can emit Promises as a middle ground.
- It’d be great if JavaScript supported code that can be run either synchronously or asynchronously. I did some experiments a while ago, but was never happy with the results

- ## Generators are _so_ handy for stuff like AST walkers or similar traversing algorithms.
- https://twitter.com/DasSurma/status/1373226617938571264
- generators are everywhere in Python. I’m surprised they don’t get more attention in JS. I love them for tree traversal.
- Wow, this is so cool. Not only for AST, but for any type of nested datastructure

- ## Most (all?) non-collection iterables created by JS are iterators
- https://twitter.com/rauschma/status/1402202573646540802

```JS
const IterProto = Object.getPrototypeOf(Object.getPrototypeOf([][Symbol.iterator]()));
IterProto.isPrototypeOf([].keys()) // true
IterProto.isPrototypeOf(new Map().keys()) // true

Uint8Array.prototype[Symbol.iterator] === Float64Array.prototype[Symbol.iterator] // true
```

- ## I wish there were a way in JavaScript for generators to tell that they have been closed, like when breaking out of a for loop.
- https://twitter.com/justinfagnani/status/1407879232311619587
  - Closing iterators seems to be a concept that's just not part of the iteration protocol?
- A generator is like an array of functions, how does a function know if it's never called? But I'd be curious if you do a try/finally, is the finally called when the .return() is called?
  - Yes, if you call `return()` on a generator, the `finally` block will be called. 
  - If you iterate a generator with `for-of` , it will also be called. 
  - If you call `throw()` on a generator, the `catch` block will be called, then the `finally` . 
  - Also works with async generators. 
  - RxJS leverages this.

```JS
let canceled = true;
try {
  yield 'foo';
  canceled = false;
} finally {
  if (canceled) // ...
}
```

- I think since V8 fixed how try/catch is optimized, I like wrapping the whole function in try/finally so that any reason that the generator exits will run the cleanup code.
  - Sure, depends on the cleanup code you're running. I really hate the whole pattern. It's super unintuitive, only works with for-of I think, and causes certain edge cases which no programmer would reasonably expect without being told of this behavior.
- `done` property is only for the consumer of the generator, and if the producer has returned. The generator function itself can't see that the iterator was closed by the VM when breaking from a loop.
