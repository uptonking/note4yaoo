---
title: page-css-styling-blog
tags: [blog, css, styling]
created: '2020-12-26T20:35:14.808Z'
modified: '2020-12-26T20:35:48.013Z'
---

# page-css-styling-blog

## [Why We Don't Use a CSS Framework](https://www.infoq.com/news/2020/06/css-variables-design-systems/)

- Tolinski demonstrated how developers who do not need to support IE11 can leverage CSS variables to implement a custom design system with characteristically less overhead than a framework.
- The variable can be updated either via CSS or JavaScript. 
  - When such an update occurs, all dependent variables will be updated reactively. 
- CSS variables are scoped to the element(s) they are declared on and participate in the cascade.
- Tolinski reduced a design system to key components that make the design unique: color, type, spacing, characters, elevation, and elements (e.g. cards or accordions).
- Always use variables for any color, typography, spacing, 
  - and your entire site can be updated or configured in one fell swoop.
  - Don’t worry about creating unique components if they are all using custom properties.
