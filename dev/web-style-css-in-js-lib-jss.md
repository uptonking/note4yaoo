---
title: web-style-css-in-js-lib-jss
tags: [css-in-js, jss, style]
created: 2020-10-29T17:37:32.823Z
modified: 2021-01-01T20:06:31.225Z
---

# web-style-css-in-js-lib-jss

> material-ui v5 is migrating from jss to styled-components

# faq

- [[Question] Advantage over One Class One Property](https://github.com/cssinjs/jss/issues/536)
  - Whats the profit of this method compared to used in Fela and Styleron (single class per property.)?
  - I guess you are talking about atomic rendering, where every css rule contains only one property, right?
  - The biggest problem with this approach is convenience. 
  - If you tried styletron, you will see that if you change in dev tools one value, it will break everything on that page. 
  - Also this is a good list http://fela.js.org/docs/introduction/Drawbacks.html
  - I was thinking to add atomic rendering as a plugin or evtl as a renderer. 
  - I didn't see enough benefit though so far to do this myself. You are free to try though.
- [Full static extraction to CSS file while keeping all dynamic parts intact.](https://github.com/cssinjs/jss/issues/579)

# guide

# docs

- JSS is an authoring tool for CSS which allows you to use JavaScript to describe styles in a declarative, conflict-free and reusable way. 
  - It can compile in the browser, server-side or at build time in Node.
  - JSS is framework agnostic. 
  - It consists of multiple packages: the core, plugins, framework integrations and others.

- Is it possible to fully extract CSS and use it with link tag?
  - Yes. The easiest way to do so is to export styles from modules. 
  - During the build process, import those modules and use JSS to convert the styles to CSS. 
  - After that, you can save CSS to a file and bundle it up.

- To optimize time to first paint, you can use server-side rendering and extract critical CSS. 
  - You can couple the rendering of CSS with the rendering of HTML so that no unused CSS gets generated. 
  - It will result in a minimal critical CSS extracted during server-side rendering and allow you to inline it.
- The React-JSS package provides some additional features:
  - Dynamic Theming - allows context based theme propagation and runtime updates.
  - Critical CSS extraction - only CSS from rendered components gets extracted.
  - Lazy evaluation - Style Sheets get created when a component gets mounted.
  - The static part of a Style Sheet gets shared between all elements.
  - Function values and rules are updated automatically with props as an argument.

- SheetsRegistry
  - When rendering on the server, you will need to get all rendered styles as a CSS string. 
  - The `SheetsRegistry` class allows you to aggregate and stringify them.

# pieces
