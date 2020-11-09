---
title: lib-lit-html-dev
tags: [lib, lit-html, tagged-template-literals]
created: '2020-11-08T10:39:49.902Z'
modified: '2020-11-08T10:40:45.221Z'
---

# lib-lit-html-dev

## guide

## pieces

- [What's the purpose of lit-html and hyper-html?](https://www.reddit.com/r/javascript/comments/8iydo2/whats_the_purpose_of_lithtml_and_hyperhtml/)
  - lit-html is a replacement for vdom, and is a little lower level than what something like react does. 
    - It may someday be the basis for a framework like react though.
  - It's a different take on solving the same problem that VDOM solves; declarative DOM construction.
    - You write your DOM how you'd like it to look, and you pass values directly to the elements (either as properties or as attributes) in the DOM (like with React etc.). 
    - This way, your mental model of the DOM is simpler, since you don't have to juggle document.createElement and document.querySelector etc.
  - It's a solution that doesn't use JSX, template strings serve the same purpose, 
    - so you don't have to spend half your time on the boilerplate Webpack/build setup before you actually code. 
    - It's just plain JS. 

## lit-repos

- https://github.com/jmas/lit-redux
  - lit-redux is implementation of react-redux API for lit-html library.
- https://github.com/Festify/fit-html
  - fit-html is a combination of lit-html, web components and redux
- https://github.com/toddpress/lit-html-redux-experiment
- https://github.com/thepassle/create-lit-app
  - Create LitHTML apps with no build configuration. (LitHTML/Redux/Webpack/Express)

- https://github.com/Spectory/lithtml-todomvc
  - TodoMVC app using lit-html and Redux
- https://github.com/jmas/lit-todo-example
- https://github.com/toddpress/lit-html-redux-experiment
- https://github.com/jmas/foocart
  - 只依赖lit-html

## ref

- [The history of hyperHTML followed by lit-html](https://gist.github.com/WebReflection/ab43649d9e4a53ac900b5924c77a310e)
- [Easy apps with hyperHTML — 1, wire/bind_201809](https://dev.to/pinguxx/easy-apps-with-hyperhtml-1-31cc)
