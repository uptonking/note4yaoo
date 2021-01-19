---
title: lib-ui-bootstrap-dev
tags: [bootstrap, lib]
created: '2020-10-19T09:04:03.787Z'
modified: '2020-12-08T13:33:11.249Z'
---

# lib-ui-bootstrap-dev

# bootstrap 5

## [Theming](https://getbootstrap.com/docs/5.0/customize/css-variables/)

- Bootstrap 5 includes around two dozen CSS custom properties (variables) in its compiled CSS, with dozens more on the way for improved customization on a per-component basis.
  - These provide easy access to commonly used values like our theme colors, breakpoints, and primary font stacks when working in your browser’s inspector, a code sandbox, or general prototyping.
  - All our custom properties are prefixed with `bs-` to avoid conflicts with third party CSS.
- Root variables
  - Here are the variables we include (note that the `:root` is required) that can be accessed anywhere Bootstrap’s CSS is loaded. 
  - They’re located in our `_root.scss` file and included in our compiled dist files.
- Component variables
  - We’re also beginning to make use of custom properties as local variables for various components. 
    - This way we can reduce our compiled CSS, ensure styles aren’t inherited in places like nested [tables](https://getbootstrap.com/docs/5.0/content/tables/#how-do-the-variants-and-accented-tables-work), 
    - and allow some basic restyling and extending of Bootstrap components after Sass compilation.
  - We’re also using CSS variables across our grids—primarily for gutters—with more component usage coming in the future.
- CSS variables offer similar flexibility to Sass’s variables, but without the need for compilation before being served to the browser.

## components-catalog

- Buttons
  - Close button
- Button group
- Breadcrumb
- Layout
  - Containers
  - Grid
  - Columns
  - Gutters
  - Breakpoints、Z-index、Utilities
- NavTab
- Navbar
- Collapse
- Pagination
- Forms
  - Form control: input, textarea
  - Select
  - Checks & radios
  - File
  - Range
  - Input group
  - Layout
  - Validation
- Dropdowns
- Card
- Badge
- List group
- Tables
- Carousel
- Alerts
- Modal
- Popovers
- Tooltips
- Toasts
- Progress
- Scrollspy
- Spinners

## tables

- Due to the widespread use of `<table>` elements across third-party widgets like calendars and date pickers, Bootstrap’s tables are opt-in. 
  - Add the base class `.table` to any `<table>`, then extend with our optional modifier classes or custom styles. 
  - All table styles are not inherited in Bootstrap, meaning any nested tables can be styled independent from the parent.

- **How do the variants and accented tables work?**
- For the accented tables (striped rows, hoverable rows, and active tables), we used some techniques to make these effects work for all our table variants:
  - We start by setting the background of a table cell with the `--bs-table-bg` custom property. 
    - All table variants then set that custom property to colorize the table cells. 
    - This way, we don’t get into trouble if semi-transparent colors are used as table backgrounds.
  - Then we add a gradient on the table cells with `background-image: linear-gradient(var(--bs-table-accent-bg), var(--bs-table-accent-bg));` to layer on top of any specified `background-color`. 
    - Since `--bs-table-accent-bg` is transparent by default, we have an invisible transparent linear gradient by default.
  - When either `.table-striped, .table-hover or .table-active` classes are added, the `--bs-table-accent-bg` is set to a semitransparent color to colorize the background.
  - For each table variant, we generate a `--bs-table-accent-bg` color with the highest contrast depending on that color. 
    - For example, the accent color for `.table-primary` is darker while `.table-dark` has a lighter accent color.
  - Text and border colors are generated the same way, and their colors are inherited by default.

## issues

- ### [WIP: More CSS vars](https://github.com/twbs/bootstrap/pull/32424)
- This PR adds additional CSS custom properties to `:root` in the hopes of improving ease of customization and extensibility.
  - I'm creating CSS vars for some situations and replacing their Sass variables with interpolated CSS vars (e.g., instead of `$body-bg` it's `var(--bs-body-bg)` which has a computed value of `$body-bg`).
- I'm not in favor of declaring those on `:root` since it increases file size quite a lot and is not what allows customization: using `var()` in appropriate places is what allows it.
  - I think a component-basis would be a better approach for this.
  - Moreover there's no need to rush on this, since we should be able to instantiate more and more custom properties without breaking anything, thanks to `var()` fallback mechanism. 
  - IMHO that'll be a long-term project.

## Bootstrap Optional JavaScript plugins

