---
title: web-ui-comp-design-pgd-features
tags: ['@pgd', components, design-tokens]
created: 2020-10-02T11:42:34.698Z
modified: 2021-04-11T17:42:26.580Z
---

# web-ui-comp-design-pgd-features

# ux-design-effects
- codeblock的light主题设计，可参考 https://www.joshwcomeau.com/
# prospect-garden-design-in-action
- features
  - framework agnostic kept in mind [WIP]
  - themeable components ~~following the Theme Specification(maintain consistency with constraint-based design)~~
  - fully customizable, built on top of headless react-aria
  - choices
    - playful with pluggable extensions
    - ~~built for~~ better datable and documentation experience
      - 参考文档编辑器网站的设计，很多页面背景是灰蓝色，文档背景是纯白色

- packages
  - @pgd/design-tokens: across platform kept in mind
  - @pgd/css: themeable
  - @pgd/components-react: headless
  - @pgd/components-react-lab: experimental latest react
  - @pgd/components-react-ina11y: with smaller bundle size
  - @pgd/web-components: lit-html/preact-custom-element
  - @pgd/components-webgl: r3f/babylonjs
  - more
    - @pgd/design-system-site

- css
  - 主题样式实现一套css，再实现一套css in js
    - github-primer,adobe-spectrum
  - css-global-config
    - theme, size, dir/left-right

- themeable 设计样式时theming可参考
  - dark/darcula, material, bootstrap, flat/metro, monochrome, neumorphism, hand-drawn(papercss), glass-ui
    - 甚至所有的theme主题样式都可以在bootstrap的基础上修改
  - 基于粒子/particles的设计，或偏向于某一种dot dash的设计
    - 特别适合表达地理位置，常用在[logo](https://github.com/maplibre/maplibre-gl-js/issues/65)和icon
  - 设计logo可参考抽象图形、印象派风格

- 公共api/variant
  - borderless
    - 部分组件提供无边框的版本，如modal
  - dark mode形式的组件
  - disable mode形式的组件，组件变灰色，常作为背景
  - scalable，如下拉列表列表选项变多时会变modal
  - auto-responsive-animation: 屏幕由窄变宽时组件预览图更新动画

- logo: green plum
- design-system-tokens
  - text: sans serif(衬线体多用于印刷)
  - color: mineral-ui-color-palette, primary-mediumseagreen
  - bezel-less
- interaction
  - hover-color
  - click-ripple
  - loader-flower
- animation
  - flip
  - misc
    - rotate
    - unfold
    - point movement
- shape
  - point/polygon-shape-based
  - https://medium.com/google-design/you-need-a-shape-system-8d2aa9016817
# opinionated
- 技术选型
  - all in js
- ui设计
  - portal的target容器默认是组件自身或document.body
  - Inline Editing is a very common feature in a table, 
    - but it's highly coupled with specific ui libraries, so it won't be a part of BaseTable itself.
- 交互设计
  - should we show a indeterminate for the header's checkbox if partial is selected
  - should we select all the children if the parent is selected
  - how to sync the staled keys if those rows are removed
- 参考现有ui解决方案：dom密集操作、状态数据频繁更新
- 流行typescript库很多都用的class，所以是否用class可参考现有成熟方案的选择
- 通用组件库
  - 组件库结构包括的通用的design tokens，通用的core，core可用来共享locale、theme、工具方法、类型定义
    - 具体框架会实现各自组件的生命周期、状态管理、样式交互、事件处理，这也是组件互操作的因素
    - 最好支持切换不同css框架提供的design tokens
    - 实现方式1：vanilla js组件加上胶水层可移植到其他库
    - 实现方式2：各框架的组件单独实现
    - 实现方式3：web components，或类似api的库
# 现有组件库参考
- carbon-components: a collection of reusable HTML and SCSS partials
- carbon-components-react: components implemented using React.
  - built React first. We also support core parts of the system in vanilla JS, Angular, and Vue. 
- 只共用样式，组件分开实现，而不是简单wrapper，因为不同框架解决状态更新、数据同步、事件等的方案不同
- 选用已有框架的重要原因是借鉴处理状态、事件、路由等问题较成熟的解决方案
- 最新的web components和stencil再等等看，思路是framework as compiler
  - web components本身使用浏览器标准的runtime，特别适合替代vue/react的runtime
  - web components难以替代其他框架，因为这些框架的目标不止浏览器环境，还支持native、ssr
  - 在其他框架中使用w-c组件，无需w-c框架层的依赖，这是通用组件重要的优势
  - 但在w-c中使用其他框架组件，则需组件源码加上框架runtime的依赖，并且每次导入组件都会导入一次框架层的依赖
- stencil vs svelte
  - stencil编译到w-c，svelte还能编译到framework-less的纯js
  - stencil组件基于vdom，svelte组件会编译到js代码
  - stencil的状态管理更类似react
  - stencil的dom模版使用jsx，svelte使用的是自定义指令
  - svelte暂不支持ts
  - stencil的css基于shadow dom，且写在单读文件，svelte的css写在style块
- 参考现有ui解决方案：dom密集操作、状态数据频繁更新
- 流行typescript库很多都用的class，所以是否用class可参考现有成熟方案的选择
- ref
  - https://github.com/jaywcjlove/awesome-uikit
  - [Compiler like Svelte.js or Stencil.js](https://github.com/vuejs/vue/issues/9011)
# dev-log
- design-tokens支持theming
  - 最终的用法是，用户修改theme.js/json，然后触发切换样式
  - 样式配置对象 > css vars形式的样式表 > 通过style属性设置/动态创建class样式表/直接修改cssom
