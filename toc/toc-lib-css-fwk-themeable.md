---
title: toc-lib-css-fwk-themeable
tags: [css-vars, theming, toc]
created: 2020-10-23T17:21:21.861Z
modified: 2023-02-26T18:25:45.484Z
---

# toc-lib-css-fwk-themeable

# guide

- 切换theme的实现方式与具体技术栈紧密相关
  - react组件需传入新theme对象或新样式
  - 对于css modules的实现
  - 普通组件要切换class
  - 参考主流组件库的实现
# popular
- https://github.com/denali-design/denali-css
  - https://denali.design/
  - https://denali-design.github.io/denali-css
  - Themeable CSS framework of Denali Ui components
  - theming基于scss变量
  - 官方文档示例做得好，但实际使用一般

- https://github.com/Marcisbee/chipolette /202107/less/inactive
  - http://marcisbee.com/chipolette/
  - It is designed to replace Bootstrap and to be used with CSS variables.
  - Chipolette is a tiny CSS framework/Starter kit.
  - 🍴 It's a fork from Shoelace and Bootstrap, that fully embraces CSS variables/custom properties.
  - It's written in LESS, because of nesting and other neat features

## switch-themes

- primitive/skeleton-css  /760Star/MIT/202010/scss/NoDeps
  - https://github.com/taniarascia/primitive
  - https://taniarascia.github.io/primitive/
  - https://taniarascia.github.io/primitive/test.html
  - 完全基于sass，提供了基础页面模版
  - 提供了通过改变link的href属性值来切换theming的示例
  - A front-end design toolkit built with Sass for developing responsive web apps.
  - [Skeleton CSS](http://getskeleton.com/), the original inspiration
  - 实现细节
    - 使用了normalize.css和单独的reset.css，scaffolding.scss重置了大多数内置元素的样式
    - 测试页面link标签默认href为空字符串，即默认不加载css，但传入undefined不会变为空
    - 测试页面只有3处使用class设置了样式名，只用了`.small-container`和`.radio`两个类名

- https://github.com/alexandersandberg/theme-switcher
  - https://alexandersandberg.github.io/theme-switcher/unlimited.html
  - A website theme switcher using CSS only
  - 基于css vars实现，使用:checked伪类修改css vars的值

- https://github.com/kemar/html-elements
  - https://kemar.github.io/html-elements/
  - 通过下拉列表选择主题名
  - This repo contains an HTML page with all HTML5 elements and a style switcher (like it's 2001) for previewing various CSS frameworks.

- https://github.com/dohliam/dropin-minimal-css
  - https://dohliam.github.io/dropin-minimal-css
  - This is a quick drop-in CSS switcher to allow for previewing some of the many minimal CSS-only frameworks that are available.

- https://github.com/Artik-Man/material-theme-creator
  - https://artik-man.github.io/material-theme-creator-demo-page/
  - Converting Angular Material themes to CSS Custom Properties (Variables)
  - 提供了创建theme以及切换theme的示例，但依赖angular

- https://github.com/terence55/themes-switch
  - Toolset for switch multiple themes in application based on webpack
  - Multiple themes supported via custom variables.
  - Generating themes via webpack.

- https://github.com/fiatjaf/classless
  - https://classless.alhur.es/
  - The same HTML, multiple CSS themes.
  - 示例页面的主题名称非常小众，各个样式很不美观
# dark-mode
- https://github.com/ash-rocks/ash-css
  - http://ashcss.rocks/
  - 基于less变量实现
  - Modern CSS-only semantic framework with a built-in dark mode. 
  - No JavaScript required!

- https://github.com/sandoche/Darkmode.js
  - https://darkmodejs.learn.uno/
  - This library uses the CSS mix-blend-mode to bring Dark Mode to any of your websites
- https://github.com/ColinEspinas/darken
  - https://colinespinas.github.io/darken/
  - A lightweight and cross-browser library that allows you to easily manage your dark mode
  - Written in plain vanilla javascript
- https://github.com/nickdeny/darkmode-js
  - https://nickdeny.github.io/darkmode-js/
  - auto detect user's time and switch theme to darkside.
  - Pure Javascript, without any plugins and jQuery
- https://github.com/coliff/dark-mode-switch
  - https://coliff.github.io/dark-mode-switch/index.html
  - Add a dark-mode theme toggle with a Bootstrap Custom Switch.
  - Turning dark mode on will add `data-theme="dark"` to the `body` tag

- https://github.com/donavon/use-dark-mode
  - A custom React Hook to help you implement a "dark mode" component.

 

- https://github.com/taniarascia/new-moon
  - New Moon is the optimized dark theme for web development. 
  - New Moon is available for: vscode, chrome, sublime
- https://github.com/liangjingkanji/DrakeTyporaTheme
  - JetBrains Darcula theme of Typora theme
- https://github.com/mjacobsen4DFM/slack-darcula-css
  - Dark theme for Slack
- https://github.com/LucaScorpion/prismjs-darcula-theme
  - PrismJS Darcula syntax highlighting theme based on the JetBrains IDEs
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
# theming-with-css-vars
- https://github.com/shoelace-style/shoelace
  - A forward-thinking library of web components.
  - The default theme is included as part of shoelace.css and should always be loaded first, even if you want to use another theme exclusively. 
    - The default theme contains important base tokens and utilities that many components rely on.
    - You can do this with the `<sl-theme>` component. 
    - Only the elements inside of `<sl-theme>` will inherit the theme's styles.
  - 没有组件级的css vars
  - dark主题提供了一套全局变量，还提供了各组件在该主题下的特殊样式
  - 使用了 `::part` 伪元素选择器，选择shadow tree中含有part属性的元素
  - [part | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/part) global attribute contains a space-separated list of the part names of the element. Part names allows CSS to select and style specific elements in a shadow tree via the `::part` pseudo-element.
- https://github.com/bruegmann/bluce
  - Make Bootstrap customizable with CSS variables only
  - You can already customize Bootstrap. But only at build time.
  - With Bluce you can use CSS Variables to change color settings.
- https://github.com/spymastermatt/thunderbird-monterail
  - themes for thunderbird inspired by a Monterail blog post
  - 5个css文件
- https://github.com/ibrahima92/dark_light_mode
  - https://codepen.io/ibrahima92/full/KKPMoqG
  - Dark-Light mode switcher with CSS variables
  - theming基于 `html[data-theme='dark']` ，无依赖
- https://github.com/techiediaries/dynamic-themes-css-variables
  - Demo example of dynamic theming with CSS variables and JavaScript
- https://github.com/Artik-Man/material-theme-creator
  - https://artik-man.github.io/material-theme-creator-demo-page/
  - Converting Angular Material themes to CSS Custom Properties (Variables)
- https://github.com/akrck02/Akstrap-The_modern_CSS_Framework
  - Modular, variable based CSS framework.
- https://github.com/psbhagat/dark-mode-toggle
  - https://codepen.io/priyanka-bhagat/pen/ExgQgJZ
  - A simple dark mode toggle implemented using CSS variables.
# theming-tools
- https://github.com/intuit/postcss-themed
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
# more-themeable-examples
- react
  - https://github.com/markdalgleish/react-themeable
  - https://github.com/javivelasco/react-css-themr

- https://github.com/FrontendRangers/platoon
  - A themeable UI kit for React & Svelte