- We provide a version of Bootstrap built as ESM (bootstrap.esm.js and bootstrap.esm.min.js) which allows you to use Bootstrap as a module in your browser
  - some of our plugins, namely Dropdown, Tooltip and Popover plugins, cannot be used in a `<script>` tag with `module` type because they depend on Popper.js. 
- Bootstrap 5 is designed to be used without jQuery, but it’s still possible to use our components with jQuery. 
  - If Bootstrap detects `jQuery` in the `window` object it’ll add all of our components in jQuery’s plugin system; 
  - this means you’ll be able to do `$('[data-toggle="tooltip"]').tooltip()` to enable tooltips. 
  - The same goes for our other components.
- Nearly all Bootstrap plugins can be enabled and configured through HTML alone with `data` attributes 
  - (our preferred way of using JavaScript functionality). 
  - Be sure to only use one set of data attributes on a single element 
  - (e.g., you cannot trigger a tooltip and modal from the same button.)
  - Currently to query DOM elements we use the native methods `querySelector` and `querySelectorAll` for performance reasons
- Bootstrap provides custom events for most plugins' unique actions. 
  - Generally, these come in an infinitive and past participle form
  - where the infinitive (ex. `show` ) is triggered at the start of an event, 
  - and its past participle form (ex. `shown` ) is triggered on the completion of an action.
- Bootstrap will detect jQuery if `jQuery` is present in the `window` object and there is no `data-no-jquery` attribute set on `<body>` . 
  - If `jQuery` is found, Bootstrap will emit events thanks to jQuery’s event system. 
  - So if you want to listen to Bootstrap’s events, you’ll have to use the jQuery methods ( `.on/.one` ) instead of `addEventListener` .
- All constructors accept an optional options object or nothing (which initiates a plugin with its default behavior)
- If you’d like to get a particular plugin instance, each plugin exposes a `getInstance` method. 
  - In order to retrieve it directly from an element, do this: `bootstrap.Popover.getInstance(myPopoverEl)` .
- All programmatic API methods are asynchronous and return to the caller once the transition is started but before it ends.
  - In order to execute an action once the transition is complete, you can listen to the corresponding event.
  - In addition, a method call on a transitioning component will be ignored.
  - 方法执行异步的，在一个方法触发后且正在执行时，若再次调用此方法，则再次调用方法的语句会不执行，会被忽略掉
- Bootstrap’s plugins don’t fall back particularly gracefully when JavaScript is disabled. 
  - If you care about the user experience in this case, use `<noscript>` to explain the situation (and how to re-enable JavaScript) to your users, and/or add your own custom fallbacks.
- Bootstrap’s side project RFS is a unit resizing engine which was initially developed to resize font sizes. 
  - Nowadays RFS is capable of rescaling most CSS properties with unit values like margin, padding, border-radius, or even box-shadow.
  - The mechanism automatically calculates the appropriate values based on the dimensions of the browser viewport. 
  - It will be compiled into `calc()` functions with a mix of `rem` and viewport units to enable the responsive scaling behavior.
- Bootstrap’s grid system uses a series of containers, rows, and columns to layout and align content. 
  - It’s built with flexbox and is fully responsive.
- Columns build on the grid’s flexbox architecture. 
  - Flexbox means we have options for changing individual columns and modifying groups of columns at the row level. 
  - You choose how columns grow, shrink, or otherwise change.
- When building grid layouts, all content goes in columns. 
  - The hierarchy of Bootstrap’s grid goes from container to row to column to your content. 
- While not a part of Bootstrap’s grid system, z-indexes play an important part in how our components overlay and interact with one another.
  - We utilize a default ` z-index` scale in Bootstrap that’s been designed to properly layer navigation, tooltips and popovers, modals, and more.
  - We need a standard set of these across our layered components—tooltips, popovers, navbars, dropdowns, modals—so we can be reasonably consistent in the behaviors.
  - We don’t encourage customization of these individual values; should you change one, you likely need to change them all.

``` SCSS
$zindex-dropdown:                   1000;
$zindex-sticky:                     1020;
$zindex-fixed:                      1030;
$zindex-modal-backdrop:             1040;
$zindex-modal:                      1050;
$zindex-popover:                    1060;
$zindex-tooltip:                    1070;
```

- To handle overlapping borders within components (e.g., buttons and inputs in input groups), 
  - we use low single digit `z-index` values of 1, 2, and 3 for default, hover, and active states. 
  - On hover/focus/active, we bring a particular element to the forefront with a higher `z-index` value to show their border over the sibling elements.

