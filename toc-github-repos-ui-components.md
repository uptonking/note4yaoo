---
title: toc-github-repos-ui-components
tags: [components, github, toc]
created: '2020-09-28T17:05:16.252Z'
modified: '2020-09-28T17:05:48.422Z'
---

# toc-github-repos-ui-components

## framework-agnostic components

- 通用组件库
  - 结构一般包括的通用的design tokens，通用的core，然后具体框架实现交互与样式更新
  - 组件库参考
    - carbon-components: a collection of re-usable HTML and SCSS partials for building products
    - carbon-components-react: A collection of Carbon Components implemented using React.
      - built React first. We also support core parts of the system in vanilla JS, Angular, and Vue. 
    - 只共用样式，组件分开实现，而不是简单wrapper，因为不同框架解决状态更新、数据同步、事件等的方案不同
  - ref
    - [Wrap a Vanilla JavaScript Package for Use in React](https://www.digitalocean.com/community/tutorials/wrap-a-vanilla-javascript-package-for-use-in-react)

- https://github.com/Tradeshift/tradeshift-ui
  - /33Star/Free4PlatformOnly/202009  
  - a framework-agnostic JavaScript library to provide reusable UI components.
- https://github.com/jeric17/arv
  - /18kStar/MIT/202007
  - A custom-element(shadowdom) UI library
  - Inspired by Material-ui library, made with Stencil
- https://github.com/shoelace-style/shoelace
  - /4.1kStar/MIT/202009
  - Components are built with Stencil, a compiler that generates standards-based web components.
- https://github.com/final-form/final-form
  - Framework agnostic, high performance, subscription-based form state management
- more
  - https://github.com/davatron5000/awesome-standalones
    - A curated list of awesome framework-agnostic standalone web components
  - https://github.com/Wildhoney/Standalone
    - /205Star/MIT/201609
    - using the HTML5 custom elements API to extend HTML's vocabulary.

- https://github.com/firebase/firebaseui-web/
  - /3.1kStar/Apache2.0/202007
  - provides UI bindings on top of Firebase SDKs to eliminate boilerplate code 
  - https://github.com/firebase/firebaseui-web-react
    - React Wrapper for firebaseUI Web

- https://github.com/material-components/material-components-web/
  - /14.9kStar/MIT/202009
  - Modular and customizable Material Design UI components for the web
  - https://github.com/jamesmfriedman/rmwc
    - a React UI Kit built on Google's official Material Components Web library v5

- https://github.com/SAP/ui5-webcomponents
  - /787Star/Apache2.0/202009
  - the enterprise-flavored sugar on top of native APIs
  - https://github.com/SAP/openui5
    - based on JavaScript, using jQuery as its foundation and follows web standards
  - https://github.com/SAP/ui5-webcomponents-react
    - A wrapper implementation for React of the UI5 Web Components

- more
  - https://github.com/audi/audi-ui
    - Audi UI components in CSS, Vanilla JavaScript, and HTML
  - https://github.com/DavidVujic/vanillajs-components
    - examples on how to create a web site with reusable building blocks (aka components)
  - https://github.com/amazeui/amazeui
    - https://github.com/amazeui/amazeui-react

## headless-ui

- guide
  - 有状态无渲染，有渲染无状态，且状态尽量与具体业务解耦，状态逻辑尽量通用，这也是hooks设计的思路
  - I wonder... should these be called ui patterns rather than components.

- https://github.com/downshift-js/downshift
  - A set of primitives to build simple, flexible, WAI-ARIA compliant React autocomplete, combobox or select dropdown components. 
- https://github.com/tailwindlabs/headlessui
  - /992Star/MIT/202009
  - unstyled, fully accessible UI components, designed to integrate beautifully with Tailwind CSS
  - still in early development
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

- more
  - https://github.com/jxom/awesome-react-headless-components
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

## web-components

- https://github.com/riot/riot
  - /14.3kStar/MIT/202009/js
  - component-based UI library，Riot.js is Web Components for everyone.
  - Riot.js brings custom elements to all modern browsers without the use of any polyfill!
- https://github.com/Tencent/omi
  - /11.4kStar/MIT/202009
  - Merge Web Components, JSX, Virtual DOM, Functional style, observe or Proxy into one framework
- https://github.com/OnsenUI/OnsenUI
  - /8.1kStar/Apache2.0/202009
  - Based on Web Components, and provides bindings for Angular 1, 2, React and Vue.js.
- https://github.com/Gomah/bulmil
  - /68Star/MIT/202009
  - An agnostic UI components library based on Web Components, made with Bulma & Stencil.
- https://github.com/BlazeSoftware/atoms
  - a set of web components powered by Blaze CSS.
- https://github.com/SAP/ui5-webcomponents
  - UI5 Web Components
- https://github.com/salesforce/lwc
  - Enterprise-Grade Web Components Foundation
- more
  - Vaadin components are built on the Web Components standard.
  - https://github.com/Wildhoney/ReactShadow
    - Utilise Shadow DOM in React with all the benefits of style encapsulation
  - https://github.com/reactive-elements/reactive-elements
    - /700Star/MIT/201908
    - Allows to use React.js component as HTML element (web component)
