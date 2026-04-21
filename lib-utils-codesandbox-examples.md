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
# popular
- https://github.com/coplane/localsandbox /MIT/202601/python/ts
  - Lightweight AgentFS sandbox that runs bash and python.
  - A Python SDK for sandboxed filesystem operations, built on just-bash, AgentFS, and Pyodide. Provides AI agents with a persistent, isolated environment backed by SQLite.
  - Sandboxed Execution: Run bash commands in an isolated environment
  - Run Python via Pyodide (WebAssembly) on the same virtual filesystem
  - All file operations persist across commands in SQLite
  - Key-Value Store: Separate KV API for agent state management
  - Snapshot & Resume: Export/restore complete sandbox state
  - Full async API via asyncio.to_thread
  - [Localsandbox: A Lightweight Agent Sandbox _202601](https://coplane.com/perspectives/localsandbox)
  - https://github.com/manojlds/heimdall
    - A TypeScript MCP server providing sandboxed Python and Bash execution using Pyodide (Python compiled to WebAssembly) and just-bash.
    - Virtual Filesystem: Read, write, list, and delete files in a persistent workspace
    - Secure Sandbox: Python code runs in an isolated WebAssembly environment
    - Install pure Python packages via micropip
    - Native Integration: Direct Pyodide and just-bash integration (no subprocess bridge)
    - Bash and Python share the same workspace filesystem
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
- https://github.com/codesandbox/sandpack /5.8kStar/apache2/202502/ts/inactive
  - https://sandpack.codesandbox.io/
  - https://sandpack.codesandbox.io/docs
  - Sandpack is a component toolkit for creating your own live running code editing experience powered by CodeSandbox.
  - 依赖codemirror6、lz-string、react-devtools-inline
  - 未实现跳转到定义的功能
  - Sandpack Client: This is a small foundation package that sits on top of the bundler. It is framework agnostic and facilitates the handshake between your context and the bundler iframe.
  - Sandpack React: React components that give you the power of editable sandboxes that run in the browser
  - [Is sandpack as a project dead/legacy? _202501](https://github.com/codesandbox/sandpack/issues/1243)
    - 👷: I think that we have been slow on this repo in particular. We have been mostly working on CodeSandbox itself and completely forgot about the Sandpack repo. This slipped through the cracks when Danilo left.
      - I think that running NodeJS in the browser is still a valid and interesting space. The challenge here is that all revenue (in CodeSandbox's case) comes from our VM offering (and indeed, specifically for AI agents & text->app builders). Because of this, there has been less focus on Sandpack lately.
    - Given that huge leap forwards in Ai capabilities re. software engineering, together with huge speed and cost improvements in cloud-based containerisation, I am starting to wonder if running NodeJs in the browser is itself somewhat of a dead end?
- https://github.com/AaronPowell96/sandpack-file-explorer /MIT/202312/ts
  - Enhanced File Explorer for Sandpack. Providing immense flexibility to Sandpack's capabilities.
  - https://github.com/fewismuch/sandpack-file-explorer

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

- https://github.com/dabbott/javascript-playgrounds /1.4kStar/BSD/202411/ts/inactive
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
  - [Is there an open-source alternative to e2b (e2b.dev. Code interpreting for your AI app)? : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1chsx7z/is_there_an_opensource_alternative_to_e2b_e2bdev/)
    - The reason we aren't using containers for code execution is because they aren't secure. We're using Firecracker micro VMs under the hood instead.
- https://github.com/e2b-dev/open-computer-use /apache2/202503/python
  - A secure cloud Linux computer powered by E2B Desktop Sandbox and controlled by open-source LLMs.
  - Uses E2B for secure Desktop Sandbox
  - Operates the computer via the keyboard, mouse, and shell commands
  - Supports 10+ LLMs, OS-Atlas/ShowUI and any other models you want
  - Live streams the display of the sandbox on the client computer
  - User can pause and prompt the agent at any time
  - Uses Ubuntu, but designed to work with any operating system
  - [How I taught an AI to use a computer _202501](https://blog.jamesmurdza.com/how-i-taught-an-ai-to-use-a-computer)

- https://github.com/microsandbox/microsandbox /3.5kStar/apache2/202507/rust
  - https://docs.microsandbox.dev/
  - Self-Hosted Plaform for Secure Execution of Untrusted User/AI Code
  - Strong Isolation - Hardware-level VM isolation with microVMs
  - Self-hosted with full control
  - OCI Compatible - Works with standard container images
  - AI-Ready - Built-in MCP support for seamless AI integration
  - microsandbox server is also an MCP server, so it works directly with Claude, Agno and other MCP-enabled AI tools and agents.
  - libkrun - The lightweight virtualization library that powers our secure microVM isolation
  - 源码未使用 Firecracker
  - [Microsandbox vs. Docker](https://github.com/microsandbox/microsandbox/blob/main/MSB_V_DOCKER.md)
    - Microsandbox leverages microVM technology (KVM on Linux, Hypervisor.framework on macOS), providing true hardware-level virtualization. Each sandbox runs its own isolated kernel, creating a significantly stronger security boundary through CPU virtualization extensions.
    - Docker uses container technology with process-level isolation through Linux namespaces and cgroups. While efficient, all containers share the host kernel
  - [Microsandbox - A self-hosted alternative to AWS Lambda, E2B. Run AI code in fast lightweight VMs : r/Python _202505](https://www.reddit.com/r/Python/comments/1ktg6mm/microsandbox_a_selfhosted_alternative_to_aws/)
    - Cloud sandboxes like AWS Lambda, E2B, Flyio, give you less control and slower dev cycles, Docker containers offer limited isolation for untrusted multi-tenant code, traditional VMs are slow to start and resource-heavy, and running code directly on your machine is a no-go
    - Do you have to push a file with the code you want to run the msb? Or can you also inject code at runtime? E.g. lets say an llm generates some test code, do i need to package it first?
      - You can just inject the code at runtime.
    - How does this work from a resource consumption perspective, does each msb instance consume a thread?
      - There is just the msb server that receives your code and commands and runs it in a virtual machine. And as for concurrency, msb server can run multiple of vms at once. These are lightweight vms with very low overhead
    - how would you run this on a separate machine? Do I need to wrap and api, bash scripts or something else?
      - You simply install the msb CLI and start the server on the machine. There is nothing to wrap. The SDK handles the part of sending the code to the right msb server for execution.
    - It uses microVMs - lightweight virtual machines with amazingly low overhead. You probably have heard of Firecracker, the tech behind Amazon Lambda. You basically get the same sandbox guarantees as a traditional virtual machine. These are hardware-enabled virtualization. Each sandbox runs its own kernel.

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

- https://github.com/daytonaio/daytona /21.1kStar/AGPL/202508/go
  - https://daytona.io/
  - Secure and Elastic Infrastructure for Running Your AI-Generated Code.
  - OCI/Docker Compatibility: Use any OCI/Docker image to create a Sandbox
  - [Top Daytona.io alternatives for running AI code in secure sandboxed environments | Blog — Northflank _202507](https://northflank.com/blog/top-daytona-io-alternatives-for-running-ai-code-in-secure-sandboxed-environments)
    - Daytona pivoted in February 2025 from development environments to become infrastructure for running AI-generated code. They provide sandboxes through an SDK that lets AI agents execute code in isolated environments.
    - Under the hood, Daytona's default configuration uses standard Docker containers, though they support enhanced isolation through Kata Containers and Sysbox when explicitly configured. This tiered approach means security depends heavily on your configuration choices.
    - Daytona is built for AI agent workflows, not comprehensive infrastructure. If you're trying to run production workloads beyond just code snippets, like databases, long-running services, or GPU jobs, you'll need a more complete platform
    - E2B.dev uses Firecracker microVMs with great persistence features but no self-hosting in production.
    - Vercel Sandbox uses Firecracker microVMs for development environments but with session limits.
    - Cloudflare Workers uses V8 isolates for blazing-fast edge functions but no persistent state.
    - Modal provides fast Python containers with gVisor isolation, ideal for ML workloads but Python-only. Modal uses gVisor containers
    - Northflank offers production-proven Kata Containers powered microVMs, and gVisor, with full orchestration, GPU support, long-running jobs, Bring Your Own Cloud (BYOC), and runs your entire infrastructure, not just sandboxes.
      - Technologies like Kata Containers with Cloud Hypervisor (CLH) and gVisor, giving you flexibility in your secure compute stack

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

- https://github.com/BinSquare/ERA /202511/python/go
  - Open source secure sandboxing for running Agents.
  - [Building an opensource local sandbox to run agents : r/LocalLLM](https://www.reddit.com/r/LocalLLM/comments/1okfrp6/building_an_opensource_local_sandbox_to_run_agents/)

- https://github.com/superagent-ai/vibekit /MIT/202511/ts
  - Run Claude Code, Gemini, Codex — or any coding agent — in a clean, isolated sandbox with sensitive data redaction and observability baked in.
  - Local sandbox - Runs agent output in isolated Docker containers
  - Built-in redaction - Auto-removes secrets, api keys, and other sensitive data completions
  - Universal agent support - Works with Claude Code, Gemini CLI, Grok CLI, Codex CLI, OpenCode, and more
  - Works offline & locally - No cloud dependencies or internet required
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
# ai-sandbox 👾
- https://github.com/anthropic-experimental/sandbox-runtime /1.6kStar/apache2/202511/ts
  - A lightweight sandboxing tool for enforcing filesystem and network restrictions on arbitrary processes at the OS level, without requiring a container.
  - `srt` uses native OS sandboxing primitives (`sandbox-exec` on macOS,  `bubblewrap` on Linux) and proxy-based network filtering. 
    - The sandbox uses OS-level primitives to enforce restrictions that apply to the entire process tree
  - It can be used to sandbox the behaviour of agents, local MCP servers, bash commands and arbitrary processes.
  - This package provides a standalone sandbox implementation that can be used as both a CLI tool and a library.
  - Network restrictions: Control which hosts/domains can be accessed via HTTP/HTTPS and other protocols
  - Filesystem restrictions: Control which files/directories can be read/written (defaulting to allowing writes to the current working directory)
  - Unix socket restrictions: Control access to local IPC sockets
  - 🌰 可搜索使用示例

- https://github.com/openai/codex/tree/main/codex-rs/windows-sandbox-rs /apache2/202603/rust
  - Codex app for Windows 中的 windows-sandbox-rs 也一并开源了。
  - https://x.com/zhangjintao9020/status/2029357059913798119
    - 我大致看了下，感觉这个沙箱主要是创建了一个在登陆界面隐藏的使用随机密码的用户，然后获取该用户令牌后进行 XP 时期提供的创建受限令牌操作，Job Objects 限制基本没做啥……就个人感觉隔离程度有但还没有令人放心到放手一搏的地步（强度比 Chromium 沙盒和 Sandboxie 低很多）
    - 我很多年前倒是在 NSudo 研究过通过创建受限令牌降权到 UAC 提升之前的方式，关于我的研究最终发现还是获取 Linked Token 最好，倒是 Codex 那个沙盒的受限令牌创建 LUA 实现我之前在 NSudo 实现过类似的（只是创建受限令牌的时候我没有引入 DISABLE_MAX_PRIVILEGE 和 WRITE_RESTRICTED）

- https://github.com/vercel-labs/just-bash /152Star/apache2/202601/ts
  - A simulated bash environment with an in-memory virtual filesystem, written in TypeScript.
  - Designed for AI agents that need a secure, sandboxed bash environment.
  - Supports optional network access via curl with secure-by-default URL filtering.
  - 能执行curl
  - ❓ 能执行安装依赖/binary包吗
  - https://x.com/cramforce/status/2004992618913251786
  - I'm introducing my holiday project: just-bash _20251228
    - just-bash is a pretty complete implementation of bash in TypeScript designed to be used as a bash tool by AI agents. Because it turns out agents love exploring data via shell scripts, even beyond coding.
    - It comes with grep, sed, awk and the 99th percentile features that an agent like Claude Code or Cursor would use. In fact, Claude Code can use it for secure bash execution.
    - An overlay filesystem to feed files to your agent securely
    - A Vercel Sandbox compatible API, so you can quickly upgrade to a real VM if you need to run binaries
    - It was essentially entirely written by Opus 4.5. Coding agents love bash and they are good at reproducing it. They are also great at text-book recursive descent parsers and AST tweet-walk interpreters. 
    - It has cURL already

- https://github.com/rivet-dev/agent-os /1.4kStar/apache2/202604/ts/rust
  - https://www.rivet.dev/agent-os
  - A portable open-source operating system for agents. 
  - Powered by WebAssembly and V8 isolates.
  - Near-zero cold starts (~6 ms), up to 32x cheaper than sandboxes.
  - Supports Pi, Claude Code *, Codex*, Amp*, and OpenCode* 
  - Runs inside your process: No VMs to boot, no containers to pull. Agents start in milliseconds with minimal memory overhead.
  - Embeds in your backend: Agents call your functions directly via host tools. No network hops, no complex auth between services.
  - Granular security: Deny-by-default permissions for filesystem, network, and process access. The same isolation technology trusted by browsers worldwide.
  - Deploy anywhere: Just an npm package. Works on your laptop, Rivet Cloud, Railway, Vercel, Kubernetes, or any container platform.
  - agentOS is a lightweight VM that runs inside your process. Sandboxes are full Linux environments. 
  - You don't have to choose: agentOS works with sandboxes through the sandbox extension, spinning up a full sandbox on demand and mounting the sandbox's file system when the workload needs it.
  - agentOS mounts anything as a familiar directory tree: - S3 buckets - SQLite databases - Google Drive - Host file system
  - agentOS is built on an in-process operating system kernel written in JavaScript. Three runtimes mount into the kernel:
    - WebAssembly: POSIX utilities (coreutils, grep, sed, etc.) compiled to WASM
    - V8 isolates: JavaScript/TypeScript agent code runs in sandboxed V8 contexts
    - The kernel manages a virtual filesystem, process table, pipes, PTYs, and a virtual network stack. Everything runs inside the kernel -- nothing executes on the host.
    - runs anywhere: Your laptop. Railway. Vercel. Kubernetes. ECS. Lambda. Cloud Run. A Raspberry Pi.
  - https://x.com/rivet_dev/status/2039015678959853678
    - A portable open-source OS built just for agents. Powered by WASM & V8 isolates.
    - Embedded in your backend
    - Mount anything as a file system (S3, SQLite, …)
  - Why WebAssembly + V8? 
    - Traditional sandboxes boot entire VMs or containers. agentOS runs agents inside lightweight VMs within your own process. Same isolation technology behind Google Chrome. Battle-tested
    - No VMs. No containers. No Docker images to pull. Just fast, secure execution.
  - How is this different from Anthropic's srt?
    - With wasm capabilities are additive so rather than starting with attack surface area and progressively securing it you begin with security and add who you want.
    - Different layers:
      - agentOS: Zero shared syscall surface, fully portable, runs everywhere including browsers
      - srt/bubblewrap: Policy enforcement on real processes. Great for interactive coding agents where a human is in the loop. Not suitable for production deployments (security is a spectrum, full thoughts will not fit in this tweet.)
      - gVisor: Reimplements Linux syscalls in userspace. Strong isolation but wide attack surface. Linux-only, needs elevated privileges on most managed platforms.
      - 👀 srt has ~100% Linux support, agentOS is an entirely new OS, so not everything works out of the box.
      - Highly recommend reading about our sandbox extensions too
  - https://x.com/NathanFlurry/status/2039428265283391581
    - Memory of coding harnesses in agentOS (portable WASM OS for agents): 🥇 Codex (WASM): 122 MB, 🥈 Pi (V8): 153 MB, 🥉 Claude Code (V8): 316 MB
    - This is the memory for the *entire* VM, including bash, Node.js, Python, git fully loaded
    - This is Python / Node.js fully loaded without any libraries, correct? Also what do you mean by "Python fully loaded"? Isn't CPython quite sizable in memory usage when you actually use it
      - Not loaded in memory, it's just on disk. Emphasizing that agentOS is POSIX-compliant in contrast with the memory overhead of a heavier-weight VM
    - I wonder how you got Claude Code running here
      - Little bit of http://secureexec.dev magic, lotta bit of API shims
  - https://x.com/NathanFlurry/status/2039802278904053799
    - Why we built Rivet agentOS with WebAssembly:
    - Agents need file systems on S3
    - Agents expect Linux tools to work with the file system
    - Virtual machines require a lot of memory
    - agentOS uses WASM with a fraction of the RAM
    - Most importantly, agentOS supports Sandbox Mounting in order to use a VM in use cases where it makes sense, such as: Heavy-weight workloads, Computer/Browser Use

- https://github.com/rivet-dev/sandbox-agent /536Star/apache2/202602/rust/ts
  - https://sandboxagent.dev/
  - Introducing Sandbox Agent SDK: A universal API for automatic coding agents in sandboxes
  - Universal Session Schema: Standardized schema that normalizes all agent event formats for storage and replay
  - Human-in-the-Loop: Approve or deny tool executions and answer agent questions remotely over HTTP
  - Runs Inside Any Sandbox: Lightweight static Rust binary. One curl command to install inside E2B, Daytona, Vercel Sandboxes, or Docker
  - Server or SDK Mode: Run as an HTTP server or embed with the TypeScript SDK
  - The Sandbox Agent acts as a universal adapter between your client application and various coding agents. 
  - Embedded Mode: Runs agents locally as subprocesses
  - Server Mode: Runs as HTTP server from any sandbox provider, Rust daemon (sandbox-agent server) exposing the HTTP + SSE AP
  - https://x.com/rivet_dev/status/2016548084696727842 _202601
    - Claude Code, Codex, OpenCode, Amp all have different APIs. Sandbox Agent SDK unifies them.
    - 100% open-source
    - Universal session schema means no more parsing five different formats.
    - Pairs with Rivet Actors for automatic transcript persistence, real-time streaming to clients, and full session replay.
  - https://github.com/rivet-dev/sandbox-agent/tree/main/gigacode
    - https://x.com/NathanFlurry/status/2019759962482725149
    - Introducing Gigacode: Use @opencode 's UI with any coding agent
    - Supports Claude Code, Codex, & Amp harness
    - Not a fork (opencode attach)
    - Powered by Sandbox Agent SDK ( @rivet_dev )

- https://github.com/ColeMurray/background-agents /MIT/202601/python/ts
  - https://backgroundagents.dev/
  - open-source background coding agent system inspired by Ramp's Inspect.
  - https://x.com/_colemurray/status/2016210023366717818
    - OpenInspect is an open source implementation of Ramp's background agent blog post.
  - https://x.com/_colemurray/status/2034664228272099474
    - VSCode Code Server In-browser
    - OpenInspect now contains a hosted VSCode instance which runs inside of the sandbox. 
    - You can now make manual changes without having to clone the repo locally
  - [Why We Built Our Own Background Agent: Inspect — Ramp Builders Blog _202601](https://builders.ramp.com/post/why-we-built-our-background-agent)
    - Inspect writes the code like any other coding agent, but closes the loop on verifying its work by having all the context and tools needed to prove it
    - Each session runs in a sandboxed VM on Modal with everything an engineer would have locally: Vite, Postgres, Temporal, the works.

- https://github.com/pydantic/monty /695Star/MIT/202602/rust/python
  - A minimal, secure Python interpreter written in Rust for use by AI
  - https://x.com/samuelcolvin/status/2019604402399768721  _202602
    - Monty: a new python implementation, from scratch, in rust, for LLMs to run code without host access.
    - This will power CodeMode in @pydantic AI.
  - https://x.com/mitsuhiko/status/2019731099870777532
    - I'm really happy that we're not just seeing full VM sandbox approaches but also stiff like vercel's just-bash and now monty.

- https://github.com/agent-infra/sandbox /1.7kStar/apache2/202512/python/ts/字节/docker
  - https://sandbox.agent-infra.com/
  - All-in-One Sandbox for AI Agents that combines Browser, Shell, File, MCP and VSCode Server in a single Docker container.
  - https://x.com/ByteDanceOSS/status/2037355958897369167
    - AIO Sandbox ships a complete, pre-wired environment in a single Docker container.
    - The AIO (All-in-One) Sandbox is a containerized environment designed for both human developers and AI agents. 
    - Its architecture is built around a "Batteries-Included" philosophy, providing a full Linux desktop-like environment inside a single Docker container.
    - Unified Environment: One Docker container with shared filesystem. Files downloaded in the browser are instantly accessible in Terminal and VSCode.
    - Out of the Box: Built‑in VNC browser, VS Code, Jupyter, file manager, and terminal—accessible directly via API/SDK.

- https://github.com/alibaba/OpenSandbox /3.8kStar/apache2/202603/python/go
  - https://open-sandbox.ai/zh/
  - 面向 AI 应用场景设计的「通用沙箱平台」，为LLM相关的能力（命令执行、文件操作、代码执行、浏览器操作、Agent 运行等）提供 多语言 SDK、沙箱接口协议和沙箱运行时。
  - 沙箱协议：定义了沙箱生命周期管理 API 和沙箱执行 API。你可以通过这些沙箱协议扩展自己的沙箱运行时。
  - 沙箱运行时：沙箱全生命周期管理，支持 Docker 和自研高性能 Kubernetes 运行时，实现本地运行、企业级大规模分布式沙箱调度。
  - 沙箱环境：内置 Command、Filesystem、Code Interpreter 实现。并提供 Coding Agent（Claude Code 等）、浏览器自动化（Chrome、Playwright）和桌面环境（VNC、VS Code）等示例。
  - 网络策略：提供统一的 Ingress Gateway 实现，并支持多种路由策略；提供单实例级别的沙箱出口网络限制。

- https://github.com/TencentCloud/CubeSandbox /apache2/go/rust/c
  - https://docs.cubesandbox.ai/
  - Instant, Concurrent, Secure & Lightweight Sandbox Service for AI Agents
  - sandbox service built on RustVMM and KVM. 
  - It supports both single-node deployment and can be easily scaled to a multi-node cluster. 
  - It is compatible with the E2B SDK, capable of creating a hardware-isolated sandbox environment with full service capabilities in under 60ms, while maintaining less than 5MB memory overhead.
  - https://x.com/TencentAI_News/status/2046511216907157678
    - Dedicated kernel per sandbox (hardware-level isolation) 
    - Sub-60ms cold start (2.5-50x faster)
    - Thousands of concurrent sandboxes per node 
    - 100% E2B SDK compatible. Swap the endpoint, zero code changes

- https://github.com/boxlite-ai/boxlite /apache2/202601/rust
  - https://boxlite-ai.github.io/website/
  - Embedded micro-VM runtime for AI agents running OCI containers with hardware-level isolation — no daemon required.
  - BoxLite lets you spin up lightweight VMs ("Boxes") and run OCI containers inside them. 
  - It's designed for use cases like AI agent sandboxes and multi-tenant code execution, where Docker alone isn't enough and full VM infrastructure is too heavy.
  - Hardware isolation: each Box has its own kernel (not just namespaces).
  - Embeddable: link a library; no root; no background service to manage.
  - OCI compatible: use Docker/OCI images (python:slim, node:alpine, alpine:latest).
  - Async-first: run many boxes concurrently; stream stdout/stderr.

- https://github.com/CelestoAI/SmolVM /apache2/202603/python
  - fast, secure microVM runtime designed for high-density isolation. It provides AI agents and tools with a safe, hardware-virtualized environment to execute untrusted code without risking the host system.
  - Secure Isolation: Hardware-level virtualization (utilizing Firecracker) for strong sandbox boundaries.
    - Linux + Firecracker backend: KVM support (Ubuntu/Debian/Fedora).
    - macOS + QEMU backend: Homebrew and QEMU (qemu-system-*).
  - MicroVMs boot in sub-second time with minimal overhead.
  - Python Native: Clean, high-level SDK for managing VM lifecycles and command execution.
  - Automatic Networking: Built-in NAT, port forwarding, and SSH tunneling.
  - Custom Images: Build specialized Debian-based rootfs images with your own tools.
  - MicroVM-based Security: Unlike containers that share the host kernel, SmolVM uses KVM-backed microVMs. This provides a significantly smaller attack surface and stronger hardware-level isolation.
  - Agent-First Design: SmolVM abstracts away the complexity of microVM networking, storage, and TAP devices into a simple, pythonic API.

- https://github.com/boxlite-labs/boxlite-mcp /apache2/202512/python
  - embeddable sandbox with hardware-level isolation and no daemon. The SQLite of sandbox, coming soon as open source

- https://github.com/Coooolfan/onlyboxes /AGPL/202603/go
  - a self-hosted code execution sandbox platform for individuals and small teams.
  - [[开源-OnlyBoxes]面向个人与小型团队的自托管代码执行沙箱平台｜一键部署｜私有化｜Docker｜MCP｜开箱即用  - LINUX DO _202603](https://linux.do/t/topic/1849666)
    - 自托管所有组件：控制节点（console）+ 执行节点（worker）
    - 系统采用控制面（console ）与执行面（worker ）分离架构。执行面提供多个运行时，适用于不同部署场景。
    - worker-docker	runc	Docker 容器	常见的云服务器场景，更好的兼容性
    - worker-boxlite	KVM	boxlite	内核级隔离

- https://github.com/xicilion/boxsh /MIT/202604/cpp/js
  - A sandboxed POSIX shell with a concurrent JSON-line RPC mode
  - https://x.com/xicilion/status/2040879181316407720
    - boxsh — a sandboxed POSIX shell for AI agents. Single static binary. No Docker, no root.
  - https://x.com/xicilion/status/2043911257108164942
    - Agent 和执行环境必须分离，这个结论是对的。不过他们实现有些差别。
    - 关注沙箱可以了解一下 @anthropic-ai/sandbox-runtime，实现原理和 boxsh 一样，区别在于 sandbox-runtime 目标在于安全，boxsh 在安全之上规划了零成本 cow worktree 工作流。 boxsh 的沙箱单位是会话。
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

- https://github.com/macaly/almostnode /191Star/MIT/202602/ts
  - http://almostnode.dev/
  - lightweight, browser-native Node.js runtime environment. 
  - Run Node.js code, install npm packages, and develop with Vite or Next.js - all without a server.
  - Built by the creators of Macaly.com — a tool that lets anyone build websites and web apps, even without coding experience. Think Claude Code for non-developers.
  - Virtual File System - Full in-memory filesystem with Node.js-compatible API
  - Node.js API Shims - 40+ shimmed modules (fs, path, http, events, and more)
  - Install and run real npm packages in the browser
  - Service Worker Architecture - Intercepts requests for seamless dev experience
  - Optional Web Worker Support - Offload code execution to a Web Worker for improved UI responsiveness
  - Built-in Vite and Next.js development servers
  - First-class TypeScript/TSX transformation via esbuild-wasm
  - Secure by Default - Cross-origin sandbox support for running untrusted code safely
  - https://x.com/PetrBrzek/status/2020161329470828932
    - Vibe coded an open-source library that runs Node.js entirely in the browser. 
    - Full virtual filesystem with POSIX-compatible API (using just-bash from @cramforce )
    - No server. No backend. No cold starts.
    - was it really vibe-coded in a sense that you let it run autonomously and make decisions, or did you replace coding by hand in favor of explaining in natural language what you wanted to code?
      - I said "Let's make it possible to run Express.js in the browser". It had a test environment ready and just kept iterating in a feedback loop until the Express example actually worked. Then I said "Cool, now let's run the Next.js dev server" same thing. Loop until it works.
    - how does the http server listen on a port if it's running in the browser?
      - it shims Node's http module using browser APIs like Service Workers to intercept and handle requests virtually, without binding to real ports
    - It’s basically an open alternative to webcontainer
    - But why would you run Node.js in the browser?
      - Before AI coding, the answer was niche: show library examples in docs, or quick prototyping on StackBlitz. 
      - With AI coding platforms like Macaly, it's a different story. If you're building an AI coding platform (Bolt, Lovable, our platform Macaly), your users are generating Next.js apps, React + Vite projects, using Supabase, Convex, etc. 
      - You need to run that code somewhere. Two options:
      - Cloud sandboxes ( @e2b , etc.) — full Linux VM, most flexible, but expensive. Every user session costs you money.
      - Run it in the browser — fake Node.js environment, zero server cost. That's what WebContainers do inside Bolt.
      - The problem: WebContainers aren't open source.
      - With a TDD approach and enough shims, you can get Next.js, Vite, and Express dev servers running entirely in the browser.
      - I didn't write a single line of code in this project. All vibe coded.
      - It's experimental, it has bugs, but it works. And it's fully open source.
    - I would just use emscriptem. emscripten already has the fs shims. 
      - Got it. You can definitely do it in WASM as well. WebContainers work like that. I didn’t have a strong preference, I was just orchestrating it.

- https://github.com/lifo-sh/lifo /MIT/202602/ts
  - https://lifo.sh/
  - A Linux-like operating system that runs natively in the browser. Not a VM
  - Virtual Filesystem (VFS) -- synchronous in-memory INode tree with full POSIX-like semantics (read, write, stat, mkdir, symlinks, hard links, permissions)
  - Persistence -- IndexedDB-backed filesystem persistence with serialization/deserialization of the entire INode tree

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
