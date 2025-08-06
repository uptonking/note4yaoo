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

- fans-sandbox
  - https://github.com/mcuking/vitesandbox-client
# js-sandbox
- https://github.com/codesandbox/codesandbox-client /12.9kStar/GPLv3+apache2/202404/js
  - https://codesandbox.io/
  - An online IDE for rapid web development
  - CodeSandbox is licensed under GPLv3, except for `packages/common` and `packages/sandpack-core` and `packages/app/src/sandbox`, which are licensed under the Apache License, Version 2.0.
  - 🍴 forks
  - https://github.com/NetEase/codesandbox-client /tango
  - [Does it use codemirror or monaco ? _202102](https://github.com/codesandbox/codesandbox-client/discussions/5495)
    - we use VSCode that uses Monaco, the only part we use codemirror is the embedded because it's lighter to load
    - react-sandpack uses codemirror but we're looking into having monaco as an option as well
  - [Add a collaborative mode _201709](https://github.com/codesandbox/codesandbox-client/issues/206)
    - it's here now _201803
- https://github.com/codesandbox/sandpack /4.5kStar/apache2/202405/ts
  - https://sandpack.codesandbox.io/
  - https://sandpack.codesandbox.io/docs
  - Sandpack is a component toolkit for creating your own live running code editing experience powered by CodeSandbox.
  - 依赖codemirror6、lz-string、react-devtools-inline
  - 未实现跳转到定义的功能
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

- https://github.com/divriots/browser-vite /600Star/MIT/202203/ts/inactive
  - This is a fork of vite v2 which aims at being used in a browser (served by service worker).
  - Used in Backlight.dev and in the upcoming Replic.dev
  - [Vite in the browser _202203](https://divriots.com/blog/vite-in-the-browser)

- https://github.com/endojs/endo /apache2/js
  - a distributed secure JavaScript sandbox, based on SES
  - Endo is a JavaScript platform under development for secure communication among objects within one process and distributed between mutually suspicious machines
  - [SES is hardened JavaScript. Hardened JavaScript is highly compatible with ordinary JavaScript. ](https://github.com/endojs/endo/tree/master/packages/ses)
    - SES safely executes third-party JavaScript 'strict' mode programs in compartments that have no excess authority in their global scope. 

- https://github.com/codesandbox/nodebox-runtime /ts
  - Nodebox is a runtime for executing Node.js modules in the browser
  - we did not fully open-source Nodebox for a variety of reasons

- https://github.com/laverdet/isolated-vm /ISC/202503/cpp
  - Secure & isolated JS environments for nodejs
  - a library for nodejs which gives you access to v8's Isolate interface
  - This allows you to create JavaScript environments which are completely isolated from each other. 
  - currently in maintenance mode. New features are not actively being added

- https://github.com/patriksimek/vm2 /MIT/202307/js/deprecated
  - Advanced vm/sandbox for Node.js
  - vm2 is a sandbox that can run untrusted code with whitelisted Node's built-in modules.
  - It uses the internal `VM` module to create a secure context.
  - It uses Proxies to prevent escaping from the sandbox.
  - It overrides the built-in require to control access to modules.
  - The original intent was to devise a method for running untrusted code in Node, with a keen focus on maintaining in-process performance.
  - Unfortunately, the growing complexity of Node has brought us to a crossroads. We now find ourselves facing an escape so complicated that fixing it seems impossible.
  - 💡 We would recommend migrating your code to the `isolated-vm`, a library which employs a slightly different, yet equally effective, approach to sandboxing untrusted code.

- https://github.com/bplok20010/eval5 /MIT/202110/ts/inactive
  - https://bplok20010.github.io/eval5/
  - 基于 TypeScript 编写的 JavaScript 解释器，支持完整 ES5 语法
  - 支持浏览器、node.js、小程序等 JavaScript 运行环境
  - https://github.com/HuolalaTech/eval5

- https://github.com/sablejs/sablejs /LGPL/202209/js/inactive
  - The safer and faster ECMA5.1 interpreter written by JavaScript
  - covered ~95% test262 es5-tests cases
  - it can be used:
    - Sandbox (like Figma Plugin Sandbox, but better and easier to use);
    - Protect JavaScript source code via AOT compiling to opcode.
  - [plan to charge or be free? _202011](https://github.com/sablejs/sablejs/issues/1)
    - 类似tinypng，分为免费/会员收费，免费有上传次数限制和代码大小限制，会员没有此类限制。
    - 编译器闭源，解释器混淆后公开，客户端本地执行编译
    - 协议有调整

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

- https://github.com/sebastianwessel/quickjs /MIT/202503/ts
  - https://sebastianwessel.github.io/quickjs/
  - allows you to safely execute JavaScript AND TypeScript code within a WebAssembly sandbox using the QuickJS engine. 
  - File System: Can mount a virtual file system.
  - Can provide a fetch client to make http(s) calls.

- https://github.com/jonathan-fielding/nodejs-runner /202005/ts
  - A docker based Node.js code runner which will execute JavaScript sent to it
  - This Node.js runner is a docker container designed to run Node.js within the docker sandbox.
  - To use this docker container first connect to it using websockets, you can then send the JavaScript code you want to execute to the container and it will stream back the output.
  - https://github.com/jonathan-fielding/use-node-runner

- https://github.com/danielduarte/es-eval /MIT/202409/js
  - Evaluate JavaScript expressions safely. No more being afraid of what the users enter
  - No access to require/import modules.
  - No access to global objects. All access to global objects is emulated and there's no real access to natives.
  - No access to OS features like file system, network, etc.
  - All user code is parsed to an AST and analyzed step by step, representing the code statements and functions in own components. No native functions are created with the user input.
  - Standard ECMAScript features are implemented and not delegated to the underlying engine.
  - https://github.com/danielduarte/es-eval-playground /202409/js

## iframe-sandbox

- https://github.com/dabbott/javascript-playgrounds /ts
  - https://unpkg.com/javascript-playgrounds/public/index.html
  - An interactive JavaScript sandbox
  - It's designed to be loaded as an iframe for easy inclusion in any webpage.
  - There are a variety of configuration options, including a React preset and a React Native preset.
  - The sandbox may be included on your site in one of two ways: as a React component, directly as an iframe

- https://github.com/krakenjs/zoid /apache2/202412/js
  - A cross-domain component toolkit
  - Render an iframe or popup on a different domain, and pass down props, including objects and functions
  - [Iframes are just terrible. Here’s how they could be better.](https://bluepnume.medium.com/iframes-are-just-terrible-heres-how-they-could-be-better-974b731f0fb4)
# iframe
- 支持iframe的网站
  - https://www.bilibili.com/
  - https://weixin.qq.com/

- https://github.com/web-infra-dev/unport /MIT/202407/ts/还可参考openrpc
  - A Universal Port with strict type inference capability for cross-JSContext communication.
  - Unport emerges as a well-architected solution, meticulously designed to simplify the complexity revolving around various JSContext environments.
    - Node.js, ChildProcess, Webview, Web Worker, worker_threads, WebSocket, iframe, MessageChannel, ServiceWorker, and much more.
  - Each of these JSContext environments exhibits distinct methods of communicating with the external world
    - the lack of defined types can make handling the code for complex projects an arduous task.
  - You only need to define the message types (MessageDefinition) and Intermediate communication channel (Channel) that different JSContexts need to pass, and you will get a unified type of Port
    - a MessageDefinition is a crucial concept that defines the structure of the messages that can be sent and received through a Channel.
    - a Channel is a fundamental concept that represents a Intermediate communication pathway between different JavaScript contexts
  - unrpc: Starting with the 0.6.0 release, we are experimentally introducing support for Typed RPC

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
# sandbox-by-vm/docker
- https://github.com/firecracker-microvm/firecracker /apache2/202405/rust/python
  - http://firecracker-microvm.io/
  - Secure and fast microVMs for serverless computing.
  - Firecracker is an open source virtualization technology that is purpose-built for creating and managing secure, multi-tenant container and function-based services that provide serverless operational models. 
  - Firecracker runs workloads in lightweight virtual machines, called microVMs, which combine the security and isolation properties provided by hardware virtualization technology with the speed and flexibility of containers.
  - The main component of Firecracker is a virtual machine monitor (VMM) that uses the Linux Kernel Virtual Machine (KVM) to create and run microVMs. 
  - Firecracker has a minimalist design. It excludes unnecessary devices and guest-facing functionality to reduce the memory footprint and attack surface area of each microVM.
  - Firecracker was developed at Amazon Web Services to accelerate the speed and efficiency of services like AWS Lambda and AWS Fargate. 

- https://github.com/e2b-dev/e2b /apache2/202405/ts/python
  - https://e2b.dev/docs
  - Secure cloud runtime for AI apps & AI agents. Fully open-source
  - E2B Sandbox is a secure sandboxed cloud environment made for AI agents and AI apps. Sandboxes allow AI agents and apps to have long running cloud secure environments. 
  - The E2B sandbox can be connected to any LLM and any AI agent or app.
  - Cloud browsers
  - We have built a dedicated SDK for building custom code interpreters in your AI apps. It's build on top of E2B and our core E2B SDK.
  - sdk支持python、js、cli
  - [Show HN: We are building an open-source IDE powered by AI | Hacker News _202304](https://news.ycombinator.com/item?id=35440552)
  - https://github.com/e2b-dev/infra /apache2/202408/go
    - Infrastructure powering E2B - Secure Runtime for AI Agents & Apps
    - there are several components written in Go and a Terraform configuration for the deployment.
  - [Self-hosting E2B on Google Cloud](https://github.com/e2b-dev/infra/blob/main/self-host.md)
    - 🧐 Supported cloud providers: GCP (wip: AWS, Azure, General linux machine)
    - We ask for Terraform v1.5.x because starting from v1.6 Terraform switched their license from Mozilla Public License to Business Source License.
    - PostgreSQL database (Supabase's DB only supported for now)
    - E2B is using Firecracker for Sandboxes. You can build your own kernel and Firecracker version from source by running make build-and-upload-fc-components
- https://github.com/e2b-dev/open-computer-use /apache2/202503/python
  - A secure cloud Linux computer powered by E2B Desktop Sandbox and controlled by open-source LLMs.
  - Uses E2B for secure Desktop Sandbox
  - Operates the computer via the keyboard, mouse, and shell commands
  - Supports 10+ LLMs, OS-Atlas/ShowUI and any other models you want
  - Live streams the display of the sandbox on the client computer
  - User can pause and prompt the agent at any time
  - Uses Ubuntu, but designed to work with any operating system
  - [How I taught an AI to use a computer _202501](https://blog.jamesmurdza.com/how-i-taught-an-ai-to-use-a-computer)

- https://github.com/abshkbh/arrakis /AGPL/202504/go
  - A fully customizable and self-hosted sandboxing solution for AI agent code execution and computer use. 
  - It features out-of-the-box support for backtracking, a simple REST API and Python SDK, automatic port forwarding, and secure MicroVM isolation. 
  - Arrakis provides a secure, fully customizable, and self-hosted solution to spawn and manage Sandboxes for code execution and computer use. It has out-of-the box support for backtracking via snapshot-and-restore.
  - Secure by design, each sandbox runs in a MicroVM.
    - MicroVMs are lightweight Virtual Machines (compared to traditional VMs) powered by Rust based Virtual Machine Managers such as firecracker and cloud-hypervisor.
    - Arrakis uses `cloud-hypervisor` as the VMM.
  - 🐧 Each sandbox runs Ubuntu inside with a code execution service and a VNC server running at boot.
  - Automatically sets up and manages port forwarding from the self-hosted public server to the sanboxes running on it 
  - Supports snapshot-and-restore out of the box i.e. AI Agents can do some work, snapshot a sandbox, and later backtrack to the exact previous state by restoring the snapshot
  - `cloud-hypervisor` only works with `/dev/kvm` for virtualization on Linux machines. Hence, we only support Linux machines.
  - Arrakis also comes with a MCP server that lets MCP clients like Claude Desktop App, Windsurf, Cursor etc.. spawn and manage sandboxes.
  - ✨ customize the default packages and binaries running in a sandbox.
  - Every sandbox comes with a VNC server running at boot. It also comes with Chrome pre-installed.
  - 🆚 any reason why you chose hypervisor over firecracker?
    1. Chv had stable snapshot/restore support. Firecracker didn't
    2. Hotplugging of memory that I thought would help with memory management
    3. I didn't want to be at the mercy of Amazon close sourcing Firecracker

- https://github.com/jamsocket/forevervm /MIT/202503/rust/python/ts/paid
  - https://forevervm.com/
  - foreverVM provides an API for running arbitrary, stateful Python code securely.
  - The core concepts in foreverVM are machines and instructions.
  - Machines represent a stateful Python process. You interact with a machine by running instructions (Python statements and expressions) on it, and receiving the results. A machine processes one instruction at a time.
  - You don't need to terminate machines -- foreverVM will automatically swap them from memory to disk when they are idle, and then automatically swap them back when needed. This is what allows foreverVM to run repls “forever”.
  - [ForeverVM: Run AI-generated code in stateful sandboxes that run forever | Hacker News _202502](https://news.ycombinator.com/item?id=43184686)
  - https://x.com/JamsocketHQ/status/1884660472076513468
    - a Python REPL-as-a-service

- https://github.com/oomol-lab/ovm-core
  - The minimal virtual machine to run podman.
  - Linux kernel: v6.1.50
  - Buildroot: 2023.11.1
  - https://github.com/oomol-lab/ovm
    - Run ovm-core virtual machine on Apple Virtualization Framework
  - https://x.com/realxxnuo/status/1902215577483239875
    - 发现了一个底层开源的 Manus for Code，使用 VSCode 做 IDE + 本地运行的 Podman 虚拟机，支持 GPU 加速、社区共享工作流
    - OOMOL Studio: https://oomol.com

- https://github.com/Exact-Realty/lot /ISC/202405/ts
  - Sandbox for isolating ECMAScript code
  - Our sandbox supports multiple runtimes and allows for bidirectional communication, ensuring you have the flexibility and security to run your code in various environments.
  - Support for multiple runtimes: browser/nodejs/worker
  - Browser isolation using Content Security Policy (CSP)
  - Message passing using the `MessageEvent` class and event listeners for secure communication using the structured clone algorithm
  - Hardening of global variables, including `Function` and `eval`, to prevent direct code execution
  - Bidirectional communication, enabling the parent to call into the sandbox and vice versa
  - Running untrusted code in Node.js is especially risky due to its inherent platform limitations. Our sandbox relies on `node:vm`, which was not designed for running untrusted code.
    - To mitigate these risks, we strongly recommend taking a security-in-depth approach and relying on additional security mechanisms such as process isolation, seccomp(2), pledge(2), ProcessSystemCallDisablePolicy and SELinux, to name a few. 
    - Where feasible, we also recommend static code analysis and code reviews, as well as adequate auditing and logging.
  - Note that the sandbox does not prevent denial-of-service attacks such as infinite loops or memory exhaustion. It's important to take appropriate measures to prevent these types of attacks, such as setting resource limits or using timeouts.

- https://github.com/engineer-man/piston /MIT/202410/js
  - https://emkc.org/run
  - Piston is a high performance general purpose code execution engine. It excels at running untrusted and possibly malicious code without fear from any harmful effects.
  - Piston uses `Isolate` inside Docker as the primary mechanism for sandboxing. 
    - There is an API within the container written in Node which takes in execution requests and executes them within the container safely.
    - High level, the API writes any source code and executes it inside an Isolate sandbox.
    - Piston uses `Isolate` which makes use of Linux namespaces, chroot, multiple unprivileged users, and cgroup for sandboxing and resource limiting. 
    - Code execution submissions on Piston shall not be aware of each other, shall not affect each other and shall not affect the underlying host system.

- https://github.com/teknologi-umum/pesto /apache2/202409/ts/fork
  - Remote Code Execution Engine that lets you execute any piece of code on a remote server via REST API
  - It is heavily inspired by Piston. Pesto is not a fork of Piston, it's an entire rewrite from scratch and therefore it's not compatible with Piston but should be similar
  - Pesto was written with a fresh start, minimizing the dependencies needed, and system controlled for limited resources usage.

- https://github.com/leaningtech/webvm /apache2+NonCommercial/202312/js
  - https://webvm.io/
  - This repository hosts the source code for https://webvm.io, a Linux virtual machine that runs in your browser.
  - WebVM is a server-less virtual environment running fully client-side in HTML5/WebAssembly. 
  - It's designed to be Linux ABI-compatible. It runs an unmodified Debian distribution including many native development toolchains.
  - WebVM is powered by the CheerpX virtualization engine, and enables safe, sandboxed client-side execution of x86 binaries on any browser.
  - CheerpX includes an x86-to-WebAssembly JIT compiler, a virtual block-based file system, and a Linux syscall emulator.
  - This project depends on:
    - CheerpX, made by Leaning Technologies for x86 virtualization and Linux emulation
    - xterm.js, for providing the Web-based terminal emulator
    - Tailscale, for the networking component
    - lwIP, for the TCP/IP stack, compiled for the Web via Cheerp
  - The public CheerpX deployment is provided as-is and is free to use for technological exploration, testing and non-commercial uses.
  - If you want to build a product on top of CheerpX/WebVM, please get in touch with sales
  - https://x.com/tom_doerr/status/1857505332274278907
    - Using linux and open your browser to use linux 😏
    - Works in XR too
    - Very cool. I wonder if it can be leveraged to enhance @vscode to include a terminal too.

- https://github.com/remoteinterview/compilebox /1kStar/MIT/201711/js/inactive
  - CompileBox is a Docker based sandbox to run untrusted code and return the output to your app. 
  - The client-side app submits the code and the languageID to the server through the API. The API then creates a new Docker container and runs the code using the compiler/interpreter of that language. 
  - Once the output is ready it is sent back to the client-side app. The Docker container is destroyed and all the files are deleted from the server.
# browser-emulator 🧭
- https://github.com/thecodacus/OpenWebContainer /MIT/202501/ts
  - https://open-web-container.vercel.app/
  - A browser-based virtual container runtime that enables server-like JavaScript execution environments directly in the browser. 
  - OpenWebContainer provides a sandboxed environment with a virtual file system, process management, and shell capabilities, making it possible to run server-side JavaScript applications entirely in the browser.
  - 依赖quickjs-emscripten
  - The architecture consists of three main layers:
    - UI Layer: React-based user interface with terminal and file explorer
    - Container Manager: Handles communication between UI and Worker
    - Web Worker: Runs the actual container in an isolated thread
  - Roadmap
    - NPM package manager integration
    - Network simulation implementation
    - WebSocket support
    - Add pipe support for shell commands
    - Implement environment variables
    - Add signal handling (SIGTERM, SIGKILL, etc.)
    - Create process groups and job control

- https://github.com/anbraten/nano-web-ide /202411/ts/vue
  - https://nano-ide.vercel.app/
  - Develop the web in the web. This project provides a runtime to run Node.js projects completely in the browser by mocking internals like process. In addition it includes a shell written in javascript to run commands like ls or cd and a playground to test those features.

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

## browser-devtools

- https://github.com/ChromeDevTools/devtools-frontend /BSD/202503/ts
  - The client-side of the Chrome DevTools, including all TypeScript & CSS to run the DevTools webapp.
  - https://github.com/iam-medvedev/chrome-devtools
    - This repository contains a Github Action that runs once a week on a schedule, builds the Chrome DevTools frontend source code, and sends the build code to the main 
- https://github.com/christian-bromann/devtools-backend /apache2/202202/js/inactive
  - A Node. JS implementation of the Chrome DevTools backend for debugging arbitrary web platforms (e.g. HbbTV applications on Smart TVs).

- https://github.com/jiangzhuo/devtools-frontend-demo /202503/js
  - A web interface to manage locally running headless Chrome instances and connect to their DevTools, or manually connect to a remote instance. 
  - Includes a locally hosted Chrome DevTools frontend.

- https://github.com/wanwu/devtools-pro /202112/js/inactive
  - A web remote debugging tools, based on Chrome DevTools.
  - DevTools-pro 是基于chrome-devtools-frontend进行开发的，通过自建 WebSocket 通道实现 Frontend 和 Backend 的通信。
  - 可扩展，支持自定义插件
# playground
- https://github.com/nalgeon/codapi /1.2kStar/apache2/202411/go
  - https://codapi.org/
  - Embeddable code playgrounds for education, documentation, and fun.
  - Codapi is a platform for embedding interactive code snippets directly into your product documentation, online course, or blog post.
  - Codapi manages sandboxes (isolated execution environments) and provides an API to execute code in these sandboxes. 
  - It also provides a JavaScript widget codapi-js for easier integration.
  - Custom sandboxes for any programming language, database, or software.
  - Available as a cloud service and as a self-hosted version.
  - https://github.com/nalgeon/sandboxes
    - This repository contains sandboxes for Codapi
    - To use a particular sandbox, install Codapi and add the sandbox.
    - Sandbox = image + box + commands:
      - Image as a Docker image containing specific software, like a compiler or a database engine.
      - Box is a configuration for running a container: cpu and memory restrictions, file systems, etc.
      - Commands are predefined actions you can run in a container.

- https://github.com/voronianski/esnextbin /201905/js
  - Prototype JavaScript apps in the browser with ES2015's latest features and importing modules directly from NPM.

- https://github.com/langgenius/dify-sandbox /apache2/202410/go/inactive
  - https://docs.dify.ai/development/backend/sandbox
  - DifySandbox is a lightweight, fast, and secure code execution environment that supports multiple programming languages, including `Python` and `Node.js`. 
  - 我们开源了 Dify Sandbox，这是一个从 Dify 中衍生出的代码运行时项目。安全，安全，还是为了安全
  - built on `Seccomp`, a low-level security mechanism that enables support for multiple programming languages
  - It is designed to be used in a multi-tenant environment, where multiple users can submit code to be executed. 
  - The code is executed in a sandboxed environment, which restricts the resources and system calls that the code can access.
    - System Security: It implements a whitelist policy, allowing only specific system calls to prevent unexpected security breaches.
  - File System Isolation: User code runs in an isolated file system environment.
  - Network Isolation: DockerCompose or k8s-Egress
  - DifySandbox currently only supports Linux, as it's designed for docker containers
  - [I don't care about the security of the system, How can i set up permission to allow all permissions _202503](https://github.com/langgenius/dify-sandbox/issues/139)

- https://github.com/ishaan1013/sandbox /MIT/202408/ts
  - A cloud-based code editing environment with an AI copilot and real-time collaboration.
  - It's an OSS code editor with AI code autocompletion and real-time multiplayer collaboration (powered by @liveblocks )
  - Built with @nextjs + @clerkdev + @shadcn UI and it's fully self-hostable via @docker
  - https://x.com/steventey/status/1796352490100896149
    - How is it fully self-hostable if it relies on three SaaS services? Seems more like partially self-hostable?
    - I rebuilt @Replit — Sandbox is an open-source cloud code editing environment with an AI copilot and multiplayer collaboration, made with @Nextjs + @CloudflareDev Workers
    - The backend consists of a primary Express and Socket.io server, and 3 Cloudflare Workers microservices for the D1 database, R2 storage, and Workers AI.
    - 🧊 Each open sandbox instantiates a secure Linux sandboxes on `E2B`, which is used for the terminal and live preview.
    - How is it fully self-hostable if it relies on three SaaS services? Seems more like partially self-hostable?

- https://github.com/freewheel/code-kitchen /apache2/202402/ts
  - https://freewheel.github.io/code-kitchen/home
  - A pure-static live-coding playground that is easy to be used in a closed source environment for React UI Libraries
  - [Code Kitchen: 一个支持多文件与私有库的离线 React Playground 方案 | pengx17 _202203](https://pengx17.vercel.app/posts/code-kitchen-intro)
    - 可能是目前最廉价的实现多文件、支持私有库的离线 React playground 方案。
    - 目前 Code Kitchen 与 React 框架绑定。我们会持续探索如 Vue/Angular 等其他框架结合的可能性。
    - 由于 Code Kitchen 核心依赖于 esbuild-wasm，本身体积较大（经过压缩后依然有 2.5M），与 React Live 这样的方案相比不够轻量

- https://github.com/huozhi/devjar /MIT/202402/js/inactive
  - https://devjar.vercel.app/
  - live code runtime for your react project in browser
  - devjar only works for browser runtime at the moment. It will always render the default export component in index.js as the app entry.
  - 依赖sucrase
# codesandbox-like
- https://github.com/rajatmaheshwari2512/codefiddle /202308/ts
  - This project is a take on how a site like CodeSandbox could be built.
  - 依赖antd.v5、@monaco-editor/react、xterm、zustand、express、directory-tree
  - The basic layout provides a VS Code experience, wherein a user can navigate between his available files from the file manager. 
  - Integrated with this is also an iframe providing realtime feedback to changes you may make in your project. 
  - [Made an online code editor, like CodeSandbox. Think VS Code in the browser : node _202304](https://www.reddit.com/r/node/comments/12ceajg/made_an_online_code_editor_like_codesandbox_think/)
    - I've made an online code editor from scratch
    - It uses `xterm.js` to give a shell to the user on the frontend, and `monaco` editor for editing your files, and I generate the folder structure recursively. 
    - I've used `Zustand` for global state management
    - I tried to get it as close to VS Code as possible, and there's a bunch of stuff still left to do

## sandpack-examples

- https://github.com/jerrywu001/sandpack-vue3 /MIT/202402/ts
  - https://sandpack-vue3.js-bridge.com/
  - Vue3 components that give you the power of editable sandboxes that run in the browser.
# nodebox/webcontainer 🧊
- https://github.com/Sandpack/nodebox-runtime
  - https://sandpack.codesandbox.io/docs/advanced-usage/nodebox
  - Nodebox is a runtime for executing Node.js modules in the browser.
  - For personal usage, there are no limitations on how you can use Sandpack 
  - For commercial usage, you can freely use all Sandpack templates except: 
    - nextjs, any vite template, astro, node.
    - Any other sandbox that uses Nodebox as a runtime environment.
  - If you are interested in using Sandpack 2.0 or Nodebox for commercial purposes, please contact us.
  - Can I run Nodebox without Sandpack?
    - Yes, we made Nodebox available as a standalone package on npm
  - [Docs don't explain how to self host a Nodebox instance? _202308](https://github.com/Sandpack/nodebox-runtime/issues/48)
    - We can work out a solution if this is required, usually with a custom license on a per company/customer basis.

- https://github.com/RealSput/Wenode /202302/js/inactive
  - WebContainers, except it's a million times easier to use
  - https://wenode.seven7four4.repl.co (hosted on Replit to be able to use SharedArrayBuffers)
  - [I wrote a library called Wenode, which takes the concept of WebContainers and makes it so readable that even beginner programmers could even understand it. : r/webdev _202302](https://www.reddit.com/r/webdev/comments/11c1wao/i_wrote_a_library_called_wenode_which_takes_the/)

- https://github.com/olydis/node-in-browser /202209/ts/inactive
  - https://node-in-browser.pages.dev/
  - An experiment to bootstrap Node.js (version 8.0.0) in the browser in order to run Node apps or npm libraries unmodified.
  - [How to run Node.js (apps) in the browser? | by Johannes Bader | CloudBoost _201711](https://blog.cloudboost.io/how-to-run-node-js-apps-in-the-browser-3f077f34f8a5)

- https://github.com/opensumi/codeblitz /MIT/202401/ts/inactive
  - https://codeblitz.opensumi.com/
  - https://openlab.antchain.antgroup.com/ide
  - https://codeblitz.cloud.alipay.com/zh
  - 基于 OpenSumi 的纯前端 IDE 基础框架
  - Pure front-end IDE framework based on OpenSumi
  - 除了无法运行 node 服务，在前端上体验和标准的产品是完全一致的
  - 模拟文件服务以保持与 IDE 产品一致。提供多种文件系统服务，包括基于内存、基于 IndexedDB 和基于远程接口等文件系统
  - 提供了基于Worker的语言服务，支持语法高亮和LSP语言服务，具备语法分析、智能补全、格式化等功能
  - anycode扩展支持很多语言java/php
  - https://github.com/opensumi/codeblitz-sample
  - [会和stackblitz一样吗？特别是web container方面 _202309](https://github.com/opensumi/codeblitz/issues/16)
    - 这次开源的是无需容器在浏览器的运行的 IDE 框架，类似于 stackblitz 提供的 IDE 产品一样，通过 codeblitz 可能做出类似于 stackblitz 一样的 IDE 产品，
    - 但是 stackblitz 除了 IDE 还有一块就是你说的 web container 的技术，这块本次没有开源，内部还在验证中，如果你有需要也可以直接使用 stackblitz 提供的 webcontainers.io/guides/quickstart 或者用 codesandbox 提供的 codesandbox/nodebox-runtime 来和 codeblitz 集成
  - [极速版 IDE 框架 CodeBlitz 开源啦！ - 知乎_202309](https://zhuanlan.zhihu.com/p/656515617)
    - 在OpenSumi的基础上对文件系统、通信系统、插件机制等模块进行扩展，以更好地适用于没有容器、本地客户端环境的纯浏览器环境
    - CodeBlitz提供了一种只需使用浏览器即可体验
    - IDE的场景。与github.dev和vscode.dev不同的是，CodeBlitz是一个框架，通过OpenSumi模块和插件的方式，可以为上层产品量身定制符合其业务场景的WebIDE。
  - [如何评价阿里 & 蚂蚁自研 IDE 研发框架 OpenSumi？ - 知乎](https://www.zhihu.com/question/519740662)
    - 高性能、高定制性的双端（Web 及 Electron）IDE 研发的框架
    - 设计之初就是要兼容 VS Code 插件生态，我们计划每三个月时间去完成一次 VS Code 插件 API 的适配工作
  - [比快更快，极速版 IDE 框架 CodeBlitz 开源 ](https://www.sohu.com/a/719044467_355140)
    - 文件系统：利用 BrowserFS 的能力，在浏览器实现了七种文件读写策略，可以应对不同的业务场景；如果内置的文件系统不能满足需求，集成方也可以提供 FileSystemProvider 自己实现文件系统接口
    - 语言服务：通过和蚂蚁代码分析团队的合作，CodeBlitz 支持了 Java、TS、JS 三种语言的离线语言服务索引（LSIF）服务，可在代码提交时离线计算当前代码索引用于语言服务的展示；
      - 同时借助于 Tree-sitter 技术，对于 Python、Go 、Rust、C++、Php 几种语言也支持简单的定义跳转、查找引用等功能
      - 正在尝试将 OpenSumi Node.js 插件进程运行在浏览器 WASM 环境，提供与有容器版本一致的 TS/JS 语言服务能力，进一步增强语言服务体验
    - 通信方式改造：将之前基于 WebSocket 调用的方式改造为前端 Function 直接的调用，前端无需感知环境的变化，调用后端无需修改替换前端 Provider 实现，直接通过 DI 方式替换后端模块实现即可
  - [我们用大模型给 IDE 升了个级，这是我们总结的万字心得 ](https://www.53ai.com/news/qianyanjishu/1996.html)
    - 尽管有补全和对话视图这样的基础 API 功能，VS Code 对于其他研发活动开放出来 AI 扩展功能非常有限，无法对运行、调试、问题面板、终端、Git 等 IDE 功能进行更多的扩展，包括最新的 Participant API 也只供给 GitHub Copilot 对话进行扩展，以至于 Anysphere 的 Cursor、字节的 MarsCode 需要 Fork VS Code 进行定制化开发，以便满足其特殊需求，但这样的分叉又不可避免地增加了后续升级和解决冲突的成本。
    - 市面上迫切需要一个可以高度定制和扩展的 AI 原生 IDE 框架，这个框架应当能够对代码补全、问题诊断、终端操作、调试、对话、IDE 设置等功能进行 AI 封装，并提供即插即用的集成方式
    - OpenSumi 在 2023 年 7 月份开始进行 AI 方向的改造，目标是将 OpenSumi 从传统 IDE 框架升级至 AI Native IDE Framework

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

## nodebox-examples

## webcontainer-examples

- https://github.com/kat-tax/vslite /MIT/202312/ts/inactive
  - https://vslite.dev/
  - More than Monaco, less than VSCode
  - 依赖@monaco-editor/react、@webcontainer/api、dockview
  - https://discord.com/channels/364486390102097930/681363253607006238/1115011573891735645
    - I'm working on a lite version of VSCode 
    - There's a file system tree, Webcontainer shell w/ terminal, docking system, and more.
    - Eventually the plan is to be able to embed it easily into other projects and manipulate it via postMessage.

- https://github.com/xun082/online-edit /MIT/202309/ts/inactive
  - https://xun082.github.io/online-edit/
  - 在线代码编辑器
  - [我开源了一个能在浏览器上执行 npm 命令的在线代码编辑器 _202308](https://juejin.cn/post/7272869799960281151)

- https://github.com/wangrongding/web-ide /202311/ts/vue/inactive
  - 从零到一实现一个基于 web 的在线代码编辑器，目前正在开发阶段。
  - terminal : 运行在 web 上的终端，基于 WebContainer 实现
  - editor : 基于 web 的编辑器
  - file : 基于 web 的文件管理器

- https://github.com/neverUsedGithub/WebEditor /202304/js/inactive
  - A basic online code editor using Webcontainers.
# sandbox-linux
- https://github.com/netblue30/firejail /GPL/202504/c
  - https://firejail.wordpress.com/
  - Linux namespaces and seccomp-bpf sandbox
  - Firejail is a lightweight security tool intended to protect a Linux system by setting up a restricted environment for running (potentially untrusted) applications.
  - it is an SUID sandbox program that reduces the risk of security breaches by using Linux namespaces, seccomp-bpf and Linux capabilities. It allows a process and all its descendants to have their own private view of the globally shared kernel resources, such as the network stack, process table and mount table. 
  - Firejail can work in an SELinux or AppArmor environment, and it is integrated with Linux Control Groups.
  - Written in C with virtually no dependencies, the software runs on any Linux computer with a 3.x kernel version or newer.
  - The sandbox is lightweight, the overhead is low. There are no complicated configuration files to edit, no socket connections open, no daemons running in the background. All security features are implemented directly in Linux kernel and available on any Linux computer.
# utils
- https://github.com/ximing/jsvm2 /202402/ts
  - Javascript Interpreter implemented by typescript（TS实现的JS解释器）
  - https://github.com/ximing/jsvm3 /202402/ts
    - 自定义字节码的jsvm
  - https://x.com/XGHeaven/status/1797982601569058816
    - 笑死了，原本想看看自己的 jsvm 性能好不好，一开始发现跑不起来，辛辛苦苦补了一堆缺失的 API 后跑起来了（才发现连 while 都没支持），终于跑起来了。
    - 结果，只能到 sablejs 的 10%，我就知道，一开始没把性能作为主要目标是对的。

- https://github.com/unjs/jiti /ts
  - Runtime Typescript and ESM support for Node.js
# wasm-based
- https://github.com/ktock/container2wasm /apache2/202405/cpp
  - https://ktock.github.io/container2wasm-demo/
  - a container-to-wasm image converter that enables to run the container on WASM.
  - Converts a container to WASM with emulation by Bochs (for x86_64 containers) and TinyEMU (for riscv64 containers).
  - Runs on WASI runtimes (e.g. wasmtime, wamr, wasmer, wasmedge, wazero)
  - Runs on browser
  - contaienr2wasm creates a WASM image that runs the container and the Linux kernel on the emulated CPU.
  - Though more and more programming languages start to support WASM, it's not easy to run the existing programs on WASM. 
    - This sometimes requires re-implementing and re-compiling them and costs extra time for development. 
    - This is a PoC converter tries to solve it by enabling running unmodified containers on WASM.
# miniprogram/小程序
- https://github.com/yeliex/cromosjs /202310/ts/inactive
  - 简单的小程序跨平台解决方案
  - 实验性质的小程序web运行时
  - 传统解决方案中, 小程序相关的跨端解决方案主要有
    - 将web代码运行在小程序上, 低成本的比如webview, 高级的比如kbone
    - 将web代码编译成小程序原生, 比如taro
    - 将小程序代码编译成跨端代码, 比如morjs
# cloud-browser
- https://github.com/m1k1o/neko /12.5kStar/apache2/202507/go
  - https://neko.m1k1o.net/
  - A self hosted virtual browser that runs in docker and uses WebRTC.
  - you can browse the web, run applications, and perform other tasks just as you would on a regular browser, all within a secure and isolated environment
  - Neko offers the ability for multiple users to access it simultaneously
  - This app uses WebRTC to stream a desktop inside of a docker container
  - It is not only limited to a browser; it can run anything that runs on linux (e.g. VLC). Browser only happens to be the most popular and widely used use-case.
  - Compared to clientless remote desktop gateway (e.g. Apache Guacamole or websockify with noVNC), installed with remote desktop server along with desired program (e.g. linuxserver/firefox) provides neko additionally: built-in audio, Multi-participant control
# more
- https://github.com/BrowserBox/BrowserBox /AGPLv3/js
  - https://dosyago.com/
  - BrowserBox is Web application virtualization via zero trust remote browser isolation and secure document gateway technology.
  - Remote browser isolation is a cybersecurity model that physically isolates a user's browsing activity away from their local networks and infrastructure. With BrowserBox, this isolation provides an extra layer of security against web-based threats.
