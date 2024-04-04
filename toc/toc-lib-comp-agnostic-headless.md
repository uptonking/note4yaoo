---
title: toc-lib-comp-agnostic-headless
tags: [components, headless, toc]
created: 2021-04-11T06:17:15.216Z
modified: 2021-04-11T06:17:51.318Z
---

# toc-lib-comp-agnostic-headless

# guide

- 组件库组成
  - state, styling, a11y, animation

- pick-ui-components
  - framework-agnostic
  - headless/unstyled
    - headless, renderless, no styling, unstyled, accessible
  - accessible

- 💡️ 不必执着于完整的现有组件库，可分析其他组件支持多个框架的方法，如tanstack-table
- 有状态无渲染，有渲染无状态，且状态尽量与具体业务解耦，状态逻辑尽量通用，这也是hooks设计的思路
- I wonder... should these be called ui patterns rather than components.

- headless组件是否表明react将view与logic耦合在一起封装为component的思路是错误的?
  - 与view视图无关的component本身就是个简单的函数或eventemitter-pattern

- headless-ui-examples
  - popular: floating-ui, dnd-kit, autocomplete
  - radix-ui
    - 提供了自研stitches的样式解决方案
  - react-spectrum
    - based on react-stately,react-aria
  - headlessui
    - listbox/select,dropdown/menu,switch,radio-group
    - dialog,popover,disclosure,transition
    - 示例组件的动画体验非常好
  - ariakit/reakit
    - used-by: bumbag-ui
  - adaptui/renderlesskit-react
    - 依赖reakit,react-aria,chakra-ui
  - zendesk-garden-react-containers: 2种使用方式 hook, render-prop
  - zag
  - reach-ui
  - downshift
  - react-bootstrap依赖的restart/hooks

- 没必要执着于render agnostic
  - 具体场景需求不同，如ui组件、图表、动画
  - 跨平台的差异
  - react-canvas/webgl，在一定程度也是将vdom渲染到不同平台

- ref
  - https://github.com/jxom/awesome-react-headless-components
# headless-ui
- zag /1.5kStar/MIT/202210/ts
  - https://github.com/chakra-ui/zag
  - https://zagjs.com/overview/introduction
  - Finite state machines for accessible JavaScript components
  - The component interactions are modelled in a framework agnostic way. 
  - We provide adapters for JS frameworks like React, Solid, or Vue.
  - Zag.js (low-level state machine) => Ark (headless components) => Chakra (Ark + CSS-in-JS)
  - The machine APIs are completely unstyled and gives you the control to use any styling solution you prefer.
  - Zag is built on top of the latest ideas in Statecharts. We don't follow the SCXML specifications

