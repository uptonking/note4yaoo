---
title: lib-utils-codesandbox-examples
tags: [codesandbox, examples, plugin-system, scripts, utils]
created: 2023-09-02T02:56:54.921Z
modified: 2023-09-02T09:17:22.992Z
---

# lib-utils-codesandbox-examples

# guide

- usecase
  - csb做好了observable-notebook/d3showcase要做的事
# js-sandbox
- https://github.com/codesandbox/codesandbox-client /12.9kStar/GPLv3+apache2/202404/js
  - https://codesandbox.io/
  - An online IDE for rapid web development
  - CodeSandbox is licensed under GPLv3, except for `packages/common` and `packages/sandpack-core` and `packages/app/src/sandbox`, which are licensed under the Apache License, Version 2.0.
  - 🍴 forks
  - https://github.com/NetEase/codesandbox-client /tango
- https://github.com/codesandbox/sandpack /4.5kStar/apache2/202405/ts
  - https://sandpack.codesandbox.io/
  - https://sandpack.codesandbox.io/docs
  - Sandpack is a component toolkit for creating your own live running code editing experience powered by CodeSandbox.
  - 依赖codemirror6、lz-string、react-devtools-inline
  - Sandpack Client: This is a small foundation package that sits on top of the bundler. It is framework agnostic and facilitates the handshake between your context and the bundler iframe.
  - Sandpack React: React components that give you the power of editable sandboxes that run in the browser
  - https://github.com/AaronPowell96/sandpack-file-explorer /MIT/202312/ts
    - Enhanced File Explorer for Sandpack. Providing immense flexibility to Sandpack's capabilities.

- https://github.com/ameerthehacker/blazepack /LGPLv3/202106/js/inactive
  - Blazing fast dev server powered by sandpack
  - I always wanted the super fast feedback that codesandbox provides in my local environment, so I have built a tiny wrapper around the codesandbox bundler sandpack and it runs locally
  - Supports private npm packages 
  - Supports React, Vue, Angular, Preact, Svelte and more

