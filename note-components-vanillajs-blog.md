---
title: note-components-vanillajs-blog
tags: [components, vanillajs]
created: '2020-11-06T13:55:26.840Z'
modified: '2020-11-06T13:56:14.504Z'
---

# note-components-vanillajs-blog

## react-like

## more-vanillajs-components

### [Vanilla Components Draft](https://github.com/websdk/vanilla)

- The primary design goals are to refine the boundaries/seams of components, and maximise the ergonomics of authoring components. 
- This is to separate out the concerns of and enable further customisations and innovations to take place orthogonal to the implementation of components. 
- The components are framework-agnostic, but not the lowest common denominator at the cost of being a long-term solution.

``` JS
/* Define - component.js */
export default function component(node, data) {.. }
```

``` CSS
/* Style - component.css */
:host {}
```

``` JS
// Communicate
node.addEventListener('event', d => {.. })
node.dispatchEvent(event)
```

``` JS
// The simplest way to invoke a component
import { component } from 'component'
component.call(node, data)
```

- There are a few example repo's that covers all the above points:
  - https://github.com/pemrouz/sweet-alert
  - pemrouz/markdown-editor
  - pemrouz/d3-chosen
  - https://github.com/vanillacomponents/ux-input

## ref

- [Vanilla JavaScript Components](https://medium.com/bunnyllc/vanilla-js-components-8d20c58b69f4)
