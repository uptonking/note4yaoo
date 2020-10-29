---
title: note-style-css-in-js-near-zero-runtime
tags: [css-in-js, style]
created: '2020-10-06T16:44:49.163Z'
modified: '2020-10-28T10:35:24.019Z'
---

# note-style-css-in-js-near-zero-runtime

## solutions

- 技术选型时，参考知名项目或大公司项目的选择

## [astroturf](https://github.com/4Catalyzer/astroturf)

- keep your CSS fully static with no runtime style parsing.
- Use your existing tools – Sass, PostCSS, Less – but still write your style definitions in your JavaScript files
- Whole component in the single file.

- When processed, the `css` block will be extracted into a `.css` file, taking advantage of any and all of the other loaders configured to handle css.
- `styled` will be compiled to `css` block and a separate React. Component with className prop
- css-in-js libraries are a replacement for css preprocessors, in that they provide ways of doing variables, composition, mixins, imports etc. 
- astroturf doesn't try to do any of that because it's not trying to replace preprocessors, but rather, make component-centric javascript work better with existing styling tooling. 
- This means at a minimum it needs to scope styles to the component (handled by css-modules) and map those styles to your component's API (props), which is what the above API strives for. 
- This approach gains us:
  - No additional work to extract styles for further optimization (autoprefixer, minifying, moving them to a CDN, etc)
  - The smallest runtime, it's essentially zero
  - Blazing Fast™ because there is zero runtime evaluation of styles
  - Leverage the well-trod and huge css preprocessor ecosystems
- It also means we sacrifice:
  - A fine-grained style mapping to props. Props map to classes, its all very BEM-y but automated
  - Dynamism in sharing values between js and css
  - A unified JS-only headspace, you still need to think in terms of JS and CSS

## [stitches](https://stitches.dev/docs/introduction)

- styled返回的是一个高阶组件，Button组件编译后的代码如下
  - styled高阶函数参数传入了整体theme tokens的信息，被复用
  - 而Base是调用styled后生成的组件，每次render时都会计算组件属性，若无变化则不重渲染，但仍计算过了

``` JS
var Base = styled('button', {
  alignItems: 'center',
  border: 0,
  borderRadius: 3
});

return (React.createElement(Base, __assign({}, variants, attrs),
  React.createElement(Content, null, children)));
```

- stitches项目示例
  - [Modulz Design System](https://github.com/modulz/design-system)
  - [Fxtrot UI](https://github.com/LexSwed/fxtrot-ui)
    - https://fxtrot-ui.vercel.app/
  - [Byrd is a minimal design system](https://github.com/peduarte/byrd)
  - [Foursevens Web 3.0](https://github.com/Foursevens/f7-web)

- Stitches avoids unnecessary prop interpolations at runtime, making it significantly more performant than other styling libraries. 
- How does Stitches work behind-the-scenes?
  - Each CSS property in your application is mapped to an atomic class and cached. 
  - Once a class is injected, it will never be injected again. 
  - From then on, it will just return the same class.
- CSS rules are at zero risk of specificity wars. Since every rule gets its own class

- Stitches introduces variants as a first-class citizen, so you can design composable component APIs.
- One of the most exciting features is the ability to define your own tokens and seamlessly apply them as CSS values. 
  - CSS Properties are automatically mapped to token scales. 
  - Tokens can even be used in shorthand CSS properties.
- Stitches provides a simple theming experience out of the box. 
  - Create as many themes as you need, and apply them wherever you want. 
  - Each theme generates a CSS class name which overrides the default tokens.

- There are no prop interpolations. 
  - Changes to styles are defined as variants and composed in the consumption layer. 
  - This means there are no style re-evaluations at runtime.
  - **The only work Stitches does in terms of evaluation is the first time a unique rule occurs. It creates an atomic class**. 
  - If it occurs again, the cached class is reused.
- styled-components generates Object-Oriented CSS. 
  - It creates a CSS rule per component, containing all of its necessary properties.
- Stitches generates Atomic CSS. 
  - It creates a single CSS rule for every property. 
  - Each property is given its own selector, and they're added as class names to the element.

## [compiled](https://compiledcssinjs.com/docs/how-it-works)

- Compiled compiles your CSS in JS at build time by statically analyzing your code and then transforming it into Compiled Components. 
- Everything we need to use the component is included along side it in the JavaScript bundle.
- CSS can't be generated at runtime.
- While Compiled currently only targets inline Compiled Components, we'll eventually get to more exciting grounds - optional CSS extraction. 

``` typescript
// 源代码
import React from 'react';
import { ClassNames } from '@compiled/css-in-js';

export const Dynamic = ({ children, color }) => (
  <ClassNames>
    {({ css, style }) => (
      <span
        style={style}
        className={css({
          color,
        })}>
        {children}
      </span>
    )}
  </ClassNames>
);
// 编译后
import React from 'react';
import { CC, CS } from '@compiled/css-in-js';
export const Dynamic = ({ children, color }) => (
  <CC>
    <CS hash="13rakij">{['.cc-1sbi59p{color:var(--var-1ylxx6h)}']}</CS>
    <span style={{ '--var-1ylxx6h': color }} className={'cc-1sbi59p'}>
      {children}
    </span>
  </CC>
);
```

## [otion](https://github.com/kripod/otion/tree/main/packages/otion)

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