- https://github.com/mcuking/vitesandbox-client /MIT/202211/js/inactive
  - https://github.com/mcuking/vitesandbox-client-example
  - https://mcuking.github.io/vitesandbox-client-example/
  - An Online Vite Sandbox that compiles web projects based on browser-vite
  - 🧊🆚️ [搭建一个浏览器版 Vite 沙箱 _202201](https://github.com/mcuking/blog/issues/111)
    - CodeSandbox 方案在构建规模较大的前端应用比较耗时的问题，并在文章结尾提到会尝试采用 bundless 构建模式来解决这个问题
    - 针对通用的应用进行实时构建可以采用云端沙箱（Cloud Sandbox）模式。该方案首先会在服务器中出初始化一个代码运行环境（Docker 或 microVM 等），然后将需要被构建的应用代码从指定位置（例如某个 git 代码仓库）拷贝到该运行环境中，安装依赖，最后执行构建命令对应用进行构建。该种模式对应用所采用的编程语言等没有特定要求，完全等同于本地环境。
    - 如果仅构建前端应用，则可以将应用的编译构建的过程迁移到浏览器中进行，最终的构建结果直接在浏览器中执行 —— 渲染出最终的页面，也就是浏览器端沙箱（Browser Sandbox）模式
    - CodeSandbox 本质上是在浏览器中运行的简化版 Webpack
    - 本方案主要对 Vite / esm.sh 等开源方案的改造，再结合 Web Worker / Service Worker / Broadcast Channel / Cache Storage / iframe 等浏览器技术，以实现在浏览器中对前端应用按照 bundless 模式进行实时构建的目的

- https://github.com/endojs/endo /apache2/js
  - a distributed secure JavaScript sandbox, based on SES
  - Endo is a JavaScript platform under development for secure communication among objects within one process and distributed between mutually suspicious machines
  - [SES is hardened JavaScript. Hardened JavaScript is highly compatible with ordinary JavaScript. ](https://github.com/endojs/endo/tree/master/packages/ses)
    - SES safely executes third-party JavaScript 'strict' mode programs in compartments that have no excess authority in their global scope. 

- https://github.com/codesandbox/nodebox-runtime /ts
  - Nodebox is a runtime for executing Node.js modules in the browser
  - we did not fully open-source Nodebox for a variety of reasons

- https://github.com/bplok20010/eval5 /ts
  - 基于 TypeScript 编写的 JavaScript 解释器，支持完整 ES5 语法
  - 支持浏览器、node.js、小程序等 JavaScript 运行环境

- https://github.com/sablejs/sablejs /js
  - The safer and faster ECMA5.1 interpreter written by JavaScript
  - covered ~95% test262 es5-tests cases
  - it can be used:
    - Sandbox (like Figma Plugin Sandbox, but better and easier to use);
    - Protect JavaScript source code via AOT compiling to opcode.

- https://github.com/NeilFraser/JS-Interpreter /js
  - https://neil.fraser.name/software/JS-Interpreter/
  - A sandboxed JavaScript interpreter in JavaScript. 
  - Execute arbitrary JavaScript code line by line in isolation and safety.

- https://github.com/endojs/Jessie /js
  - Tiny subset of JavaScript for ocap-safe universal mobile code
  - Whereas JSON is a simple universal representation for safe mobile data, Jessie is a simple universal representation for safe mobile data and behavior.

- https://github.com/asvd/jailed /js/inactive
  - Jailed is a small JavaScript library for running untrusted code in a sandbox. 
  - The library is written in vanilla-js and has no dependencies.
  - Load an untrusted code into a secure sandbox; 
  - Export a set of external functions into the sandbox.
  - The code is executed as a plugin, a special instance running as a restricted subprocess (in Node.js), or in a web-worker inside a sandboxed frame (in case of web-browser environment). 

- https://github.com/HynekPetrak/malware-jail /js
  - Sandbox for semi-automatic Javascript malware analysis, deobfuscation and payload extraction. Written for Node.js
  - malware-jail is written for Node's 'vm' sandbox. 
  - Currently implements WScript (Windows Scripting Host) context env/wscript.js
  - browser context is partially implemented env/browser.js.

- https://github.com/patriksimek/vm2 /MIT/202307/js/deprecated
  - Advanced vm/sandbox for Node.js
  - vm2 is a sandbox that can run untrusted code with whitelisted Node's built-in modules.
  - It uses the internal `VM` module to create a secure context.
  - It uses Proxies to prevent escaping from the sandbox.
  - It overrides the built-in require to control access to modules.
  - The original intent was to devise a method for running untrusted code in Node, with a keen focus on maintaining in-process performance.
  - Unfortunately, the growing complexity of Node has brought us to a crossroads. We now find ourselves facing an escape so complicated that fixing it seems impossible.
  - We would recommend migrating your code to the `isolated-vm`, a library which employs a slightly different, yet equally effective, approach to sandboxing untrusted code.

- https://github.com/laverdet/isolated-vm /cpp
  - Secure & isolated JS environments for nodejs
  - a library for nodejs which gives you access to v8's Isolate interface
  - This allows you to create JavaScript environments which are completely isolated from each other. 
  - currently in maintenance mode. New features are not actively being added

- https://github.com/svaarala/duktape /clang/js
  - embeddable Javascript engine with a focus on portability and compact footprint
  - easy to integrate into a C/C++ project
  - ECMAScript E5/E5.1 compliant, with some semantics updated from ES2015
  - Partial support for ECMAScript 2015 (E6) and ECMAScript 2016 (E7)

- https://github.com/naruaway/npm-in-browser /ts
  - npm package to run npm CLI in web browsers
  - https://twitter.com/naruaway/status/1706984800081605062
    - It builds the library using Webpack to inject shims. For globals such as "process", it uses ProvidePlugin.
    - And then the whole code is wrapped by a closure, which makes sure such "globals" are actually not global. "process" will be different per invocation.

- https://github.com/tc39/proposal-shadowrealm /s3
  - [ES6 Realms API](https://gist.github.com/dherman/7568885)
  - A realm object abstracts the notion of a distinct global environment, with its own global object, copy of the standard library, and "intrinsics" (standard objects that are not bound to global variables, like the initial value of Object.prototype).
  - Extensible web: This is the dynamic equivalent of a same-origin `<iframe>` without DOM.
  - https://github.com/tc39/proposal-compartments /s1
    - Compartments are a mechanism for isolating and providing limited power to programs within a shared realm. 
    - Each compartment shares the intrinsics of a realm, but a different set of evaluators (eval, Function, and a new evaluator, Module) and a global object. 
    - Having a separate global object allows each compartment to be granted access to only those powerful objects it needs, its own isolated evaluators, powerless constructors, and shared prototypes.

- https://github.com/XGHeaven/jsscript /202404/js
  - A flexible JavaScript engine running on another JavaScript engine.
  - Inspired by QuickJS
  - Only support strict mode and modern JavaScript feature.
  - Not implement with, eval, var, label etc.
  - 尝试性的把微任务在 jsscript 里面实现了一下，发现比我预想的简单，也没有八股文中那么多弯弯绕的东西。 又有了新的理解，微任务其实就是 JS 标准内的，而宏任务则是外部 IO 环境的任务。

## iframe-sandbox

- https://github.com/dabbott/javascript-playgrounds /ts
  - https://unpkg.com/javascript-playgrounds/public/index.html
  - An interactive JavaScript sandbox
  - It's designed to be loaded as an iframe for easy inclusion in any webpage.
  - There are a variety of configuration options, including a React preset and a React Native preset.
  - The sandbox may be included on your site in one of two ways: as a React component, directly as an iframe

- https://github.com/krakenjs/zoid /js
  - A cross-domain component toolkit
  - Render an iframe or popup on a different domain, and pass down props, including objects and functions
  - [Iframes are just terrible. Here’s how they could be better.](https://bluepnume.medium.com/iframes-are-just-terrible-heres-how-they-could-be-better-974b731f0fb4)
# iframe
- https://github.com/bluwy/whyframe /js
  - https://whyframe.dev/
  - enables rendering any UI framework markup within an iframe, including Svelte, Vue, Solid, Preact, and React. 

- https://github.com/niutech/x-frame-bypass /js
  - https://niutech.github.io/x-frame-bypass/
  - Web Component extending IFrame to bypass X-Frame-Options: deny/sameorigin
  - X-Frame-Bypass is using a CORS proxy to allow this

- https://github.com/robbestad/react-iframe /ts
  - Simple React component for including an iframed page.

- https://github.com/vb/lazyframe /js
  - Lazyframe creates a responsive placeholder for embedded content and requests it when the user interacts with it. This decreases the page load and idle time.

- https://github.com/davidjbradshaw/iframe-resizer /js
  - http://davidjbradshaw.github.io/iframe-resizer/
  - This library enables the automatic resizing of the height and width of both same and cross domain iFrames to fit their contained content.
  - Works with multiple and nested iFrames.
  - Detects changes to the DOM that can cause the page to resize using `MutationObserver`.
  - Simplified messaging between iFrame and host page via `postMessage`.
  - Works with ViewerJS to support PDF and ODF documents

- https://github.com/niutech/x-frame-bypass /js
  - https://niutech.github.io/x-frame-bypass/
  - Web Component extending IFrame to bypass X-Frame-Options: deny/sameorigin
  - X-Frame-Bypass is using a CORS proxy to allow this

- https://github.com/ryanseddon/react-frame-component /js
  - http://ryanseddon.github.io/react-frame-component/
  - allows you to encapsulate your entire React application or per component in an iFrame.
  - [Rendering to iFrames in React](https://medium.com/@ryanseddon/rendering-to-iframes-in-react-d1cb92274f86)

- https://github.com/its-devtastic/framestack /202204/ts
  - An iframe manager. Easily create, layout, animate, communicate with and clean up iframes.
# sandbox-using-vm
- https://github.com/firecracker-microvm/firecracker /apache2/202405/rust/python
  - http://firecracker-microvm.io/
  - Secure and fast microVMs for serverless computing.
  - Firecracker is an open source virtualization technology that is purpose-built for creating and managing secure, multi-tenant container and function-based services that provide serverless operational models. 
  - Firecracker runs workloads in lightweight virtual machines, called microVMs, which combine the security and isolation properties provided by hardware virtualization technology with the speed and flexibility of containers.
  - The main component of Firecracker is a virtual machine monitor (VMM) that uses the Linux Kernel Virtual Machine (KVM) to create and run microVMs. 
  - Firecracker has a minimalist design. It excludes unnecessary devices and guest-facing functionality to reduce the memory footprint and attack surface area of each microVM.
  - Firecracker was developed at Amazon Web Services to accelerate the speed and efficiency of services like AWS Lambda and AWS Fargate. 
# browser-emulator
- https://github.com/jvilk/BrowserFS
  - an in-browser filesystem that emulates the Node JS filesystem API and supports storing and retrieving files from various backends.

- https://github.com/humphd/browser-shell
  - A Linux command-line shell in the browser
  - A Linux shell in the browser via forked v86, with bi-directional POSIX filesystem (via Filer) shared over Plan 9 resource sharing.
  - The Filer filesystem in the browser is mounted in the Linux VM at /mnt.

- https://github.com/humphd/nohost /201904/js
  - A web server in your web browser
  - nohost uses Filer to run a node'js style, POSIX filesystem inside a Service Worker, and handle requests for static files and directories.

- browsix /3.1kStar/MIT/201904/ts/inactive
  - https://github.com/plasma-umass/browsix
  - Browsix is a Unix-like operating system for the browser.
  - outdated. requires node 6 (latest is node 19)
  - Browsix uses `BrowserFS` for its filesystem
  - Browsix makes core Unix features available to web applications (including pipes, processes, signals, sockets, and a shared file system) and extends JavaScript runtimes for C, C++, Go, and Node.js programs so they can run in a Unix-like environment within the browser. 
  - Browsix also provides a POSIX-like shell that makes it easy to compose applications together for parallel data processing via pipes.
  - Browsix enables you to compose the in-browser part of your web applications out of processes. 
    - This process model is implemented on top of existing browser APIs, like web workers, so it works in all modern browsers.
  - 🍴 forks
  - https://github.com/milahu/browsix
  - https://github.com/SamGinzburg/browsix

- https://github.com/intigos/possimpible
  - A (UNIX|Plan9) Kernel for the browser written in TypeScript

- https://github.com/niksy/node-stdlib-browser
  - Node standard library for browser.
  - Based on `node-libs-browser` for Webpack
  - Works with Webpack, Rollup, Vite, esbuild and Browserify, but should also work with other bundlers

- https://github.com/DustinBrett/daedalOS
  - https://dustinbrett.com/
  - Desktop environment in the browser
# dynamic-js
- https://github.com/unjs/jiti /ts
  - Runtime Typescript and ESM support for Node.js
# playground
- https://github.com/nalgeon/codapi /apache2/202312/go
  - https://codapi.org/
  - Embeddable code playgrounds for education, documentation, and fun.
  - Codapi is a platform for embedding interactive code snippets directly into your product documentation, online course, or blog post.
  - Codapi manages sandboxes (isolated execution environments) and provides an API to execute code in these sandboxes. 
  - It also provides a JavaScript widget codapi-js for easier integration.
  - Custom sandboxes for any programming language, database, or software.
  - Available as a cloud service and as a self-hosted version.

- https://github.com/voronianski/esnextbin /201905/js
  - Prototype JavaScript apps in the browser with ES2015's latest features and importing modules directly from NPM.
# codesandbox-like
- https://github.com/rajatmaheshwari2512/codefiddle /202308/ts
  - This project is a take on how a site like CodeSandbox could be built.
  - 依赖antd.v5、@monaco-editor/react、xterm、zustand、express、directory-tree
  - The basic layout provides a VS Code experience, wherein a user can navigate between his available files from the file manager. 
  - Integrated with this is also an iframe providing realtime feedback to changes you may make in your project. 
  - [Made an online code editor, like CodeSandbox. Think VS Code in the browser : node_202304](https://www.reddit.com/r/node/comments/12ceajg/made_an_online_code_editor_like_codesandbox_think/)
    - I've made an online code editor from scratch
    - It uses xterm.js to give a shell to the user on the frontend, and monaco editor for editing your files, and I generate the folder structure recursively. 
    - I've used Zustand for global state management
    - I tried to get it as close to VS Code as possible, and there's a bunch of stuff still left to do
# nodebox/webcontainer
- https://github.com/Sandpack/nodebox-runtime
  - https://sandpack.codesandbox.io/docs/advanced-usage/nodebox
  - [Docs don't explain how to self host a Nodebox instance?](https://github.com/Sandpack/nodebox-runtime/issues/48)

- browsix /3.1kStar/MIT/201904/ts/inactive
  - https://github.com/plasma-umass/browsix
  - Browsix is a Unix-like operating system for the browser.
  - outdated. requires node 6 (latest is node 19)
  - Browsix uses `BrowserFS` for its filesystem
  - Browsix makes core Unix features available to web applications (including pipes, processes, signals, sockets, and a shared file system) and extends JavaScript runtimes for C, C++, Go, and Node.js programs so they can run in a Unix-like environment within the browser. 
  - Browsix also provides a POSIX-like shell that makes it easy to compose applications together for parallel data processing via pipes.
  - Browsix enables you to compose the in-browser part of your web applications out of processes. 
    - This process model is implemented on top of existing browser APIs, like web workers, so it works in all modern browsers.
  - 🍴 forks
    - https://github.com/milahu/browsix
    - https://github.com/SamGinzburg/browsix
# utils
- https://github.com/ximing/jsvm2 /202402/ts
  - Javascript Interpreter implemented by typescript（TS实现的JS解释器）
  - https://github.com/ximing/jsvm3 /202402/ts
    - 自定义字节码的jsvm
# more
- https://github.com/BrowserBox/BrowserBox /AGPLv3/js
  - https://dosyago.com/
  - BrowserBox is Web application virtualization via zero trust remote browser isolation and secure document gateway technology.
  - Remote browser isolation is a cybersecurity model that physically isolates a user's browsing activity away from their local networks and infrastructure. With BrowserBox, this isolation provides an extra layer of security against web-based threats.
