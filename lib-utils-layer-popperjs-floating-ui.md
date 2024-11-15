---
title: lib-utils-layer-popperjs-floating-ui
tags: [floating-ui, layer, lib, popperjs, utils]
created: 2022-05-22T17:31:46.307Z
modified: 2022-06-04T00:44:40.955Z
---

# lib-utils-layer-popperjs-floating-ui

# guide

- 实现浮层的2个要点
  - 浮层元素 visible
  - 浮层元素 anchored to reference element

- 官方提供了很多示例
  - popover
  - tooltip
  - dialog
  - dropdown-menu
  - context-menu
  - select/macos-select/virtualized-select
  - autocomplete/combobox
  - emoji-picker
  - safe-polygon: 二级菜单支持三角形安全区

- resources
  - [HTMLElement API: popover | Can I use](https://caniuse.com/mdn-api_htmlelement_popover)
# dev-xp
- 在包含popover的组件逻辑中提前return可能会导致问题
  - fewer hooks
# blogs

## [Dialogs and popovers seem similar. How are they different? _202309](https://hidde.blog/dialog-modal-popover-differences/)

- This post goes into the differences between dialogs, popovers, overlays and disclosure widgets. 

- `popover` is available:
  - Chrome (116) and Edge (115)
  - Safari 17
  - Firefox from 114 (behind dom.element.popover.enabled flag)

## [Everything I Know About Positioning Poppers (Tooltips, Popovers, Dropdowns) in UIs by popperjs-author_202004](https://dev.to/atomiks/everything-i-know-about-positioning-poppers-tooltips-popovers-dropdowns-in-uis-3nkl)

Problem 1: Preventing overflow if the popper will be clipped or overflow the main axis of a boundary
Problem 2: Flipping when the popper will be clipped or overflow the alt axis of a boundary
Problem 3: Scrolling containers
Problem 4: offsetParent
Problem 5: Hiding due to different clipping contexts
Problem 6: The arrow
Problem 7: Virtual elements
Problem 8: Size
Problem 9: Browser bugs

# docs
- docs-repeat
  - [useHover#safePolygon | Floating UI](https://floating-ui.com/docs/usehover#safepolygon)
  - [Better Context Menus With Safe Triangles — Smashing Magazine](https://www.smashingmagazine.com/2023/08/better-context-menus-safe-triangles/)

- floating-ui offers two main features:
- Anchor positioning: 
  - Anchor a floating element (such as a tooltip) to another element (such as a button) while simultaneously ensuring it stays in view as best as possible by avoiding collisions. 
  - This feature is available for all platforms.
- User interactions for React:
  - Hooks and components for composing interactions to create accessible floating UI components.

- Floating elements are absolutely positioned, typically anchored to another UI element. 
  - Ensuring a floating element remains anchored next to another element can be challenging, especially in unique layout contexts like scrolling containers.
  - Absolute positioning can also cause problems when the floating element is too close to the edge of the viewport and becomes obscured, also known as a collision. 

- A middleware is a piece of code which runs between the call of `computePosition()` and its eventual return, to modify or provide data to the consumer.

- Middleware behavior is dependent on order. 
  - Each middleware returns new coordinates which middleware later in the array will use. 
  - The `offset()` middleware is one that should be before most other ones, because they should modify their coordinates based on the offset ones.

- Unlike other middleware, the `arrow()` middleware doesn’t modify the main x and y coordinates. 
  - Instead, it provides data for us to use. We can access this piece of information provided via `middlewareData`.

- To keep the tooltip anchored to the button while scrolling or resizing, you’ll want to use the `autoUpdate` utility.

- computePosition
  - returns a Promise that resolves with the coordinates that can be used to apply styles to the floating element.
  - By default, the floating element will be placed at the bottom center of the reference element.
- It runs only once — autoUpdate is used with it to ensure the floating element remains anchored by continually re-running the calculation as necessary.

- 👉🏻 To ensure positioning works smoothly, the dimensions of the floating element should not change before and after being positioned.
- Certain CSS styles must be applied before computePosition() is called
  - position: absolute
  - width: max-content (or a fixed value)
  - top, left
  - These properties prevent the floating element from resizing when it overflows a container, removing layout interference that can cause incorrect measurements.

## usecase

- A tooltip is a floating element that displays information related to an anchor element when it receives keyboard focus or the mouse hovers over it.
  - Tooltips should **not contain interactive content**. Use a Popover instead!

- A popover is an interactive mini-dialog floating element that displays information related to an anchor element when the element is clicked.
  - Focus is managed for non-modal or modal behavior.

- A dialog is a floating element that displays information that **requires immediate attention**, appearing over the page content and **blocking interactions with the page until it is dismissed**.
  - Focus is fully trapped inside the dialog and must be dismissed by the user.

- 💡 Dialog has similar interactions to a popover but with two key differences:
  - It is centered in the viewport, not anchored to any particular reference element.
  - It is modal and renders a backdrop behind the dialog that dims the content behind it, making the rest of the page inaccessible.
# more
