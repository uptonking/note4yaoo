---
title: note-style-css-in-js-zero-runtime
tags: [css-in-js, style]
created: '2020-10-06T16:44:49.163Z'
modified: '2020-10-06T16:45:34.792Z'
---

# note-style-css-in-js-zero-runtime

## solutions

- 技术选型时，参考知名项目或大公司项目的选择

- ### [linaria](https://github.com/callstack/linaria/blob/master/docs/BASICS.md)
- [Why use Linaria](https://github.com/callstack/linaria/blob/master/docs/BENEFITS.md)
  - Advantages over regular CSS
    1. Selectors are scoped
    2. Styles are in same file as the component
    3. Refactor with confidence: 可放心修改和删除样式而不影响其他组件
    4. No pre-processor needed
    5. Automatic unused styles removal
    6. Automatic vendor prefixing
    7. Declarative dynamic styling with React
  - Advantages over CSS preprocessors
    1. No new syntax to learn
    2. Same advantages as regular CSS
  - Advantages over inline styles
    1. Full power of CSS
    2. Performance: class names perform much faster than inline styles.
  - Advantages over other CSS-in-JS solutions
    1. CSS is downloaded and parsed separately from JS
    2. No extra parsing needed for CSS
    3. No style duplication on SSR
    4. Catch errors early due to build-time evaluation
    5. Familiar CSS syntax
    6. Works without JavaScript
- [原理 How it works](https://github.com/callstack/linaria/blob/master/docs/HOW_IT_WORKS.md)
  - The Babel plugin will look for css and styled tags in your code, extract the CSS out and return it in the file's metadata. It will also generate unique class names based on the hash of the filename
  - When using the styled tag, dynamic interpolations will be replaced with CSS custom properties.
  - Plugins for bundlers such as webpack and Rollup use the Babel plugin internally and write the CSS text along with the sourcemap to a CSS file. 
  - The CSS file is then picked up and processed by the bundler (e.g. css-loader in case of webpack) to generate the final CSS.

- ### [treat](https://seek-oss.github.io/treat/background)
- Usage
  - Write your styles in js/ts within treat files (e.g. Button.treat.js) that get executed at build time.
  - All CSS rules are created ahead of time, so the runtime is very lightweight—only needing to swap out pre-existing classes. 
  - In fact, if your application doesn’t use theming, you don’t even need the runtime at all.
  - Your project must be using webpack with the supplied webpack plugin
- Tradeoffs
  - The primary goals of treat are full static extraction, minimal runtime code, type safety and legacy browser support. 
    - While a great developer experience is important to us, it will never come at the cost of these goals.
  - Unlike a lot of CSS-in-JS approaches, treat is much more similar to CSS Modules, requiring a bit more work to bind styles to your components.
  - It’s also unable to generate styles at runtime, which means it cannot handle dynamic theming.
  - The upside of treat is that it allows you to craft themeable, statically extracted CSS using JavaScript (or TypeScript) with little impact to bundle size and negligible runtime performance cost.
  - If you’re used to libraries like styled-components or Emotion, treat might seem like a step backwards. 
    - These libraries can quickly and easily create dynamic component-oriented styles. 
    - However, they come with a bundle size and performance cost.
  - If you’re familiar with static CSS-in-JS libraries like Linaria and Astroturf, treat is very similar but with a couple of notable differences. 
    - Firstly, treat’s theming mechanism doesn’t require CSS custom property support (i.e. CSS variables)
    - Secondly, styles are written as objects rather than template literals, to both ensure type safety, and to encourage you to think of your styles as data rather than strings of CSS.
  - Our design system Braid was originally built with CSS Modules, but authored in JavaScript (via css-in-js-loader). 
  - Problem #1: We were unable to author our CSS Modules in TypeScript.
    - TypeScript compiler can’t make sense of what is exported without an understanding of the transformation happening within webpack. 
    - When looking at the raw source code, this doesn’t make sense from a type perspective.
  - Problem #2: CSS Modules only provided a single flat namespace to work with.
    - We were forced to manually namespace properties with underscores
    - TypeScript made this particularly painful because we also had to maintain type definitions for these extra translation steps.
  - Potential solution: Runtime CSS-in-JS?
    - changes in bundle size and runtime performance
  - Potential solution: Static CSS-in-JS?
    - Astroturf is a really lean solution to this problem, essentially supporting CSS Modules and standard preprocessors within JavaScript template literals. 
      - That makes it much more ergonomic than more traditional approaches, 
      - but it also inherits all of the limitations we were experiencing with CSS Modules.
    - Linaria looked a lot more promising due to its theming support, but it came with an important caveat. Theming is achieved via CSS custom properties (i.e. CSS variables)
  - Potential solution: Something new?
    - Early API designs looked promising, and initial prototypes proved that the concept could be supported by webpack.
- [How it works](https://seek-oss.github.io/treat/how-it-works)
  - In order to support static extraction of CSS from JavaScript code, styles are authored in JavaScript files with a special extension (.treat.js / .treat.ts by default). We refer to these files as treat files.
    - Conceptually, this is no different to preprocessors like Sass and Less. The difference is that, rather than using a custom domain-specific language, treat lets you use JavaScript as your preprocessor.
  - For themed styles, treat generates a separate block of CSS for each theme.
    - runtime API can be used to resolve the correct class for the desired theme.
    - Theming in this way allows full static extraction of themed styles. 
    - However, it comes with an important trade-off.
    - themed styles are generated with higher precedence than non-themed styles
    - To avoid this issue, it’s recommended that you try not to rely on style overrides across multiple classes.
  - If you’re not using themed styles, the runtime is not required.
    - The treat runtime is extremely lightweight, only needing to perform a simple lookup to figure out which pre-generated CSS class belongs to which theme

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
