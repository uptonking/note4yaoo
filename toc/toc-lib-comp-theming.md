---
title: toc-lib-comp-theming
tags: [css-vars, theming]
created: '2020-10-23T17:21:21.861Z'
modified: '2020-11-13T07:31:38.730Z'
---

# toc-lib-comp-theming-css-vars

# guide

- 切换theme的实现方式与具体技术栈紧密相关
  - react组件需传入新theme对象或新样式
  - 对于css modules的实现
  - 普通组件要切换class
  - 参考主流组件库的实现

- 设计样式时theming可参考
  - dark, material, bootstrap, flat/metro, neumorphism, monochrome, hand-drawn(papercss), glass-ui

# popular

- https://github.com/denali-design/denali-css
  - Themeable CSS framework of Denali Ui components
  - theming基于scss变量
- https://github.com/Marcisbee/chipolette
  - http://marcisbee.com/chipolette/
  - It is designed to replace Bootstrap and to be used with CSS variables.
  - Chipolette is a tiny CSS framework/Starter kit.
  - It's a fork from Shoelace and Bootstrap, that fully embraces CSS variables/custom properties.
  - It's written in LESS, because of nesting and other neat features
  - It is designed to replace Bootstrap and to be used with CSS variables.

# react-theming

- https://github.com/seek-oss/braid-design-system
  - Themeable design system for the SEEK Group
- https://github.com/CAAPIM/themer
  - /1Star/MIT/201704/js
  - Framework agnostic utility to make generic JavaScript components themeable and extensible.
  - This library supports all class-based styling mechanisms, for example: Global CSS, CSS Modules, JSS, CSJS, Aphrodite
- https://github.com/bumbag/bumbag-ui
  - Build accessible & themeable React applications with your Bumbag
  - https://bumbag.style/theming
  - theme基于@emotion/styled实现
- https://github.com/trendmicro-frontend/styled-ui
  - A themeable UI component library built with Emotion and Styled System
- https://github.com/flipace/react-themeit
  - theme your components using css modules and js style objects thanks to aphrodite.

# theming-tools

- https://github.com/intuit/postcss-themed
  - /26Star/MIT/202010
  - A PostCSS plugin for generating themes.
- https://github.com/salesforce/themify /201908
  - Themify is a PostCSS plugin that generates your theme during the build phase
  - themify will replace your CSS colors with CSS variables, and also take care to provide a fallback for unsupported browsers (such as IE11).
- https://github.com/fwrlines/swatch
  - https://swatch.dev/docs/introduction
  - modern theming library based on CSS4 variables and the [setter/getter pattern](https://swatch.dev/docs/guides-setters-getters).
  - 规定了读写css vars的选择器命名规则，x-名称 用来写，名称-x 用来读
- https://github.com/adobe/leonardo
  - https://leonardocolor.io/
  - Generate colors based on a desired contrast ratio

- https://github.com/siddharthkp/theme.css
  - Experimental: convert system-ui themes to css variables
    - 将theme object的各属性，转换成css vars，内层属性名使用-连接
  - [theme-ui已经自己实现了@theme-ui/custom-properties](https://github.com/system-ui/theme-ui/blob/develop/packages/custom-properties/test/__snapshots__/test.js.snap)

# theming-with-css-vars

- https://github.com/shoelace-style/shoelace
  - A forward-thinking library of web components.
  - The default theme is included as part of shoelace.css and should always be loaded first, even if you want to use another theme exclusively. 
    - The default theme contains important base tokens and utilities that many components rely on.
    - You can do this with the `<sl-theme>` component. 
    - Only the elements inside of `<sl-theme>` will inherit the theme's styles.
  - 没有组件级的css vars
  - dark主题提供了一套全局变量，还提供了各组件在该主题下的特殊样式
  - 使用了`::part`伪元素选择shadow tree中含有part属性的元素
- https://github.com/bruegmann/bluce
  - Make Bootstrap customizable with CSS variables only
  - You can already customize Bootstrap. But only at build time.
  - With Bluce you can use CSS Variables to change color settings.

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
- https://github.com/spymastermatt/thunderbird-monterail
  - themes for thunderbird inspired by a Monterail blog post
  - 5个css文件

- https://github.com/ibrahima92/dark_light_mode
  - https://codepen.io/ibrahima92/full/KKPMoqG
  - Dark-Light mode switcher with CSS variables
  - theming基于`html[data-theme='dark']`，无依赖
- https://github.com/techiediaries/dynamic-themes-css-variables
  - Demo example of dynamic theming with CSS variables and JavaScript
- https://github.com/Artik-Man/material-theme-creator
  - Converting Angular Material themes to CSS Custom Properties (Variables)
- https://github.com/akrck02/Akstrap-The_modern_CSS_Framework
  - Modular, variable based CSS framework.
- https://github.com/psbhagat/dark-mode-toggle
  - https://codepen.io/priyanka-bhagat/pen/ExgQgJZ
  - A simple dark mode toggle implemented using CSS variables.

# more-themeable-examples

- react
  - https://github.com/markdalgleish/react-themeable
  - https://github.com/javivelasco/react-css-themr

- https://github.com/FrontendRangers/platoon
  - A themeable UI kit for React & Svelte

- https://github.com/ash-rocks/ash-css
  - http://ashcss.rocks/
  - 基于less变量实现
  - Modern CSS-only semantic framework with a built-in dark mode. 
  - No JavaScript required!
