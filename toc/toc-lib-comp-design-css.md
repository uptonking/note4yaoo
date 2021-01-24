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

- 设计样式时theming可参考
  - material, bootstrap, flat/metro, neumorphism, monochrome, hand-drawn

- ref
  - search: pure css, css only
  - https://github.com/topics/css-framework?o=desc&s=updated
  - https://github.com/troxler/awesome-css-frameworks

# css-themes-popular

## material

- https://github.com/Dogfalo/materialize
  - https://materializecss.com/
  - a CSS Framework based on Material Design
- https://github.com/maxsite/berry
  - https://maxsite.org/berry
  - A utility-first CSS framework with full support Material Design.
- https://github.com/ManuTheCoder/material-design-pro
  - https://material-design-pro.hostman.site/
  - a responsive front end framework based on Material Design

## flat/metro

- https://github.com/daniruiz/flat-remix-css
  - http://drasite.com/flat-remix-css
  - CSS library that provides a set of predesigned elements
  - It follows a modern flat design using a colorful palette
- https://github.com/codyogden/press-css
  - https://press-css.io/
  - A flat, material, no bullshit, highly extensible CSS button library.
- https://github.com/Tropix126/wincss
  - https://tropix126.github.io/wincss
  - WinCSS is SASS framework which emulates the styles of Fluent Design applications as seen in WinUI 2.4.

## neomorphism

- https://github.com/ismail9k/neomorphism
  - https://ismail9k.github.io/neomorphism/
  - UI components library in the new neomorphism design style

## monochrome

- https://github.com/kokushin/mono.css
  - https://kokushin.github.io/mono.css/
  - Minimal design based on black and white.

## hand-drawn

- https://github.com/fxaeberhard/handdrawn.css
  - Handdrawn.css lets you prototype your web site with a hand drawn look and feel.
- https://github.com/papercss/papercss /字体变成手写体
  - https://www.getpapercss.com/
  - The Less Formal CSS Framework

# css-framework-popular

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
- halfmoon /2.1kStar/MIT/202010/js
  - https://github.com/halfmoonui/halfmoon
  - https://www.gethalfmoon.com/
  - 未模块化，一个css文件一万多行
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
- primer-css /MIT/9.7kStar/202010/scss
  - https://github.com/primer/css
  - https://primer.style/css
  - The CSS implementation of GitHub's Primer Design System
- pure-css /BSD/21kStar/202007/Yahoo
  - https://github.com/pure-css/pure
  - http://purecss.io/
  - A set of small, responsive CSS modules
- https://github.com/finnhvman/matter /870Star/MIT/201907/js
  - Material Design Components in Pure CSS
  - Materializing HTML at just one class per component
  - The purpose of Matter is to provide the most easy-to-use but accurate implementation of Material Design Components.
  - Matter is built with theming in mind
  - more-material
    - https://github.com/mildrenben/surface

# css vars

