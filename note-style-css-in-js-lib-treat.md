---
title: note-style-css-in-js-lib-treat
tags: [css-in-js, style]
created: '2020-10-27T05:45:54.419Z'
modified: '2020-10-27T06:49:02.544Z'
---

# note-style-css-in-js-lib-treat

## faq

- 当有多个theme时，如何提高首屏加载速度，如先加载默认theme，渲染后再下载其他theme的css
- treat doesn't do any class optimization as it could introduce specificity issues

## guide

- treat-dev-tips
  - useStyles/useClassName，底层会调用resolveStyles/ClassName(themeObj, treatStyles)
    - 目的是在runtime根据当前theme对象选择对应的class名称
    - the treat runtime caches the resolved styles object in memory

- treat缺点或局限
  - 样式书写只支持style object的形式，不支持css字符串TTLs
  - 样式文件要写在单独的文件，如Button.treat.js，较繁琐
  - [Webpack 5` support not yet](https://github.com/seek-oss/treat/issues/139)
- theming
  - Themes must be statically known at build time. 
    - This is because all CSS is is created at build time. 
    - You can create multiple themes and swap them out at runtime (e.g. switch from dark to light theme) but you cannot create a new theme with new values.
  - If you need truly dynamic theme values then you'll need a CSS-in-JS library that creates CSS client side, like emotion or styled-components.
  - [createTheme dynamically?](https://github.com/seek-oss/treat/issues/72)
  - 无法实现手动选择任意颜色，实时切换主题
    - 选择任意颜色的需求并不频繁，易与其他组件原有设计冲突，如冷暖色背景、对比度
    - 主流设计系统都是提供多套预定义的主题供选择切换

- glaze
- otion

## docs

- ### [introduction](https://seek-oss.github.io/treat/)
- Write your styles in js/ts within treat files (e.g. Button.treat.js) that get executed at build time.
- All CSS rules are created ahead of time, so the runtime is very lightweight — only needing to swap out pre-existing classes. 
- In fact, if your application doesn’t use theming, you don’t even need the runtime at all.
  - Because theming is achieved by generating multiple classes, legacy browsers are supported.
- Your project must be using webpack with the supplied webpack plugin

- ### [background](https://seek-oss.github.io/treat/background)
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

- ### [How it works](https://seek-oss.github.io/treat/how-it-works)
- In order to support static extraction of CSS from JavaScript code, styles are authored in JavaScript files with a special extension (.treat.js / .treat.ts by default). We refer to these files as treat files.
  - Conceptually, this is no different to preprocessors like Sass and Less. 
  - The difference is that, rather than using a custom domain-specific language, treat lets you use JavaScript as your preprocessor.
- Within treat files, treat provides a set of styling APIs for generating CSS. 
  - Calling these APIs will result in styles being added to your application bundle. 
  - In order to expose these styles to your application code, they must be explicitly exported
  - When treat files are executed at build time, all of the exports are inlined into your bundle. 
  - Generated styles are separately passed through the webpack loader pipeline, which allows you to create static CSS files via mini-css-extract-plugin.

- For themed styles, treat generates a separate block of CSS for each theme.
  - Now that we’ve generated styles for each theme, the runtime API can be used to resolve the correct class for the desired theme.
  - Theming in this way allows full static extraction of themed styles. 
  - However, it comes with an important trade-off.
  - themed styles are generated with higher precedence than non-themed styles
  - To avoid this issue, it’s recommended that you try not to rely on style overrides across multiple classes.

- If you’re not using themed styles, the runtime is not required.
  - The treat runtime is extremely lightweight, only needing to perform a simple lookup to figure out which pre-generated CSS class belongs to which theme
  - The core API for performing this task is the resolveStyles function (or useStyles if you’re using React).
  - In this case, the styles object is a deep clone of the styleRefs object, with all themed classes resolved relative to greenTheme
  - Because module exports are static, the treat runtime caches the resolved styles object in memory, which means that this cloning and class resolution process only happens once per treat file and theme, for the lifetime of your application.
  - It’s important to note that this resolved styles object has the same type signature as the original styleRefs object, which means that themed styles remain type safe.

## treat-repos

- https://github.com/seek-oss/braid-design-system
  - Themeable design system for the SEEK Group
- https://github.com/autoguru-au/overdrive
  - Overdrive is a product component library, and design system for AutoGuru. 
  - Built with React, TypeScript, Treat, Playroom and Storybook.


