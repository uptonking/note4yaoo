---
title: toc-lib-css-fwk-css-vars
tags: [css, css-vars, toc]
created: '2021-02-09T13:39:10.507Z'
modified: '2021-02-09T13:39:41.705Z'
---

# toc-lib-css-fwk-css-vars

# guide

- css-vars-tips
  - css变量名区分大小写
  - css变量名中可包含dash和underscore，，注意sass变量的下划线和横杠不区分
  - css变量值遵循css样式属性值的层叠规则
  - css变量值的赋值可以使用另一个css变量
  - css变量值会提升，所以可先使用再声明
  - 使用css变量值时，不能用加号构建字符串，可用`width: calc(var(--offset) * 1px);`
    - 不能用`font-size: var(--scale) + 'px';`
  - css变量值不能用在普通样式属性名，不能用在media query名称中，可用sass插值

# popular

- pico.css /65Star/MIT/202010/scss/文档优秀
  - https://github.com/picocss/pico
  - https://picocss.com/
  - theming通过添加`data-theme` + css vars到html标签实现
    - theming只处理了颜色
    - 最顶层处理了 `prefers-color-scheme: dark`
  - Graceful & Minimal CSS design system in pure semantic HTML
  - use simple native HTML tags as much as possible. Only 6 .classes are used in Pico.
  - No dependencies, package manager, external files or JavaScript.
  - Responsive everything: Elegant and consistent adaptative spacings and typography on all devices.
  - Shipped with two beautiful color themes, automatically enabled according to the user preference.
  - Pico provide a .classless version ([Example](https://picocss.com/examples/classless/)).
    - `<header>/<main>/<footer>` as direct childs of `<body>` provide a responsive vertical `padding`
    - act as containers to define a centered or a fluid viewport.

- halfmoon /2.1kStar/MIT/202010/css/js
  - https://github.com/halfmoonui/halfmoon
  - https://www.gethalfmoon.com/
  - theming基于css vars，dark-mode变量名前缀为`--dm`
  - 未提供组件级css vars
  - 未模块化，一个css文件一万多行
    - [More modular approach in the roadmap](https://github.com/halfmoonui/halfmoon/issues/78)
  - Front-end framework with a built-in dark mode and full customizability using CSS variables
    - Great for building dashboards and tools
  - Halfmoon comes with a built-in, toggleable dark mode
  - The framework is built entirely using CSS variables 
    - There are close to 1,500 CSS variables, which means that almost everything can be customized by overriding a property
  - [Complete page demo](https://www.gethalfmoon.com/page-sections-demo/)
  - [Starter template generator](https://www.gethalfmoon.com/docs/page-building/#starter-template-generator)
  - Optional JS library—Many of the components found in Halfmoon are built to work without JavaScript. 
    - However, the framework still comes with a powerful JavaScript library with no extra dependencies, such as jQuery.
  - The class names should be instantly familiar to anyone who has used Bootstrap.
  - the containers, grid system and the flex utilities found in Halfmoon CSS are almost direct copies of the ones found in Bootstrap

- infima /60kStar/MIT/202102/css
  - https://github.com/facebookincubator/infima
  - https://facebookincubator.github.io/infima/
  - A modern styling framework for content-driven websites 
  - It's just CSS, so it works with React, Vue, Angular, anything!
  - Built using modern CSS approaches - CSS variables and Postcss, BEM naming.
  - built-in support for theming and dark mode!
  - The main difference between Infima and existing CSS frameworks (e.g. Bootstrap, Bulma) is that it's built with a modern theming approach (CSS variables), modern tooling and has dark mode support out of the box, which makes it perfect for building content-driven websites such as documentation websites.

- cutestrap /1.6kStar/GPLv3/201910/css
  - https://github.com/tylerchilds/cutestrap
  - http://www.cutestrap.com/features/themes
  - 样式源码基于css，文档是多个html，但默认首页的html可单独使用
  - 定义了组件级css变量，但组件级变量未提供回退值
  - 提供了dark主题demo，另外的css文档使用了kss生成
  - 文档界面切换主题颜色、大小、网格线是基于`data-theme/rhythm/grid`
  - A strong, independent CSS Framework. Only 2.7KB gzipped.
  - The two constraints for browser support are Custom Properties and CSS Grid.

- chipolette /5Star/MIT/202008/less
  - https://github.com/Marcisbee/chipolette
  - http://marcisbee.com/chipolette/
  - 源码基于less，使用了css vars，都是全局级变量，但组件级变量依名称易分离
  - 单页文档，但通过js修改innerHTML实现展示多个html文件的内容
  - 未提供暗主题，但可通过修改css vars实现
  - Chipolette is a tiny CSS framework/Starter kit.
  - It is designed to replace Bootstrap and to be used with CSS variables.
  - It's a fork from Shoelace and Bootstrap, that fully embraces CSS variables/custom properties.
  - It's written in LESS, because of nesting and other neat features

# css-vars-fwk

- https://github.com/alphardex/aqua.css /250Star/scss
  - https://aquacss.netlify.com/
  - 纯CSS框架，没有任何JS。许多CSS变量，易换肤
  - 定义了组件级css变量，但组件级变量未提供回退值，利用了scss支持嵌套语法
  - 文档基于vue，仓库中提供了很多纯html demo示例
  - [dashboard demo](https://codepen.io/alphardex/full/yLNwKqx)

- https://github.com/zaydek/duomo /scss
  - https://codepen.io/zaydek/pen/vYXjBra (dashboard skeleton)
  - 无docs网站，没有具体ui组件，本项目专门解决层叠上下文次序和显示的问题
  - 源码scss大量运用mixin，超级复杂
  - Stackable, themeable CSS library
  - Duomo is a stack-based CSS framework.(stacks are based on Flexbox)
  - Duomo is a spiritual successor of Tailwind CSS.
  - Uses HStack and VStack instead of Flexbox for rows and columns
  - Uses ZStack to layer along the z-axis
  - Introspection via CSS variables; Duomo tokens can be overridden without Sass
  - Small JavaScript runtime for toggling dark mode, etc.

- https://github.com/elishaterada/feathercss /2Star/css
  - https://feathercss.makerkits.co/
  - 没有组件级css vars
  - 文档单页，文档基于next，每个组件并排显示明暗两种样式，设计简洁干净
  - FeatherCSS is a Dark Mode ready minimalist CSS Framework with support for RTL and Accessibility
  - It purposefully excludes features like grid layout, media queries, or icons which tends to require per-project customization.
  - It’s Just CSS™ with CSS variables. Bring your own LESS/SaaS/CSS-in-JS solution
  - How Dark Mode works
    - In order to provide maximum flexibility of turning it on, off, or automatically switch based on user display settings, you can toggle `data-theme="dark"` attribute to your markup with a minimal JavaScript code

- https://github.com/jenil/chota /css
  - https://jenil.github.io/chota/
  - 没有组件级css vars
  - 文档单页，纯html
  - Easy to extend with CSS variables
  - Easy dark mode switch，虽然支持，但未提供主题demo

- https://github.com/johannschopplich/buldy /scss
  - 只有极少数组件有组件级变量，几乎都是全局级
  - 无docs网站
  - Modern CSS framework distilled from the best of larger frameworks
  - Easily editable and extendable CSS variables

- https://github.com/lnolte/und-css /scss
  - https://css.und-pohlen.de/tokens/
  - 文档单页，样式过于简单，不推荐
  - Custom Property based CSS Framework fully configurable using SASS
  - und CSS aims to make working with CSS easier by providing robust compositions and tools to flexibly set up visual languages fast.
  - und CSS consists of three parts: Tokens, Objects and Utilities
- https://github.com/fortrabbit/teutonic-css /scss
  - https://teutonic.co/
  - 文档多页，样式很不美观，不推荐
  - A modern CSS framework — versatile, well documented.
  - It's based on CSS Variables for easy customization and extension. 
  - It features cool tech like CSS Grid. 
  - The source is a collection of SCSS modules

# more-css-vars

- https://github.com/yairEO/ui-range
  - Beautiful UI-Range input component, highly customisable, based on CSS variables.
  - A CSS-only component which is designed to work along-side the corresponding markup 
