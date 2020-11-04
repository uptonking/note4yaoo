---
title: lib-reef-dev
tags: [dev, lib, reef, state]
created: '2020-11-04T17:36:59.087Z'
modified: '2020-11-04T17:53:06.883Z'
---

# lib-reef-dev

- Reef /631Star/MIT/202010/js/NoDeps
  - https://github.com/cferdinandi/reef
  - https://reefjs.com/
  - A lightweight library for creating reactive, state-based components and UI. 
  - Reef is a simpler alternative to React, Vue, and other large frameworks.
  - [Changelog](https://reefjs.com/about/#changelog)

## docs

- Features
  - Simple templating with JavaScript strings or template literals.
  - No transpiling required.
  - Uses DOM diffing to update only the things that have changed.
  - Has Redux/Vuex-like data stores, setters and getters baked right in.
  - Work with native JavaScript methods and browser APIs instead of custom methods and pseudo-languages.

- Why use Reef?
  - Reef is an anti-framework.
    - It does a lot less than the big guys like React and Vue.
    - It doesn’t have a Virtual DOM.
    - It doesn’t require you to learn a custom templating syntax. 
    - It doesn’t provide a bunch of custom methods.
  - Reef does just one thing: render UI.
    - Couldn’t you just use some template strings and innerHTML? Sure. 
    - But Reef only updates things that have changed instead clobbering the DOM and removing focus from your form fields. 
    - It also automatically renders a new UI when your data updates, and helps protect you from XSS attacks.

## ref

- https://github.com/sreekotay/reefer
  - Lightweight Vanilla JS HTML/JS UI Library
  - declarative reef
