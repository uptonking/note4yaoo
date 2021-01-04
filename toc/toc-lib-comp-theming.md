---
title: toc-lib-comp-theming
tags: [theming]
created: '2020-10-23T17:21:21.861Z'
modified: '2020-11-13T07:31:38.730Z'
---

# toc-lib-comp-theming

# guide

- 切换theme的实现方式与具体技术栈紧密相关
  - react组件需传入新theme对象或新样式
  - 对于css modules的实现
  - 普通组件要切换class
  - 参考主流组件库的实现

# popular

- https://github.com/denali-design/denali-css
  - Themeable CSS framework of Denali Ui components

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
  - modern theming library based on CSS4 variables and the setter/getter pattern.
  - 规定了读写css vars的选择器命名规则，x-名称 用来写，名称-x 用来读
- https://github.com/adobe/leonardo
  - https://leonardocolor.io/
  - Generate colors based on a desired contrast ratio
- https://github.com/siddharthkp/theme.css
  - Experimental: convert system-ui themes to css variables
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
- https://github.com/halfmoonui/halfmoon
  - 未模块化，一个css文件一万多行
  - Front-end framework with a built-in dark mode and full customizability using CSS variables
  - Halfmoon comes with a built-in, toggleable dark mode
  - The framework is built entirely using CSS variables 
    - There are close to 1,500 CSS variables, which means that almost everything can be customized by overriding a property
  - Great for building dashboards and tools
  - Optional JS library—Many of the components found in Halfmoon are built to work without JavaScript. 
    - However, the framework still comes with a powerful JavaScript library with no extra dependencies, such as jQuery.
  - The class names should be instantly familiar to anyone who has used Bootstrap.
- https://github.com/spymastermatt/thunderbird-monterail
  - themes for thunderbird inspired by a Monterail blog post
  - 5个css文件

# more-themeable-examples

- react
  - https://github.com/markdalgleish/react-themeable
  - https://github.com/javivelasco/react-css-themr
- https://github.com/themeable-ui/themeable-css
- https://github.com/FrontendRangers/platoon
  - A themeable UI kit for React & Svelte
- https://github.com/KyleAMathews/typography.js
  - http://kyleamathews.github.io/typography.js/
  - /3.5kStar/MIT/202008/js
  - Typography is a complex system of interrelated styles. 100s of style declarations on dozens of elements must be in harmonious order. Trying one design change can mean making dozens of tedious recalculations and CSS value changes. Creating new Typography themes with CSS feels hard.
  - You can provide configuration to the Typography.js JS api and it uses its Typography engine to generate CSS for block and inline elements.
  - Typography.js themes are simple Javascript objects. As such they're easy to share across projects
