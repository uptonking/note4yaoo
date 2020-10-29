---
title: note-style-css-in-js-lib-jss
tags: [css-in-js, style]
created: '2020-10-29T17:37:32.823Z'
modified: '2020-10-29T17:37:53.948Z'
---

# note-style-css-in-js-lib-jss

## faq

- [[Question] Advantage over One Class One Property](https://github.com/cssinjs/jss/issues/536)
  - Whats the profit of this method compared to used in Fela and Styleron (single class per property.)?
  - I guess you are talking about atomic rendering, where every css rule contains only one property, right?
  - The biggest problem with this approach is convenience. 
  - If you tried styletron, you will see that if you change in dev tools one value, it will break everything on that page. 
  - Also this is a good list http://fela.js.org/docs/introduction/Drawbacks.html
  - I was thinking to add atomic rendering as a plugin or evtl as a renderer. 
  - I didn't see enough benefit though so far to do this myself. You are free to try though.
- [Full static extraction to CSS file while keeping all dynamic parts intact.](https://github.com/cssinjs/jss/issues/579)

## guide

## docs

- JSS is an authoring tool for CSS which allows you to use JavaScript to describe styles in a declarative, conflict-free and reusable way. 
  - It can compile in the browser, server-side or at build time in Node.
  - JSS is framework agnostic. 
  - It consists of multiple packages: the core, plugins, framework integrations and others.

- Is it possible to fully extract CSS and use it with link tag?
  - Yes. The easiest way to do so is to export styles from modules. 
  - During the build process, import those modules and use JSS to convert the styles to CSS. 
  - After that, you can save CSS to a file and bundle it up.

## pieces
