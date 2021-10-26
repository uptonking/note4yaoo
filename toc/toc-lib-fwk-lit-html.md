---
title: toc-lib-fwk-lit-html
tags: [framework, lit-element, lit-html, toc]
created: '2021-01-01T19:15:20.376Z'
modified: '2021-01-01T19:16:38.879Z'
---

# toc-lib-fwk-lit-html

# popular

- https://github.com/Polymer/lit-element
  - A simple base class for creating fast, lightweight web components
- https://github.com/rough-stuff/wired-elements
  - Collection of custom elements that appear hand drawn.

 

- https://github.com/matthewp/haunted
  - React's Hooks API but for standard web components and lit-html or hyperHTML.

# lit-examples

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

# lit-html-like

- ## [A recap of WebReflection's FE/DOM related libraries](https://gist.github.com/WebReflection/761052d6dae7c8207d2fcba7cdede295)
  - Vue => uce-template
  - React => uland/uhooks/kaboobie
  - Svelte => heresy/-ssr
  - template-literal => uhtml/-ssr
  - Custom Elements => polyfill with built in extends
- Minimalistic Libraries(do one thing only and do it well)
- ## Minimalistic Libraries
- do one thing only and do it well
  - [µhtml](https://github.com/WebReflection/uhtml) (HTML/SVG auto-keyed and manual keyed render)
    - A micro HTML/SVG render
    - micro html is a ~2.5K lighterhtml subset to build declarative and reactive UI via template literals tags.
    - lighterhtml is at pair with uhtml features, but not vice-versa, 
      - meaning if you need anything more, you can always switch to lighterhtml later on, and without changing a single line of code.
  - [augmentor](https://github.com/WebReflection/augmentor) (hooks for anything)
    - Extensible, general purpose, React like hooks for the masses.
  - [wickedElements](https://github.com/WebReflection/wicked-elements) (custom elements without custom elements ... _wait, what?_)
    - A library to handle any element as if it was a Custom Element.

- ## Enriched Libraries
- compromise between small and features rich
  - [µce](https://github.com/WebReflection/uce) Custom Elements via _µhtml_
  - [µce-template](https://github.com/WebReflection/uce-template) a toolless _Vue 3_ like approach
  - [lighterhtml](https://github.com/WebReflection/lighterhtml) (HTML/SVG auto-keyed and manual keyed render)
    - The hyperHTML strength & experience without its complexity
  - [hyperHTML](https://github.com/WebReflection/hyperHTML) (HTML/SVG with no auto-keyed but optional manually keyed render)
  - [HyperHTMLElement](https://github.com/WebReflection/hyperHTML-Element) (custom elements via _hyperHTML_)
  - [dom-augmentor](https://github.com/WebReflection/dom-augmentor) (_augmentor_ with DOM auto-hooked _useEffect_)

- ## Combo Libraries
- integrated libraries
  - [hookedElements](https://github.com/WebReflection/hooked-elements) (_wickedElements_ + _augmentor_)
  - [neverland](https://github.com/WebReflection/neverland) (_lighterhtml_ + _dom-augmentor_)
  - [µland](https://github.com/WebReflection/uland) (_µhtml_ + _dom-augmentor_)
  - [heresy](https://github.com/WebReflection/heresy) and [heresy-ssr](https://github.com/WebReflection/heresy-ssr) (_lighterhtml_ + _augmentor_ + Custom Elements)

- ## choose what to use
  - _wickedElements_ & _µhtml_ or _lighterhtml_ (easy)
  - _hookedElements_ & _µhtml_ or _lighterhtml_ (even easier)
  - _dom-augmentor_ & _µhtml_ or _lighterhtml_ (not easy at all, try _µland_ or _neverland_ instead)
  - native Custom Elements and _µhtml_ or _lighterhtml_ [are an option too](https://webcomponents.dev/edit/EZjX0ZIN0nnESD0PjQPh)

- ## lit-packages
- https://github.com/WebReflection/hyperHTML
  - /2.7kStar/ISC/202006/js
  - A Fast & Light Virtual DOM Alternative available for Node.js and NativeScript too
  - https://github.com/WebReflection/hyperHTML-Element
    - An extensible class to define hyperHTML based Custom Elements.
- https://github.com/WebReflection/lighterhtml
  - The hyperHTML strength & experience without its complexity
  - faster than hyperHTML
  - simpler than lit-html
  - fueling both neverland and heresy
  - If you want 90% of functionalities offered by lighterhtml for 2/3rd of its size, check µhtml
- https://github.com/WebReflection/uhtml
  - micro html is a ~2.5K lighterhtml subset to build declarative and reactive UI via template literals tags.
- https://github.com/WebReflection/neverland
  - React like Hooks for lighterhtml
  - As React Hooks were born to simplify some framework pattern, 
    - Neverland goal is to simplify lighterhtml usage, in a virtual component way, through the mighty dom-augmentor.
  - This library simulates Custom Elements, without needing polyfills, simply by passing zero, one, or more arguments to every desired components in each template literal hole
  - All hooks are provided by augmentor, via dom-augmentor that takes care or injecting life-cycle DOM events when useEffect is used.
  - if you're looking for something even smaller than neverland, don't miss µland!
- https://github.com/WebReflection/uland
  - micro land, or unicorn land, is a µhtml take at neverland.
  - Same API, except the exports are {Component, render, html, svg}
- https://github.com/WebReflection/viperHTML
  - /216Star/ISC/201811/js/deprecated
  - Isomorphic hyperHTML
  - hyperHTML lightness, ease, and performance, for the server.
  - Similar to its browser side counterpart, viperHTML parses the template string once, decides what is an attribute, what is a callback, what is text and what is HTML, and any future call to the same render will only update parts of that string.
  - The result is a blazing fast template engine that makes templates and renders shareable between the client and the server.

- https://github.com/polymer/lit-html
  - /6.8kStar/BSD/202009/ts
  - An efficient, expressive, extensible HTML templating library for JavaScript.
  - lit-html lets you write HTML templates in JavaScript with template literals.
  - lit-html templates are plain JavaScript and combine the familiarity of writing HTML with the power of JavaScript. 
  - lit-html takes care of efficiently rendering templates to DOM, including efficiently updating the DOM with new values.
- https://github.com/Polymer/lit-element
  - A simple base class for creating fast, lightweight web components with lit-html
  - LitElement uses lit-html to render into the element's Shadow DOM and adds API to help manage element properties and attributes.
  - [uce vs lit-element](https://gist.github.com/WebReflection/ae3451c17c5e882bbc7f0714c14eefcd)

# more

- https://github.com/claviska/sushi-element
  - an expressive way to create standards-based web components that work with (and without) your favorite framework. 
  - At the core of Sushi Element is a class factory called `createElement()` that accepts an object and returns a custom element. 
  - You can use the resulting element in your HTML or with your favorite framework.
  - Sushi Element is designed to be lightweight and stick to the platform as closely as possible. 
  - It uses template literals powered by `lit-html` for fast, efficient rendering with no virtual DOM requirement.
