---
title: lib-utils-gesture-use-gesture-dev
tags: [dnd, use-gesture]
created: 2023-07-03T08:54:34.802Z
modified: 2023-07-03T08:55:09.372Z
---

# lib-utils-gesture-use-gesture-dev

# guide
- who is using #use-gesture
  - antd-mobile, react-vant, zarm, nutui-react
  - @react-three/drei
  - gutenberg-components
# examples
- https://github.com/tackboon/react-grid-rearrange /ts
  - Rearrange grid items via drag and drop
  - 依赖use-gesture、react-spring/web

- https://github.com/woofers/react-sheet-slide /ts
  - https://jaxs.onl/react-sheet-slide/
  - A responsive React draggable sheet and dialog component
  - 依赖use-gesture、react-spring/web

- https://github.com/Mattixes/bottomsheet /ts
  - https://bottomsheet.mattixes.com/
  - built on top of @react-spring/web and @use-gesture/react

- https://github.com/marcoromag/react-tiles-dnd /ts
  - https://codesandbox.io/s/react-tiles-dnd-responsive-bd0ly
  - Manage tiles that can be reordered with drag and drop
  - tiles in multiple sizes: each tile can span an arbitrary number of columns and rows of the grid

- https://github.com/xcfox/react-tile-pane /ts
  - https://xcfox.github.io/react-tile-pane/demo/
  - A React tiling pane manager
  - use @use-gesture/react, react-use-measure as peerDependencies

- https://github.com/beamworks/react-csv-importer /ts/依赖少
  - This library combines an uploader + CSV parser + raw file preview + UI for custom user column mapping, all in one.
  - drag-drop UI to remap input columns as needed
  - 1GB+ CSV file size (true streaming support without crashing browser)
  - automatically strip leading BOM character in data
  - Papa Parse for CSV parsing
  - react-dropzone for file upload
  - @use-gesture/react for drag-and-drop

- https://github.com/jotform/dnd-builder /43Star/MIT/202305/js
  - https://www.jotform.com/open-source/dnd-builder/
  - accessible drag and drop page builder with React
  - 依赖use-gesture、fuse.js、react-dnd-cjs、react-quill、recharts
  - 示例很好

- https://github.com/qiuxiang/canvas-tilemap /ts
  - Super smooth 2d tilemap build with canvas2d.

- https://github.com/wobsoriano/svelte-gesture
  - utility for component-tied mouse/touch gestures in Svelte.
# blogs

## [building mobile-friendly UI interfaces](https://use-gesture.netlify.app/docs/extras/)

- `touch-action` css property
  - you don't want the `body` of your page to scroll along with the user manipulating the item horizontally. 
  - Your first instinct might be to prevent the event default action by calling `event.preventDefault()` in your handler. 
  - But there is a simpler, more effective solution, which has to do with a simple CSS property.
  - `touch-action` is a CSS property that sets how an element's region can be manipulated by a touchscreen user.
    - `auto`: 默认值。 Enable browser handling of all panning and zooming gestures.
    - `none`: Disable browser handling of all panning and zooming gestures.
    - By default, panning (scrolling) and pinching gestures are handled exclusively by the browser. 
    - By explicitly specifying which gestures should be handled by the browser, an application can supply its own behavior in pointermove and pointerup listeners for the remaining gestures. 
    - Applications using Touch events disable the browser handling of gestures by calling `preventDefault()`, but should also use `touch-action` to ensure the browser knows the intent of the application before any event listeners have been invoked.
    - When a gesture is started, the browser intersects the `touch-action` values of the touched element and its ancestors, up to the one that implements the gesture (in other words, the first containing scrolling element). 
    - This means that in practice,  `touch-action` is typically applied only to top-level elements which have some custom behavior, without needing to specify touch-action explicitly on any of that element's descendants.
    - After a gesture starts, changes to touch-action will not have any impact on the behavior of the current gesture.

- https://github.com/willmcpo/body-scroll-lock /js
  - When you have a menu overlay on top of your page you generally don't want the body to scroll along with the menu content. Body scroll lock is a javascript library that disable body scroll.
  - Make sure you can't solve your problem scroll problem with touch-action before using this library though.

- https://github.com/d4nyll/lethargy
  - help distinguish between scroll events initiated by the user, and those by inertial scrolling
# faq
- ## What are the differences between using `use[Gesture]` hooks and adding listeners manually?
- Not a lot! 
  - Essentially these `useXXXX` hooks simplify the implementation of the drag and pinch gestures, calculate kinematics values you wouldn't get out of the box from the listeners, and debounce move, scroll and wheel events to let you know when they end.

- ## Why is drag being triggered when I just click on an element?
- This is typically a-feature-not-a-bug situation 🙃 
  - Drag is triggered as soon as you mouse down on your component, which means it will be triggered when you just briefly click on it. 
  - However, there is an option to not trigger the drag handler before a certain delay, using the config option `delay`.

- ## Why can't I properly drag an image or a link?
- Dragging an image or a link might interfere with the browser native drag and drop. 
  - This is why you need to set additional styling on top of `touch-action: none`.
  - Unfortunately, that may not be enough for Firefox because of this issue, so you should also prevent default.
# docs
- @use-gesture is a set of gestures that let you bind mouse and touch events to any node.
- A secondary aspect of @use-gesture is to upgrade gestures with additional kinematics attributes, such as **velocity, distance, delta and more**, that don't come with native browser events.
- @use-gesture also debounces `scroll`,  `wheel` and `move` events, which gives you the capacity to trigger logic when the gesture starts or ends out of the box.

- handle different gestures
  - drag
  - move
  - scroll
  - **wheel**
  - hover
  - **pinch**
  - gesture

- `state` is an object containing all attributes of the gesture, including the original event. 
  - That state is passed to your handler every time the gesture updates. 
- `config` is an object containing options for the gesture.

- Because of the way pointer events work, dragging might cause conflict with scrolling on touch-based devices. 
  - So to signify that your element is draggable and therefore shouldn't trigger the browser scrolling, you need to use the `touch-action` css property.

- The pinch gesture is a bit specific because depending on your device input, it might behave differently. 
  - On touch devices, two pointers (generally your fingers) allow for zooming and rotating.
  - But Macbook trackpads also support pinching and rotating in Safari. To make sure the zooming gesture doesn't interfere with Safari accessibility zoom, you will need to preventDefault

- useGesture allows you to manage different gestures at the same time
- useGesture hook allows drag, wheel, scroll, pinch and move gestures to have two additional handlers that let you perform actions when they start or end. 
  - Note that end event handlers for `wheel`,  `scroll` and `move` are **debounced** because of the way these events work in the DOM.

- The `useGesture` hook conveniently offers all gestures out of the box. This comes at the expense of one or two kb of extra gzipped javascript.

- 
- 
- 
- 
- 

# more
