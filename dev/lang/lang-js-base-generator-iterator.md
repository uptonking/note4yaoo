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
