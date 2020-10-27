---
title: note-style-css-in-js-zero-runtime
tags: [css-in-js, style]
created: '2020-10-06T16:44:49.163Z'
modified: '2020-10-27T06:50:44.874Z'
---

# note-style-css-in-js-zero-runtime

## solutions

- 技术选型时，参考知名项目或大公司项目的选择

- ### [astroturf](https://github.com/4Catalyzer/astroturf)
  - astroturf expects uncompiled JavaScript code, 
  - If you are using babel or Typescript to transform tagged template literals, ensure the loader runs before babel or typescript loaders.

- ### [stitches](https://stitches.dev/docs/introduction)
- Stitches avoids unnecessary prop interpolations at runtime, making it significantly more performant than other styling libraries. 
- How does Stitches work behind-the-scenes?
  - Each CSS property in your application is mapped to an atomic class and cached. 
  - Once a class is injected, it will never be injected again. 
  - From then on, it will just return the same class.
- CSS rules are at zero risk of specificity wars. Since every rule gets its own class
- Stitches introduces variants as a first-class citizen, so you can design composable component APIs.
- There are no prop interpolations. 
  - Changes to styles are defined as variants and composed in the consumption layer. 
  - This means there are no style re-evaluations at runtime.
  - The only work Stitches does in terms of evaluation is the first time a unique rule occurs. It creates an atomic class. 
  - If it occurs again, the cached class is reused.

- ### [compiled](https://compiledcssinjs.com/docs/how-it-works)
- Compiled compiles your CSS in JS at build time by statically analyzing your code and then transforming it into Compiled Components. 
- Everything we need to use the component is included along side it in the JavaScript bundle.
- CSS can't be generated at runtime.
- While Compiled currently only targets inline Compiled Components, we'll eventually get to more exciting grounds - optional CSS extraction. 
