---
title: toc-lib-components-theming
tags: [theming]
created: '2020-10-23T17:21:21.861Z'
modified: '2020-10-25T09:56:46.611Z'
---

# toc-lib-components-theming

## guide

- 切换theme的实现方式与具体技术栈紧密相关
  - react组件需传入新theme对象或新样式
  - 对于css modules的实现
  - 普通组件要切换class
  - 参考主流组件库的实现

## popular

- https://github.com/denali-design/denali-css
  - Themeable CSS framework of Denali Ui components

## react-theming

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

## theming-with-css-variables

- https://github.com/intuit/postcss-themed
  - /26Star/MIT/202010
  - A PostCSS plugin for generating themes.

## more-themeable-examples

- react
  - https://github.com/markdalgleish/react-themeable
  - https://github.com/javivelasco/react-css-themr
- https://github.com/themeable-ui/themeable-css
- https://github.com/FrontendRangers/platoon
  - A themeable UI kit for React & Svelte
