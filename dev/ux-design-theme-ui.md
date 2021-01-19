---
title: ux-design-theme-ui
tags: [design-system, theme-ui, theming]
created: '2020-12-27T19:31:52.925Z'
modified: '2021-01-01T20:08:51.345Z'
---

# ux-design-theme-ui

# guide

- 开始出现挑战用theme对象实现theming的思路
  - css vars

# discuss

- ## [Expose theme values as CSS Variables](https://github.com/system-ui/theme-ui/issues/979)
- @theme-ui/custom-properties: Generate CSS custom properties for use with Theme UI.

- ## [Can Theme-UI be statically extracted somehow?](https://github.com/system-ui/theme-ui/discussions/1051)
- Theme UI is built on top of Emotion, and AFAIK it can't be statically extracted.
  - JSX pragma transforms `sx` props into `className` at runtime.
  - Similarly, themes are passed through React context.
- @compiled/css-in-js has statically extracted CSS prop. 
  - If you knew the theme statically, it would possible to write a TS transform/babel plugin to compile `sx` prop into `css` prop and then run @compiled/css-in-js, but this is honestly a big undertaking.

# pieces

- One of the primary motivations behind Theme UI is to make building themeable, constraint-based user interfaces in React as simple and as interoperable as possible.

# chakra-ui

- [RFC: Static CSS Extraction](https://github.com/chakra-ui/chakra-ui/issues/859)
  - One of the downsides of CSS-in-JS, particularly the styled-system approach is the runtime performance issues.
    - You pass some style props to any component
    - Chakra UI uses styled-system functions to transform the style props you pass to CSS objects
    - Chakra UI uses emotion to convert the CSS object to a class name (using some hashing strategy) and appends a style tag to the head of the browser
  - This process happens very often during the lifetime of any Chakra component, and performance issues might become noticeable with very fast, frequent updates.
  - Ideas on how to solve this
  - Static CSS Extraction
    - Figure out how to generate static CSS files based on the style props at build time, so there's almost zero runtime cost.
  - Prefer CSS variables to Context
    - Because CSS variables work like React context, we can simply switch the current implementation to write theme specs to `:root` via css variables. 
    - Then update styled-system functions.
  - discussion
  - After some research, Compiled CSS-in-JS by the Atlassian team seems to be an amazing solution.
  - there could be something interesting looking into seek-oss/treat, they seem have a good solution in how they use it for their Braid design system
  - why not using CSS variables from the start 

# ref

- https://github.com/PaulieScanlon/skin-ui /202004
  - https://www.skin-ui.com/
  - A Theme UI Live Preview and Code Editor