- https://github.com/alphardex/aqua.css
  - https://aquacss.netlify.com/
  - 纯CSS框架，没有任何JS。许多CSS变量，易换肤
  - [dashboard demo](https://codepen.io/alphardex/full/yLNwKqx)
- https://github.com/zaydek/duomo
  - https://codepen.io/zaydek/pen/vYXjBra (dashboard skeleton)
  - Stackable, themeable CSS library
  - Duomo is a stack-based CSS framework.(stacks are based on Flexbox)
  - Duomo is a spiritual successor of Tailwind CSS.
  - Uses HStack and VStack instead of Flexbox for rows and columns
  - Uses ZStack to layer along the z-axis
  - Introspection via CSS variables; Duomo tokens can be overridden without Sass
  - Small JavaScript runtime for toggling dark mode, etc.

- https://github.com/elishaterada/feathercss /设计简洁干净
  - https://feathercss.makerkits.co/
  - FeatherCSS is a Dark Mode ready minimalist CSS Framework with support for RTL and Accessibility
  - It purposefully excludes features like grid layout, media queries, or icons which tends to require per-project customization.
  - It’s Just CSS™ with CSS variables. Bring your own LESS/SaaS/CSS-in-JS solution
  - How Dark Mode works
    - In order to provide maximum flexibility of turning it on, off, or automatically switch based on user display settings, you can toggle `data-theme="dark"` attribute to your markup with a minimal JavaScript code (consult your framework specific solutions).

- https://github.com/jenil/chota
  - https://jenil.github.io/chota/
  - Easy to extend with CSS variables
  - Easy dark mode switch

- https://github.com/johannschopplich/buldy
  - Modern CSS framework distilled from the best of larger frameworks
  - Easily editable and extendable CSS variables

- https://github.com/tylerchilds/cutestrap
  - http://www.cutestrap.com/features/themes
  - A strong, independent CSS Framework. Only 2.7KB gzipped.
  - The two constraints for browser support are Custom Properties and CSS Grid.
- https://github.com/fortrabbit/teutonic-css
  - https://teutonic.co/
  - A modern CSS framework — versatile, well documented.
  - It's based on CSS Variables for easy customization and extension. 
  - It features cool tech like CSS Grid. 
  - The source is a collection of SCSS modules
- https://github.com/lnolte/und-css
  - Custom Property based CSS Framework fully configurable using SASS
  - und CSS aims to make working with CSS easier by providing robust compositions and tools to flexibly set up visual languages fast.
  - und CSS consists of three parts: Tokens, Objects and Utilities

# css-framework

- vanilla-framework /438Star/LGPLv3/202009/scss
  - https://github.com/canonical-web-and-design/vanilla-framework
  - https://vanillaframework.io/
  - a simple extensible CSS framework, built using Sass
- milligram /MIT/8.8kStar/202006/文档单页
  - https://github.com/milligram/milligram
  - https://milligram.io/
  - A minimalist CSS framework.
- Skin /111Star/MIT/202010/less/ebay
  - https://github.com/eBay/skin
  - https://ebay.github.io/skin/
  - Pure CSS framework designed & developed by eBay for e-commerce marketplace.
  - Skin follows the BEM methodology of "Block, Element and Modifier" to ensure our HTML class name and structure is human readable and understandable.
- https://github.com/Dogfalo/materialize /38.3kStar/MIT/202006
  - https://materializecss.com/
  - a CSS Framework based on material design
- https://github.com/muicss/mui 
  - https://www.muicss.com/
  - /4.5kStar/MIT/202006
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
- https://github.com/OfficeDev/office-ui-fabric-core
  - Fabric is a responsive, mobile-first collection of styles and tools designed to make it quick and simple for you to create web experiences using the Office Design Language.

 

- https://github.com/ajusa/lit
  - https://ajusa.github.io/lit
  - a ridiculously small responsive css framework.
  - preserve everything Skeleton, Milligram, and other micro frameworks have to offer.
- https://github.com/andrearufo/nova.css
  - https://andrearufo.github.io/nova.css/
  - minimalistic CSS framework for your webpages.
  - Made in pure SCSS and compiled with Gulp.

# classless

- water.css /5.7kStar/MIT/202010/css/classless
  - https://github.com/kognise/water.css
  - a CSS framework that doesn't require any classes. 
- https://github.com/xz/new.css
  - A classless CSS framework to write modern websites using only HTML.
- https://github.com/kevquirk/simple.css
  - a classless CSS template that allows you to make a good looking website really quickly.
- https://github.com/oxalorg/sakura
  - a minimal classless css framework/theme
- https://github.com/yegor256/tacit
  - Tacit's goal is to be super simple and always with the same look-and-feel.
  - Here are some frameworks built on top of Tacit: kacit, Bahunya

# more-css-framework

- https://github.com/sitetent/tentcss
  - Includes only the essentials to make camp.
  - not currently receiving updates.
- https://github.com/AliBahaari/Jikan
  - https://alibahaari.github.io/Jikan/
  - CSS framework for better, faster and more beautiful UIs.
