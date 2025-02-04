---
title: lib-utils-gesture-use-gesture-docs
tags: [docs, use-gesture]
created: 2023-07-03T08:55:15.446Z
modified: 2023-07-03T08:55:25.659Z
---

# lib-utils-gesture-use-gesture-docs

# guide

# changelog
- [v10_20210928](https://github.com/pmndrs/use-gesture/tags?after=%40use-gesture%2Fvanilla%4010.1.0)
  - `@use-gesture/react` replaces `react-use-gesture` completely and relies on a universal core,  `@use-gesture/core` that also powers `@use-gesture/vanilla`.
  - The API is 95% the same as before, the main one being the `domTarget` option being renamed to `target`.
  - [breaking changes for v10](https://github.com/pmndrs/use-gesture/blob/main/packages/react/CHANGELOG.md#1000)
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
    - By explicitly specifying which gestures should be handled by the browser, an application can supply its own behavior in `pointermove` and `pointerup` listeners for the remaining gestures. 
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
  - Note that end event handlers for `wheel`/`scroll` and `move` are **debounced** because of the way these events work in the DOM.

- The `useGesture` hook conveniently offers all gestures out of the box. This comes at the expense of one or two kb of extra gzipped javascript.

## config/options

- `threshold` (per axis)
  - By default, your gesture handler will be triggered as soon as an event is fired
  - `threshold` is the minimum displacement the gesture movement needs to travel before your handler is fired.
  - threshold works per axis: if the gesture exceeds the threshold value horizontally, you will get updates for horizontal displacement, but vertical threshold will have to be reached before vertical displacement is registered
  - If you still want your handler to be triggered for non intentional displacement, this is where the `triggerAllEvents` config option and the intentional state attribute become useful.

- `triggerAllEvents` (boolean)
  - Forces the handler to fire even for non intentional displacement (ignores the `threshold`). 

- `axis` makes it easy to constrain the user gesture to a specific axis.
  - in reality axis does slightly more than just locking the gesture direction: if it detects that the user intent is to move the component in a different direction, it will stop firing the gesture handler. 
  - `axis: 'lock'` allows you to lock the movement of the gesture once a direction has been detected. In other words, if the user starts moving horizontally, the gesture will be locked on the x axis.

- If you want to set constraints to the user gesture, then you should use the `bounds` option. 
  - In that case, both the gesture `movement` and `offset` will be clamped(夹在... 之间) to the specified bounds. 
  - `bounds` will be defaulted to `Infinity` when not set.
  - Since v10 and for the drag gesture only,  `bounds` can be a React ref or an HTMLElement, in which case the dragged element will be constrained to the element bounds (calculated with `getBoundingClientRect`).

- React warning: if you want events not to be `passive`, you will need to attach events directly to a node using `target` because of the way React handles events

- `delay` delays the drag gesture for the amount of milliseconds you specify. 
  - This might be useful if you don't want your logic to fire right away.
  - 👉🏻 Note that if the the pointer is moved by the user, the drag gesture will fire immediately without waiting for the delay.
  - When using `delay` and `threshold` options at the same time, the **drag will start after the delay no matter what**.

- `filterTaps`: Making a draggable component tappable or clickable can be tricky: differentiating a click from a drag is not always trivial.
  - When you set `filterTaps` to true, the tap state attribute will be true on release if the total displacement is inferior(低的、次要的) to `3 pixels` while down will remain false all along.
  - When using the filterTaps option, taps are only triggered when the displacement is inferior to 3 pixels. You can customize that value by using `tapsThreshold`.

- `from`: Everytime a gesture starts, the `offset` state attribute starts with its previous value. 
  - But in some cases, you might want to start offset from an initial position that is external to your logic.
  - Unless your initial position is static or depends on state, make sure you use a function rather than a static array.

- pointer.capture
  - By default, drag uses `setPointerCapture` to track the pointer movement. 
  - When a pointer is captured by a target, it won't trigger any listener from another target (even a CSS `:hover`). 
  - Most of the time this is fine, but in some situations, you may want to drag an element and still receive events from another target.

- pointer.lock
  - Set lock to true and the drag gesture will requestPointerLock when the drag starts and exitPointerLock when the drag gesture ends. 
  - This feature is only relevant on non-touch devices.

- pointer.touch
  - 👉🏻 Most gestures, drag included, use pointer events. 
  - This works well in 99 situations in 100, but **pointer events get canceled on touch devices when the user starts scrolling**. 
  - Usually this is what you actually want, and the browser does it for you. 
  - But in some situations you may want the drag to persist while scrolling. 
  - In that case you'll need to indicate @use-gesture to use touch events, which aren't canceled on scroll.

- `preventScroll` is a convenient way to have both vertical drag and vertical scrolling coexist. 
  - Note that scroll will always have precedence over drag. To drag vertically the user will have to press and hold the draggable area for 250ms (or the specified duration) without moving. After this duration, the element is draggable and scrolling is prevented. 

## instance/state

- Every time a handler is called, it will get passed a gesture state that includes the source event and adds multiple attributes such as velocity, previous value, and much more.
  - States structure doesn't vary much across different gestures: the only distinction comes from the `pinch` gesture which handles distance and angle values (how distant your fingers are on screen, and what is their angle), when all other hooks deal with x and y coordinates.
  - With the exception of `xy/cancel/canceled` all the attributes below are common to all gestures.

- `movement` and `offset` are the attributes you're going to use most of the time when dragging or pinching.
  - They represent relative values of the gesture, in contrast with `xy and da` which are absolute values of your pointers. 
  - `movement` expresses the gesture movement, while `offset` is the sum of all gesture movements on the same component. 
  - `xy`: [x, y] values (pointer position or scroll offset)
  - initial: xy value when the gesture started
  - `offset`: offset since the first gesture
  - lastOffset: offset when the last gesture started
  - `movement`: displacement between offset and lastOffset
  - `delta`: movement delta (movement - previous movement)
  - `distance`: offset distance per axis
  - We're using the word "movement" to mean "the vector distance this motion has travelled from its origin", for which I believe the correct physics word is "displacement". 
  - I agree with the terminology, displacement is a better word than movement, but I didn't think of it two years ago unfortunately.
  - [Drag movement does not include pre-threshold movement](https://github.com/pmndrs/use-gesture/issues/314)
    - 👉🏻 As a clarification, `offset` represents the cumulative(累积的) `movement` across gestures: `movement` is reset to zero when the gesture starts, while `offset` isn't.
    - `initial` is the position of the mouse when the drag starts, so it doesn't depend on the threshold being set.

- `memo` stores the value returned by the previous call of your handler. 
  - The most common usecase for using memo should be simplified by using initial
  - `memo`: value returned by your handler on its previous run

- swipe (drag only) is a convenient state attribute for the drag gesture that will help you detect swipes. 
  - swipe is a vector which both components are either -1, 0 or 1. 
  - The component stays to 0 until a swipe is detected. 
  - 1 or -1 indicates the direction of the swipe (left or right on the horizontal axis, top or bottom on the vertical axis).
- Here are the conditions for a swipe to be detected on the x axis:
  - The drag gesture is over.
  - The drag gesture didn't last more than 220ms.
  - movement[0] is superior to the swipe.distance[0] option.

- tap (drag only) is a boolean state attribute for the drag gesture that will be set to true if the drag gesture can be assimilated to a tap or click. 
  - 👉🏻 In other words, tap will be true on mouse or touch release only when the drag displacement is inferior to 3 pixels.
# more
