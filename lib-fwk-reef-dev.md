---
title: lib-fwk-reef-dev
tags: [dev, lib, reef, state]
created: '2020-11-04T17:36:59.087Z'
modified: '2020-12-08T13:33:48.900Z'
---

# lib-fwk-reef-dev

- To make vanillajs great again

- Reef /631Star/MIT/202010/js/NoDeps
  - https://github.com/cferdinandi/reef
  - https://reefjs.com/
  - A lightweight library for creating reactive, state-based components and UI. 
  - Reef is a simpler alternative to React, Vue, and other large frameworks.
  - [Changelog](https://reefjs.com/about/#changelog)

# docs

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

# reef-repos

- https://github.com/sreekotay/reefer
  - Lightweight Vanilla JS HTML/JS UI Library
  - declarative reef
- https://github.com/MathiasWP/TeroyJS
  - /deprecated
  - TeroyJS is a state-based component UI renderer library made up of 100 lines of code; 
  - Create components with states, and watch how they automatically are updated in your GUI whenever they are changed.
  - TeroyJS focuses mainly on one thing: size. A minified TeroyJS takes only 2.75kb(1.36kb gzip)
  - TeroyJS works silently behind the scenes with the power of JavaScript Proxies 
    - and will only update the necessary DOM-components on state changes. 
  - There's no virtual DOM (like in React), and the speed of TeroyJS is not limited by thousands of line with code.
  - https://www.reddit.com/r/javascript/comments/gaiqpb/ive_tried_to_create_the_tiniest_statebased/
    - it looks like it overwrites the old HTML entirely on an update? That might problematic once you get into forms (e.g. toggling a class on the input as the user types).
- https://github.com/kieranbarker/guess-the-color
  - This project was inspired by @clairy_charles' color game.
