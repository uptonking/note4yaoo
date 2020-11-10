---
title: toc-lib-web-framework
tags: [framework, lib, web]
created: '2020-11-09T09:04:03.243Z'
modified: '2020-11-09T09:04:58.539Z'
---

# toc-lib-web-framework

## trending

### DataFormsJS

- DataFormsJS /80Star/MIT/202011/js
  - https://github.com/dataformsjs/dataformsjs
  - https://www.dataformsjs.com
  - A minimal JS Framework and standalone components for rapid development of single page applications.
  - 支持react, vue, handlebars, graphql
  - A few of the reasons for fast development include displaying JSON services using only Markup and Templating (Handlebars, Underscore, etc.) and defining App and Site features using HTML attributes and small JavaScript Plugins.
  - Now that both React and Vue have become very popular. 
    - separate React Components have been developed to help with React Development 
    - and the Framework has been expanded to support Vue. 
    - Additionally separate Web Components have been developed to allow for similar functionality in modern browsers without using a JavaScript framework.

### SolidJS

- solid /4.4kStar/MIT/202011/ts
  - https://github.com/ryansolid/solid
  - Solid is a declarative JavaScript library for creating user interfaces. 
  - It does not use a Virtual DOM. 
  - Instead it opts to compile its templates down to real DOM nodes and wrap updates in fine grained reactions. 
  - This way when your state updates only the code that depends on it runs.
  - [Introducing the SolidJS UI Library_202003](https://dev.to/ryansolid/introducing-the-solidjs-ui-library-4mck)

``` JS
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

## web-ui-framework

- https://github.com/flowxjs/typeclient
  - https://flowxjs.github.io/TypeClient/
  - 在后端开发的模型中，多个client应对单个server的模型给了我们很大灵感。
    - 在前端，无非就是单个client应对单个server的情况，那么我们就可以将后端的理念移植到前端。
    - 非常幸运的是，后端触发请求流转的事件也可以对应到前端，所以我们可以认为，用户的页面请求就是一个相对于后端的request请求
  - 为了将请求处理逻辑解偶，我们采用了AOP和iOC理念来作为这个架构的基础设计，在代码层面上可以实现几乎类似JAVA注解的模式。
    - 再加上将前端各大框架作为渲染引擎，一个完整的架构设计就出来了。
  - 采用了第三方开源的架构inversify实现ioc

## more-web-framework

- https://github.com/corpusculejs/corpuscule
  - a set of libraries built on top of Web Components standard. 
  - It provides all necessary tools to built whole application from scratch including redux connector, router and form utils.
