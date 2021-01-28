---
title: toc-lib-css-themes
tags: [css, css-vars, themes, theming, toc]
created: '2021-01-28T21:12:30.674Z'
modified: '2021-01-28T21:35:00.167Z'
---

# toc-lib-css-themes

# guide

- 设计样式时theming可参考
  - dark/darcula, material, bootstrap, flat/metro, neumorphism, monochrome, hand-drawn(papercss), glass-ui

- ref
  - search: pure css, css only, css framework, css vars
  - https://github.com/topics/css-framework?o=desc&s=updated
  - https://github.com/troxler/awesome-css-frameworks

# themes-popular

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

# themes-ui

- https://github.com/ciucacristi/elementric
  - https://ciucacristi.github.io/elementric/
  - Elementric is a free front-end package of UI element
  - 样式设计基于白底的圆角方形，设计感很强

# css-vars

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

- https://github.com/tylerchilds/cutestrap
  - http://www.cutestrap.com/features/themes
  - 样式源码基于css，文档是多个html，但默认首页的html可单独使用
  - 提供了dark主题demo，另外的css文档使用了kss生成
  - A strong, independent CSS Framework. Only 2.7KB gzipped.
  - The two constraints for browser support are Custom Properties and CSS Grid.

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
  - 文档单页，纯html，
  - Easy to extend with CSS variables
  - Easy dark mode switch，虽然支持，但未提供主题demo

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

# more-themes

- https://github.com/yashdiniz/FRUI
  - Flat & Round User Interface, is a minimalistic and professional UI framework 
