---
title: lib-ui-spectrum-codebase-architecture
tags: [adobe-spectrum, architecture, codebase]
created: '2021-04-12T17:14:17.736Z'
modified: '2021-04-12T18:06:57.616Z'
---

# lib-ui-spectrum-codebase-architecture

# guide

- For React Spectrum v3, a new architecture is proposed taking advantage of hooks in React 16.8, 
  - which abstracts components into three reusable pieces: 
    - platform agnostic state management, 
    - theme agnostic behavior, 
    - and themed components. 
  - This will allow new platforms to reuse common state, and new themes to utilize common behavior while getting accessibility and more out of the box.

# react-stately

- implements state management and core logic for each component. 
  - It handles complex logic for things like collections and selection in a fully cross-platform way that you could reuse on the web, in react-native, etc.
  - React Stately hooks can be used independently in your own components, or paired with React Aria hooks to get more of the behavior and user interactions for web applications out of the box. 
  - We do not yet have behavior hooks for other platforms however, so if you're working in react-native or another view system, you'll need to use React Stately directly.

# react-aria

- implements behavior and accessibility for the web according to WAI-ARIA Authoring Practices. 
  - It includes full screen reader and keyboard navigation support, along with mouse and touch interactions that have been tested across a wide variety of devices and browsers. 
  - It also implements internationalization for over 30 languages, including right-to-left specific behavior, localized date and number formatting, and more.
  - Most importantly, React Aria is fully customizable, since it doesn't implement any rendering or impose a DOM structure or styling methodology. 
  - You just need to spread the props returned by each React Aria hook onto the appropriate DOM elements, and you get high quality interactions, behavior, and accessibility pretty much for free. 
  - All you need to do is provide the styling.

# react-spectrum

- puts all of these pieces together and implements the Adobe-specific styling. 
  - It's designed to be adaptive, and works across mouse, touch, and keyboard interactions, on devices of any screen size. 
  - It supports theming, including automatic support for dark mode and responsive scaling for large hit targets on touch devices.
  - If you're integrating with Adobe software, React Spectrum is a great way to make your UI consistent. 
  - It's also a really great example of how to use React Aria and React Stately to build a full design system

# [Architecture](https://react-spectrum.adobe.com/architecture.html)

- each company tends to reimplement many of the same components from scratch. 
  - This has become easier to do with React and other modern view libraries, 
  - but implementing full support for accessibility, internationalization, keyboard, mouse, and touch interactions, and other features is still extraordinarily difficult.
- While each design system is unique, there is often more in common between components than different.
  - Most components typically found in a design system, like buttons, checkboxes, selects, and even tables, usually have very similar behavior and logic. 
  - There are even specifications that describe how many of the most common components should behave in terms of accessibility semantics and keyboard interactions. 
  - The main difference between design systems is the styling.
- This opens up to the possibility of sharing much of the behavior and component logic between design systems and across platforms. 
  - For example, user interactions, accessibility, internationalization, and behavior can be reused, while allowing custom styling and rendering to live within individual design systems. 
  - This has the potential to improve the overall quality of applications, while saving companies money and time, and reducing duplicated effort across the industry.

- In order to allow reusing component behavior between design systems, React Spectrum splits each component into three parts: state, behavior, and the rendered component.
  - Some components don't have all of these pieces. 
  - For example, some simple components do not require any state, 
  - and others are only compositions of other components, 
  - so each component has the pieces of this architecture that make sense for their purpose.
- This architecture is made possible by React Hooks, 
  - which enable the ability to reuse behavior between multiple components. 
  - Hooks allow accessing React features like state and effects from functions which can be called from any component.

- State hook
- At the bottom is the state hook. 
  - This hook is shared across platforms — it could work on the web, react-native, or any other platform, and makes no assumptions about the view system it is running on. 
  - It also has no theme or design system specific logic.
  - The state hook accepts common props from the component and provides state management. 
  - It implements the core logic for the component and returns an interface for reading and updating the component state.
  - Not all components have a state hook. 
    - For example, many components are read-only — they display something to the user but don't allow them to change it. 
    - State hooks are found in interactive components that allow data entry, or have some kind of visual state that the user can update (e.g. expanding/collapsing).

- Behavior hook
- In the middle is the behavior hook. 
  - This hook is platform specific, and depends on the platform API (e.g. the DOM or react-native). 
  - It also has no theme or design system specific logic. 
  - It implements event handling, accessibility, internationalization, etc. — all the parts of a component that could be shared across multiple design systems.
  - The behavior hook uses the state hook in order to implement component behavior. 
  - It returns one or more sets of platform specific props (e.g. DOM props) that can be spread onto the elements rendered by the component. 
    - These include semantic properties like ARIA, and event handlers. 
    - The event handlers in turn call methods on the state interface to implement the behavior for the component.
  - Some components may not have any user interactions, but still have a behavior hook. 
    - Most components have some kind of semantics that they need to expose for accessibility (a form of behavior). 
    - The only components that won't have a behavior hook of their own are those that only compose together other components.

- Component
  - At the top is the component, which lives in each design system and composes all of these pieces together. 
  - It provides the theme and design system specific logic, and renders the actual platform elements. 
  - It applies styles, which could be implemented in many different ways (e.g. CSS classes, CSS-in-JS, etc.).
  - The component uses props returned by the behavior hook and state from the state hook to implement the visual appearance. 
  - It spreads props returned from the behavior hook onto elements that it renders to apply semantics and interactions, and can use the state from the state hook to adjust its visual appearance. 
  - This allows complete control over the rendering of the component, including things like adding extra elements as needed for styling or layout control.

- Our implementation of this architecture splits each piece into three npm scopes
  - Within a component, the hooks are designed to be highly composable, with individual features split into many hooks. 
  - This allows you to combine them together and achieve your design with only the features you need in your design system.
- The overall goal for the project is to make reusing behavior across design systems as easy as possible, while allowing full design customizability and avoiding code bloat.
