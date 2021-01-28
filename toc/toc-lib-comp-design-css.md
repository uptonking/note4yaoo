---
title: toc-lib-comp-design-css
tags: [components, css, lib, toc]
created: '2020-10-22T12:57:49.045Z'
modified: '2020-11-13T07:28:50.844Z'
---

# toc-lib-comp-design-css

# guide

- 设计样式时theming可参考
  - material, bootstrap, flat/metro, neumorphism, monochrome, hand-drawn

- ref
  - search: pure css, css only, css framework, css vars
  - https://github.com/topics/css-framework?o=desc&s=updated
  - https://github.com/troxler/awesome-css-frameworks

# css-themes-popular

## material

- materialize /38.3kStar/MIT/202006
  - https://github.com/Dogfalo/materialize
  - https://materializecss.com/
  - 文档多页，基于jade
  - a CSS Framework based on material design
  - 视觉上边框线不明显，大量运用色块
- https://github.com/mildrenben/surface
  - https://mildrenben.github.io/surface/
  - /345Star/MIT/201709/css/inactive/文档多页
  - A Material Design CSS only framework
- https://github.com/maxsite/berry
  - https://maxsite.org/berry
  - A utility-first CSS framework with full support Material Design.
- https://github.com/ManuTheCoder/material-design-pro
  - https://material-design-pro.hostman.site/
  - a responsive front end framework based on Material Design
- https://github.com/finnhvman/matter
  - /870Star/MIT/201907/js
  - Material Design Components in Pure CSS
  - Materializing HTML at just one class per component
  - The purpose of Matter is to provide the most easy-to-use but accurate implementation of Material Design Components.
  - Matter is built with theming in mind
- more-material
  - mui /4.5kStar/MIT/202006
    - https://github.com/muicss/mui 
    - https://www.muicss.com/
    - lightweight CSS framework that follows Google's Material Design guidelines.
    - Small footprint: mui.min.css - 6.6K, mui.min.js - 5.4K

## flat/metro

- https://github.com/daniruiz/flat-remix-css
  - http://drasite.com/flat-remix-css
  - CSS library that provides a set of predesigned elements
  - It follows a modern flat design using a colorful palette
  - 视觉上，边框线特别明显，轮廓分明
- https://github.com/ajusa/lit
  - https://ajusa.github.io/lit
  - 单页文档
  - a ridiculously small responsive css framework.
  - preserve everything Skeleton, Milligram, and other micro frameworks have to offer.
- https://github.com/olton/Metro-UI-CSS
  - https://metroui.org.ua/
  - Build responsive projects on the web in Metro Style
- https://github.com/codyogden/press-css
  - https://press-css.io/
  - A flat, material, no bullshit, highly extensible CSS button library.
- https://github.com/Tropix126/wincss
  - https://tropix126.github.io/wincss
  - WinCSS is SASS framework which emulates the styles of Fluent Design applications as seen in WinUI 2.4.
- https://github.com/siimple/siimple
  - https://docs.siimple.xyz/examples/index.html
  - The minimal CSS toolkit for flat and clean designs
  - started as a small css framework with basic UI elements.

## neomorphism

- https://github.com/ismail9k/neomorphism
  - https://ismail9k.github.io/neomorphism/
  - UI components library in the new neomorphism design style

## monochrome

- https://github.com/asvvvad1/mono-color
  - https://asvvvad1.github.io/mono-color/
  - /57Star/MIT/202008
  - CSS-only framework built with responsivity, readability, modularity, and a dual-theme in mind.
- https://github.com/kokushin/mono.css
  - https://kokushin.github.io/mono.css/
  - /8Star/MIT/201707/css
  - Minimal design based on black and white.
- https://github.com/cihankoseoglu/shades
  - A Sass/CSS framework for minimalist websites that use black, white and shades of gray as a design choice

## hand-drawn

- https://github.com/papercss/papercss /字体变成手写体
  - https://www.getpapercss.com/
  - /3.2kStar/ISC/202011/scss
  - The Less Formal CSS Framework
- https://github.com/fxaeberhard/handdrawn.css
  - http://fxaeberhard.github.io/handdrawn.css/
  - /61Star/CC0-1.0/201606/css
  - Handdrawn.css lets you prototype your web site with a hand drawn look and feel.

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
- spectre /MIT/10.3kStar/202007
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
  - Front-end framework with a built-in dark mode and full customizability using CSS variables; great for building dashboards and tools.
  - Halfmoon is designed to have classes very similar to the ones found in Bootstrap
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
- cirrus /694Star/MIT/202101/scss
  - https://github.com/Spiderpig86/Cirrus
  - https://cirrus-ui.netlify.app/
  - 文档单页，文档样式非常友好
  - A fully responsive CSS framework with beautiful controls and simplistic structure. 
  - Cirrus is designed to be adaptable to existing themes or when starting fresh.
  - The only component that requires the use of jQuery is the Header component for toggling the dropdown menu on mobile.

 

