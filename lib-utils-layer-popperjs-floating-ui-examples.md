---
title: lib-utils-layer-popperjs-floating-ui-examples
tags: [examples, floating-ui, popperjs]
created: 2023-03-27T11:59:40.865Z
modified: 2023-03-27T11:59:53.482Z
---

# lib-utils-layer-popperjs-floating-ui-examples

# guide

# popular
- popper.js/floating-ui /15.4kStar/MIT/202007
  - https://github.com/floating-ui/floating-ui
    - https://floating-ui.com/docs/motivation
    - Floating UI is the evolution of Popper v2, with a more modern API.
    - Cross-platform
      - Floating UI supports React Native, Canvas, WebGL, and more with the right interface logic.
    - Inversion of control
      - There were many issues opened surrounding the nature of `computeStyles` and `applyStyles` in Popper due to their opinionated defaults. 
      - Floating UI is just a function that returns some unrounded numbers for you, which you can use as you please.
    - More intuitive API
      - Popper's API is verbose and encourages mutation, which can be awkward to configure and hard to debug. 
      - Floating UI is pure with more ergonomic usage
    - Modular
      - Popper is not tree-shakeable by default
      - everything is modular by default, and thus tree-shakeable. 
      - This means you can use Floating UI starting at its most fundamental level, without any middleware enabled already
    - Improved extensibility
      - Modifiers in Popper are hard to write.
      - Floating UI removes all of it, making it much easier to write custom middleware. 
      - The order of the array is yours to control and configure. 
      - The new architecture also supports finer control over the middleware lifecycle.
    - Strongly typed by default
      - TypeScript is a first-class citizen
- https://github.com/popperjs/popper-core
  - https://popper.js.org/
  - https://github.com/popperjs/react-popper
  - https://popper.js.org/react-popper/
  - bootstrap.v5仍然依赖popper
  - It will position any UI element that "pops out" from the flow of your document and floats near a target element

- https://github.com/atomiks/tippyjs
  - https://atomiks.github.io/tippyjs/v6/headless-tippy/
  - The complete tooltip, popover, dropdown, and menu solution for the web
  - 依赖 @popperjs/core.v2
  - https://github.com/atomiks/tippyjs-react
    - we recommend using Floating UI's React DOM Interactions package
  - [Stretching the popover to the full width and height of the screen](https://github.com/atomiks/tippyjs/issues/897)
# examples-repos
- https://github.com/ycs77/headlessui-float
  - https://headlessui-float.vercel.app/
  - Easily use Headless UI with Floating UI to position floating elements.
  - 支持react、vue

- https://github.com/ariakit/ariakit
  - Toolkit for building accessible web apps with React

- https://adobe.github.io/spectrum-web-components/components/overlay
  - Overlays in Spectrum Web Components are created via the Overlay class system

- https://github.com/fabric-ds/react
  - @fabric-ds/core contains shared business logic between our Fabric JS implementations: Web Components, React and Vue.

- https://github.com/nodestrap/popup
  - A generic element with dynamic visibility (show/hide).

- design system libs using @floating-ui/dom
  - https://github.com/element-plus/element-plus
    -  A Vue.js 3 UI Library made by Element team
  - https://github.com/ant-design/ant-design-mobile
    - Essential UI blocks for building mobile web apps.
  - https://github.com/shoelace-style/shoelace
    - A forward-thinking library of web components.
    - Works with all frameworks
  - https://github.com/sibiraj-s/ngx-editor
    - Rich Text Editor for angular using ProseMirror
  - @wordpress/components
    - https://www.npmjs.com/package/@wordpress/components
    - github.com/WordPress/gutenberg
# more-popper-layer-examples
- https://github.com/wix/ricos/tree/master/packages/toolbars-v3
