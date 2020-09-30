---
title: toc-github-repos-ui-components
tags: [components, github, toc]
created: '2020-09-28T17:05:16.252Z'
modified: '2020-09-28T17:05:48.422Z'
---

# toc-github-repos-ui-components

## framework-agnostic components

- 通用组件库
  - 组件库结构包括的通用的design tokens，通用的core，然后具体框架实现交互、样式更新、事件处理
    - core一般用来共享locale、theme、工具方法、类型定义
    - 实现方式1：vanilla js组件加上胶水层可移植到其他库
    - 实现方式2：各框架的组件单独实现
    - 实现方式3：web components，或类似api的库
  - 组件库参考
    - carbon-components: a collection of reusable HTML and SCSS partials
    - carbon-components-react: components implemented using React.
      - built React first. We also support core parts of the system in vanilla JS, Angular, and Vue. 
    - 只共用样式，组件分开实现，而不是简单wrapper，因为不同框架解决状态更新、数据同步、事件等的方案不同
    - 选用已有框架的重要原因是借用成熟的状态、事件、路由等解决方案
    - 最新的web components和stencil再等等看
      - web components本身就是一个runtime，特别适合替代vue/react的runtime
      - web components难以替代其他框架，因为这些框架的目标不止浏览器环境，还支持native、ssr
  - ref
    - https://github.com/jaywcjlove/awesome-uikit

- https://github.com/winjs/winjs
  - build applications using HTML/JS/CSS technology
  - /4kStar/MIT/201809
  - https://github.com/winjs/react-winjs
    - A React wrapper around WinJS's controls.
- https://github.com/IgniteUI/ignite-ui
  - /464Star/Apache2.0/202007
  - Ignite UI for jQuery is built on jQuery and jQuery UI 
  - https://github.com/IgniteUI/igniteui-react-wrappers
    - ignite UI components for React. 
    - 基于createReactClass批量生成，依赖jquery
- https://github.com/phonon-framework/phonon
  - /421Star/MIT/202004
  - responsive front-end framework with a focus on flexibility in Sass and TS
- https://github.com/Tradeshift/tradeshift-ui
  - /33Star/Free4PlatformOnly/202009  
  - a framework-agnostic JavaScript library to provide reusable UI components.
- https://github.com/ksc-fe/kpc
  - /214Star/MIT/202009
  - A UI Components Library for Intact, Vue, React and Angular.
  - kpc是基于intact框架实现的js组件库，然后通过胶水层自动生成react/vue/angular的组件
  - https://github.com/Javey/intact /46Star/MIT/202006
    - An inheritable and strong logic template front-end mvvm framework
    - 基于vdt，vdt是基于虚拟DOM实现的模板引擎，支持前后端渲染
  - https://github.com/ksc-fe/intact-react
    - A compatibility layer for running intact component in react
    - intact提供了react、vue、angular的胶水层
  - https://github.com/Javey/vdt.js
    - A powerful template engine based on virtual dom
    - 基于misstime(a virtual-dom lib forked from inferno and inspired by virtual-dom)
- https://github.com/coreui/coreui
  - built on top of Bootstrap 4 and plain JS without any additional libs like jQuery
  - https://github.com/coreui/coreui-react
    - Components built from scratch as true React hook components, without jQuery and unneeded dependencies.
    - 依赖popperjs、Tippy.js(tooltip,popover)
- https://github.com/GoldWorker/SluckyUI
  - /16Star/Apache2.0/202001
  - 所有组件使用纯css去实现，以最小代价进行二次开发成各个框架的组件库，如React，Angular，Vue


 

- https://github.com/jeric17/arv
  - /18kStar/MIT/202007
  - A custom-element(shadowdom) UI library
  - Inspired by Material-ui library, made with Stencil
- https://github.com/shoelace-style/shoelace
  - /4.1kStar/MIT/202009
  - Components are built with Stencil, a compiler that generates standards-based web components.
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
- https://github.com/vasturiano/kapsule
  - A closure based Web Component library
  - https://github.com/vasturiano/react-kapsule
    - React wrapper for kapsule-style web components

 

- https://github.com/shipshapecode/shepherd
  - a JavaScript library for guiding users through your app. It uses Popper.js
  - https://github.com/shipshapecode/react-shepherd
  - a React wrapper for the Shepherd
- https://github.com/usablica/intro.js
  - Better introductions for websites and features with a step-by-step guide
  - https://github.com/HiDeoo/intro.js-react
  - A small React wrapper around Intro.js.
- https://github.com/stripe/stripe-js
  - Use Stripe.js as an ES module. JavaScript library for building payment flows.
  - https://github.com/stripe/react-stripe-elements
  - React components for Stripe.js and Stripe Elements

- more
  - https://github.com/audi/audi-ui
    - Audi UI components in CSS, Vanilla JavaScript, and HTML
  - https://github.com/DavidVujic/vanillajs-components
    - examples on how to create a web site with reusable building blocks (aka components)
  - https://github.com/amazeui/amazeui
    - https://github.com/amazeui/amazeui-react
  - https://github.com/final-form/final-form
    - Framework agnostic, high performance, subscription-based form state management
  - https://github.com/davatron5000/awesome-standalones
    - A curated list of awesome framework-agnostic standalone web components
  - https://github.com/Wildhoney/Standalone
    - /205Star/MIT/201609
    - using the HTML5 custom elements API to extend HTML's vocabulary.
  - https://storybook.js.org/
    - Interactive UI component dev & test: React, React Native, Vue, Angular
  - https://github.com/uswds/uswds

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

- https://github.com/microsoft/fast
  - /4.8kStar/MIT/202009
  - FAST is a collection of technologies built on Web Components and modern Web Standards
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
  - https://github.com/adobe/coral-spectrum
    - A JavaScript library of Web Components following Spectrum design patterns.
    - Coral Spectrum derives from Custom Elements v1 with native support 
    - https://github.com/adobe/spectrum-css
