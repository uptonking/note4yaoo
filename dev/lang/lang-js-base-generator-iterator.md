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
