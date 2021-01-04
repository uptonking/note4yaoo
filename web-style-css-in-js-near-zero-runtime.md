---
title: web-style-css-in-js-near-zero-runtime
tags: [css-in-js, style, zero-runtime]
created: '2020-10-06T16:44:49.163Z'
modified: '2021-01-01T20:06:44.439Z'
---

# web-style-css-in-js-near-zero-runtime

# solutions

- 技术选型时，参考知名项目或大公司项目的选择

# [astroturf](https://github.com/4Catalyzer/astroturf)

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

# [stitches](https://stitches.dev/docs/introduction)

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

# [compiled](https://compiledcssinjs.com/docs/how-it-works)

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

# [StyleSheet](https://github.com/giuseppeg/style-sheet)

- StyleSheet is a library to author styles in JavaScript.
- It is fast and generates optimized, tiny bundles by compiling rules to atomic CSS that can then be extracted to .css file with a Babel plugin.
- StyleSheet comes with built-in support for pseudo classes and media queries, i18n, React and customizable css prop.
