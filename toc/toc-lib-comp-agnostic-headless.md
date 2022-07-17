---
title: toc-lib-comp-agnostic-headless
tags: [components, headless, toc]
created: 2021-04-11T06:17:15.216Z
modified: 2021-04-11T06:17:51.318Z
---

# toc-lib-comp-agnostic-headless

# guide

- 有状态无渲染，有渲染无状态，且状态尽量与具体业务解耦，状态逻辑尽量通用，这也是hooks设计的思路
- headless, renderless, no styling, unstyled, accessible
- I wonder... should these be called ui patterns rather than components.

- headless-ui-examples
  - headlessui
    - listbox/select,dropdown/menu,switch,radio-group
    - dialog,popover,disclosure,transition
    - 示例组件的动画体验非常好
  - react-spectrum
    - based on react-stately,react-aria
  - radix-ui
    - 提供了自研stitches的样式解决方案
  - renderlesskit-react
    - 依赖reakit,react-aria,chakra-ui
  - reakit/ariakit
    - who is using: bumbag-ui
  - reach-ui
  - react-containers: 有2种使用方式: hook, render prop
  - downshift
  - react-bootstrap依赖的restart/hooks
# popular-headless-ui
- https://github.com/tailwindlabs/headlessui
  - /992Star/MIT/202009
  - unstyled, fully accessible UI components, designed to integrate beautifully with Tailwind CSS
  - [Headless UI: Unstyled, Accessible UI Components](https://blog.tailwindcss.com/headless-ui-unstyled-accessible-ui-components)
  - [@headlessui/react](https://github.com/tailwindlabs/headlessui/tree/main/packages/%40headlessui-react), @headlessui/vue
  - https://github.com/GavinJoyce/ember-headlessui
    - a work-in-progress implementation of: tailwindlabs/headlessui
- https://github.com/timelessco/renderlesskit-react
  - https://renderlesskit-react.vercel.app/
  - Collection of headless components/hooks that are accessible, composable, customizable from low level to build your own UI & Design System powered by Reakit System.
- https://github.com/zendeskgarden/react-containers
  - https://github.com/zendeskgarden/react-components
  - https://garden.zendesk.com/components/
  - /873Star/Apache2/202105/ts
  - 依赖styled-components
  - Garden React provides consistent styling and behavior for Garden components. 

- makeup-js /7Star/MIT/202105/js
  - https://github.com/makeup/makeup-js
  - https://makeup.github.io/makeup-js/
  - A suite of vanilla JavaScript modules for building accessible user interfaces.
  - (i.e. they come with no styles or branding out of the box).
  - They are fully compatible with Skin CSS.
  - https://github.com/eBay/skin
    - https://ebay.github.io/skin/
    - Pure CSS framework designed & developed by eBay

- https://github.com/ueberdosis/tiptap
  - https://tiptap.dev/
  - A headless, framework-agnostic and extendable rich text editor, based on ProseMirror.
- https://github.com/jieter/leaflet-headless
  - Leaflet for node.(Has Leaflet 1.1.x as dependency.)
  - Uses jsdom to fake ad DOM.
  - Uses Image implementation and canvas from node-canvas. 
  - Tiles, Markers and vector layers work well with leaflet-image
- https://github.com/atomiks/tippyjs
  - https://atomiks.github.io/tippyjs/
  - 只依赖 @popperjs/core.v2
  - Tippy.js is the complete tooltip, popover, dropdown, and menu solution for the web, powered by Popper.
  - "Headless Tippy" refers to Tippy without any of the default element rendering or CSS. 
    - This allows you to create your own element from scratch and use Tippy for its logic only.
- https://github.com/elastic/search-ui
  - https://github.com/elastic/search-ui/tree/master/packages/search-ui
  - 依赖date-fns、history、qs
  - The "Headless Search UI" that serves as a foundation for the react-search-ui library.
- https://github.com/algolia/autocomplete
  - https://www.algolia.com/doc/ui-libraries/autocomplete/introduction/what-is-autocomplete/
  - JavaScript library for building autocomplete experiences.
  - The data that populates the autocomplete results are called sources. 
  - You can use whatever you want in your sources: a static set of searches terms, search results from an external source like an Algolia index, recent searches, and more.
  - The library creates an input and provides the interactivity and accessibility attributes, but you’re in full control of the DOM elements to output.
  - Unlike InstantSearch, Autocomplete doesn’t provide a library of ready-made UI widgets
- https://github.com/TBear79/headless-datepicker
  - Provides the logic for a datepicker. Apply your own UI on top.
  - Relies on moment.js

- https://github.com/downshift-js/downshift
  - /8.7kStar/MIT/202009
  - A set of primitives to build simple, flexible, WAI-ARIA compliant React autocomplete, combobox or select dropdown components.
- https://github.com/formium/formium
  - https://formium.io/
  - Formium is an API-first, headless online form builder and automation tool
  - In addition to hosting forms and surveys on formium.io, you can use your own React components to natively render your forms and surveys in your existing apps 
  - 依赖 formik
  - https://github.com/formium/formik
    - Formik is the world's most popular open source form library for React and React Native.
- https://github.com/ivan-dalmet/formiz
  - https://formiz-react.com/
  - React forms with ease! Composable, headless & with built-in multi steps
- accessible-ui /inactive
  - https://github.com/accessible-ui
  - Accessible style-agnostic components for React

- https://github.com/jshjohnson/Choices
  - https://joshuajohnson.co.uk/Choices/
  - configurable select box/text input plugin.
  - Similar to Select2 and Selectize but without the jQuery dependency.
  - Flexible styling
# framework-agnostic
- https://github.com/appbaseio/searchbox
  - https://github.com/appbaseio/searchbox
  - a lightweight and performance focused search UI component library to query and display results from your ElasticSearch index using declarative props. 
  - It's available for React, Vue, React Native and Flutter.
- https://github.com/appbaseio/reactivesearch
  - https://opensource.appbase.io/reactivesearch
  - Search UI components for React and Vue: powered by appbase.io / Elasticsearch
- https://github.com/appbaseio/reactivecore
  - Core architecture of reactive UI libraries
  - 依赖redux、redux-thunk、xdate
# headless-based-on-browser-puppeteer
- https://github.com/PDFTron/web-to-pdf
  - Convert any web technology to PDF (HTML to PDF, html2pdf)
  - 依赖chokidar、live-server、passport、puppeteer、react
  - Please note that React components are not required for web-to-pdf to work. It supports all frameworks, and even vanilla JS/HTML/CSS.
# headless-react
- https://github.com/chatscope/use-chat
  - https://chatscope.io/
  - React hook for state management in chat applications.
  - This is a headless chat library. Think of it as something like a Formik but for chat apps.
  - https://github.com/chatscope/chat-ui-kit-react
- https://github.com/Resetand/textarea-markdown-editor
  - UI headless simple markdown editor using only textarea
  - You can choose any markdown parser, any layout.
  - Can use any existing textarea Component and style it as you prefer

- https://github.com/nrkno/core-components
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
- https://github.com/Buuntu/react-final-table
  - /9Star/MIT/202009
  - A headless UI component libray for managing complex table state in React.
  - Inspired by react-table but with Typescript support built in and a simpler API.
- https://github.com/Zertz/react-headless-tabs
  - Headless, simple, and highly flexible tab-like primitives built with react hooks
- https://github.com/headless-components/headless-components-react
  - /2Star/NALic/202004
  - Headless component in React with Custom hooks
# more-headless-ui
- ref
  - https://github.com/jxom/awesome-react-headless-components

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