- https://github.com/ciucacristi/elementric
  - https://ciucacristi.github.io/elementric/
  - Elementric is a free front-end package of UI element
  - 样式设计基于白底的圆角方形，设计感很强

# css vars

- https://github.com/alphardex/aqua.css
  - https://aquacss.netlify.com/
  - 纯CSS框架，没有任何JS。许多CSS变量，易换肤
  - 文档基于vue，仓库中提供了很多纯html demo示例
  - [dashboard demo](https://codepen.io/alphardex/full/yLNwKqx)
- https://github.com/zaydek/duomo
  - https://codepen.io/zaydek/pen/vYXjBra (dashboard skeleton)
  - 无docs网站
  - Stackable, themeable CSS library
  - Duomo is a stack-based CSS framework.(stacks are based on Flexbox)
  - Duomo is a spiritual successor of Tailwind CSS.
  - Uses HStack and VStack instead of Flexbox for rows and columns
  - Uses ZStack to layer along the z-axis
  - Introspection via CSS variables; Duomo tokens can be overridden without Sass
  - Small JavaScript runtime for toggling dark mode, etc.

- https://github.com/elishaterada/feathercss /设计简洁干净
  - https://feathercss.makerkits.co/
  - 文档单页，文档基于next，每个组件并排显示明暗两种样式
  - FeatherCSS is a Dark Mode ready minimalist CSS Framework with support for RTL and Accessibility
  - It purposefully excludes features like grid layout, media queries, or icons which tends to require per-project customization.
  - It’s Just CSS™ with CSS variables. Bring your own LESS/SaaS/CSS-in-JS solution
  - How Dark Mode works
    - In order to provide maximum flexibility of turning it on, off, or automatically switch based on user display settings, you can toggle `data-theme="dark"` attribute to your markup with a minimal JavaScript code (consult your framework specific solutions).

- https://github.com/jenil/chota
  - https://jenil.github.io/chota/
  - 文档单页，纯html
  - Easy to extend with CSS variables
  - Easy dark mode switch

- https://github.com/tylerchilds/cutestrap
  - http://www.cutestrap.com/features/themes
  - A strong, independent CSS Framework. Only 2.7KB gzipped.
  - The two constraints for browser support are Custom Properties and CSS Grid.
  - 样式源码基于css，默认首页文档是多个html，另外的css文档使用了kss生成

- https://github.com/lnolte/und-css
  - https://css.und-pohlen.de/tokens/
  - 文档单页，样式过于简单，不推荐
  - Custom Property based CSS Framework fully configurable using SASS
  - und CSS aims to make working with CSS easier by providing robust compositions and tools to flexibly set up visual languages fast.
  - und CSS consists of three parts: Tokens, Objects and Utilities
- https://github.com/fortrabbit/teutonic-css
  - https://teutonic.co/
  - 样式很不美观
  - A modern CSS framework — versatile, well documented.
  - It's based on CSS Variables for easy customization and extension. 
  - It features cool tech like CSS Grid. 
  - The source is a collection of SCSS modules

- https://github.com/johannschopplich/buldy
  - 无docs网站
  - Modern CSS framework distilled from the best of larger frameworks
  - Easily editable and extendable CSS variables

# css-framework

- milligram /8.8kStar/MIT/202006
  - https://github.com/milligram/milligram
  - https://milligram.io/
  - /9.2kStar/MIT/202006/css
  - 文档单页，文档也支持多页，基于pug实现
  - A minimalist CSS framework.
- chipolette /5Star/MIT/202008/css
  - https://github.com/Marcisbee/chipolette
  - http://marcisbee.com/chipolette/
  - 单页文档，但根据多个html通过innerHTML实现
  - It is designed to replace Bootstrap and to be used with CSS variables.
  - Chipolette is a tiny CSS framework/Starter kit.
  - It's a fork from Shoelace and Bootstrap, that fully embraces CSS variables/custom properties.
  - It's written in LESS, because of nesting and other neat features
  - It is designed to replace Bootstrap and to be used with CSS variables.
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

# classless

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

- https://github.com/yashdiniz/FRUI
  - Flat & Round User Interface, is a minimalistic and professional UI framework 
