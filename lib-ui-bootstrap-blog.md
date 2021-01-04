---
title: lib-ui-bootstrap-blog
tags: [blog, bootstrap, lib]
created: '2020-10-19T09:05:34.294Z'
modified: '2020-12-08T13:33:04.764Z'
---

# lib-ui-bootstrap-blog

# Bootstrap 5 Approach Guide

- We’ll dive into each of these more throughout, but at a high level, here’s what guides our approach.
  - Components should be responsive and mobile-first
  - Components should be built with a base class and extended via modifier classes
  - Component states should obey a common z-index scale
  - Whenever possible, prefer a HTML and CSS implementation over JavaScript
  - Whenever possible, use utilities over custom styles
  - Whenever possible, avoid enforcing strict HTML requirements (children selectors)
- Bootstrap’s responsive styles are built to be responsive, an approach that’s often referred to as mobile-first. 
  - While not every component must be entirely responsive in Bootstrap, this responsive approach is about reducing CSS overrides by pushing you to add styles as the viewport becomes larger.
  - In most cases, we use `min-width` queries that begin to apply at a specific breakpoint and carry up through the higher breakpoints. 
  - For example, a `.d-none` applies from `min-width: 0` to infinity. 
  - On the other hand, a `.d-md-none` applies from the medium breakpoint and up.
- Aside from our Reboot, a cross-browser normalization stylesheet, all our styles aim to use classes as selectors. 
  - This means steering(操纵、引导、驾驶) clear of type selectors (e.g., `input[type="text"]` ) and extraneous(外面的；无关的) parent classes (e.g., `.parent .child` ) that make styles too specific to easily override.
  - As such, components should be built with a base class that houses common, not-to-be overridden property-value pairs. 
  - For example, we use `.btn` for all the common styles like `display` , `padding` , and `border-width` . 
  - We then use modifiers like `.btn-primary` to add the `color` , `background-color` , `border-color` , etc.
- Modifier classes should only be used when there are multiple properties or values to be changed across multiple variants. 
  - Modifiers are not always necessary
  - Good examples of modifiers are our theme color classes and size variants.
- There are two z-index scales in Bootstrap — elements within a component and overlay components.
- Some components in Bootstrap are built with overlapping elements to prevent double borders without modifying the border property. 
  - For example, button groups, input groups, and pagination.
  - These components share a standard `z-index` scale of 0 through 3.
  - 0 is default (initial), 1 is `:hover` , 2 is `:active` , and 3 is `:focus` .
- Bootstrap includes several components that function as an overlay of some kind. 
  - This includes, in order of highest `z-index` , dropdowns, fixed and sticky navbars, modals, tooltips, and popovers. 
  - These components have their own `z-index` scale that begins at 1000. 
  - This starting number was chosen arbitrarily and serves as a small buffer between our styles and your project’s custom styles.
  - Each overlay component increases its z-index value slightly in such a way that common UI principles allow user focused or hovered elements to remain in view at all times. 
  - For example, a modal is document blocking (e.g., you cannot take any other action save for the modal’s action), so we put that above our navbars.
- Whenever possible, we prefer to write HTML and CSS over JavaScript. 
  - HTML and CSS are also faster in your browser than JavaScript
  - This principle is our first-class JavaScript API using `data` attributes. 
  - You don’t need to write nearly any JavaScript to use our JavaScript plugins; instead, write HTML.
- Lastly, our styles build on the fundamental behaviors of common web elements. 
  - Whenever possible, we prefer to use what the browser provides. 
  - For example, you can put a `.btn` class on nearly any element, but most elements don’t provide any semantic value or browser functionality. 
  - So instead, we use `<button>` s and `<a>` s.
  - The same goes for more complex components. 
  - While we could write our own form validation plugin to add classes to a parent element based on an input’s state, thereby allowing us to style the text say red, we prefer using the `:valid/:invalid` pseudo-elements every browser provides us.
- Utility classes—formerly helpers in Bootstrap 3—are a powerful ally in combatting CSS bloat and poor page performance. 
  - A utility class is typically a single, immutable property-value pairing expressed as a class (e.g., `.d-block` represents `display: block;` ). 
  - Their primary appeal is speed of use while writing HTML and limiting the amount of custom CSS you have to write.
- While not always possible, we strive to avoid being overly dogmatic(自以为是的；教条的；武断的) in our HTML requirements for components. 
  - Thus, we focus on single classes in our CSS selectors and try to avoid immediate children selectors ( `>` ). 
  - This gives you more flexibility in your implementation and helps keep our CSS simpler and less specific.

# [Bootstrap 5 alpha!](https://blog.getbootstrap.com/2020/06/16/bootstrap-5-alpha/)

- New look and feel
  - Our docs pages are no longer full-width to improve readability and make our site feel less app-like and more content-like.
  - we’ve upgraded our sidebar to use expandable sections
- drop jQuery as a dependency, but you’d never notice otherwise
  - Now toggle buttons are powered by checkboxes and radio buttons, and are much more reliable
- CSS custom properties
  - In v4 we only included a handful of root variables for color and fonts, 
  - and now we’ve added them for a handful of components and layout options.
  - We’re working to utilize the superpowers of both Sass and CSS custom properties for a more flexible system.
- Improved customizing docs
  - v5’s Customize docs expand on v4’s Theming page with more content and code snippets for building on top of Bootstrap’s source Sass files. 
  - We’ve expanded our color palette in v5, too. 
- Updated forms
  - We’ve consolidated all our forms styles into a new Forms section (including the input group component) to give them the emphasis they deserve.
  - we’ve redesigned and de-duped all our form controls.
  - Every checkbox, radio, select, file, range, and more includes a custom appearance to unify the style and behavior of form controls across OS and browser. T
- Utilities API
  - we’ve implemented a brand new utility API into Bootstrap 5.
  - Ever since utilities become a preferred way to build, we’ve been working to find the right balance to implement them in Bootstrap while providing control and customization. 
  - In v4, we did this with global `$enable-*` classes, and we’ve even carried that forward in v5.
  - We’ve moved some of our former v4 utilities to a new Helpers section
- Enhanced grid system
  - By design Bootstrap 5 isn’t a complete departure from v4.
  - We’ve added a new grid tier! Say hello to `xxl` .
  - `.gutter` classes have been replaced with `.g*` utilities, much like our margin/padding utilities. 
  - Form layout options have been replaced with the new grid system.
  - Vertical spacing classes have been added.
  - Columns are no longer `position: relative` by default.
  - CSS’s grid layout is increasingly ready for prime time, and while we haven’t made use of it here yet, we’re continuing to experiment and learn from it.
- Docs
  - We switched our documentation static site generator from Jekyll to Hugo. 
  - Jekyll requires Ruby to be installed. Site generation was very slow
  - Hugo is written in Go, so it has no external runtime dependencies, and it’s much faster. 
- Coming soon: RTL, offcanvas, and more
  - There’s a ton we just didn’t have time to tackle in our first alpha that’s still on the todo list for future alphas. 
  - We’ve spiked out a PR using RTLCSS and are continuing to explore logical properties as well.
  - There’s a forked version of our modal that’s implementing an offcanvas menu
    - the idea of having an offcanvas wrapper to place any sidebar-worth content—navigation, shopping cart, etc—is huge
  - We’re evaluating a number of other changes to our codebase, including the Sass module system, increased usage of CSS custom properties, embedding SVGs in our HTML instead of our CSS, and more.
