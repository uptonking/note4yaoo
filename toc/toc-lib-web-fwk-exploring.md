---
title: toc-lib-web-fwk-exploring
tags: [exploring, framework, lib, web]
created: 2020-11-09T09:04:03.243Z
modified: 2020-12-31T17:05:37.410Z
---

# toc-lib-web-fwk-exploring

# trending

- crank /2.2kStar/MIT/202011/ts/NoDeps
  - https://github.com/bikeshaving/crank
  - Crank uses the same JSX syntax and diffing algorithm popularized by React, allowing you to write HTML-like code directly in JavaScript.
  - All components in Crank are just functions or generator functions. 
  - No classes, hooks, proxies or template languages are needed.
  - Crank provides first-class support for promises. 
  - The core renderer can be extended to target alternative environments such as WebGL libraries, terminals, smartphones or smart TVs.
  - [如何看待 Crank 这个前端框架？](https://www.zhihu.com/question/388457689)
    - 这个框架的源码实现，很一般，基本的更新算法都木有
    - 组件的异步处理方式，无论是 react 的 Suspense 还是 crank 的 async generator，甚至是 vue3 的 suspense（async setup）
      - 都是对异步组件的处理方式，Suspense 之所以更加讨人欢喜不是因为它找到了一个安全的异步处理方式，而是它带来的一种【调度理念】
    - generator 是不好的异步方案
    - 违背了不可变和纯函数的原则

- DataFormsJS /80Star/MIT/202011/js
  - https://github.com/dataformsjs/dataformsjs
  - https://www.dataformsjs.com
  - A minimal JS Framework and standalone components for rapid development of single page applications.
  - 支持react, vue, handlebars, graphql
  - A tiny browser-based JSX Compiler is also included as part of this Framework.
  - A few of the reasons for fast development include displaying JSON services using only Markup and Templating (Handlebars, Underscore, etc.) and defining App and Site features using HTML attributes and small JavaScript Plugins.
  - Now that both React and Vue have become very popular. 
    - separate React Components have been developed to help with React Development 
    - and the Framework has been expanded to support Vue. 
    - Additionally separate Web Components have been developed to allow for similar functionality in modern browsers without using a JavaScript framework.

- solid /4.4kStar/MIT/202011/ts
  - https://github.com/ryansolid/solid
  - Solid is a declarative JavaScript library for creating user interfaces. 
  - It does not use a Virtual DOM. 
  - Instead it opts to compile its templates down to real DOM nodes and wrap updates in fine grained reactions. 
  - This way when your state updates only the code that depends on it runs.

 

```JS
import { createState, onCleanup } from "solid-js";

const CountingComponent = () => {
  const [state, setState] = createState({ counter: 0 });

  const interval = setInterval(
    () => setState({ counter: state.counter + 1 }),
    1000
  );

  onCleanup(() => clearInterval(interval));

  return <div>{ state.counter }</div>;
};
```

# rust-web
- https://github.com/tokio-rs/axum /13kStar/MIT/202311/rust
  - https://docs.rs/axum
  - modular web framework built with Tokio, Tower, and Hyper
  - Take full advantage of the tower and tower-http ecosystem of middleware, services, and utilities.
  - what sets axum apart from other frameworks: axum doesn't have its own middleware system but instead uses `tower::Service`.
  - axum is a relatively thin layer on top of hyper and adds very little overhead. So axum's performance is comparable to hyper.

- https://github.com/DioxusLabs/dioxus /MIT/202403/rust
  - https://dioxuslabs.com/
  - Dioxus is a portable, performant, and ergonomic framework for building cross-platform user interfaces in Rust.
  - React-like GUI library for desktop, web, mobile, TUI, and more.
  - Desktop apps running natively (no Electron!) in less than 10 lines of code.
  - First-class async support with coroutines and suspense
  - Web: Render directly to the DOM using WebAssembly

- https://github.com/leptos-rs/leptos /MIT/202403/rust
  - https://leptos.dev/
  - fast web applications with Rust
  - can be used to build apps that run in the browser (client-side rendering), on the server (server-side rendering), or by rendering HTML on the server and then adding interactivity in the browser (server-side rendering with hydration)
  - 🆚️ How is this different from Dioxus?
    - While Dioxus has a performant virtual DOM (VDOM), it still uses coarse-grained/component-scoped reactivity
    - Leptos components use a different mental model, creating (and returning) actual DOM nodes and setting up a reactive system to update those DOM nodes.
    - Dioxus uses Leptos server functions in its fullstack mode, but does not have the same `<Suspense>`-based support for things like streaming HTML rendering
    - Leptos tends to prioritize holistic web performance (streaming HTML rendering, smaller WASM binary sizes, etc.), whereas Dioxus has an unparalleled experience when building desktop app
  - 🆚️ How is this different from Sycamore?
    - Sycamore and Leptos are both heavily influenced by SolidJS. 
    - At this point, Leptos has a larger community 
    - Sycamore uses a custom templating language for its views, while Leptos uses a JSX-like template format.
# web-comp
- https://github.com/lume/element /MIT/202404/ts
  - https://lume.io/
  - Easily create Custom Elements with simple templates and reactivity. 
  - This is an alternative to Lit, Stencil, and Fast.
# web-ui-framework
- https://github.com/nanojsx/nano /MIT/202401/ts
  - http://nanojsx.io/
  - SSR first, lightweight 1kB JSX library.
  - Partial Hydration: Hydrate and only the parts you really need
  - Pre-Rendering: Renders your app to static html if you want. This is possible, but requires some knowledge.
  - Uses Tagged Templates instead of JSX if you prefer
  - Prefetch: Use the built-in Link Component

- https://github.com/luwes/sinuous
  - /710Star/MIT/202010/js
  - no compile step needed, choose your view syntax.
  - A goal Sinuous strives for is to have good interoperability. 
  - Sinuous creates DOM elements via hyperscript `h` calls. 
  - This allows the developer more freedom in the choice of the view syntax.
  - The Sinuous `observable` module provides a mechanism to store and update the application state in a reactive way. 

- https://github.com/hyperhype/hyperscript /201901/js/inactive
  - Create HyperText with JavaScript, on client or server.
  - https://github.com/Raynos/mercury
    - a modular ui framework influenced by hyperscript but much more heavily optimized.
    - mercury has some interesting ideas but they are not very practical at scale.

- https://github.com/optoolco/tonic
  - A Low Profile Component Framework. Minimal, Auditable, and Build-Tool-Free.
  - Tonic is a thin wrapper around web components

- https://github.com/marko-js/marko
  - A declarative, HTML-based language that makes building web apps fun
  - Marko extends the HTML language to allow building modern applications in a declarative way.
  - Among these extensions are conditionals, lists, state, and components

- https://github.com/flowxjs/typeclient
  - https://flowxjs.github.io/TypeClient/
  - 在后端开发的模型中，多个client应对单个server的模型给了我们很大灵感。
    - 在前端，无非就是单个client应对单个server的情况，那么我们就可以将后端的理念移植到前端。
    - 非常幸运的是，后端触发请求流转的事件也可以对应到前端，所以我们可以认为，用户的页面请求就是一个相对于后端的request请求
  - 为了将请求处理逻辑解偶，我们采用了AOP和iOC理念来作为这个架构的基础设计，在代码层面上可以实现几乎类似JAVA注解的模式。
    - 再加上将前端各大框架作为渲染引擎，一个完整的架构设计就出来了。
  - 采用了第三方开源的架构inversify实现ioc
# more-web-framework
- https://github.com/gimenete/ui-state-sync
  - DIY modern JavaScript framework based on Virtual DOM
- https://github.com/corpusculejs/corpuscule
  - a set of libraries built on top of Web Components standard. 
  - It provides all necessary tools to built whole application from scratch including redux connector, router and form utils.
- https://github.com/fanduel-oss/refract
  - Handle your component effects and side-effects in a clear and declarative fashion by using asynchronous data streams (reactive programming).
  - Refract makes reactive programming possible in React, React Native, Preact and Inferno, with only a single higher-order component or a single hook

- https://github.com/gimenete/unicycle
  - Unicycle is an Electron application built using TypeScript, React and ant.design. 
  - Its purpose is to unify the design/development cycle.
  - Unicycle allows you to create, live edit and test presentational components and export them to different frameworks (React and Vue.js by now). 
- https://github.com/MithrilJS/mithril.js /202307/js
  - client-side JS framework for building Single Page Applications. 
  - It's small (9.79 KB gzipped), fast and provides routing and XHR utilities out of the box.
  - used by companies like Vimeo and Nike
  - [Framework comparison](https://mithril.js.org/framework-comparison.html)
    - Why use Mithril? In one sentence: because Mithril is pragmatic
      - Mithril is all about getting meaningful work done efficiently. 
      - No extra libraries, no magic.
