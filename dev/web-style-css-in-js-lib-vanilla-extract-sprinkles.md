---
title: web-style-css-in-js-lib-vanilla-extract-sprinkles
tags: [css-in-js, vanilla-extract]
created: '2021-08-22T16:07:00.096Z'
modified: '2021-08-22T16:08:42.552Z'
---

# web-style-css-in-js-lib-vanilla-extract-sprinkles

# guide

# discuss
- ## Are CSS Modules or Vanilla Extract suitable for a reusable component library?
- https://twitter.com/housecor/status/1429043686478909443
  - My concern: It would be difficult to override the styles as a consumer, right? (since generated classname hash may change if the parent DOM elements change)
- If you're trying to create an opinionated look and feel I would try and avoid class overrides all together. It removes your ability to make changes to the library as everything is now public API. Props and CSS variables make a much better API in my experience
  - With vanilla-extract specifically, the hashes are based on the .css.ts file location and the order of styles within it. DOM structure doesn't affect it.
-  In my experience, allowing style overrides removes your control as a maintainer. 
   - If you want style overrides, then copying the source code is often a better long term option as the consumer is taking ownership of the change.
   - Guess I see similar to create react app having the eject command. If you want to change the core system then you need to own it.
- Absolutely. You can still allow style overrides if desired, but you have to make an explicit API for it. 
  - I think this is a huge improvement over traditional CSS overrides—especially when you factor in static type checking—since it leads to a much stronger contract.
- Yup, primitive unstyled components that only handle logic, then style with any methodology you want, even plain old CSS. See @radix_ui
- I am building opinionated, styled components that implement the company design system. I'm currently just using BEM with Sass so consumers can easily override (because the class names are static and follow a clear convention)
  - In this particular case, I think @mattcompiles has the right approach -- it's appropriate to restrict style overrides. One additional reason this might be a good choice is that you want to encourage developers to raise inconsistencies up to the DS maintainers.
- Those tools encourage a closed design system where you customise the component with high level props and css variables.
  - If you wanna give some more control to consumer you can take `className` props for specific Dom nodes and merge it with internal classes.
  - One additional could be that you expose Base components which allows lot of overrides using above techniques. But then make variant components on top of it which only allow customisation via high level props. If consumer can't get something done with variant, they can copy it
- One way to do this is have your primitives be unstyled and use `data` attributes as selectors. Another could be an override API like Material UI.
