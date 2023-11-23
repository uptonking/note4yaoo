---
title: pattern-arch-flux-examples-elm
tags: [elm, examples, flux, toc]
created: 2023-11-21T10:17:11.369Z
modified: 2023-11-21T10:17:34.596Z
---

# pattern-arch-flux-examples-elm

# guide

- tips
  - popular-elm: elmish, hyperapp, hydux, raj, apprun

- resources
  - [The Elm Architecture · An Introduction to Elm](https://guide.elm-lang.org/architecture/)
  - [Elmish · F#](https://elmish.github.io/elmish/)
# popular
- https://github.com/sporto/awesome-elm
  - useful Elm tutorials, libraries and software

- https://github.com/dwyl/learn-elm-architecture-in-javascript /201903/js/inactive
  - Learn how to build web apps using the Elm Architecture in "vanilla" JavaScript (step-by-step TDD tutorial)

- https://github.com/ccorcos/elmish /201601/js/支持undo/示例多
  - A Javascript UI library inspired by Elm
  - This is functional programming pattern inspired by the Elm Architecture for building user interfaces.
  - [Library status](https://github.com/ccorcos/elmish/issues/1)
    - master branch is "stable" but has some flaws that I've been trying to address, primarily having to do with large-scale performance.
  - [Elmish: Functional Programming in Javascript | by Chet Corcos | Medium_201602](https://medium.com/@chetcorcos/elmish-functional-programming-in-javascript-50995f1d4b9e)

- https://github.com/jonaskello/tea-minimal /202201/ts
  - Minimal The Elm Architecture implementation in typescript
  - https://github.com/andrejewski/raj/issues/31
    - I wrote something similar to raj in typescript and since then I have re-written that library several times as I needed to add more advanced stuff like GraphQL subscriptions, caching etc.
    - Now I've ended up with a library that is much closer to the original Elm Architecture. It uses managed effects which means commands and subscriptions that are declared as data and are handled by effect managers outside the application. This way the application can consist of only pure functions. 

- https://github.com/andrejewski/raj /MIT/201806/js
  - https://jew.ski/raj/
  - https://github.com/andrejewski/raj-by-example /使用说明
  - The Elm Architecture for JavaScript
  - 34 lines; 190 bytes minified. This framework can fit in your head or even a tweet.
  - view layer agnostic. The view is a side effect of state.
  - Raj applications are structured as programs. Every program begins with an initial state, which can be anything, and an optional effect.
  - "Effects" are functions which receive a function dispatch. Effects handle asynchronous work like data-fetching, timers, and managing event listeners
  - A "message" can be anything; a server response, the current time, even undefined.
  - The view is a special effect that receives both the current state and the dispatch function
  - Elm and Raj handle subscriptions and side-effects differently. 
    - In Raj any side-effect can be a subscription. 
    - In Elm there are commands (single dispatch) and subscriptions (multi-dispatch).
    - In Elm, the same subscription uses effect managers and requires help from the low-level Elm runtime to work. Elm's solution fits its language. The Raj solution fits JavaScript.
  - [Raj, the Elm Architecture for JavaScript, releases v1.0!_201806](https://www.reddit.com/r/javascript/comments/8st3bi/raj_the_elm_architecture_for_javascript_releases/)
    - I try to follow HyperApp closely. When it first came out I was so anxious that something had beaten Raj to the market.They are pretty different and I think HyperApp 2.0 will widened the gap
    - Raj is view-layer agnostic.HyperApp is doing it's own baked in thing
    - Raj has a huge value prop of forcing side-effects to the edges of your system. In HyperApp you have async actions which I don't care for. In Raj the nasty async bits do not "infect" the business logic.
  - https://github.com/andrejewski/raj-ts /202301/ts
    - Raj written in Typescript
    - Raj.ts re-packages the standard library of Raj packages in a single package
    - Besides a few minor renames, the documentation for Raj is applicable to Raj.ts.
  - https://github.com/andrejewski/raj-react-realworld /201806/js
    - demonstrate a fully fledged fullstack application built with React and Raj including CRUD operations, authentication, routing, pagination, and more.
  - https://github.com/andrejewski/raj-spa /201809/js
    - Single Page Applications for Raj
  - https://github.com/andrejewski/raj-compose
    - Program composition for Raj
- https://github.com/RonaldDijks/ts-elmish /201812/ts
  - A lightweight general purpose Elm-like runtime for TypeScript, based off of raj
  - view layer agnostic. Here we use the browser's built-in view to play the part
- https://github.com/Zhang-WJ/Elmish-with-javascript /202009/js
  - function UI component with raj/react implement the elm language theory
- https://github.com/rluiten/rajts /201807/ts
  - Convert raj into typescript

- https://github.com/Gozala/reflex /202204/js
  - https://gozala.gitbooks.io/reflex/content/
  - a reactive UI library that is heavily inspired by (pretty much is a port of) elm
  - In order to keep a major attraction of elm — algebraic data types & type safety — the library uses flow
    - Unlike other derivations of Elm, Reflex recognizes essential role type system plays in Elm. 
    - It full embraces design choices driven by type system & in conjunction with flow provide a strong guarantees
  - Architecture is taken from Elm due to it's simplicity and emphasis on type safety
  - In reflex all effects are managed. 
    - Traditionally all the IO (Networking, Database Access, Filesystem access, Time Access, etc.) in JS is performed as side effects. That makes code non-deterministic. In plain English - Reproducing failures & writing tests for such code is very difficult. 
    - Managed effects tackle non-determinism same as Redux tackles state updates - via centralized transactions.
    - Tasks in reflex are the way to describe non-deterministic operations.
    - Effect in reflex is a description of result of the Task instance is fed back into update
  - https://github.com/Gozala/elmjs /202311/js
    - Elm in JS
  - https://github.com/mozilla/reflex
    - [Tutorial/Guide](https://github.com/mozilla/reflex/issues/51)
  - https://github.com/mozilla/reflex-virtual-dom-driver
    - This is a reflex application view driver that uses virtual-dom library for rendering into a DOM.
  - https://github.com/mozilla/reflex-react-driver
    - This is a reflex application view driver that uses react for rendering into a DOM

- https://github.com/iyegoroff/ts-elmish /202206/ts/archived
  - https://elmish.github.io/elmish/
  - Elmish architecture in Typescript
  - modular, supports different view layers and effect handling strategies
  - subscriptions are out of scope for ts-elmish - just use view layer capabilities for listening to events (e.g. useEffect hook in react).
  - https://github.com/iyegoroff/ts-railway
    - ROP flavoured Result & AsyncResult types. 
    - Based on Railway oriented programming article by Scott Wlaschin.

- https://github.com/ScepLab/fun-ts /202303/ts
  - Monorepo with features like the elmish architecture or a rest client based on functional programming with TypeScript.
  - 提供了 elmish-react-client 和 rest-client-api 的示例

- https://github.com/jas-chen/elm-architecture /MIT/201611/js
  - The Elm Architecture in JavaScript
  - Code structure is almost the same as The Elm Architecture in elm
  - It works with React, Snabbdom, Deku or any virtual DOM library.
  - It comes with an observable model, you can use RxJS, Most.js or xstream to transform it.
  - 依赖rxjs.v5或xtream
  - [The Elm Architecture in JavaScript | by Jas Chen | Medium_201611](https://medium.com/@JasChen/the-elm-architecture-in-javascript-eb4d5201272b)

- https://github.com/gordonbrander/store-element /202210/js
  - A deterministic web component class, loosely inspired by The Elm App Architecture pattern.

- https://github.com/derrickbeining/effect-mvu /202311/ts
  - A port of the Elm application architecture to the effect-ts ecosystem
  - provides a minimal setup to get React working in Vite with HMR 

- https://github.com/SantaClaas/elmish-web-components /202306/ts
  - Web App Component Framework built with Elmish on top of lit-html. 
  - And a Mastodon App built with it.
  - This library is using Elmish. The code was copied and converted to TypeScript by me

- https://github.com/steos/elmar.js /201610/js
  - https://steos.github.io/elmar.js
  - An experiment in applying the Elm Architecture to JavaScript.
  - This is just an experiment. It’s neither reactive nor does it actually work anything like Elm at all.
  - If you’re looking for a true Elm-like FRP implementation in JavaScript check out reflex.
  - [Elm Architecture for React. An Experiment in React App Architecture_201601](https://medium.com/javascript-inside/elm-architecture-for-react-951b383fcd65)

- https://github.com/typescript-tea/core /202207/ts
  - an implementation of The Elm Architecture (TEA) for typescript
  - Note: TEA has managed effects, meaning that things like HTTP requests or writing to disk are all treated as data in TEA. When this data is given to an Effect Manager, it can do some "query optimization" before actually performing the effect. Your application should consist of pure functions only and all effects should be handled in Effect Managers outside your application.
  - TEA has two kinds of managed effects: commands and subscriptions.

- https://github.com/hojberg/gongfu /202004/ts
  - The Elm Architecture in TypeScript
  - It has composable update functions and Effects build-in.

- https://github.com/pocarist/elmish-ts /201811/ts
  - The Elm Architecture by Typescript implementation like Elmish.
- https://github.com/jichang/elm-ts /202107/ts
  - Implement Elm architecture with TypeScript

- https://github.com/blackChef/rce /201911/js
  - https://blackchef.github.io/rce/
  - rce 代表 react, cursor, elm。是一个轻量级的 react 架构
  - 仅有两个 api，设计思路与 react 一致
  - 利用数据指针，让你能把组件的 state 保存 app 的最上一层，但又能让将管理 state 的方法写在组件内部。
  - 受 elm 启发的模式，你能轻易写出可高度复用的组件，每个组件都分为 init/view/update

- https://github.com/kaleidos/olmo /201602/js
  - attempt to port the core ideas of The Elm Architecture to a JavaScript library
  - There's a standarized interface for effects.
  - Rendering is no different and is treated as an effect. Actually Olmo don't take any action in which library it uses for rendering, that's your app's decision.

- https://github.com/xaviervia/tessellation /201612/js
  - https://xaviervia.github.io/tessellation/
  - Tessellation is a Redux-inspired architecture for applications
  - A JavaScript way of doing the Elm architecture

- https://github.com/levo-framework/core /202007/ts/inactive
  - a frontend framework that supports Server-Side Rendering (SSR) and The Elm Architecture (TEA) out of the box.

- https://github.com/yysun/apprun /1.2kStar/MIT/202309/ts
  - https://apprun.js.org/
  - https://dev.to/yysun
  - a JavaScript library for developing high-performance and reliable web applications using the elm inspired architecture, events and components.
  - view is a pure function to display the state
  - State management and routing included
  - No proprietary syntax to learn (no hooks)
  - Use directly in the browser or with a compiler/bundler
  - Advanced features: JSX, Web Components, Dev Tools, SSR, etc.
  - An AppRun component is a mini-application with elm architecture, which means inside a component, there are state, view, and update. In addition, components provide a local scope.
  - [AppRun runs on both client and server side to allow event firing and handling between the frontend app and backend business logic modules using WebSockets, no REST API.](https://twitter.com/apprunjs/status/1237064423191252992)
  - [What is your take on AppRun?_201904](https://www.reddit.com/r/elm/comments/beizxg/what_is_your_take_on_apprun/)
    - it looks basically like Hyperapp.
    - No tracking of effects, so reasoning about anything becomes much more difficult when compared to Elm - in Elm everything is pure and the runtime does all the effectful stuff

- https://github.com/artydev/mvu /202310/js
  - Simple Model View Update library for in Browser use
  - Based on DML, Morphdom and HTL

- https://github.com/foxbunny/movium /202107/js
  - an implementation of the MVU architecture (a.k.a. Elm architecture) in JavaScript. 
  - This package provides the base framework built on top of Snabbdom as well a few helper functions.
  - Integrated HTTP request functions
  - Easily extensible at multiple levels

- https://github.com/0918nobita/mvu /202301/ts/自研vdom
  - MVU framework + VDOM runtime (inspired by Elm)
# hyperapp
- https://github.com/jorgebucaran/hyperawesome
  - https://hyperapp.dev/
  - A curated list of awesome projects built with Hyperapp

- hyperapp /19kStar/MIT/202205/js
  - https://github.com/jorgebucaran/hyperapp
  - The tiny framework for building hypertext applications
  - an ultra-lightweight Virtual DOM, highly-optimized diff algorithm, and state management library obsessed with minimalism.
  - [Hyperapp V2_201905](https://github.com/jorgebucaran/hyperapp/pull/726)
    - Middleware: const enhance = oldDispatch => newDispatch
    - Payload creators: const NewValue = (state, value) => ({ ...state, value })
  - [RFC: Hyperapp 2.0_201804](https://github.com/jorgebucaran/hyperapp/issues/672)
    - Hyperapp holds firm on the functional programming front when managing your state, but takes a pragmatic approach to allowing for side effects, asynchronous actions, and DOM manipulations.
    - All Things Dynamic — First class support for code splitting and dynamically loading actions and views using import()
    - Introduce a subscriptions API inspired by Elm
  - [V2 What if?_201810](https://github.com/jorgebucaran/hyperapp/issues/765)
    - Effects need to be represented as objects.If you use a function to represent an effect, then it's impossible to test effects using a strict equality check
    - I designed this part of the API looking at Elm.

- https://github.com/hydux/hydux /201902/ts/未实现undo
  - A light-weight Elm-like alternative for Redux ecosystem, inspired by Hyperapp and Elmish.
  - Elm Architecture, split your whole app with init, state, actions.
  - Elm-like side effect manager and subscribe API
  - Support any vdom library, including react
  - hyperapp compatible API
  - Official support for react-router
  - 未实现undo，但devtools支持时间旅行
  - logger, persist, Redux Devtools with time traveling, ultradom(1kb vdom), **All in One**
  - built-in support for HMR, logger, persist, Redux Devtools
  - I create this to support different vdom libraries, like React(official support), ultradom(built-in), Preact, inferno 
  - https://github.com/hydux/hydux-preact
  - https://github.com/hydux/hydux-react-router

- https://github.com/jorgebucaran/superfine /1.6kStar/MIT/202104/js
  - a minimal view layer for building web interfaces. 
  - we use the `h()` and `text()` functions to create a lightweight representation of the DOM (or virtual DOM for short), and `patch()` to actually render the DOM.
  - Superfine won't re-create the entire DOM every time we use patch(). By comparing the old and new virtual DOM we are able to change only the parts of the DOM that need to change instead of rendering everything from scratch.

- https://github.com/loteoo/hyperapp-starter /202104/ts
  - Clean web app starter using Hyperapp with strong focus on developer experience.
  - https://github.com/anticrisis/hyperapp-starter /202003/ts
  - https://github.com/bonniss/hyparcel /202005/js
  - https://github.com/antsegcan/ts-hyperapp /202004/ts

- https://github.com/dangvanthanh/hyperapp-todomvc /202109/js
  - TodoMVC using Hyperapp

- https://github.com/adamdawkins/elm-tutorials-in-hyperapp /201909/ts
  - Copies of the Elm Tutorials in Hyperapp v2

- https://github.com/hlibco/hypersamples /202007/ts
  - https://hypersamples.vercel.app/
  - an unofficial collection of components and recipes for Hyperapp V2

- https://github.com/kwasniew/hyperapp2-real-world-example /202006/js
  - Real Word Example App in Hyperapp v2
- https://github.com/kwasniew/hyperapp-realworld-example-app /201908/js
  - A Single Page Application written in Hyperapp 1

- https://github.com/jacobtipp/hypernews /201807/js
  - hackernews clone with hyperapp
- https://github.com/mrozbarry/hyperapp-hn /202003/js
  - Hacker News Reader using Hyperapp
  - 依赖hyperapp、firebase

- https://github.com/zaceno/sevenguis-hyperapp /202104/js
  - https://zaceno.github.io/sevenguis-hyperapp/
  - 7GUIs implemented in hyperapp v2

- https://github.com/lanceturbes/hyperapp-drag-n-drop /202308/js
  - 依赖hyperapp.v2、hyperlit

- https://github.com/amoutonbrady/ha-sticky /202001/js
  - A semi-advanced sticky notes inspired by windows with offline capabilities

- https://github.com/os-js/osjs-gui /202209/js
  - https://manual.os-js.org/
  - open-source web desktop platform with a window manager, application APIs, GUI toolkit, filesystem abstractions and much more.
  - 依赖hyperapp.v1、hyperapp-nestable

- https://github.com/icylace/uy /202204/ts
  - a UI library for Hyperapp.

- https://github.com/PacktPublishing/Hands-On-Web-Development-with-Hyperapp-V2 /201906/js
  - Hands-On Web Development with Hyperapp V2, published by Packt

- https://github.com/SteveALee/hyperapp2-explore /201910/js
  - An exploration of the features of hyperapp v2.0

- https://github.com/sergey-shpak/hyperapp-middlewares /202105/js
  - Frequently used hyperapp#2 middlewares
# elm-react
- https://github.com/acdlite/realm /201601/js
  - A total rip-off(仿冒品; 抄袭之作) of the Elm Architecture, in React.
  - Realm components are React components, so they are interoperable with non-Realm components. Use Realm for your entire app, or just in specific places.
  - One way to think of it is as "nested Redux." Each Realm component is its own mini-Redux app, which can be composed of other Redux apps.
  - Note that while Realm is an implementation of the Elm Architecture, it does not and cannot claim to replicate the entirety of Elm the language.
  - [Pin to 0.16 Elm Arch](https://github.com/acdlite/realm/issues/4)
    - 0.17 is quite different architecture from this.

- https://github.com/ChristophP/react-model-view-update /202301/ts/100loc
  - A React microframework for pure state management and managed side effects. 
  - Inspired by the Elm architecture, no redux needed.
  - all-in-one: State management and effect handling out of the box.

- https://github.com/jamesbirtles/fpreact /201710/ts
  - provides an alternative api for creating preact components, heavily inspired by elm.
  - The api includes redux style state management and lends itself to functional programming

- https://github.com/atheck/react-elmish /202311/ts
  - brings the elmish pattern to react.
  - https://github.com/atheck/react-elmish-utils
  - https://github.com/atheck/react-elmish-snippets

- https://github.com/vankeisb/react-tea-cup /202305/ts
  - thin library that helps following The Elm Architecture, in React.

- https://github.com/iyegoroff/react-use-backlash /202308/ts
  - useReducer with effects, the elmish way
- https://github.com/iyegoroff/react-use-railway /202309/ts
  - useReducer with effects, the elmish way
# examples-elm-editor
- https://github.com/mweiss/elm-rte-toolkit /142Star/BSD/202202/elm
  - https://mweiss.github.io/elm-rte-toolkit/
  - A toolkit for creating rich text editors in Elm
- https://github.com/mweiss/elm-rte /201912/elm
  - https://mweiss.github.io/elm-rte/build/
  - An early prototype rich text editor built with elm

- https://github.com/dkodaj/rte /202309/elm
  - Pure Elm rich text editor for relatively short texts (< 2000 words / 12K characters)
  - It gets sluggish for longer texts.
  - If you need better performance, use mweiss/elm-rte-toolkit.
  - It cannot justify text.
  - Non-Western Keyboard Input. This is currently not supported, because it is hard to channel CompositionEvents to the Elm RTE object (which is not an input or textarea node).
  - To communicate with the browser's clipboard (to be able to copy text from the RTE to other apps and paste text from other apps into the RTE), you'll need to add two ports to your app











- https://github.com/SidneyNemzer/elm-text-editor /201904/elm
  - https://sidneynemzer.github.io/elm-text-editor/
  - A text editor written completely in Elm
  - This library implements an editor (duh) and a buffer. The buffer is separate from the editor to allow multiple editors to use the same buffer, such as in a multi-panel text editor

- https://github.com/jxxcarlson/elm-editor /41Star/BSD/202104/elm
  - https://jxxcarlson.github.io/app/text-editor/index.html
  - a pure Elm text editor. It relies heavily on prior work of Martin Janiczek and Sidney Nemzer.
  - The approach taken is for the editor to "see" only a small window into the full array of lines of text. That window is currently initialized in EditorModel.init at 300 lines, about ten times the number of lines visible in the editor of smalldemo.
  - distinguish between the viewport and the window. The former consists of what is visible, while the latter populates the scene defines what can be visible without moving the window in the document from which it is derived.

- https://github.com/Janiczek/elm-editor /70Star/BSD/202003/elm
  - Basic text editor written in Elm
  - 未实现 copy/paste; context-menu
  - [Text editor done in pure Elm - Show and Tell - Elm_201806](https://discourse.elm-lang.org/t/text-editor-done-in-pure-elm/1365)

- https://github.com/leahsteinberg/co /42Star/NALic/201603/elm
  - a collaborative text editor based on WoOT (Without Operational Transform)
  - front end in Elm, back in node.

- https://github.com/3tty0n/elm-online-markdown-editor /201708/elm
  - https://3tty0n.github.io/elm-online-markdown-editor/
  - An online markdown editor written in Elm.
- https://github.com/DavidTobin/elm-editor /201710/elm
  - WYSIWYG editor in Elm

- https://github.com/rofrol/elm-code-editor /201705/elm
  - Elm code editor - embeddable
  - elm-0.18

- https://github.com/Orange-OpenSource/elm-advanced-grid /202009/elm/archived
  - An Elm module to display feature rich grids in web apps.
  - a dynamically configurable grid of data
  - in-place filtering and sorting, multiple selection

- https://github.com/pierregoudjo/build-your-own-excel /202308/ts/redux
  - A Javascript version of a talk showing how to build a simle version of Excel based on functional principles.
  - This javascript version use Preact and Redux with Typescript instead of Elmish and Fable with F#.

- https://github.com/tpetricek/elmish-spreadsheet /201810/f#
  - Implement your own Excel 365 in 100 lines of F#
  - a minimal tutorial showing how to use F#, Fable and Elmish
  - [Write your own Excel in 100 lines of F# - Tomas Petricek](https://tomasp.net/blog/2018/write-your-own-excel/)
# examples
- https://github.com/evancz/elm-architecture-tutorial /201912/elm
  - How to create modular Elm code that scales nicely with your app

- https://github.com/yelouafi/snabbdom-todomvc /201507/js
  - TodoMVC using snabbdom and Elm architecture
  - [React-less Virtual DOM with Snabbdom_201507](https://medium.com/@yelouafi/react-less-virtual-dom-with-snabbdom-functions-everywhere-53b672cb2fe3)

- https://github.com/yelouafi/elm-examples-js /201511/js
  - examples for the article [Elm Architecture & Side Effects: example with Snabbdom/JSX_201511](https://medium.com/@yelouafi/elm-architecture-side-effect-examples-with-snabbdom-and-jsx-3732219d9995)

- https://github.com/yelouafi/elm-arch-with-snabbdom /201601/js
  - Elm architecture examples with JavaScript/JSX using
  - Snabbdom-jsx: a tiny library for writing Snabbdom Virtual DOM using JSX syntax
  - union-type: to represent Component Actions
  - The repository contains some examples: counter/login

- https://github.com/dmy/elm-realworld-example-app /202005/elm/inactive
  - Elm RealWorld example application architected with the Effect pattern

- https://github.com/huytd/kanelm /201904/elm
  - Kanban board built with Elm

- https://github.com/joakin/elm-7guis /202210/elm
  - https://eugenkiss.github.io/7guis
  - Elm implementation of the 7GUIs tasks
  - [7GUIs implementation in Elm - Show and Tell - Elm_201901](https://discourse.elm-lang.org/t/7guis-implementation-in-elm/3003)

- https://github.com/foxbunny/duckweed /201711/ts
  - JavaScript microframework for programming reactive interfaces using Model-Action-View architecture
  - inspired by Elm and Simon Friis Vindum's Functional Frontend Architecture. 
  - Duckweed's primary goal is not to promote or enforce functional programming paradigm. It's main goal is to provide a simple API, and functions happen to be a good step in that direction.
  - https://github.com/foxbunny/duckweed-tasks
# utils
- https://github.com/Zaid-Ajaj/elmish-composition /202012/js/f#
  - This repository includes two projects: traditional and hybrid to compare the composition technique of an Elmish application.
  - The traditional directory contains an application that follows Elm-style technique for composition.
  - The hybrid directory contains an application that is a hybrid of Elm with React to compose the application with help of Feliz. ElmishComponents.
  - [Works great](https://github.com/Zaid-Ajaj/elmish-composition/issues/5)
    - Thanks! Though I believe this sample is using the old Feliz.ElmishComponents library. Currently we recommend using Feliz.UseElmish library instead to achieve the same functionality but it is much better and gives more control. 
# elm-non-js
- [elm architecture in rust. 43loc](https://gist.github.com/kuon/b81f6397f454f0254f7476563b1794c0)

- https://github.com/sindreij/willow /201811/rust
  - Implementation of the Elm architecture in Rust
  - an experiment to see if it is possible to create a "elm-like" API using Rust.

- https://github.com/ivanceras/sauron /202310/rust
  - a versatile web framework and library for building client-side and/or server-side web applications
  - inspired by elm-lang and is following The Elm Architecture.
  - [Show HN: Sauron – A web framework in Rust that adheres to the Elm architecture | Hacker News_201904](https://news.ycombinator.com/item?id=19756505)

- https://github.com/iced-rs/iced /202311/rust
  - A cross-platform GUI library for Rust, inspired by Elm
  - Modular ecosystem split into reusable parts: runtime, renderer, shell
  - Inspired by The Elm Architecture, Iced expects you to split user interfaces into four different concepts: state/msg/view/update-logic
  - Cross-platform support (Windows, macOS, Linux, and the Web)
  - Built-in widgets (including text inputs, scrollables, and more!)

- https://github.com/antoyo/relm /202311/rust
  - GTK+-based, GUI library, inspired by Elm, written in Rust
  - https://github.com/Relm4/Relm4
    - GUI library inspired by Elm and based on gtk4-rs. 
    - Relm4 is a new version of relm that's built from scratch and is compatible with GTK4 and libadwaita.

- https://github.com/veeso/tui-realm /202311/rust
  - A tui-rs framework inspired by Elm and React
  - a framework for tui and ratatui to simplify the implementation of terminal user interfaces

- https://github.com/mitchmindtree/elmesque /201512/rust
  - An attempt at porting Elm's incredibly useful, purely functional std graphics modules.
# more