# bootstrap 4

## [Theming](https://getbootstrap.com/docs/4.5/getting-started/theming/)

- In Bootstrap 3, theming was largely driven by variable overrides in LESS, custom CSS, and a separate theme stylesheet that we included in our dist files. 
  - With some effort, one could completely redesign the look of Bootstrap 3 without touching the core files. 
  - Bootstrap 4 provides a familiar, but slightly different approach.
- Now, theming is accomplished by Sass variables, Sass maps, and custom CSS. 
  - There’s no more dedicated theme stylesheet; 
  - instead, you can enable the built-in theme to add gradients, shadows, and more.
- Utilize our source Sass files to take advantage of variables, maps, mixins, and more.
- Every Sass variable in Bootstrap 4 includes the `!default` flag allowing you to override the variable’s default value in your own Sass without modifying Bootstrap’s source code. 
- Many of Bootstrap’s components and utilities are built with `@each` loops that iterate over a Sass map. 
  - This is especially helpful for generating variants of a component by our `$theme-colors` and creating responsive variants for each breakpoint. 
  - As you customize these Sass maps and recompile, you’ll automatically see your changes reflected in these loops.

- Bootstrap 4 includes around two dozen CSS custom properties (variables) in its compiled CSS. 
  - These provide easy access to commonly used values like our theme colors, breakpoints, and primary font stacks when working in your browser’s Inspector, a code sandbox, or general prototyping.
  - CSS variables offer similar flexibility to Sass’s variables, but without the need for compilation before being served to the browser

# bootstrap-ecosystem

- https://github.com/easysoft/zui
  - /2.4kStar/MIT/202010/js/less
  - 一个基于Bootstrap深度定制开源前端实践方案，帮助你快速构建现代跨屏应用
- https://github.com/wenzhixin/bootstrap-table
  - An extended table to integration with some of the most widely used CSS frameworks.

# blog

## [Bootstrap源码分析系列之整体架构 基于v3](https://www.cnblogs.com/jesse131/p/5966145.html)

## [bootstrap4源码阅读体会](http://zhenhua-lee.github.io/css/bootstrap.html)

- 移动优先
  - 相对单位: %、rem的大量使用
  - grid系统: grid系统对xs、sm、md、lg、xl进行了响应式设计，通过media query做到适配不同设备
  - 支持flexbox: mobile应该很快就可以使用flexbox
- 代码结构
  - 从less到saas
    - 通过sass预处理器，可以根据功能将css模块化
    - 复用: 变量、mixin、function等技术，可以方便地进行代码复用
    - 简洁: 支持each、if等语法，动态输出内容，例如繁琐的grid系统，是通过少量的sass代码做到的
  - 根据代码的层次，sass的源码分为如下几部分:
    - 基本支撑: 包括变量定义、大量的mixin文件，支持覆盖和定制
    - 全局部分: normalize.scss用于覆盖各种浏览器的默认行为，保证起始样式的一致性
    - 基础样式部分: 包含了reboot、typography、images、code、table、forms、buttons等，主要是一些常用的基础html元素
    - grid部分: 选择性支持flexbox，默认情况下是关闭的，只要将$enable-flex=true就可以使用flexbox完成页面的栅格布局
    - 组件部分: 包含大量常用的基础组件，有些需要添加jQuery plugin
    - 工具类部分: 常用的简单样式，例如间距、文本对齐、字体加粗等
- Grid
  - Grid用于页面的整体布局，同时css3也在起草grid布局模块。
  - bootstrap4提供了一个单独的文件(bootstrap-grid.scss)来实现栅格系统
  - 默认情况下是12栅格
  - 栅格可以嵌套使用
  - 支持5种尺寸下的响应式样式，5个尺寸可以组合使用，适配不同终端下终端
  - 支持使用flexbox
- flex
  - 通过$enable-flex=true来启动flexbox
  - 可伸缩性: 通过flex来实现空间的伸缩，在响应式设计中更加灵活(无需关注margin、padding、border等)
  - 顺序定制: flexbox的一大亮点，通过order指定元素的显示顺序
  - 轻松对齐: 通过jsutify-content、align-items方便实现元素对齐
  - 提供了大量的常用组件
    - 无需js配合: 大多数组件
    - 需js配合: Modal、Tooltips、Popovers、Carousels
  - v4新增组件：Card

# ref
