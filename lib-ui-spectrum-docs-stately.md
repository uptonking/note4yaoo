---
title: lib-ui-spectrum-docs-stately
tags: [adobe-spectrum, docs]
created: '2021-04-12T17:58:20.417Z'
modified: '2021-04-12T18:07:42.879Z'
---

# lib-ui-spectrum-docs-stately

> - platform-agnostic; - theme-agnostic; 

# [overview](https://react-spectrum.adobe.com/react-stately/getting-started.html)

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

- Our main design goal was to provide a consistent API across many types of collection components that is easy to learn, performant on large collections, and extensible for advanced features
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

- Static collections
  - Sections
- Dynamic collections
  - Unique keys
  - Why not array map?
  - Updating data
  - Sections
- Asynchronous loading
  - Infinite loading
