---
title: lib-ui-bootstrap-dev
tags: [bootstrap, lib]
created: '2020-10-19T09:04:03.787Z'
modified: '2020-12-08T13:33:11.249Z'
---

# lib-ui-bootstrap-dev

## bootstrap5

### components-catalog

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

### Bootstrap Optional JavaScript plugins

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
  - So if you want to listen to Bootstrap’s events, you’ll have to use the jQuery methods ( `.on` , `.one` ) instead of `addEventListener` .
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

## bootstrap4

## bootstrap-ecosystem

- https://github.com/easysoft/zui
  - /2.4kStar/MIT/202010/js/less
  - 一个基于 Bootstrap 深度定制开源前端实践方案，帮助你快速构建现代跨屏应用
- https://github.com/wenzhixin/bootstrap-table
  - An extended table to integration with some of the most widely used CSS frameworks.
