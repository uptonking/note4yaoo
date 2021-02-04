---
title: toc-lib-css-vars-themes
tags: [css, css-vars, themes, theming, toc]
created: '2021-01-28T21:12:30.674Z'
modified: '2021-01-29T18:54:36.865Z'
---

# toc-lib-css-vars-themes

# guide

- 设计样式时theming可参考
  - dark/darcula, material, bootstrap, flat/metro, monochrome, neumorphism, hand-drawn(papercss), glass-ui
    - 甚至所有的theme主题样式都可以在bootstrap的基础上修改
  - 基于粒子/particles的设计，或偏向于某一种dot dash的设计
    - 特别适合表达地理位置，常用在[logo](https://github.com/maplibre/maplibre-gl-js/issues/65)和icon

- ref
  - search: pure css, css only, css framework, css vars
  - https://github.com/topics/css-framework?o=desc&s=updated
  - https://github.com/troxler/awesome-css-frameworks

# css-fwk-popular

- bootstrap v5.0.0-beta1(202012)
  - reset: normalize.css8，进行了定制，移除无关浏览器，添加新样式

- primitive ui v1.5.3(202004)
  - reset: normalize.css8, scaffolding.scss

- pico.css v1.2.1(202011)
  - reset: normalize.css8, sanitize.css12, sectioning.scss

# themes-popular

## material

- https://github.com/material-components/material-components-web
  - 现在的theming功能主要通过sass实现，只有极少数变量可以通过css vars配置
    - 没有直接提供dark theme，但有提供sass实现的示例
    - [roadmap: Add Dark Mode support](https://github.com/material-components/material-components-web/issues/5253)
- materialize /38.3kStar/MIT/202006/scss
  - https://github.com/Dogfalo/materialize
  - https://materializecss.com/
  - 视觉上边框线不明显，大量运用色块
  - 文档多页，基于jade
  - a CSS Framework based on material design
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

## bootstrap-like

- chipolette /5Star/MIT/202008/css
  - https://github.com/Marcisbee/chipolette
  - http://marcisbee.com/chipolette/
  - 单页文档，但根据多个html通过innerHTML实现，使用了css vars
  - It is designed to replace Bootstrap and to be used with CSS variables.
  - Chipolette is a tiny CSS framework/Starter kit.
  - It's a fork from Shoelace and Bootstrap, that fully embraces CSS variables/custom properties.

## flat/metro

- https://github.com/daniruiz/flat-remix-css /202008/css
  - http://drasite.com/flat-remix-css
  - 视觉上，边框线特别明显，轮廓分明
  - CSS library that provides a set of predesigned elements
  - It follows a modern flat design using a colorful palette
- https://github.com/ajusa/lit /202005/css
  - https://ajusa.github.io/lit
  - 单页文档
  - a ridiculously small responsive css framework.
  - preserve everything Skeleton, Milligram, and other micro frameworks have to offer.
- https://github.com/olton/Metro-UI-CSS
  - https://metroui.org.ua/
  - Build responsive projects on the web in Metro Style
  - https://github.com/TalksLab/metro-bootstrap
    - http://talkslab.github.com/metro-bootstrap
    - Simple bootstrap from Twitter with Metro style.
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

- https://github.com/designmodo/Flat-UI
  - https://designmodo.github.io/Flat-UI/
  - Flat UI Free - Design Framework (html/css3/less/js)
  - Flat UI is a beautiful theme for Bootstrap. 
    - We have redesigned many of its components to look flat in every pixel.

## monochrome

- https://github.com/asvvvad1/mono-color
  - https://asvvvad1.github.io/mono-color/
  - /57Star/MIT/202008
  - 提供了dark主题demo
  - CSS-only framework built with responsivity, readability, modularity, and a dual-theme in mind.
- https://github.com/kokushin/mono.css
  - https://kokushin.github.io/mono.css/
  - /8Star/MIT/201707/css
  - Minimal design based on black and white.
- https://github.com/cihankoseoglu/shades
  - A Sass/CSS framework for minimalist websites that use black, white and shades of gray as a design choice

## neomorphism

- https://github.com/ismail9k/neomorphism
  - https://ismail9k.github.io/neomorphism/
  - UI components library in the new neomorphism design style

## hand-drawn

- https://github.com/papercss/papercss /字体变成手写体
  - https://www.getpapercss.com/
  - /3.2kStar/ISC/202011/scss
  - The Less Formal CSS Framework
- https://github.com/fxaeberhard/handdrawn.css
  - http://fxaeberhard.github.io/handdrawn.css/
  - /61Star/CC0-1.0/201606/css
  - Handdrawn.css lets you prototype your web site with a hand drawn look and feel.

- https://github.com/saurabhdaware/text-to-handwriting
  - https://saurabhdaware.github.io/text-to-handwriting/
  - converts text to an image that looks like handwriting

## particles-tracks

- https://github.com/matteobruni/tsparticles
  - https://particles.js.org/
  - TypeScript library for creating particles. Dependency free

- https://github.com/Wufe/react-particles-js
  - https://rpj.bembi.dev/
  - Particles React component, using tsParticles

- https://github.com/tim-soft/react-particles-webgl
  - https://timellenberger.com/particles
  - A 2D/3D particle library built on React, Three.js and WebGL
  - react-particles-webgl was inspired by the popular particles.js library and built with react-three-fiber to offer smooth 60FPS high-count particle fields in both two and three dimensions.

- https://github.com/kennethcachia/shape-shifter
  - http://www.kennethcachia.com/shape-shifter/
  - A canvas experiment in which a set of particles is used to render different shapes based on the user's input.
  - It supports multiple modes: text, countdown, time and icons.
  - 粒子动画示例的效果amazing

- more-particles
  - https://github.com/chainlito/dot-dashboard
    - https://dot-dashboard.vercel.app/
    - 依赖react, redux-saga, react-chartjs
    - dot-dashboard 一个暗黑系的首页示例

# themes-ui-design

- https://github.com/ciucacristi/elementric
  - https://ciucacristi.github.io/elementric/
  - 样式设计基于白底的圆角方形，设计感很强
  - Elementric is a free front-end package of UI element

- https://github.com/arwes/arwes
  - https://arwes.dev/
  - Arwes is a web framework to build user interfaces based on futuristic science fiction designs, animations, and sound effects.
  - The concepts behind are opinionated with influences from Cyberpunk, Cyberprep, and Synthwave, and productions like Star Citizen, Halo, and TRON: Legacy.
  - It tries to inspire advanced space and alien technology.

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

- https://github.com/tylerchilds/cutestrap /1.6kStar
  - http://www.cutestrap.com/features/themes
  - 样式源码基于css，文档是多个html，但默认首页的html可单独使用
  - 提供了dark主题demo，另外的css文档使用了kss生成
  - A strong, independent CSS Framework. Only 2.7KB gzipped.
  - The two constraints for browser support are Custom Properties and CSS Grid.

- https://github.com/elishaterada/feathercss /2Star
  - https://feathercss.makerkits.co/
  - 文档单页，文档基于next，每个组件并排显示明暗两种样式，设计简洁干净
  - FeatherCSS is a Dark Mode ready minimalist CSS Framework with support for RTL and Accessibility
  - It purposefully excludes features like grid layout, media queries, or icons which tends to require per-project customization.
  - It’s Just CSS™ with CSS variables. Bring your own LESS/SaaS/CSS-in-JS solution
  - How Dark Mode works
    - In order to provide maximum flexibility of turning it on, off, or automatically switch based on user display settings, you can toggle `data-theme="dark"` attribute to your markup with a minimal JavaScript code

- https://github.com/jenil/chota
  - https://jenil.github.io/chota/
  - 文档单页，纯html
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
