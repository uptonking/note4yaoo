---
title: toc-lib-web-framework-tagged-template-literals
tags: [es6, javascript, repos, tagged-template-literals]
created: '2020-11-05T09:27:49.883Z'
modified: '2020-11-09T09:03:49.112Z'
---

# toc-lib-web-framework-tagged-template-literals

## lit-html-uhtml

- [A recap of WebReflection's FE/DOM related libraries](https://gist.github.com/WebReflection/761052d6dae7c8207d2fcba7cdede295)
- Minimalistic Libraries(do one thing only and do it well)
- ### Minimalistic Libraries
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

- ### Enriched Libraries
- compromise between small and features rich
  - [µce](https://github.com/WebReflection/uce) Custom Elements via _µhtml_
  - [µce-template](https://github.com/WebReflection/uce-template) a toolless _Vue 3_ like approach
  - [lighterhtml](https://github.com/WebReflection/lighterhtml) (HTML/SVG auto-keyed and manual keyed render)
    - The hyperHTML strength & experience without its complexity
  - [hyperHTML](https://github.com/WebReflection/hyperHTML) (HTML/SVG with no auto-keyed but optional manually keyed render)
  - [HyperHTMLElement](https://github.com/WebReflection/hyperHTML-Element) (custom elements via _hyperHTML_)
  - [dom-augmentor](https://github.com/WebReflection/dom-augmentor) (_augmentor_ with DOM auto-hooked _useEffect_)

- ### Combo Libraries
- integrated libraries
  - [hookedElements](https://github.com/WebReflection/hooked-elements) (_wickedElements_ + _augmentor_)
  - [neverland](https://github.com/WebReflection/neverland) (_lighterhtml_ + _dom-augmentor_)
  - [µland](https://github.com/WebReflection/uland) (_µhtml_ + _dom-augmentor_)
  - [heresy](https://github.com/WebReflection/heresy) and [heresy-ssr](https://github.com/WebReflection/heresy-ssr) (_lighterhtml_ + _augmentor_ + Custom Elements)

- ### choose what to use
  - _wickedElements_ & _µhtml_ or _lighterhtml_ (easy)
  - _hookedElements_ & _µhtml_ or _lighterhtml_ (even easier)
  - _dom-augmentor_ & _µhtml_ or _lighterhtml_ (not easy at all, try _µland_ or _neverland_ instead)
  - native Custom Elements and _µhtml_ or _lighterhtml_ [are an option too](https://webcomponents.dev/edit/EZjX0ZIN0nnESD0PjQPh)

- ### more-packages
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

- https://github.com/developit/htm
  - htm is JSX-like syntax in plain JavaScript - no transpiler necessary.
  - JSX alternative using standard tagged templates, with compiler support.
  - HTM (Hyperscript Tagged Markup)
  - Develop with React/Preact directly in the browser, then compile htm away for production.

- https://github.com/Festify/fit-html
  - fit-html is a combination of lit-html, web components and redux, bringing efficient rendering and a functional application architecture together.
- https://github.com/toddpress/lit-html-redux-experiment

## more-ttls

- https://github.com/zspecza/common-tags
  - A set of well-tested, commonly used template literal tag functions for use in ES2015+
  - common-tags initially started out as two template tags I'd always find myself writing - one for stripping indents, and one for trimming multiline strings down to a single line.
  - Over time, I found myself needing a few more template tags to cover edge cases - ones that supported including arrays, or ones that helped to render out tiny bits of HTML not large enough to deserve their own file or an entire template engine. So I packaged all of these up into this module.

``` JS
import { html } from 'common-tags'
let fruits = ['apple', 'orange', 'watermelon']
html `
  <div class="list">
    <ul>
      ${fruits.map(fruit => `<li>${fruit}</li>`)}
      ${'<li>kiwi</li>\n<li>guava</li>'}
    </ul>
  </div>
`
```
