---
title: toc-lib-comp-design-css
tags: [components, css, lib, toc]
created: '2020-10-22T12:57:49.045Z'
modified: '2020-11-13T07:28:50.844Z'
---

# toc-lib-comp-design-css

## guide

- top-css-lib
  - bootstrap, bulma, materialize, spectre, primer

## popular

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
      - [Support for css variables_202007](https://github.com/jgthms/bulma/issues/3028)
        - I have a few branches working on it. I only need to find the best way to implement it.
      - [Optional CSS Variables and multi-theme ability_202006](https://github.com/jgthms/bulma/pull/2981)
        - This PR does this successfully with a lot of ingeniosity by maximizing backward compatibility, the framework can be compiled exactly like before with no css variables, it can be compiled with all the css variables for outside theming or it can be compiled with a set of themes for bundled theming
        - The only tradeoff of this solution is that because of the wrapping of each variable, the git diff is large
        - will require future PR to follow the new syntax (though it's not a hard syntax, just slightly repetitive)
        - I also think it’s not necessary to transform all Bulma variables into CSS variables. For theming purposes and dark mode support, colors would largely suffice.
  - https://github.com/wtho/bulma-css-vars
    - Bulma CSS Vars extends Bulma to use CSS variables, 
    - that can be set to arbitrary values at runtime on the website and installs fallbacks for browsers without CSS variables capabilities.
- pure-css /BSD/21kStar/202007/Yahoo
  - https://github.com/pure-css/pure
  - http://purecss.io/
  - A set of small, responsive CSS modules
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
- water.css /5.7kStar/MIT/202010/css/classless
  - https://github.com/kognise/water.css
  - a CSS framework that doesn't require any classes. 
- spectre /MIT/10.3kStar/202007
  - https://github.com/picturepan2/spectre
  - https://picturepan2.github.io/spectre/
  - a responsive CSS framework based on flexbox
  - Designed and built by Yan Zhu(Microsoft MVP)
- milligram /MIT/8.8kStar/202006
  - https://github.com/milligram/milligram
  - https://milligram.io/
  - A minimalist CSS framework.
- primer-css /MIT/9.7kStar/202010/scss
  - https://github.com/primer/css
  - https://primer.style/css
  - The CSS implementation of GitHub's Primer Design System

## css-design-system

- vanilla-framework /438Star/LGPLv3/202009/scss
  - https://github.com/canonical-web-and-design/vanilla-framework
  - https://vanillaframework.io/
  - a simple extensible CSS framework, built using Sass
- Skin /eBay
  - /111Star/MIT/202010/less
  - https://github.com/eBay/skin
  - https://ebay.github.io/skin/
  - Pure CSS framework designed & developed by eBay for e-commerce marketplace.
  - Skin follows the BEM methodology of "Block, Element and Modifier" to ensure our HTML class name and structure is human readable and understandable.
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

## atomic-css

- https://github.com/stowball/hucssley
  - a full-featured, consistent, atomic utility class library for rapidly building performant UI

## css-tools

- https://github.com/zicht/zss
  - Sass for design systems

## more-css-repos

- https://github.com/BafS/Gutenberg
  - Modern framework to print web pages correctly
  - To hide elements to be printed, you can simply add the class `no-print`.
