---
title: web-style-css-in-js-lib-treat
tags: [css-in-js, style, treat]
created: '2020-10-27T05:45:54.419Z'
modified: '2021-01-01T20:06:40.149Z'
---

# web-style-css-in-js-lib-treat

- Themeable, Statically Extracted CSS-in-JS

# guide

- treat pros
  - 框架无关
  - 内置支持theming，theming的实现不依赖css vars
    - theme的定义使用js对象，复用十分简单方便
  - 可代替的传统css预处理器，极其灵活
    - 一个style object样式对象既可以打包为一个类名，也可以打包为atomic形式的多个类名

- treat cons
  - 样式书写只支持style object的形式，不支持css字符串TTLs
  - 样式文件要写在单独的文件，如Button.treat.js，较繁琐
  - 未实现基于styleMap API的atomic CSS patterns，只提供了简单示例
  - [Webpack 5 support not yet](https://github.com/seek-oss/treat/issues/139)
- theming
  - Themes must be statically known at build time. 
    - This is because all CSS is is created at build time. 
    - You can create multiple themes and swap them out at runtime (e.g. switch from dark to light theme) but you cannot create a new theme with new values.
  - If you need truly dynamic theme values then you'll need a CSS-in-JS library that creates CSS client side, like emotion or styled-components.
  - [createTheme dynamically?](https://github.com/seek-oss/treat/issues/72)
  - 无法实现手动选择任意颜色，实时切换主题
    - 选择任意颜色的需求并不频繁，易与其他组件原有设计冲突，如冷暖色背景、对比度
    - 主流设计系统都是提供多套预定义的主题供选择切换

- treat-dev-tips
  - useStyles/useClassName，底层会调用resolveStyles/ClassName(themeObj, treatStyles)
    - 目的是在runtime根据当前theme对象选择对应的class名称
    - the treat runtime caches the resolved styles object in memory

- **treat生成样式的原理解析**
- 不包含theme的样式

``` JS
// 组件源码
import * as styles from './MyTreatTitle.treat';
const UnThemedTitle = (props) => <h2 className={styles.sBtn}>{props.children}</h2>;

// bundle后
var UnThemedTitle = function UnThemedTitle(props) {
  return /*#__PURE__*/ react__WEBPACK_IMPORTED_MODULE_0___default.a.createElement("h2", {
    // sBtn在打包后的文件中是一个字符串变量
    className: _MyTreatTitle_treat__WEBPACK_IMPORTED_MODULE_3__["sBtn"]
  }, props.children);
};
```

- 包含theme的样式

``` JS
// 组件源码
import { TreatProvider, useStyles } from 'react-treat';
import theme from './theme1.treat';
import * as styles from './MyTreatTitle.treat';

export const ThemedTitle = (props) => {
  const styles1 = useStyles(styles);

  return (
    <h2 {...props} className={styles1.tBtn}>
            {props.children}
        </h2>
  );
};
<TreatProvider theme={theme}>
  <ThemedTitle>brand 主题 style</ThemedTitle>
</TreatProvider>

// 打包后
var ThemedTitle = function ThemedTitle(props) {
  // 这里已经是字符串了，这里会通过useTheme从context中取theme名称
  var styles1 = Object(react_treat__WEBPACK_IMPORTED_MODULE_1__["useStyles"])(_MyTreatTitle_treat__WEBPACK_IMPORTED_MODULE_3__);
  return /*#__PURE__*/ react__WEBPACK_IMPORTED_MODULE_0___default.a.createElement("h2", _extends({}, props, {
    className: styles1.tBtn // 这里只是从map中根据key取value的简单计算
  }), props.children);
};
```

# faq

- 当有多个theme时，如何提高首屏加载速度，如先加载默认theme，再下载其他theme的css
  - [使用dynamic import进行split your themes into separate CSS files.](https://seek-oss.github.io/treat/setup#bundle-splitting)
  - This is achieved by dynamic importing your treat files that call createTheme.
  - You can then dynamically load the desired theme and use it to resolve styles.
- 一套主题包含所有组件 vs 一个组件的样式包含多套主题
  - theme-ui给出的方案是前者，使用带约束的样式值

``` JS
import { resolveStyles } from 'treat';
import styleRefs from './styles.treat';

// Inject the theme name somehow:
const themeName = getThemeName();

import(`../themes/${themeName}.treat`).then(theme => {
  const styles = resolveStyles(theme.default, styleRefs);
  // You now have access to themed styles!
});
```

# roadmap

- treat doesn't do any class optimization as it could introduce specificity issues
- 作为类sass预处理器的js版
  - 考虑提供编译出多套css的功能，或按组件编译出css
  - 编译出带有css variables的版本和不带css variables的版本(参考post-preset-env)
- 静态提取
  - 为加快首屏渲染，编译出首屏相关的关键路径样式和其他样式

# docs

- ## [introduction](https://seek-oss.github.io/treat/)
- Write your styles in js/ts within treat files (e.g. Button.treat.js) that get executed at build time.
- All CSS rules are created ahead of time, so the runtime is very lightweight — only needing to swap out pre-existing classes. 
- In fact, if your application doesn’t use theming, you don’t even need the runtime at all.
  - Because theming is achieved by generating multiple classes, legacy browsers are supported.
- Your project must be using webpack with the supplied webpack plugin

- ## [background](https://seek-oss.github.io/treat/background)
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

- ## [How it works](https://seek-oss.github.io/treat/how-it-works)
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

# treat-repos

- https://github.com/seek-oss/braid-design-system
  - Themeable design system for the SEEK Group
- https://github.com/autoguru-au/overdrive
  - Overdrive is a product component library, and design system for AutoGuru. 
  - Built with React, TypeScript, Treat, Playroom and Storybook.

# pieces

- If you're interested in CSS-in-JS, but can't get yourself to drop CSS Modules due to its lean(瘦小的，精干的，高效的) bundle size and performance footprint, you really need to have a look at treat.
  - https://twitter.com/markdalgleish/status/1154530205215518720
  - Why not just use css modules tho?
    - In my experience, most people don't "just use CSS Modules" though. It's often paired with a preprocessor. At its core, this is similar to using JavaScript as your CSS Modules preprocessor.
  - This probably solves my problem with CSS modules where I can't cross reference styles between two modules

- I use emotion and styled-components in my personal projects, 
  - but in my professional career to date, it’s been options like CSS Modules, 
  - Vue's built-in scoped CSS support, or even good old SCSS that has generally won out — introducing a run-time cost to users is a big trade-off.

- Curious as to what was less than ideal about generating .d.ts files for your css modules. @1stdibs is moving to ts & have been using css modules for years.
  - https://twitter.com/mattcompiles/status/1154180742802374656
  - We(treat) were reliant on webpack running to generate .d.ts files for our css modules.
    - This creates a bunch of potential issues as you need to ensure the generated files are in sync with the real file. It's doable but not ideal.
- treat is both a webpack plugin and a loader that work together. 
  - It essentially compiles all treat files in isolation and executes them at build time, replacing them with their result. The babel plugin is optional and only for improving the dev experience.
  - Which means Babel alone isn't enough?
  - Babel only thinks about one file at a time. In treat you can import any dependencies you need to create your styles (lodash, polished, etc) and they are completely stripped from your final output.

- we'd theme with something like a theme class on the body and then defs such as `.greenTheme .text {color: green}` and `.redTheme .text {color: red}`. Besides the obvious, why the js runtime instead?
  - That approach increases specificity for all themed classes which means you've got to constantly take that into account. 
  - Also, you can't reliably nest themes as the closest theme isn't what's applied, it's actually applied based on CSS rule order precedence.
  - 后期研发组件层次的theme和库层次的theme，不一定能选中元素了

# [otion](https://github.com/kripod/otion/tree/main/packages/otion)

- Atomic CSS-in-JS with a featherweight runtime
- Design systems embrace a component-oriented mindset. 
- Inspired by Tailwind CSS, utility classes provide reusable styles with no unwanted side-effects. However, they have to be generated upfront.
- Atomicity generalizes the former concept by instantiating style rules on demand. Serving as a solid foundation for constraint-based layouts, atomic CSS-in-JS has come to flourish at scale.
- 缺点或局限
  - Global styles
    - Being unique by nature, non-scoped styles should not be decomposed into atomic rules. 
    - This library doesn't support injecting global styles, as they may cause unexpected side-effects. 
    - However, ordinary CSS can still be used for style sheet normalization and defining the values of CSS Custom Properties.
    - Contrary to otion-managed styles, CSS referenced from a `<link>` tag may persist in the cache during page changes. 
    - Global styles are suitable for application-wide styling (e.g. normalization/reset), 
    - while inlining the scoped rules generated by otion accounts for faster page transitions due to the varying nature of per-page styles.
  - Theming
    - Many CSS-in-JS libraries tend to ship their own theming solutions. 
    - Contrary to others, otion doesn't embrace a single recommended method, leaving more choices for developers. 
    - Concepts below are encouraged: CSS Custom Properties; A singleton or value providers (e.g. React Context)
- [implement a plugin system?](https://github.com/kripod/otion/issues/4)
  - I was thinking about a plugin system during the initial development phases, but decided against them to reduce the scope of the library.
  - I would rather support ordinary CSS (e.g. flexbox layout) than custom logic (e.g. a stack with non-standard attributes). 
  - For the latter, components could be defined in libraries like React. 
  - Frameworks like glaze could also build upon otion to bring more customizability out of the box.
- [Ahead of time style processing with static CSS extraction and a Babel or webpack plugin](https://github.com/kripod/otion/issues/37)
  - The styling code shown on the previous image can be split into two parts, possibly with a Babel plugin
  - The static part may be replaced with its corresponding hashed class name string ahead of time.

- The CSS-in-JS lib I’m working on will only allow object styles, embracing type safety and simplifying atomic decomposition.
  - **Static extraction has a lot of caveats and inconveniences, so I prefer a featherweight runtime solution with near-zero overhead instead.**
- I think the `css({…})` API provided by Emotion and Styled Components are by far the most convenient way to do styling in JS. 
  - I’m proposing that API with atomic constraints (e.g. no descendant selectors) and deterministic class names as output.
- While this may seem to be ridiculous at the first glance, here's how I'm managing rule specificities with runtime-instantiated atomic CSS classes. 
  - Even though `:hover` is declared after `:focus`, the former takes precedence as recommended by @tailwindcss
  - A pre-defined pseudoselector order is required so that subsequent rule injections cannot void the effects of each other.
  - In my library I use this ordered stylesheet that Nicolas Gallagher came up with. Your idea of bumping the specificity by repeating selectors is not bad. Do you know if it can have an impact on perf (matching)?
  - It surely has an impact, as no sorting (taking n * log n steps on average) is necessary. My rule insertion algorithm runs in constant time and now uses an even more compact lookup table, about which I'm about to tweet.
  - However, I would recommend this approach only when using atomic CSS with a constrained list of selectors (e.g. simple pseudos only). Anything more complicated is pretty hard to execute properly, especially when allowing custom combinations of selectors.

- The runtime is significantly lighter, as no parsing happens, contrary to Emotion and Styled Components. 
  - https://twitter.com/kripod97/status/1262101505383059456
  - Both libraries use Stylis, an excellent preprocessor.
  - I decided to go with string transformations and recursion instead, digging through W3C specifications about syntax.
  - Also, the former libraries don't perform atomic decomposition of style rules. Atomicity guarantees that each property–value pair only gets injected to the underlying document once. This results in smaller pre-rendered `<style>` tags for complex websites.
  - The project doesn’t provide a single opinionated solution for theming
  - However, glaze will depend on otion to make type-safe theming available.
- why should I use it instead of emotion beside the bundle size?
  - Atomicity is the main benefit. Each CSS rule is only inserted to the target `<style>` tag once. No CSS duplication should happen. Also, specificity-related issues will become a thing of the past.
- The otion project will provide the foundation to build glaze upon. Eventually, it will replace treat for static style management.
