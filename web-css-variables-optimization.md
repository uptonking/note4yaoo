---
title: web-css-variables-optimization
tags: [css, css-variables, optimization, style]
created: '2020-10-27T16:03:13.703Z'
modified: '2021-01-01T20:18:17.114Z'
---

# web-css-variables-optimization

## pieces

- ### [CSS Custom Properties and Theming](https://css-tricks.com/css-custom-properties-theming/)
- Using custom properties to set a single property is ALWAYS going to be faster than manipulating styles on each individual DOM node that needs the custom styles.
- Like, nearly 100x faster: https://jsperf.com/css-variables-vs-inline-styles

- Custom properties are ordinary properties, so they can be declared on any element, are resolved with the normal inheritance and cascade rules ref 
  - so I don't think that performance will change based on where you declare the property. 
  - The performance will depend on the HTML used with your CSS.
  - A CSS definition has no meaning without a DOM where it's applied.

- ### [CSS Custom Properties performance in 2018](https://blog.jiayihu.net/css-custom-properties-performance-in-2018/)
- So it's still clear that we must be careful with container custom properties because it affects children nodes and recalculation becomes expensive. 
- If you use Custom Properties throughout your application and by defining them at the root element, you'll incur significant performance issues.
- We can conclude that `el.setProperty('color', 'green')` is still the fastest option, but surprisingly `el.setProperty('--color', 'green')` is faster than `el.style = "color: green"`, 
  - which means that `setProperty` is always more performant than inline styles, even when setting a custom property versus an inline hard-coded value. 
  - The reason could be that setting inline styles requires parsing the CSS.
- The initial render with CSS variables is noticeable slower: 416ms vs 159ms. 
  - It's not that bad though, but still to be kept in mind when using Custom Properties in a large application.
  - You might prefer to avoid shipping custom properties if you don't need to change them at runtime. 
  - postcss-custom-properties supports the option preserve: false to remove custom properties in compilation.

- ### [Performance of CSS Variables_2017](https://lisilinhart.info/posts/css-variables-performance/)
- be aware of style recalculations, since CSS Variables are inheritable — changing a variable on a parent can affect many children
  - So the more children a parent element has using this variable, the more expensive setting a CSS variable on this element gets.
- prefer using single classes for elements to make style calculations easier for the browser
- `calc()` has good performance with variables, but still has problems with browser support with certain units like deg or ms
- prefer using `setProperty` rather than inline styles to set CSS variables in Javascript

- ### [Improving CSS Custom Properties performance](https://blogs.igalia.com/jfernandez/2020/08/13/improving-css-custom-properties-performance/)
- The design of CSS, in general, takes great care in considering how features are designed with respect to making it possible for them to perform well. 
  - However, implementations may not perform as well as they could, 
  - and it takes a considerable amount of time to understand how authors use the features and which cases are more relevant for them.
- In Chrome 83 and lower, whenever the custom property declaration changed, the new declaration would be inherited by the whole tree. 
  - This inheritance implied executing the whole CSS cascade and recalculating the styles of all the nodes in the entire tree, since with this approach, all nodes may be affected.
- Chrome had already implemented an optimization on the CSS cascade implementation for regular CSS properties that don’t depend on any other to resolve their value. 
  - These subset of CSS properties are defined as Independent Properties in the Chromium codebase.
  - The optimization mentioned before affects how the inheritance mechanism is implemented for these Independent properties. 
  - Whenever one of these properties changes, instead of recalculating the styles of the inherited properties, children can just copy the whole parent’s computed style. 
  - Blink’s style engine has a component known as Matched Properties Cache responsible of deciding when is possible to avoid the style resolution of an element and instead, performing an efficient copy of the matched computed style. 
- In the case of CSS Custom Properties, we could apply a similar approach as a good step. 
  - We can consider that the nodes with computed styles that don’t have references to custom properties declarations shouldn’t be affected by the new declaration, 
  - and we can implement the inheritance directly by copying the parent’s computed style. 
  - The patch with the optimization I’ve implemented in r765278 initially landed in Chrome 84.0.4137.0
- Obviously, resolving CSS Variables has a cost, so it’s clear that we could apply additional optimizations that reduce the impact of the variable resolution, especially for handling specific style changes that might not affect to a substantial portion of the DOM tree. 
  - I’ve been experimenting with the MPC to explore the idea an independent CSS Custom Properties cache; 
  - nodes with variables referencing the same custom property will produce cache hits in the MPC, even though other properties don’t match.
  - The preliminary approach I’ve been implementing consists on a new matching function, specific for custom properties, and a mechanism to transfer/copy the property’s data to avoid resolving the variable again, since the property’s declaration hasn’t change. 
  - We would need to apply the css cascade again, but at least we could save the cost of the variable resolution.
