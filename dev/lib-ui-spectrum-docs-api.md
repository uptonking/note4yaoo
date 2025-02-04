---
title: lib-ui-spectrum-docs-api
tags: [adobe-spectrum, api, docs]
created: 2021-04-12T16:44:13.601Z
modified: 2021-04-12T18:07:20.604Z
---

# lib-ui-spectrum-docs-api

# guide

# react-aria

## common events & states

- usePress
  - usePress handles press interactions across mouse, touch, keyboard, and screen readers. 
  - A press interaction starts when a user presses down with a mouse or their finger on the target, and ends when they move the pointer off the target. 
  - It may start again if the pointer re-enters the target. 
  - `usePress` returns the current press state, which can be used to adjust the visual appearance of the target. 
  - If the pointer is released over the target, then an `onPress` event is fired.
- functionality
  - Handles mouse and touch events
  - Handles `Enter` or `Space` key presses
  - Handles screen reader virtual clicks
  - Uses pointer events where available, with fallbacks to mouse and touch events
  - Normalizes focus behavior on mouse and touch interactions across browsers
  - Handles disabling text selection on mobile while the press interaction is active
  - Handles canceling press interactions on scroll
  - Normalizes many cross browser inconsistencies

- useMove
  - useMove handles move interactions across mouse, touch, and keyboard. 
  - A move interaction starts when a user presses down with a mouse or their finger on the target, and ends when they lift their pointer. 
  - Move events are fired as the pointer moves around, and specify the distance that the pointer traveled since the last event. 
  - In addition, move events are fired when the user focuses the target element and uses the arrow keys.
- functionality
  - Handles mouse and touch events
  - Handles arrow key presses
  - Uses pointer events where available, with fallbacks to mouse and touch events
  - Ignores emulated mouse events in mobile browsers
  - Handles disabling text selection on mobile while the press interaction is active
  - Normalizes many cross browser inconsistencies

- useFocus
  - Handles focus events for the immediate target. 
  - Focus events on child elements will be ignored.
  - useFocus handles focus interactions for an element. 
  - Unlike React's built-in focus events, useFocus does not fire focus events for child elements of the target. 
  - This matches DOM behavior where focus events do not bubble. 
  - This is similar to the `:focus` pseudo class in CSS.
  - To handle focus events on descendants of an element, see `useFocusWithin`.

- useFocusVisible
  - useFocusVisible handles focus interactions for the page and determines whether keyboard focus should be visible (e.g. with a focus ring). 
  - Focus visibility is computed based on the current interaction mode of the user. 
  - When the user interacts via a mouse or touch, then focus is not visible. 
  - When the user interacts via a keyboard or screen reader, then focus is visible. 
  - This is similar to the `:focus-visible` pseudo class in CSS.
  - To determine whether a focus ring should be visible for an individual component rather than globally, see `useFocusRing`.

- useFocusWithin
  - useFocusWithin handles focus interactions for an element and its descendants. 
  - Focus is "within" an element when either the element itself or a descendant element has focus. 
  - This is similar to the `:focus-within` pseudo class in CSS.

- useHover
  - useHover handles hover interactions for an element. 
  - A hover interaction begins when a user moves their pointer over an element, and ends when they move their pointer off of the element.
  - Uses pointer events where available, with fallbacks to mouse and touch events
  - Ignores emulated mouse events in mobile browsers
  - `:hover` is problematic on touch devices due to mouse emulation in mobile browsers.
  - Depending on the browser and device,  `:hover` may never apply, or may apply continuously until the user touches another element. 
  - `useHover` only applies when the pointer is truly capable of hovering, and emulated mouse events are ignored.

- useKeyboard
  - useKeyboard handles keyboard interactions. 
  - The only difference from DOM events is that propagation is stopped by default if there is an event handler, unless `event.continuePropagation()` is called. 
  - This provides better modularity by default, so that a parent component doesn't respond to an event that a child already handled. 
  - If the child doesn't handle the event (e.g. it was for an unknown key), it can call `event.continuePropagation()` to allow parents to handle the event.

## common utilities

- VisuallyHidden
  - VisuallyHidden is a utility component that can be used to hide its children visually, while keeping them visible to screen readers and other assistive technology. 
  - This would typically be used when you want to take advantage of the behavior and semantics of a native element like a checkbox or radio button, 
  - but replace it with a custom styled element visually.
- In order to allow additional rendering flexibility, the `useVisuallyHidden` hook can be used in custom components instead of the VisuallyHidden component. 
  - It supports the same options as the component, and returns props to spread onto the element that should be hidden.

- mergeProps 
  - it is a utility function that combines multiple props objects together in a smart way. 
  - This can be useful when you need to combine the results of multiple react-aria hooks onto a single element. 
  - For example, both hooks may return the same event handlers, class names, or ids, and only one of these can be applied. 
  - mergeProps handles combining these props together so that multiple event handlers will be chained, multiple classes will be combined, and ids will be deduplicated. 
  - For all other props, the last prop object overrides all previous ones.

- useId 
  - creates an autogenerated unique id for an element. 
  - An id from props can used instead of the autogenerated id when available.

- useLabel
  - useLabel hook associates a label with a field.
  - It automatically handles creating an id for the field and associates the label with it.
  - By default,  `useLabel` assumes that the label is a native HTML label element.
  - However, if you are labeling a non-native form element, be sure to use an element other than a `<label>` and set the `labelElementType` prop appropriately.
# react-spectrum components