- ariakit/reakit /6.2kStar/MIT/202210/ts
  - https://github.com/ariakit/ariakit
  - https://github.com/reakit/reakit
  - https://ariakit.org/
  - https://ariakit.org/components/toolbar
  - https://reakit.io/
  - Toolkit for building accessible rich web apps with React.
  - [Framework-agnostic architecture for examples](https://github.com/ariakit/ariakit/issues/1854)
  - [Ariakit newsletter](https://newsletter.ariakit.org/archive)

- AdaptUI/renderlesskit-react /197Star/MIT/202207/ts
  - https://github.com/adaptui/react
  - https://github.com/adaptui/react-tailwind
  - https://github.com/timelessco/renderlesskit-react
  - https://adaptui-react-tailwind.vercel.app/
  - Collection of headless components/hooks that are accessible, composable, customizable from low level to build your own UI & Design System powered by Reakit System.

- react-spectrum /7.3kStar/Apache2/202210
  - https://github.com/adobe/react-spectrum
  - https://react-spectrum.adobe.com/react-spectrum/Dialog.html
  - A React implementation of Spectrum, Adobe’s design system
  - 组件基于hooks实现
  - React Aria: library of React Hooks that provides accessible UI primitives for your design system.
  - React Stately: library of React Hooks that provides cross-platform state management for your design system.
  - https://github.com/adobe/spectrum-css
    - CSS implementation of the Spectrum design language.

- radix-ui /6.2kStar/MIT/202210/ts
  - https://github.com/radix-ui/primitives
  - https://www.radix-ui.com/docs/primitives/components/toolbar
  - Unstyled, accessible components for building high‑quality design systems and web apps in React.
  - https://github.com/radix-ui/design-system
    - https://design-system.modulz-deploys.com/
    - 使用纯.css样式文件，未使用自研的stitches
    - Design system maintained and used by WorkOS.
    - Built with Stitches and Radix UI Primitives.
  - https://github.com/radix-ui/icons
    - https://icons.radix-ui.com/
    - A crisp set of 15×15 icons designed by the WorkOS team.

- headlessui /17kStar/MIT/202009/ts
  - https://github.com/tailwindlabs/headlessui
  - https://headlessui.com/react/dialog
  - unstyled, fully accessible UI components, designed to integrate beautifully with Tailwind CSS
  - [Headless UI: Unstyled, Accessible UI Components](https://blog.tailwindcss.com/headless-ui-unstyled-accessible-ui-components)
  - [Any way of using headlessui without react or vue](https://github.com/tailwindlabs/headlessui/discussions/984)
    - Headless UI is created and coupled to React & Vue right now

- downshift /11.2kStar/MIT/202301/js/paypal
  - https://github.com/downshift-js/downshift
  - A set of primitives to build simple, flexible, WAI-ARIA compliant React autocomplete, combobox or select dropdown components.

- Zendesk Garden /1kStar/Apache2/202210/ts
  - https://github.com/zendeskgarden/react-containers
  - https://zendeskgarden.github.io/react-containers/
  - React (no-UI) containers
  - provide an accessible foundation to to build a11y, keyboard navigable and RTL aware components.
  - https://github.com/zendeskgarden/react-components
  - https://zendeskgarden.github.io/react-components/
  - https://garden.zendesk.com/components/
  - /873Star/Apache2/202105/ts
  - 依赖styled-components
  - Garden React provides consistent styling and behavior for Garden components. 

- makeup-js /26Star/MIT/202403/js/vanillajs
  - https://github.com/makeup/makeup-js
  - https://makeup.github.io/makeup-js/
  - A suite of vanilla JavaScript modules for building accessible user interfaces.
  - come with no styles or branding out of the box
  - They are fully compatible with Skin CSS.
  - https://github.com/eBay/skin
    - https://ebay.github.io/skin/
    - Pure CSS framework designed & developed by eBay

- https://github.com/gluestack/gluestack-ui
  - https://ui.gluestack.io/
  - Universal headless components for React Native, Next.js & React with beautiful & optional styling
# ui-primitives
- webrix /399Star/Apache2/202212/js/inactive/参考use-gesture
  - https://github.com/open-amdocs/webrix
  - https://webrix.amdocs.com/
  - building blocks for React-based web applications
  - Movable, Scalable, Collapsible, Stackable, Scrollable, Pannable, Resizable, Poppable

- https://github.com/primer/primitives
  - https://primer.style/primitives
  - Color, typography, and spacing primitives in json.

- https://github.com/Bedrock-Layouts/Bedrock /202306/ts
  - https://bedrock-layout.dev/
  - Foundational Layout Primitives for your React App

- https://github.com/webeetle/react-headless-hooks
  - Hooks for build and design powerful components while retaining 100% control over markup and styles.
# headless-vanillajs
- tips
  - tanstack

- tiptap /16.1kStar/MIT/202208/ts/prosemirror
  - https://github.com/ueberdosis/tiptap
  - https://tiptap.dev/
  - A headless, framework-agnostic and extendable rich text editor, comes without any CSS. You are in full control over markup, styling and behaviour.

- https://github.com/elastic/search-ui /apache2/202403/ts
  - https://github.com/elastic/search-ui/tree/master/packages/search-ui
  - https://docs.elastic.co/search-ui/overview
  - The "Headless Search UI" that serves as a foundation for the react-search-ui library.
  - 依赖date-fns、history、qs
  - core是框架无关的
  - this library can be used in conjunction with any other framework. 
  - Instead of working with components as you do in React, you simply work directly with state and actions.

- autocomplete /2.3kStar/MIT/202212/ts
  - https://github.com/algolia/autocomplete
  - https://alg.li/autocomplete
  - [Create an end-to-end search experience with autocomplete | Algolia Blog](https://www.algolia.com/blog/product/creating-an-end-to-end-search-experience-with-autocomplete-and-instant-search-results/)
  - [Creating a custom renderer](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/creating-a-renderer/)
    - https://codesandbox.io/s/github/algolia/autocomplete/tree/next/examples/react-renderer
    - If you want to build a custom UI that differs from the autocomplete-js output, for example in React or another frontend framework, the autocomplete-core package provides all the primitives to build it.
  - JavaScript library for building autocomplete experiences.
  - 依赖preact(实现vdom)、htm
  - 示例
    - react-renderer基于autocomplete-core
    - vue基于autocomplete-js
  - The data that populates the autocomplete results are called sources. 
    - You can use whatever you want in your sources: a static set of searches terms, search results from an external source like an Algolia index, recent searches, and more.
    - Autocomplete lets you fetch from different sources and display different types of results(如更多推荐).
  - The library creates an input and provides the interactivity and accessibility attributes, but you’re in full control of the DOM elements to output.
  - Unlike InstantSearch, Autocomplete doesn’t provide a library of ready-made UI widgets
  - The rendering system of Autocomplete uses an agnostic virtual DOM implementation
  - An Autocomplete plugin is an object that implements the AutocompletePlugin interface.
    - It can provide sources, react to state changes, and hook into various autocomplete lifecycle steps
  - `autocomplete-js` package is an agnostic virtual DOM renderer. 
    - You can use it in JavaScript, Preact, React, or Vue projects. 
    - Renderers provide a UI to headless autocomplete experiences built with `autocomplete-core`.

- https://github.com/dan-lee/timescape /107Star/MIT/202403/ts/NoDeps
  - https://timescape.daniellehr.de/
  - A flexible, headless date and time input library for JavaScript
  - Provides tools for building fully customizable date and time input fields
  - support React, Preact, Vue, Svelte and Solid
  - Full A11y compliance, keyboard navigation and manual input.
  - Touch device support: Use it on any device, including touch devices.
  - 示例丰富，包括calendar、range
  - 样式较简单

- https://github.com/TanStack/time /202403/ts
  - Headless utilities for building time and calendar components
  - React, Solid, Vue, Svelte and Angular

- https://github.com/TanStack/ranger /MIT/202403/ts
  - Headless utilities for building range and multi-range sliders in React, Preact, Solid, Vue, Svelte and Angular

- https://github.com/roginfarrer/collapsed /485Star/MIT/202311/ts/inactive
  - https://react-collapsed.netlify.app/
  - Headless UI for for creating flexible and accessible expand/collapse components
  - Includes adapter for React.
  - No animation framework required! Simply powered by CSS animations

- https://github.com/handsontable/hyperformula /GPLv3/202402/ts
  - An advanced headless evaluator and parser of Excel formulas

- https://github.com/vincentdchan/blocky-editor
  - An headless editor built with blocks
  - The core of the editor. Written in vanilla JS.

- https://github.com/jieter/leaflet-headless
  - Leaflet for node.(Has Leaflet 1.1.x as dependency.)
  - Uses jsdom to fake ad DOM.
  - Uses Image implementation and canvas from node-canvas. 
  - Tiles, Markers and vector layers work well with leaflet-image

- https://github.com/plantain-00/select2-component
  - https://plantain-00.github.io/select2-component/packages/react/demo/
  - A vuejs and reactjs select component.
  - local search
  - multiple selection

- https://github.com/plantain-00/tree-component
  - https://plantain-00.github.io/tree-component/packages/react/demo/
  - A reactjs and vuejs tree component.
  - drag and drop between different tree
  - composition model(reactjs children and vuejs slot)

- https://github.com/select2/select2 /25.8kStar/MIT/202303/js/inactive
  - https://select2.org/
  - a jQuery based replacement for select boxes. 
  - It supports searching, remote data sets, and infinite scrolling of results.

- https://github.com/Choices-js/Choices /ts
  - https://github.com/jshjohnson/Choices /ts
  - https://choices-js.github.io/Choices/
  - configurable select box/text input plugin.
  - Similar to Select2 and Selectize but without the jQuery dependency.
  - Flexible styling
  - 依赖redux、fuse.js(fuzzy-search in js)

- https://github.com/ivkan/ts-select2
  - a version of Select2 written in typescript without any dependencies.

- https://github.com/appbaseio/searchbox /js
  - a lightweight and performance focused search UI component library to query and display results from your ElasticSearch index using declarative props. 
  - It's available for React, Vue, React Native and Flutter.
  - https://github.com/appbaseio/reactivesearch
    - https://opensource.appbase.io/reactivesearch
    - Search UI components for React and Vue: powered by appbase.io/Elasticsearch
  - https://github.com/appbaseio/reactivecore
    - Core architecture of reactive UI libraries
    - 依赖redux、redux-thunk、xdate

- https://github.com/yairEO/tagify /MIT/202403/js
  - https://yaireo.github.io/tagify/
  - Transforms an input field or a textarea into a Tags component
  - Tags input component in VanillaJS/React/Angular/Vue
  - Tagify is not a controlled component.

- https://github.com/willnguyen1312/zoom-image /MIT/202404/ts
  - https://willnguyen1312.github.io/zoom-image/
  - powerful framework agnostic headless library to zoom images on the web
  - Examples are written with Preact, React, Svelte, Vanilla JS and Vue.
# headless-react
- https://github.com/h6s-dev/h6s /MIT/202404/ts
  - https://h6s.dev/
  - Serve headless component development kit for React 
  - 提供了: table, calendar

- https://github.com/chatscope/use-chat
  - https://chatscope.io/demo/
  - https://demo.chatscope.io/
  - 示例非常丰富，ui交互完整
  - React hook for state management in chat applications.
  - This is a headless chat library. Think of it as something like a Formik but for chat apps.
  - https://github.com/chatscope/chat-ui-kit-react
    - open source UI toolkit for developing web chat applications.

- https://github.com/Resetand/textarea-markdown-editor  /ts
  - UI headless simple markdown editor using only textarea
  - 依赖react
  - You can choose any markdown parser, create your own layout, and use your own textarea component that is styled and behaves however you like

- https://github.com/BearStudio/formiz /MIT/202402/ts
  - https://formiz-react.com/
  - React forms with ease
  - Composable, headless & with built-in multi steps

- vechaiui /1kStar/MIT/202206/ts
  - https://github.com/vechai/vechaiui
  - 组件实现都很简单，复杂组件直接import三方
  - A set of accessibility React components & pre-designed headlessui + radix-ui components + tailwindcss

- https://github.com/op-ent/unstyled-ui
  - an headless react library.

- https://github.com/nrkno/core-components /MIT/202310/js/inactive
  - https://static.nrk.no/core-components/latest/
  - A kit of lightweight, unstyled and accessible Javascript and React/Preact components.
- https://github.com/smakosh/ontwik-ui
  - https://ontwik-ui.smakosh.com/
  - A headless UI library and CLI theme generator
- https://github.com/InfiniteXyy/just-ui
  - /1Star/NALic/202009
  - [WIP] A headless React component library
- https://github.com/joshuapbritz/SexyHeadlessComponents
  - Demo of Headless UI Components with React
  - [The Sexiness of Headless UI Components](https://www.joshbritz.co/posts/the-sexiness-of-headless-ui/)
- https://github.com/alexkrolick/react-renderless
  - /31Star/MIT/201802
  - Utilities for creating and working with renderless React components
  - withRender combines a container and presenter (renderless and stateless) into a new component that acts like a normal React component.
  - similar to Unstated by Jamie Kyle
- https://github.com/tannerlinsley/react-ranger
  - Hooks for building range and multi-range sliders in React
- https://github.com/Buuntu/react-final-table /32Star/MIT/202104/ts/inactive
  - A headless UI component libray for managing complex table state in React.
  - Inspired by react-table but with Typescript support built in and a simpler API.

- https://github.com/Zertz/react-headless-tabs /202303/ts
  - https://react-headless-tabs.pierluc.io/#examples
  - Headless and highly flexible tab-like primitives built with react hooks
  - 支持dropdown显示更多

- https://github.com/headless-components/headless-components-react
  - /2Star/NALic/202004
  - Headless component in React with Custom hooks
# accessible
- https://github.com/accessible-ui /inactive
  - Accessible style-agnostic components for React
# more-headless-ui
- https://github.com/coveo/ui-kit
  - Coveo UI kit repository, home of @coveo/headless, @coveo/atomic, and more.
- https://github.com/ice9js/headless-components /article
- https://github.com/TBear79/headless-datepicker
- https://github.com/hennessyevan/radform
- https://github.com/tonix-tuft/react-headless-components
  - /1Star/MIT/202007
  - Headless React UI components which can be used to build UI kits
  - 组件为空
- https://github.com/nikeshmhr/react-headless-ui-demo
  - Simple demo and WIP regarding concept of headless ui component library
  - 组件为空
- https://github.com/americanexpress/react-albus
  - building declarative multi-step flows (wizards)
- https://github.com/ianstormtaylor/react-values
  - components for handling state with render props.
- https://github.com/mohammedabualsoud/react-headless-table

- https://github.com/lxsmnsyc/solid-headless
  - Headless UI for SolidJS
