---
title: toc-lib-css-fwk
tags: [css, lib, toc]
created: '2020-10-22T12:57:49.045Z'
modified: '2021-01-28T21:14:14.667Z'
---

# toc-lib-css-fwk

# css-framework-popular

- bootstrap /143kStar/MIT/202007
  - https://github.com/twbs/bootstrap
  - https://getbootstrap.com/
  - The most popular HTML, CSS, and JS framework for developing responsive, mobile first projects on the web.

- bulma /40.5kStar/MIT/202007
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

- spectre /10.3kStar/MIT/202007
  - https://github.com/picturepan2/spectre
  - https://picturepan2.github.io/spectre/
  - 文档多页，文档基于pug实现
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

- halfmoon /2.1kStar/MIT/202010/js
  - https://github.com/halfmoonui/halfmoon
  - https://www.gethalfmoon.com/
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

- skeleton /18kStar/MIT/201412/css
  - https://github.com/dhg/Skeleton
    - http://www.getskeleton.com/
    - A Dead Simple, Responsive Boilerplate
  - https://github.com/atomicpages/skeleton-sass
    - https://atomicpages.github.io/skeleton-sass/
    - Skeleton Sass is a highly modular version of Skeleton CSS
    - 提供了themes
  - https://github.com/WhatsNewSaes/Skeleton-Sass
    - Sass Version of Skeleton (2.0.4)
  - more-skeleton
    - https://github.com/amdelamar/osseous
      - A project based off of Skeleton and other popular libraries.
      - a small CSS framework that only includes some (bony) elements

- primer-css /9.7kStar/MIT/202010/scss
  - https://github.com/primer/css
  - https://primer.style/css
  - The CSS implementation of GitHub's Primer Design System
- pure-css /BSD/21kStar/202007/Yahoo
  - https://github.com/pure-css/pure
  - http://purecss.io/
  - A set of small, responsive CSS modules
- cirrus /694Star/MIT/202101/scss
  - https://github.com/Spiderpig86/Cirrus
  - https://cirrus-ui.netlify.app/
  - 文档单页，文档样式非常友好
  - A fully responsive CSS framework with beautiful controls and simplistic structure. 
  - Cirrus is designed to be adaptable to existing themes or when starting fresh.
  - The only component that requires the use of jQuery is the Header component for toggling the dropdown menu on mobile.

# css-framework-ui

- chipolette /5Star/MIT/202008/css
  - https://github.com/Marcisbee/chipolette
  - http://marcisbee.com/chipolette/
  - It is designed to replace Bootstrap and to be used with CSS variables.
  - 单页文档，但根据多个html通过innerHTML实现
  - Chipolette is a tiny CSS framework/Starter kit.
  - It's a fork from Shoelace and Bootstrap, that fully embraces CSS variables/custom properties.
  - It's written in LESS, because of nesting and other neat features
  - It is designed to replace Bootstrap and to be used with CSS variables.
- milligram /8.8kStar/MIT/202006
  - https://github.com/milligram/milligram
  - https://milligram.io/
  - /9.2kStar/MIT/202006/css
  - 文档单页，文档也支持多页，基于pug实现
  - A minimalist CSS framework.
- vanilla-framework /438Star/LGPLv3/202009/scss
  - https://github.com/canonical-web-and-design/vanilla-framework
  - https://vanillaframework.io/
  - a simple extensible CSS framework, built using Sass
- Skin /111Star/MIT/202010/less/ebay
  - https://github.com/eBay/skin
  - https://ebay.github.io/skin/
  - Pure CSS framework designed & developed by eBay for e-commerce marketplace.
  - Skin follows the BEM methodology of "Block, Element and Modifier" to ensure our HTML class name and structure is human readable and understandable.

- https://github.com/sky-uk/toolkit
  - http://www.sky.com/toolkit
  - Sky's CSS Toolkit
  - https://github.com/sky-uk/toolkit-react
- https://github.com/OfficeDev/office-ui-fabric-core
  - Fabric is a responsive, mobile-first collection of styles and tools designed to make it quick and simple for you to create web experiences using the Office Design Language.

 

- https://github.com/andrearufo/nova.css
  - https://andrearufo.github.io/nova.css/
  - 文档单页，样式非常友好
  - minimalistic CSS framework for your webpages.
  - Made in pure SCSS and compiled with Gulp.

- https://github.com/Borderliner/Meshki
  - https://borderliner.github.io/Meshki/
  - Meshki: A Black-Colored, Responsive Boilerplate for UI Development

# classless-framework

- water.css /5.7kStar/MIT/202010/css/classless
  - https://github.com/kognise/water.css
  - https://watercss.kognise.dev/
  - I commonly make quick demo pages or websites with simple content. 
    - For these, I don't want to spend time styling them but don't like the ugliness of the default styles.
  - Water.css is a CSS framework that doesn't require any classes. 
- new.css /3.2kStar/MIT/202009/css
  - https://github.com/xz/new.css
  - https://newcss.net/
  - A classless CSS framework to write modern websites using only HTML.
- sakura /2.9kStar/MIT/202012/scss
  - https://github.com/oxalorg/sakura
  - https://oxal.org/projects/sakura/demo/
  - a minimal classless css framework/theme
- https://github.com/yegor256/tacit
  - http://yegor256.github.io/tacit/
  - Tacit's goal is to be super simple and always with the same look-and-feel.
  - Here are some frameworks built on top of Tacit: kacit, Bahunya
- https://github.com/kevquirk/simple.css
  - a classless CSS template that allows you to make a good looking website really quickly.

# more-css-framework

- https://github.com/sitetent/tentcss
  - Includes only the essentials to make camp.
  - not currently receiving updates.
- https://github.com/AliBahaari/Jikan
  - https://alibahaari.github.io/Jikan/
  - CSS framework for better, faster and more beautiful UIs.
