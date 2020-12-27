---
title: toc-lib-css-in-js
tags: [css-in-js, lib, toc]
created: '2020-08-07T18:20:02.290Z'
modified: '2020-09-25T05:56:32.022Z'
---

# toc-lib-css-in-js

## popular

- styled-components /31kStar/MIT/202009
  - https://github.com/styled-components/styled-components
  - Use the best bits of ES6 and CSS to style your apps
- emotion /11.7kStar/MIT/200208
  - https://github.com/emotion-js/emotion
  - CSS-in-JS library designed for high performance style composition
- jss /6kStar/MIT/202009
  - https://github.com/cssinjs/jss
  - https://cssinjs.org/features
  - A lib for generating Style Sheets with JavaScrip
  - Is it possible to fully extract CSS and use it with link tag?
    - Yes. The easiest way to do so is to export styles from modules.

## near-zero-runtime css in js

- linaria /6kStar/MIT/202009
  - https://github.com/callstack/linaria
  - Write CSS in JS, but with zero runtime, CSS is extracted to CSS files during build
  - 基于css variables实现
- treat /975Star/MIT/202009
  - https://github.com/seek-oss/treat
  - Themeable, statically extracted CSS‑in‑JS with near‑zero runtime.
  - 类似sass的预编译，不能在runtime生成新样式
- astroturf /1.8kStar/MIT/202004
  - https://github.com/4Catalyzer/astroturf
  - lets you write CSS in your JavaScript files without adding any runtime layer
  - 生成css，需要单独考虑css文件，额外使用autoprefix插件
- glaze /375Star/MIT/202006
  - https://github.com/kripod/glaze
  - 缺点是部分样式是动态生成的
  - 支持treat file形式的静态样式，也支持在sx方法中书写带theme约束的样式值，但这部分样式会动态生成
  - 要使用glaze的ThemeProvider传入theme，不能使用react-treat的TreatProvider传入theme
  - Glaze, the theme-ui API with almost zero runtime based on treat
  - This project was born to combine the best of its predecessors into a single solution
    - Near-zero runtime, made possible by treat: Theming support, Static style extraction
    - Utility-first CSS, as implemented by Tailwind CSS: no duplicated rules
    - Constraint-based layouts, popularized by Theme UI
  - [Production ready? no. 主程已转向研发otion](https://github.com/kripod/glaze/issues/37)
    - The otion project will provide the foundation to build glaze upon. Eventually, it will replace treat for static style management.
- https://github.com/WalltoWall/calico
  - Calico is a customizable styling library that maps React props to statically generated class names.
  - 缺点是组件必须使用提供的Box组件创建
  - 优点是预先生成所有css，使用原子类的形式，生成的样式名超级多，适合大规模应用，不适合小规模应用
  - 基于treat和react-treat，所有主题的样式均可静态提取
  - 通过styles属性直接书写theme对象中的属性值，通过类似`Button.treat.js`的treat file添加一次性的样式
  - Very light runtime made possible by the treat library.
    - Static style extraction with full type safety.
    - Dynamic styles via swapping classNames.
  - Atomic CSS as inspired by libraries like Tailwind CSS
    - Encourages reusability with a finite set of generated classNames.
  - Developer-centric as inspired by styled-system and theme-ui.
    - Define responsive styles via arrays.
    - Namespaced styles to ease type-extensibility.
    - One-off styles can be defined in .treat files with additional responsive helpers added onto your theme.
- css-zero /179Star/MIT/201912
  - https://github.com/CraigCav/css-zero
  - All of the benefits of writing CSS-in-JS, but with zero runtime code
  - Works without JavaScript, as styles are extracted at build-time.
  - Generates optimized, atomic CSS with no duplicated style rules
  - Theme support via CSS variables, allowing the cost of theming to be proportional to the size of the color palette
  - This repo was heavily inspired by linaria. The biggest behavioral difference is that linaria doesn't generate atomic CSS.
  - 参考facebook的stylex
- stylemug /51Star/MIT/202006/js
  - https://github.com/matvp91/stylemug
  - A fast css-in-js library that extracts atomic CSS rules to a .css file.
  - The stylesheet code in your bundle is replaced (no CSS in your JS) with a hash map for classnames lookup at runtime.
- reshadow /332Star/MIT/202006/js
  - https://github.com/lttb/reshadow
  - Combine the css-in-js and css-modules approaches or choose which fits you better
  - Compile-time styles processing and efficient runtime
  - 静态样式支持静态提取，动态样式基于styled，书写样式使用css字符串

## atomic css in js

- compiled /797Star/Apache2/202009
  - https://github.com/atlassian-labs/compiled
  - Build time atomic CSS in JS without the runtime cost.
  - Compiled, styled and css prop with a tiny runtime
- otion /437Star/MIT/202009
  - https://github.com/kripod/otion
  - Atomic CSS-in-JS with a featherweight runtime
  - Negligible runtime footprint, Works without a framework
  - The otion project will provide the foundation to build glaze upon. Eventually, it will replace treat for static style management.
  - [Atomic CSS-in-JS](https://sebastienlorber.com/atomic-css-in-js)
- stitches /1.3kStar/MIT/202009
  - https://github.com/modulz/stitches
  - Near-zero runtime, server-side rendering, multi-variant support, and best-in-class developer experience.
- style-sheet /220Star/MIT/202008
  - https://github.com/giuseppeg/style-sheet
  - compiling rules to atomic CSS that can then be extracted to .css file with a Babel plugin.
- style9 /246Star/MIT/202009
  - https://github.com/johanholmerin/style9
  - CSS-in-JS compiler inspired by Facebook's stylex
  - Compiles to atomic CSS
  - issues未开

## more-css-in-js

- trousers /284Star/MIT/202007
  - https://github.com/danieldelcore/trousers
  - hooks-first CSS-in-JS library, focused on semantics and runtime performance
- aesthetic-suite-framework /163Star/MIT/202009
  - https://github.com/aesthetic-suite/framework
  - multi-platform styling framework that offers a strict design system, robust atomic CSS-in-JS engine, a structural style sheet specification (SSS), a low-runtime solution
- https://github.com/segmentio/ui-box
  - ui-box is a low level CSS-in-JS solution that focuses on being simple, fast and extensible. 
  - All CSS properties are set using simple React props, which allows you to easily create reusable components that can be enhanced with additional CSS properties. 
- https://github.com/lttb/reshadow
  - MIT/296Star/202006
- https://github.com/lukejacksonn/csz
  - Runtime CSS modules with SASS like preprocessing
  - A framework agnostic css-in-js solution that uses stylis to parse styles from tagged template literals and append them to the head of the document at runtime. 
  - Loading in stylesheets dynamically – from .css files – is supported out of the box, 
  - so you can write your styles in .css files and import them via url without having to worry about flashes of unstyled content.
