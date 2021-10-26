---
title: lib-ui-spectrum-docs-stately
tags: [adobe-spectrum, docs]
created: '2021-04-12T17:58:20.417Z'
modified: '2021-04-12T18:07:42.879Z'
---

# lib-ui-spectrum-docs-stately

> - platform-agnostic; theme-agnostic; 

# [overview](https://react-spectrum.adobe.com/react-stately/getting-started.html)

- React Stately is library of React Hooks that provides cross-platform state management for your design system.
- It provides the foundation and core logic for your component library, and implements state management for many common components. 
- It returns an interface for reading and updating component state, with methods that implement much of the core logic for the component.

# [Collection components](https://react-spectrum.adobe.com/react-stately/collections.html)

- There are many components that display a collection of items of some kind. 
  - For example, lists, menus, selects, tables, trees, and grids. 
  - These collections can usually be navigated with the keyboard using arrow keys, and many have some form of selection. 
  - Many support loading data asynchronously, updating that data over time, virtualized scrolling for performance with large collections, and more.
- There are many ways one could design an API for components like this: JSX children, a list of option objects, or a datasource object. 
  - Selection, and other states like disabled, could be passed in to each item, or as a top-level prop. 
  - Each of these has various tradeoffs.

- Our main design goal was to provide a consistent API across many types of collection components that is easy to learn, performant on large collections, and extensible for advanced features.
- Some of the use-cases we considered were:
  - Static data
  - Dynamic data
  - Async loading
  - Sections/groups of data from a single source
  - Sections from different sources
  - Single and multiple selection (controlled and uncontrolled)
  - Controlled and uncontrolled expanded states for components like trees and accordions
  - Marking items as selected, expanded, disabled, etc. prior to loading them from a server
  - Drag and drop of items
  - Virtualization for large collections
  - Infinite scrolling to load more items on demand

- React Spectrum implements a JSX-based API for defining collections.

- ## Static collections

- A static collection is a collection that does not change over time (e.g. hard coded). 
  - This is common for components like action menus where the items are built into the application rather than representing user data.
- Sections or groups of items can be constructed by wrapping the items as needed.
  - The `<Item>` and `<Section>` components are shared between many collection components. 
  - This ensures that they have a consistent interface that can be learned once and applied everywhere.
  - `<Item>` and `<Section>` only define the data for the items and sections, not the rendering, visual appearance, or behavior. This is up to the individual collection component (e.g. Menu or ListBox) to implement.

- ## Dynamic collections
- A dynamic collection is a collection that is based on data, for example from an API. 
  - In addition, it may change over time as items are added, updated, or removed from the collection by a user.
- React Spectrum implements a JSX-based interface for dynamic collections, 
  - which maps over your data and applies a function for each item to render it.


- Unique keys
  - All items in a collection must have a unique `key` or `id`, which is used to determine what items in the collection changed when updates occur. 
    - By default, React Spectrum looks for an id or key property on each item, which is often returned from a database. 
    - You can also specify a custom key on each item using the `key` prop.


- Why not array map?
  -  you can do this if you want and it will work, but it will not be as performant.
  -  Using the `items` prop and providing a render function allows React Spectrum to automatically cache the results of rendering each item and avoid re-rendering all items in the collection when only one of them changes. 
  -  This has big performance benefits for large collections.


- Updating data
- When you need to update the data to add, remove, or change an item, you can do so using a standard React state update.
  - all items passed to a collection component must be immutable. 
  - Changing a property on an item, or calling array.push() or other mutating methods will not work as expected.
- The `useListData` hook can be used to manage the data and state for a list of items, and update it over time. 
  - It will also handle removing items from the selection state when they are removed from the list. 


- Sections
  - Sections can be built by returning a `<Section>` instead of an `<Item>` item from the top-level item renderer. 
  - Sections also support an `items` prop and a renderer function for their children.
- When updating nested data, be sure that all parent items change accordingly. 
  - Items are immutable, so don't use mutating methods like push, or replace a property on a parent item. 
  - Instead, copy the items that changed as needed.
- The `useTreeData` hook can be used to manage data and state for a tree of items. 
  - This is similar to `useListData`, but with support for heirarchical data. 

- ## Asynchronous loading
- Many collection components support loading data asynchronously. 
  - This is supported by passing an `isLoading` prop, which is `true` while the data is loading. 
  - Once the data is loaded, `isLoading` should be set to `false`, and the `items` prop should be set to the loaded data.
- The `useAsyncList` hook can be used to manage async data loading from an API. 
  - Pass a load function to `useAsyncList`, which returns the items to render. 
  - You can use whatever data fetching library you want, or the built-in `fetch` API.


- Infinite loading
  - The `useAsyncList` hook also supports paginated data, which is common in many APIs to avoid loading too many items at once. 
  - This is accomplished by returning a `cursor` in addition to `items` from the load function. 
  - When the `loadMore` method is called, the `cursor` is passed back to your load function, which you can use to determine the URL for the next page. 
  - The `onLoadMore` prop supported by many collection components notifies you when you should load more data as the user scrolls.

# selection
