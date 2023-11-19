---
title: toc-lib-comp-agnostic
tags: [components, lib, toc]
created: 2020-09-28T17:05:16.252Z
modified: 2020-11-13T07:28:27.824Z
---

# toc-lib-comp-agnostic

# guide

- framework-agnostic的实现思路
  - 基于css，但未解决a11y
  - 基于web-components，但仍未解决状态与视图的同步问题

- 没必要执着于render agnostic
  - 具体场景需求不同，如ui组件、图表、动画
  - 考虑和现有资源集成的场景，如figma、tldraw、excalidraw
  - 跨平台的差异，考虑拖拽、弹层
  - react-canvas/webgl，在一定程度也是将vdom渲染到不同平台

- refs
  - https://github.com/SaraVieira/ui-libraries /组件库对比
# framework-agnostic components
- https://github.com/dmitriz/un /202304/js
  - Unframework for Universal Uncomponents
  - We do not think in terms of reusable components. Instead, we focus on reusable functions.
  - Write your business logic as pure functions with no external dependencies
  - Why "uncomponent"? Because there isn't really much of a "component", the `reducer` and the `view` are just two plain functions and the initial `state` is a plain value.
    - your simply import your favorite familiar libraries that you are already using anyway
  - Currently a single tiny factory function called `createMount`. Its role is similar to `React.render`.
  - Streams are in the core of un

