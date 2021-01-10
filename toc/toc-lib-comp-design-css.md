---
title: toc-lib-comp-design-css
tags: [components, css, lib, toc]
created: '2020-10-22T12:57:49.045Z'
modified: '2020-11-13T07:28:50.844Z'
---

# toc-lib-comp-design-css

# guide

- top-css-lib
  - bootstrap, bulma, materialize, spectre, primer
- ref
  - search: pure css, css only
  - https://github.com/topics/css-framework?o=desc&s=updated
  - https://github.com/troxler/awesome-css-frameworks

# popular

- bootstrap /MIT/143kStar/202007
  - https://github.com/twbs/bootstrap
  - https://getbootstrap.com/
  - The most popular HTML, CSS, and JS framework for developing responsive, mobile first projects on the web.
- bulma /MIT/40.5kStar/202007
  - https://github.com/jgthms/bulma
  - https://bulma.io/
  - Modern CSS framework based on Flexbox
  - https://github.com/jgthms/bulma/tree/css-variables-with-fallback
    - I've been working on this CSS Variables + HSL version of Bulma.
      - The idea is to provide each value as a separate variable, so you can tweak the H, S or L independently. 
      - That way you can theme a whole page dynamically.
    - The main issue is that it requires close to 100 CSS Variables to be applied to `:root`. 
      - While this is done automatically, it might be considered noisy and verbose. 
      - It is however the most flexible approach for theming a CSS framework.
- spectre /MIT/10.3kStar/202007/文档多页
  - https://github.com/picturepan2/spectre
  - https://picturepan2.github.io/spectre/
  - a responsive CSS framework based on flexbox
  - Designed and built by Yan Zhu(Microsoft MVP)
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
- primer-css /MIT/9.7kStar/202010/scss
  - https://github.com/primer/css
  - https://primer.style/css
  - The CSS implementation of GitHub's Primer Design System
- pure-css /BSD/21kStar/202007/Yahoo
  - https://github.com/pure-css/pure
  - http://purecss.io/
  - A set of small, responsive CSS modules
- https://github.com/finnhvman/matter
  - Material Design Components in Pure CSS
  - Materializing HTML at just one class per component
  - The purpose of Matter is to provide the most easy-to-use but accurate implementation of Material Design Components.
  - Matter is built with theming in mind
  - more-material
    - https://github.com/mildrenben/surface
- https://github.com/tylerchilds/cutestrap
  - A strong, independent CSS Framework. Only 2.7KB gzipped.
  - The two constraints for browser support are Custom Properties and CSS Grid.
- https://github.com/alphardex/aqua.css
  - https://aquacss.netlify.com/
  - 纯CSS框架，没有任何JS。许多CSS变量，易换肤
  - [dashboard demo](https://codepen.io/alphardex/full/yLNwKqx)

# css framework

- vanilla-framework /438Star/LGPLv3/202009/scss
  - https://github.com/canonical-web-and-design/vanilla-framework
  - https://vanillaframework.io/
  - a simple extensible CSS framework, built using Sass
- milligram /MIT/8.8kStar/202006/文档单页
  - https://github.com/milligram/milligram
  - https://milligram.io/
  - A minimalist CSS framework.
- Skin /eBay
  - /111Star/MIT/202010/less
  - https://github.com/eB ay/skin
  - https://ebay.github.io/skin/
  - Pure CSS framework designed & developed by eBay for e-commerce marketplace.
  - Skin follows the BEM methodology of "Block, Element and Modifier" to ensure our HTML class name and structure is human readable and understandable.
- https://github.com/Dogfalo/materialize /38.3kStar/MIT/202006
  - https://materializecss.com/
  - a CSS Framework based on material design
- https://github.com/muicss/mui /4.5kStar/MIT/202006
  - https://www.muicss.com/
  - lightweight CSS framework that follows Google's Material Design guidelines.
  - Small footprint: mui.min.css - 6.6K, mui.min.js - 5.4K (gzipped)
- https://github.com/magnetis/astro
  - /89Star/Apache2/202008/css
  - https://astro.magnetis.com.br/
  - An open source design system by Magnetis
  - Astro is built based on Atomic Design
- https://github.com/sky-uk/toolkit
  - http://www.sky.com/toolkit
  - Sky's CSS Toolkit
- https://github.com/uswitch/ustyle
  - https://ustyle.guide/
  - A living styleguide and pattern library by uSwitch.
  - just import the base uSwitch styles at the start of your file
  - uStyle comes with JavaScript implementations of the custom Sass Ruby functions used by Sprockets.

# classless

- https://github.com/xz/new.css
  - A classless CSS framework to write modern websites using only HTML.
- water.css /5.7kStar/MIT/202010/css/classless
  - https://github.com/kognise/water.css
  - a CSS framework that doesn't require any classes. 

# more-css-framework

- https://github.com/sitetent/tentcss
  - Includes only the essentials to make camp.
  - not currently receiving updates.
- https://github.com/AliBahaari/Jikan
  - https://alibahaari.github.io/Jikan/
  - CSS framework for better, faster and more beautiful UIs.
