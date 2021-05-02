---
title: lib-ui-spectrum-docs-api
tags: [adobe-spectrum, api, docs]
created: '2021-04-12T16:44:13.601Z'
modified: '2021-04-12T18:07:20.604Z'
---

# lib-ui-spectrum-docs-api

# guide

# react-stately

## Collection

- The `Collection` interface provides a generic representation for many types of collections. 
  - The collection is read only (immutable), and sequential (ordered). 
  - Each item has a unique key that identifies it, which can be used to access items. 
  - It's like a combination of an array and a map: you can iterate over items in a well defined order, and also access items by key.

- The `Collection` interface can be implemented in many ways. 
  - For example, you could write a class to expose the required methods and properties for an underlying data structure like an array or Map.
- React Spectrum implements a JSX-based API for defining collections. 
  - This is implemented by the `useCollection` hook. 
  - `useCollection` iterates over the JSX tree, and recursively builds a collection of `Node` objects. 
  - Each node includes the value of the item it represents, along with some metadata about its place in the collection.
  - These nodes are then wrapped in a class that implements the Collection interface, and exposes the nodes. 
  - State management hooks like `useListState` and `useTreeState` handle building the collection and exposing the necessary interface to components.
- When implementing collection components using react-aria hooks like `useListBox`, and `useSelect`, you'll iterate over these nodes to render the data in the collection.

- useListState
  - Provides state management for list-like components. 
  - Handles building a collection of items from props, and manages multiple selection state.
  - See the docs for `useListBox` in react-aria for an example of `useListState`.

- useSingleSelectListState
  - Provides state management for list-like components with single selection.
  - Handles building a collection of items from props, and manages selection state.
  - [Add useSingleSelectListState](https://github.com/adobe/react-spectrum/pull/802)
    - This hook handles mapping the props for components supporting single selection to the internal state which is stored as a set of one key. 
    - `onSelectionChange` is now always fired, regardless of whether the key actually changed. This was to ensure that the picker closes when selecting the same item

- useTreeState
  - Provides state management for tree-like components. 
  - Handles building a collection of items from props, item expanded state, and manages multiple selection state.
    - See the docs for `useMenu` in react-aria for an example of `useTreeState`.

- useAsyncList
  - Manages state for an immutable async loaded list data structure, and provides convenience methods to update the data over time.
  - `useAsyncList` extends on `useListData`, adding support for async loading, pagination, sorting, and filtering. 
  - It manages loading and error states, supports abortable requests, and works with any data fetching library or the built-in browser `fetch` API.

- useListData
  - Manages state for an immutable list data structure, and provides convenience methods to update the data over time.
  - React requires all data structures passed as props to be immutable. 
  - This enables them to be diffed correctly to determine what has changed since the last render. 
  - This can be challenging to accomplish from scratch in a performant way in JavaScript.
  - `useListData` stores selection state for the list, based on unique item keys.

- useTreeData
  - useTreeData helps manage an immutable tree data structure, with helper methods to update the data in an efficient way. 
  - Since the data is stored in React state, calling these methods to update the data automatically causes the component to re-render accordingly.
  - `useTreeData` stores selection state for the tree, based on unique item keys.

## Selection

- Many collection components support selecting items by clicking or tapping them, or by using the keyboard. 
  - This page discusses how to handle selection events, how to control selection programmatically, and the data structures used to represent a selection.
- Selection is handled by the `onSelectionChange` event, which is supported on most collection components. 
  - Controlled behavior is supported by the `selectedKeys` prop, and uncontrolled behavior is supported by the `defaultSelectedKeys` prop. 
  - These props are passed to the top-level collection component, and accept a set of unique item keys that are selected. 
  - This allows marking items as selected by their key even before they are loaded, which can be useful when you know what items should be selected on initial render, before data loading has completed.
- Selection is represented by a `Set` object. 
  - You can also pass any iterable collection (e.g. an array) to the selectedKeys and defaultSelectedKeys props, 
  - but the `onSelectionChange` event will always pass back a `Set`.
- When data in a collection changes, the selection state may need to be updated accordingly. 
  - For example, if a selected item is deleted, it should be removed from the set of selected keys. 
  - You can do this yourself, but the `useListData` and `useTreeData` hooks can handle this automatically.
- selectedKeys and defaultSelectedKeys can also be set to `all` to programmatically select all items.
  - This represents all items in the collection, whether currently loaded or not. 
  - The application must adjust its handling of bulk actions in this case to apply to the entire collection rather than only the keys available to it locally.

- SelectionManager
  - provides a generic interface for reading and updating selection and focus state based on a Collection
  - Focus is represented by a single item key.
  - A SelectionManager wraps the state returned by useMultipleSelectionState

- useMultipleSelectionState
  - manages selection state for many components. 
  - Oftentimes, you won't need to use this hook directly, since it's included in hooks like useListState, and useSelectState. 

## stately-more-apis

- useSelectState
  - Handles building a collection of items from props, handles the open state for the popup menu, and manages multiple selection state.

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