- zag /1.5kStar/MIT/202210/ts/state-machine/panda-css
  - https://github.com/chakra-ui/zag
  - https://zagjs.com/overview/introduction
  - Finite state machines for accessible JavaScript components
  - The component interactions are modelled in a framework agnostic way. 
  - We provide adapters for JS frameworks like React, Solid, or Vue.
  - Zag.js (low-level state machine) => Ark (headless components) => Chakra (Ark + CSS-in-JS)
  - The machine APIs are completely unstyled and gives you the control to use any styling solution you prefer.
  - Zag is built on top of the latest ideas in Statecharts. We don't follow the SCXML specifications
  - https://github.com/chakra-ui/chakra-ui
    - [Roadmap - v3.0_2022-12-30](https://github.com/chakra-ui/chakra-ui/issues/7180)
    - excited to push all interactive components from Zag.js into Chakra UI in v4.
    - [The Future of Chakra UI in 4 parts_202102: styling build time, state-machine, a11y, motion](https://www.youtube.com/watch?v=I5xEc9t-HZg)

- papanasi /298Star/MIT/202211/ts
  - https://github.com/CKGrafico/papanasi
  - http://papanasi.js.org/
  - a UI library to use cross Frameworks. 
  - A set of components to use in Angular, Preact, Qwik, React, Solid, Svelte, Vue and Web Components. 
  - Is based on the `Mitosis` library 
  - https://github.com/BuilderIO/mitosis
    - Write components once, compile to every framework
    - While `Zag.js` focuses on writing framework-agnostic interactions, `Mitosis` focuses on writing framework-specific components.

- https://github.com/phonon-framework/phonon
  - /421Star/MIT/202004/ts/inactive
  - responsive front-end framework with a focus on flexibility in Sass and TS
  - theming基于sass vars
  - 提供了在react/vue(无angular)项目中使用phonon组件的示例
    - 可以使用css和dom标签，重新实现react组件，与js组件无关
    - 也可在react组件的didMount方法中，创建js组件对象，在render方法中给dom标签添加ref进行操作，而不是`return null`
  - Phonon uses a DOM MutationObserver which enables to react to DOM changes
    - This explains the ease of use of Phonon with Angular, React and Vue, etc
    - 默认根据样式名绑定js逻辑，如className='modal'

- https://github.com/material-components/material-components-web/
  - /14.9kStar/MIT/202009/ts/agnostic/MDC-Web
  - https://material.io/develop/web/components/buttons
  - 此架构在升级material-ui.v3的过程中被抛弃，v3强推lit组件库
  - Modular and customizable Material Design UI components for the web
  - [MDC Foundation Proposal](https://gist.github.com/jamesmfriedman/33c750912698f20aa9d4dda9df834e5d)
  - [Material 3 support](https://github.com/material-components/material-components-web/issues/7560)
    - this one (material-components-web) is written in plain TypeScript and the material-web is using the Lit Framework 
  - https://github.com/jamesmfriedman/rmwc
    - /1.4kStar/MIT/202009/ts/hooks
    - a React UI Kit built on Google's official Material Components Web library v5
  - ref
    - https://github.com/material-components/material-components-web-react
      - /1.9kStar/MIT/201911/ts/deprecated
      - deprecated in order to increase our focus on implementing the core, framework-independent libraries (MDC-Web and MWC)
      - 基于class组件实现
    - https://github.com/material-components/material-components-web-components
      - /2.2kStar/Apache2/202009/ts/agnostic/MWC
      - a collection of Web Components maintained by Google that implement Material Design
    - https://github.com/prateekbh/preact-material-components
      - /531Star/MIT/202007/ts/deprecated
      - preact wrapper for material-components-web
    - https://github.com/material-components/material-components-android
      - /11.2kStar/Apache2/2020209/java
      - Modular and customizable Material Design UI components for Android

- https://github.com/DouyinFE/semi-design
  - https://semi.design/zh-CN/start/overview
  - 得益于 Foundation/Adapter 架构设计以及样式文件分层原则，Semi 非常易于迁移到其他前端框架
  - [Semi Design 设计系统管理](https://semi.design/dsm/landing)
    - 支持在线定制基于semi-design的主题样式，并发布npm包
  - [Semi Design - UI组件库如何分层设计，使其具备适配多种mvvm框架能力](https://bytedance.feishu.cn/wiki/wikcnOVYexosCS1Rmvb5qCsWT1f)
  - [希望官方支持 Vue 版本](https://github.com/DouyinFE/semi-design/issues/311)
    - 我们的工作重点依然是React体系。没有计划去重新实现一个Vue版本

- https://github.com/carbon-design-system/carbon
  - /3.5kStar/Apache2/202009/js
  - carbon-components: Component styles and Vanilla JavaScript
  - carbon-components-react: 基于class组件实现
  - @carbon/elements: IBM Design Language elements like colors, type, iconography, and more

- easy-canvas /555Star/MIT/202208/js/NoDeps
  - https://github.com/Gitjinfeiyang/easy-canvas
  - https://gitjinfeiyang.github.io/easy-canvas/example/ui.html
  - 使用render函数在canvas中创建文档流布局，海报图、小程序朋友圈分享图。
  - 支持文档流，参照 web，无需设置 x、y 以及宽高
  - 支持组件化，全局组件以及局部组件
  - 高性能，scroll-view 支持脏矩形，只绘制可视部分
  - 支持操作 element，类似操作 dom 修改文档流
  - [easyCanvas实现原理解析](https://juejin.im/post/6871124987550531592)
  - 之前做dom截图用过 html2canvas 发现太慢了，然后换成 dom-to-image 好很多。foreignObject 是真香啊
  - https://github.com/Gitjinfeiyang/vue-easy-canvas
    - 将 easy-canvas 封装成vue组件进行使用 注意：内部实现是将vue节点转换成目标节点，转换过程中会有性能损失，渲染与转换时间大概4:1

- https://github.com/AgnosticUI/agnosticui
  - https://agnosticui.github.io/agnosticui
  - /3Star/Apache2/202101/js
  - 主要是复用css，组件逻辑并未复用
  - an agnostic UI component library prioritizing clean HTML and CSS, but built to agnostically work with many popular JavaScript frameworks
  - the philosophy of AgnosticUI is to curate the top-level component.html and component.css, and then to synchronize the css down into the framework-based variants. 
    - This is done via a simple Node script which literally copies the CSS over.
    - The above approach forces our framework-specific implementations to use the same single stylesheet. 

- https://github.com/stacksjs/stacks
  - https://stacksjs.dev/
  - The goal of the framework is to help you create & maintain frontends, backends, and clouds
  - Because Stacks optimizes the development of easily reusable & composable component & function libraries, the primary intention is to always keep it simple, yet configurable.
  - After you installed your Stacks generated library, you can use a "Custom Element" (Web Component)

- Reef /631Star/MIT/202010/js/NoDeps
  - https://github.com/cferdinandi/reef
  - https://reefjs.com/
  - A lightweight library for creating reactive, state-based components and UI. 
  - Reef is a simpler alternative to React, Vue, and other large frameworks.

- https://github.com/prasannavl/icomponent
  - /28Star/MIT/201902/ts
  - 只提供了一致的接口和架构，没有实现具体组件
  - A super simple, render-agnostic component library for the modern web that emphasizes framework and renderer freedom
  - icomponent provides the web component model. 
  - So, you can easily do things like these by just writing your own render functions

- tradeshift-ui /33Star/lic/202009/js/deprecated
  - https://github.com/Tradeshift/tradeshift-ui
  - a framework-agnostic JavaScript library to provide reusable UI components.
  - Check out Tradeshift new Web Component-powered UI library Elements.
  - https://github.com/Tradeshift/react-tradeshift-ui
    - https://github.com/jinglongchenTS/react-tradeshift-ui
    - React wrappers for the Tradeshift ui components.
    - 大部分class组件的render方法都是`return null`，完全通过js操作dom
    - tradeshift对象会被添加到window，然后在didUpdate方法中创建并操作dom
  - https://github.com/Tradeshift/elements /lit2
    - Reusable Tradeshift UI Components as Web Components

- https://github.com/adbayb/poc-cross-framework-component
  - experiment several approaches to implement cross-framework components.
  - Three approaches have been tested
    - Wrapper (top-down runtime approach): packages existing framework dependent components with a thin interoperability layer 
    - Primitive (bottom-up runtime approach): framework agnostic low-level building blocks.Each primitive acts as an adapter to plug framework dependent logic.
    - Compiler (build time approach): Use a build tool to generate, from a single source code, either web component (eg. via Stencil) or per framework implementations (eg. via Mitosis).
# adapters
- https://github.com/plantain-00/schema-based-json-editor
  - https://plantain-00.github.io/schema-based-json-editor/packages/react/demo/
  - A reactjs and vuejs component of schema based json editor.

- https://github.com/plantain-00/tree-component
  - https://plantain-00.github.io/tree-component/packages/react/demo/
  - A reactjs and vuejs tree component.
  - drag and drop between different tree
  - composition model(reactjs children and vuejs slot)

- https://github.com/plantain-00/select2-component /ts
  - https://plantain-00.github.io/select2-component/packages/react/demo/
  - A vuejs and reactjs select component.
  - local search
  - multiple selection

- https://github.com/plantain-00/file-uploader-component
  - https://plantain-00.github.io/file-uploader-component/packages/react/demo/
  - A reactjs and vuejs component of file uploader.
  - drag file(s) and drop to the component
  - click to choose file(s)
  - paste file from clipboard
  - progress bar
# vanillajs
- https://github.com/thepassle/generic-components /js/inactive
  - A collection of generic web components with a focus on accessibility, and ease of use

- https://github.com/vitmalina/w2ui /202305/js
  - UI widgets for modern apps. 
  - Data table, forms, toolbars, sidebar, tabs, tooltips, popups. 
  - All under 120kb (gzipped).
  - Since v2.0, w2ui has no dependencies
  - All the widgets are written as es6 classes
  - All classes in w2ui are extended from w2base class that provides basic event functionality.
# css
- https://github.com/themesberg/flowbite /ts
  - https://flowbite.com/blocks/
  - UI components based on the utility-first Tailwind CSS framework featuring dark mode support, a Figma design system, templates, and more.
  - All of the elements are built using the utility classes from Tailwind CSS and vanilla JavaScript with support for TypeScript.
  - Flowbite also offers an API for using the components programmatically with vanillajs
# xplat-ios/android
- https://github.com/framework7io/framework7
  - open source mobile HTML framework to develop hybrid mobile apps or web apps with iOS & Android native look and feel.
  - Current documentation currently doesn't cover process of compilation of Framework7 app to Cordova app.
# more
- https://github.com/vicentedealencar/react-agnostic
  - you can write your components without any direct dependencies from platform specific components. 
  - It applies inversion of control using react context pass around components.
- https://github.com/IgniteUI/ignite-ui
  - /464Star/Apache2/202007/js
  - Ignite UI for jQuery is built on jQuery and jQuery UI 
  - https://github.com/IgniteUI/igniteui-react-wrappers
    - ignite UI components for React. 
    - 基于createReactClass批量生成，依赖jquery
- https://github.com/coreui/coreui /MIT
  - 依赖perfect-scrollbar, @popperjs/core
  - 提供了部分组件交互对应的js
  - built on top of Bootstrap 4 and plain JS without any additional libs like jQuery
  - CoreUI is the fastest way to build modern dashboard
  - https://github.com/coreui/coreui-react /MIT
    - 依赖coreui的css,react-router-dom,perfect-scrollbar,@popperjs/core、Tippy.js,classnames
    - 用react hooks重写实现组件，只复用css
    - CoreUI for React.js replaces and extends the Bootstrap javascript.
    - Components built from scratch as true React hook components, without jQuery and unneeded dependencies.
    - Components are styled using @coreui/coreui CSS, but you can use them also with bootstrap CSS
- https://github.com/GoldWorker/SluckyUI
  - /16Star/Apache2/202001
  - 理念是所有组件使用纯css去实现，以最小代价进行二次开发成各个框架的组件库
    - 但作者但实现，源码只是普通的react class组件
  - 提供了创建React，Angular，Vue组件的示例
- https://github.com/winjs/winjs
  - /4kStar/MIT/201809/js
  - build applications using HTML/JS/CSS technology. 
  - 文件模块使用的是google-closure-builder的模块系统
  - https://github.com/winjs/react-winjs
    - A React wrapper around WinJS's controls.
- https://github.com/ksc-fe/kpc
  - /214Star/MIT/202009
  - A UI Components Library for Intact, Vue, React and Angular.
  - kpc是基于intact框架实现的js组件库，通过胶水层自动生成react/vue/angular的组件
- https://github.com/Javey/intact /46Star/MIT/202006/js/inactive
  - An inheritable and strong logic template front-end mvvm framework
  - 基于vdt，vdt是基于虚拟DOM实现的模板引擎，支持前后端渲染
  - https://github.com/ksc-fe/intact-react
    - A compatibility layer for running intact component in react
    - intact提供了react、vue、angular的胶水层
  - https://github.com/Javey/vdt.js
    - A powerful template engine based on virtual dom
    - 基于misstime(a virtual-dom lib forked from inferno and inspired by virtual-dom)
- https://github.com/IBM/sterling-dataviz
  - /3Star/Apache2/201911/ts
  - A reusable framework-agnostic dataviz lib implemented using D3 & typescript
  - 支持react、vue、angular，基于胶水层实现

- https://github.com/SAP/ui5-webcomponents
  - /787Star/Apache2/202009/webcomp
  - the enterprise-flavored sugar on top of native APIs
  - https://github.com/SAP/openui5
    - based on JavaScript, using jQuery as its foundation and follows web standards
  - https://github.com/SAP/ui5-webcomponents-react
    - A wrapper implementation for React of the UI5 Web Components
    - 样式基于jss
    - 基于hooks实现
- https://github.com/jeric17/arv
  - /18kStar/MIT/202007/stencil
  - A custom-element(shadowdom) UI library
  - Inspired by Material-ui library, made with Stencil
- https://github.com/shoelace-style/shoelace
  - /4.1kStar/MIT/202009/stencil
  - built with Stencil, a compiler that generates standards-based web components.
- https://github.com/proyecto26/ion-phaser-ce
  - web component to use Phaser Framework Community Edition with Angular, React, Vue 
- https://github.com/vasturiano/kapsule
  - A closure based Web Component library
  - https://github.com/vasturiano/react-kapsule
    - React wrapper for kapsule-style web components
- https://github.com/krakenjs/zoid /js
  - Render an iframe or popup on a different domain, and pass down props
  - Call callbacks natively from the child window without worrying about post-messaging or cross-domain restrictions
  - Create and expose components to share functionality from your site to others!
  - zoid is framework agnostic.

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

- https://github.com/final-form/final-form /js
  - https://github.com/final-form/react-final-form
  - Framework agnostic, high performance, subscription-based form state management

- more
  - https://github.com/amazeui/amazeui
    - https://github.com/amazeui/amazeui-react
  - https://github.com/audi/audi-ui
    - Audi UI components in CSS, Vanilla JavaScript, and HTML
  - https://github.com/DavidVujic/vanillajs-components
    - examples on how to create a web site with reusable building blocks (aka components)

  - https://github.com/davatron5000/awesome-standalones
    - A curated list of awesome framework-agnostic standalone web components
  - https://github.com/Wildhoney/Standalone
    - /205Star/MIT/201609
    - using the HTML5 custom elements API to extend HTML's vocabulary.
  - https://storybook.js.org/
    - Interactive UI component dev & test: React, React Native, Vue, Angular
  - https://github.com/uswds/uswds
  - https://github.com/qlik-demo-team/qdt-components
    - 封装一个通过ReactDOM.render渲染出DOM节点的方法，每个单独的组件都会命令式地调用此方法渲染
    - React Components to be used with Angular 6, React 16 and Vue 2.

- [The Vanilla Javascript Component Pattern](https://dev.to/megazear7/the-vanilla-javascript-component-pattern-37la)
