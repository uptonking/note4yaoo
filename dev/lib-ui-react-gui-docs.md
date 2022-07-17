---
title: lib-ui-react-gui-docs
tags: [docs, react-gui, ui]
created: 2021-07-12T05:36:51.907Z
modified: 2021-07-12T05:40:20.090Z
---

# lib-ui-react-gui-docs

> tools that can be combined and extended to create accessible and interactive user interfaces.

# overview
- https://codesandbox.io/s/react-gui-preview-l2wdl

- React GUI is designed as the foundation for React design systems and component libraries.
  - It sets you up for success in creating accessible, interactive, performant user interfaces that support the custom look and feel of your product.

- The React GUI package exports “Components”, “APIs”, and “Hooks”. 
  - Each exported module can be used in isolation or together with other modules to implement React-based design systems, product component libraries, and custom applications. 
  - Modules are imported using package subpaths.
- Components are developed in the standard React way, with **styles being defined in JavaScript** and **behaviors attached using Hooks**.
- React GUI code can be used alongside existing React DOM components, allowing for incremental adoption.

- Modern React 
  - Made with modern React APIs including function components and hooks. 
  - Ready for use with modern React APIs including Concurrent Mode and Server Components. 
  - React GUI is built upon React DOM ensuring easy adoption by existing React web design systems and applications.
  - The library integrates directly with the native DOM event system (i.e., it does not use React DOM’s synthetic event system); 
  - this provides excellent flexibility and performance, as well as broad compatibility with alternative renderers. 
  - Features not supported by React DOM (e.g., listening to passive events, custom events, and root events) are available in React GUI and straight-forward to use.

- Modular views and behaviors
  - The components for UI “primitives” do not include the event callback props you may be familiar with from React DOM. 
  - Functionality related to events, gestures, resize observation, and media queries is provided exclusively via hooks.
  - This may appear cumbersome for simple cases, but provides flexibility and clarity for design systems, 

- Behaviors
  - Hooks allow for composition without props collision. 
  - You can create custom gestures and custom combinations of behaviors, independently of the view they are later attached to. 
  - Any number of hook instances can listen to the same DOM event independently, so you don’t have to worry about merging props.

- Reliable and tested
  - React GUI is thoroughly unit tested with over 90% code coverage. 

- Dependencies
  - The import paths documented for the react-gui package rely on Node.js package entry points, which is available in Node.js 12.15 and above
  - The interaction Hooks work best with apps rendered using React DOM’s `createRoot` API; Also works with Preact.
# Accessibility
- Familiar web accessibility APIs in a platform-agnostic form.
- Accessibility in React GUI combines several separate web APIs into a cohesive system. 
  - Assistive technologies (e.g., VoiceOver, TalkBack screen readers) derive useful information about the structure, purpose, and interactivity of web apps from their HTML elements, attributes, and ARIA in HTML.
- Links
- Keyboard focus
  - All views in React GUI can be programmatically focused using the focus export to support WAI-ARIA accessibility patterns.
- Accessible HTML
  - React GUI components express semantics exclusively via the `accessibility*` props which are equivalent to `aria-*` attributes.
  - Additional compatibility with React Native accessibility props is also included.
- Semantic HTML 
  - The value of the `accessibilityRole` prop is used to infer an analogous HTML element where appropriate. 
  - This is done to rely on well-supported native mechanisms for encoding semantics and accessibility information.
  - Avoid changing accessibilityRole values over time or after user actions. Generally, accessibility APIs do not provide a means of notifying assistive technologies if a role changes.
# Styling
- React GUI relies on JavaScript to define and resolve the styles of your application. 
  - The style API avoids all the **problems with CSS at scale** and produces highly optimized CSS without the need to learn a DSL (e.g., unlike Tailwind CSS).
- classic css problems
  - No local variables.
  - Implicit dependencies.
  - No dead code elimination.
  - No code minification.
  - No sharing of constants.
  - Non-deterministic resolution.
  - No isolation.

- At the same time, it has several benefits:
  - Simple API and expressive subset of CSS.
  - Generates CSS; the minimum required.
  - Good **runtime performance**.
  - Support for static and dynamic styles.
  - Support for RTL layouts.
  - Easy pre-rendering of critical CSS.

- Style resolution is deterministic and slightly different from CSS.
  - in React GUI the most precise style property takes precedence

- Styles should be defined outside of the component. 
  - Using `StyleSheet.create` is optional but provides the best performance (by relying on generated CSS stylesheets). 
  - Avoid creating unregistered style objects.

- React GUI transforms styles objects into CSS and inline styles. 
  - Any styles defined using `StyleSheet.create` will ultimately be rendered using CSS class names.
  - Each rule is broken down into declarations, properties are expanded to their long-form, and the resulting key-value pairs are mapped to unique “atomic CSS” class names.
  - This ensures that CSS order doesn’t impact rendering and CSS rules are efficiently deduplicated. 
- Class names are deterministic, which means that the resulting CSS and HTML is consistent across builds – important for large apps using code-splitting and deploying incremental updates.
- At runtime registered styles are resolved to DOM style props and memoized. 
  - Any dynamic styles that contain declarations previously registered as static styles can also be converted to CSS class names. 
  - Otherwise, they render as inline styles.

- What about Media Queries?
  - Media Queries may not be most appropriate for component-based designs.
  - If you do choose to use Media Queries, using them in JavaScript via the `matchMedia` DOM API has the benefit of allowing you to swap out entire components, not just styles.
- What about pseudo-classes and pseudo-elements?
  - Pseudo-classes like `:hover` and `:focus` can be implemented with events (e.g. `onFocus`). 
  - Pseudo-elements are not supported; elements should be used instead.

- Do I need a CSS reset?
  - No. 
  - React GUI includes a very small CSS reset that removes unwanted User Agent styles from (pseudo-)elements beyond the reach of React (e.g., `html, body`) or inline styles (e.g., `::-moz-focus-inner`). 
  - The rest is handled at the component-level.
# components

```JS
<Image {...props} />;

<RichTextArea {...props}></RichTextArea>;
```

## View: The fundamental layout primitive.

- View has built in accessibility controls, enforces flexbox columns by default (and supports grid and float layout). 
- Raw text nodes are not allowed as children or siblings of View, and no text-related styling is supported. 
- A View nested within a Text will render inline without altering its display or that of its children. 
- Accessibility props map directly to WAI-ARIA properties (excluding properties and values that are deprecated, redundant, or to be avoided).
