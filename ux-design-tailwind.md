---
title: ux-design-tailwind
tags: [design, ux]
created: '2020-10-03T15:29:12.552Z'
modified: '2021-01-03T17:11:47.916Z'
---

# ux-design-tailwind

# guide

# pieces

- ## [Tailwind the switch statement](https://lukejacksonn.github.io/blog/oceanwind)
- Oceanwind is my very own runtime implementation of Tailwind.
- Tailwind (like Tachyons before it) takes advantage of atomic styles.
- The idea, generally, is that instead of using class names like btn-primary which might add a multitude of style rules to a given element, we'd use more granular class names like, for example p-10 bg-blue border-1 font-bold which are often more self explanatory and usually map to a single CSS rule.
- Tailwind will swap these directives out at build time with all of its generated CSS. 

# tailwind-examples

- https://github.com/tailwindlabs/tailwindcss
  - /28kStar/MIT/202009
  - https://tailwindcss.com/
  - A utility-first CSS framework for rapidly building custom user interfaces.
- https://github.com/tailwindlabs/headlessui
  - /1.4kStar/MIT/202009
  - https://headlessui.dev/
  - Completely unstyled, fully accessible UI components, designed to integrate beautifully with Tailwind CSS.
- https://github.com/lukejacksonn/oceanwind
  - /153Star/NALic/202010/js
  - compiles tailwind like shorthand syntax into css at runtime
  - This library takes inspiration from Tailwind and utilizes Otion to provide means of efficiently generating atomic styles from shorthand syntax and appending them to the DOM at runtime.
  - Server side rendering and static extraction is also supported.
- ref
  - https://tailwindui.com/
    - Fully responsive HTML components
