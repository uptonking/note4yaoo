---
title: lib-ui-spectrum-docs-aria
tags: [adobe-spectrum, docs]
created: '2021-04-12T17:59:04.250Z'
modified: '2021-04-12T18:07:23.824Z'
---

# lib-ui-spectrum-docs-aria

> - platform-specific; theme-agnostic; 

# [overview](https://react-spectrum.adobe.com/react-aria/getting-started.html)

- It provides accessibility and behavior for many common UI components
- It implements adaptive interactions to ensure the best experience possible for all users, including support for mouse, touch, keyboard, and screen readers.
- It provides behavior and accessibility through React Hooks. 
  - Since it **does not provide any rendering**, you are responsible for defining the DOM structure for your component and passing the DOM props returned by each React Aria hook to the appropriate elements. 
  - This is powerful because it allows you to be in complete control over the DOM structure that you render.
  - you may need to add extra elements for styling or layout control. 
  - You also get complete control over how you style your components: you could use CSS classes, inline styles, CSS-in-JS, etc.

- Many components are stateless — they display information to a user. 
  - Examples of stateless components include buttons, progress bars, and links. 
  - These components don't update as the user interacts with them.
- A stateful component has some state, and allows a user to interact with the component in order to update that state. 
  - Examples of stateful components include text fields, checkboxes, and selects.
- react-aria separates the state management logic into a separate hook that lives in react-stately.

# [Why React Aria](https://react-spectrum.adobe.com/react-aria/why.html)

- The fully styleable primitives that the web offers (e.g. `<div>`) are quite powerful, but they lack semantic meaning. 
  - This means that accessibility is often missing
  - Even if you use ARIA to provide semantics, you still need to implement all of the behavior for each component from scratch using JavaScript, 
  - and this can be tricky to do across many devices and interaction models.
- react-aria separates the behavior and accessibility implementation for many common UI components out into React Hooks, which enables them to be reused easily between design systems. 
  - You remain in complete control over the rendering and styling aspects of your components, but get most of the behavior, accessibility, and internationalization support for free.
- react-aria is intentionally very low level: unlike many open source component libraries, it provides no rendering at all, just behavior and accessibility. 
  - We impose no specific DOM structure or styling methodology. 
  - The hooks are small and composable, which allows you to combine them together and achieve your design with only the features you need in your component.
