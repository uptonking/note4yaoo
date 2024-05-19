---
title: lib-utils-codesandbox-community-webcontainer-nodebox
tags: [codesandbox, nodebox, wasm, webcontainer]
created: 2023-04-11T12:33:49.507Z
modified: 2024-01-25T13:32:35.137Z
---

# lib-utils-codesandbox-community-webcontainer-nodebox

# guide

# docs-nodebox
- Nodebox is a runtime for executing Node.js code in the browser. 
  - Sandpack 2.0 uses Nodebox to run server-side examples directly in the browser. 

## [Nodebox – Sandpack](https://sandpack.codesandbox.io/docs/advanced-usage/nodebox)

- Nodebox is a runtime for executing Node.js code in the browser. 
  - Sandpack 2.0 uses Nodebox to run server-side examples directly in the browser. 
  - For example, you can run a Vite template such as React and Vue directly on your website.

- Nodebox with out-of-the-box support for Next.js, Vite and Astro, but we’re growing to support just about any server-side framework you can imagine.
  - However, bear in mind it can’t run napi or any other low-level C++/Rust package you can use in Node.js—only WebAssembly and JavaScript modules. 
  - Postgres, MongoDB and MySQL are also currently not supported because of the lack of raw socket support in browsers.

- Difference with WebContainers
  - Web Containers use modern browser technologies like `SharedArrayBuffer`, which makes it impossible to run in Safari and requires the user to set additional `Cross-Origin-Isolation` headers on the server to run any code.
  - Nodebox however, is implemented without modern browser technologies, to make it run in any browser (like iOS and Safari) with minimal setup.

### [Frequently Asked Questions – Sandpack](https://sandpack.codesandbox.io/docs/resources/faq)

- Why is the bundler hosted externally (iframe) and not a simple JavaScript module?
  - 

- What Node.js version does Sandpack 2.0 run?
  - We are aiming for compatibility with the last version. Currently, this would be Node.js@18 (experimental features might be missing).

- How does Nodebox work?
  - Nodebox establishes a worker that contains an environment capable of running Node.js code. 
  - This is achieved by polyfilling some of the Node.js standard APIs, like `fs` and `net`, which guarantees Node.js compatibility but not complete feature parity.

- Does Nodebox work offline?
  - Starting Nodebox requires a network connection to download all the node modules from the sandpack cdn https://sandpack-cdn-v2.codesandbox.io and load the preview domain for each port https://id-port.nodebox.codesandbox.io, once the previews have loaded Nodebox will work entirely offline.

- Is it possible to connect to a database in Nodebox?
  - No. Nodebox is currently unable to connect to any external databases. However, serverless databases (Supabase, DynamoDB, Google Cloud Datastore, for example) can still be used normally since these options rely on standard REST APIs.
  - Still, we are currently exploring other alternatives for standard databases, like microVMs, which still need to be integrated into Sandpack.

- How does the Nodebox compare to WebContainers?
- While both Nodebox and WebContainers allow running Node.js on the browser, they have several fundamental differences:
  - Nodebox runs on any browser because it was built from the ground up with cross-browser support in mind, avoiding modern features like `SharedArrayBuffer`.
  - Nodebox does not have an install/setup step, making it faster to boot up. It installs `node_modules` in the background.
  - Nodebox uses an internal dependency manager that is fine-tuned to deliver optimal initial load time by utilizing dependency caching via Sandpack CDN.
  - Nodebox tends to use slightly more memory when multiple processes/workers are involved. Unfortunately, this is a trade-off for cross-browser support as the only way to optimize this is by using SharedArrayBuffers.
  - Nodebox does not support synchronous cross-process communication as this would require Atomics and SharedArrayBuffers.
  - Nodebox does not emulate Node.js's event loop, resulting in processes needing to be exited manually using `process.exit()` or by stopping the shell.
  - Nodebox is not feature complete yet, some API's are still missing: `async_hooks, vm, worker_threads` and probably some more.

- 
- 
- 
- 

# blogs-nodebox

## [How to run Node.js (apps) in the browser? | by Johannes Bader | CloudBoost _201711](https://blog.cloudboost.io/how-to-run-node-js-apps-in-the-browser-3f077f34f8a5)

- There are several reasons why a JavaScript developer may want to run Node.js code in the browser, including:
  - developed a Node.js app — now want to also offer it online
  - found a useful npm package that relies on Node.js
  - want to use Node.js APIs (buffer, crypto, fork, events, streams, …)
  - prefer to write CommonJS-style modules with require

- One will a number of solutions fulfilling at least some of the above wishes, such as webpack.js.org, browserify.org or nodular.js. 
  - However, all of those approaches are based on some form of the source code transformation — either ahead of time (webpack and browserify) or at runtime (nodular).

- I bootstrap the JavaScript part of Node.js inside of a web worker. 
# blogs-webcontainer

## docs-webcontainer

- [Enterprise | WebContainers](https://webcontainers.io/enterprise)
  - Licensing is required for production usage of the API in a for-profit setting (feel free to prototype as much as you like without a license). 
  - If you're using the API to meet the needs of your customers, prospective customers, and/or employees you need a license 

## 🤔 [除了webContainer之外，还有什么办法能在浏览器上运行node代码 - 掘金 _202309](https://juejin.cn/post/7281912738862841896)

- 总结: 通过 web worker 的方式去启动一个虚拟机，该虚拟机模拟了一个 Node.js 环境，从而实现在浏览器上面允许 node 的代码。
  - 那么问题来了，如何在浏览器上面运行世界上最好的语言呢？

## [Stackblitz 的 WebContainer 探秘 - 知乎 _202112](https://zhuanlan.zhihu.com/p/446329929)

## [Labor，首个 web container 开源实现 - 掘金 _202105](https://juejin.cn/post/6966262450878414884)

# discuss-nodebox
- ## 

- ## 

- ## 🤔 [Could you share how to build node as webassembly target using emscripten or some other tools · Sandpack/nodebox-runtime _202311](https://github.com/Sandpack/nodebox-runtime/issues/53)
- In essence it's almost all javascript, we didn't actually compile node to wasm that would be too big and slow.
  - Instead we use the native browser functionality and write a bunch of wrappers and polyfills to make it compatible with node, some sprinkles of wasm is used here and there to make it fast

- ## [[Question] How to use nodebox-runtime in browser without any online resource's support · Sandpack/nodebox-runtime](https://github.com/Sandpack/nodebox-runtime/issues/34)
- Unfortunately, we did not fully open-source Nodebox for a variety of reasons

- [Working Offline · Sandpack/nodebox-runtime](https://github.com/Sandpack/nodebox-runtime/issues/37)
  - Currently nodebox takes a new domain for the preview every time you create a nodebox instance as it was the safest way to ensure consistent update logic and a single nodebox instance is connected to the preview.
  - Because of this we need a network connection for the initial render and once it's rendered you can remove internet for any additional changes.
  - We could make our caching on service workers a bit more aggressive but the core issue will remain and is really hard to fix properly without introducing more issues.

- ## 🚀 [Nodebox: A Node.js runtime that runs in any browser | Hacker News _202302](https://news.ycombinator.com/item?id=34824635)
  - Nodebox runs on any browser because it was built from the ground up with cross-browser support in mind, avoiding modern features like SharedArrayBuffer.
- Usually you have a bundler/transpiler running on the host, with sandpack we moved that step to the browser so you can share a link with anyone and they instantly get a development friendly (JSX, TS, ...) project that works without having to install any tooling. It's also a lot faster than something like webpack as most of the bundling complexities are taken away as sandpack transpiles files on demand without the need for bundling as it also controls code execution. With nodebox we pushed this a bit further by also implementing most of the Node.js standard libraries.

- The benefit is that you can use a web editor with the same dev tools (TypeScript, Babel, vite, webpack, etc) without a server VM. That saves them a lot of money in cloud instances, and speeds up things for the end user.
  - Other than that a posible niche use case is to emulate a full-stack for prototyping or testing purposes.

- Everything nodebox does is scoped to the current browser window, it has no access to any part of the hostmachine, it's not really a vm but actually a new web worker which runs the Node.js code you request. This is heavily relying on the sandboxing browsers do by default and is therefore really secure.
  - It's very interesting. In that example with the express router, where you're creating index.js inside a filesystem inside nodebox, is that whole filesystem just stored by that one webworker? Also, when you invoke express to listen on port 3000 and get back some URL to set the previewIframe.src, is that some blob URL returned from the webworker? (in which case how would you set up sockets?) Or is that URL accessible to any other browser tab?

- Nice. Stackblitz did this first and this is a killer feature all fiddles now need
# discuss-webcontainer/stackblitz
- ## 

- ## 

- ## 

- ## Is stackblitz open source and can i self host it _202403
- https://discord.com/channels/364486390102097930/680953097354215446/1214952721132818522
- Portions of it is, but the product is not. You can use WebContainers to build upon though. 
  - If you want self-hosted StackBlitz, you might consider the enterprise licensing they offer.

- ## Possible to Port NodeJS to Other Languages by Compiling to WASI Supported WASM Module? _20240330
- https://discord.com/channels/364486390102097930/1223486985981923369/1223486985981923369
  - As far as i understand how WebContainers work, NodeJS seems to be compiled to WASM. (QuickJS maybe? WasmEdge uses QuickJS compiled to WASM too for NodeJS support in their edge workers, afaik)
  - Although this could be considered out of scope for Stackblitz's interests, we have an interest in porting NodeJS to different programming languages through WASM and I am curious if Stackblitz's technologies could assist (in any way) in this endeavour.
  - not sure how much more context you require for a better understanding of our needs, we have NodeJS code and we need to compile it to a WASI supported WASM module. from our research, the only other projects that successfully compiled NodeJS to WASM seem to be Stackblitz and WasmEdge

- You might be interested in Javy or ComponentizeJS from BytecodeAlliance
  - both Javy and ComponentizeJS seem to be to used to compile regular JS to WASM, but not NodeJS, 
  - Javy specifically states that it does not support compiling NodeJS

- I'm not exactly sure what y'all are doing, but Webctontainers in general does require chrome (ofc), but one way you could look at integrating is via our WebContainer API.

- maybe i have a misconception here, does Stackblitz compile a JS runtime to WASM? (such as QuickJS or V8 with the --jitless flag)
  - No we don’t compile a JS runtime and it all depends on the browser environment. 
  - WebContainer is a NodeJS runtime for the browser that allows to execute Node apps natively if that makes sense. 
  - What that catch phrase from our docs means is that you can compile for example Ruby or Python or any other language to a WASI compatible module and run it inside WebContainer. 
  - The easiest way is to use the wasm command from the terminal which works similar to other Wasm runtimes like wasmtime. 
  - But WebContainer is not a compiler but a runtime similar to how Node.js is a runtime.
  - And WebContainer is fully closed source at this point in time.

- unfortunately there are no open source projects that aid in using NodeJS through Wasm.
  - Also doubt that TCP/UDP is something that will be exposed by browsers for security reasons, but never say never
  - right now all of our technology is closed source and our core is not something that can be consumed except for the WebContainer public API which gives you the ability to run Node.js/JavaScript apps on your own without using it through our editor. 
  - we can't share implementation details so we can definitely discuss on a higher level if you think that helps.

- 👣 You might be interested in something similar to WebVM (CheerpX) like container2wasm (https://github.com/ktock/container2wasm). 
  - They don't do nodejs->wasm but they can run nodejs in the container. Afaik both have some networking support.
- that is an option, but the overhead that would add would presume quite a performance decrease, we've been talking with someone from WasmEdge too, he states that NodeJS's APIs are still mostly JS, and that compiling QuickJS to WASM (which is what i understand they are doing) to run NodeJS with WASM mostly needs networking adapted
  - I understand that WASM does not support JIT, and that QuickJS is JITless, and V8 has a --jitless flag, but JS also has a requirement of GC, and WASM-GC is still at proposal stage as far as i understand
- container2wasm has networking support through a socket proxy. Have you tried the online demo? It does take a minute to load but it's fast once it's loaded (tested risc python container on mobile) 

- ## [WebContainer API | Hacker News _202302](https://news.ycombinator.com/item?id=34793858)
- Eric (CEO of StackBlitz) here- your explanation is 100% correct regarding why & how servers need to be used to power parts of WebContainer environments (i.e. proxying npm, git, transforming binaries, amongst a handful of other things).
  - Some of these operations can be cacheable which is ideal for scalability, but even the ones that cannot tend to be far cheaper than running VMs which incur by the minute CPU costs.

- you can actually self host StackBlitz! You’ll just need our Enterprise Edition which can be run on any cloud or on-prem. 
  - Self-hosting does require a paid license though

- ## [Opt out of wasm swapping _202308](https://github.com/stackblitz/webcontainer-core/issues/1163)
  - WebContainers interferes with npm install to swap certain packages for their wasm versions.
  - I'm noticing this for esbuild and lightningcss as this behavior gives inaccurate results on Pkg Size

- ## Today marks a big milestone: you can now self-host all of @StackBlitz . _20240125
- https://twitter.com/ericsimons40/status/1750539087675785670
  - [Announcing StackBlitz Self-hosted _20240125](https://blog.stackblitz.com/posts/stackblitz-self-hosted/)
  - We’re excited to share today that StackBlitz Enterprise Server, a self-managed build of StackBlitz, is generally available to any team

- ## If laptops keep getting faster, cloud based developer tooling is going to become less appealing. 
- https://twitter.com/ericsimons40/status/1719473082459378041
  - These machines are so powerful that most of the value add can run locally. 
  - Maybe we'll get a hybrid model, SaaS running locally, but it's clear where things are heading.
- 💡 This is a core reason why we bet big on Wasm building http://WebContainers.io. Unlocks SaaS experiences powered entirely by (ever increasing) client side compute. 

- ## 💡 [Open-sourcing for the webplatform ? · stackblitz/webcontainer-core _202112](https://github.com/stackblitz/webcontainer-core/issues/458)

- webcontainer is a compatibility layer for node apps, similar to wine (Wine Is Not an Emulator)
- so were looking for a compatibility layer between node.js apis and web apis
  - some node apis have polyfills
    - https://github.com/niksy/node-stdlib-browser
  - but some node apis are hard to polyfill

- https://github.com/leaningtech/webvm /未开源
  - WebVM is a server-less virtual Linux environment running fully client-side in HTML5/WebAssembly.
  - WebVM is powered by the CheerpX virtualization engine, which enables safe, sandboxed client-side execution of x86 binaries on any browser. 
  - JIT-compiling binaries to WASM = fast
# discuss
- ## 

- ## 

- ## 

- ## [Unix in the Browser Tab | Hacker News _202201](https://news.ycombinator.com/item?id=29823022)

- I'm one of the authors
  - The biggest problem with Browsix today stems from Spectre mitigations: Shared Array Buffers aren't enabled by default in browsers, and static hosting sites like GitHub Pages don't let you set the right COOP/COEP headers to get them enabled AFAICT.
  - I don't have a lot of time for Browsix these days, but it would be straightforward to update Browsix with WASI support which would free us from having to use a modified Emscripten toolchain (and instantly enable running Rust binaries under Browsix).
  - we use Shared Array Buffers to give the kernel and program a shared view of a process's address space to enable fast system calls between Web Workers and the kernel (running in the main browser thread/context).
  - I think there is a straightforward path to having Browsix generically support the WebAssembly WASI system interface[0] -- any toolchain that emitted binaries targeting that would then work in Browsix without e.g. Emscripting needing to know anything about Browsix.

- 🤔 What is the use case this is solving?
  - (author here) Without something like Browsix you have to make a choice: find a JavaScript library or implement the functionality you want to run client side, or run existing Unix programs and libraries (that expect a filesystem, to be able to fork children, etc) server side. 
  - If you run software server side, now you have to worry about containerizing/security as well as horizontal scaling.
  - Browsix addresses this by letting you run Unix programs directly in the browser, taking advantage of the significant compute power on peoples laptops (and even phones nowadays!), eliminating a whole class of security issues (software explicitly will only have access to the current users data in the browser tab) and scaling concerns.

- So emscripten is still the compiler, but this is an OS which can be targeted by emscripten? Am I understanding it right?
  - That's pretty right, with the addition that other things can target Browsix (like the gopherjs toolchain). 
  - Emscripten provides default implementations of a bunch of syscalls (and even a way to embed a file system), and we override those to instead do actual syscalls to a shared kernel (running in JS)

- AFAICT, Browsix is meant to work more like Wine than like jslinux. 
  - The goal is to allow devs to deploy native executables to the web browser more seamlessly because it provides ways for standard javascript to interact with the program. 
  - JSLinux is a full system emulator and thus has more overhead and doesn't have a method to cleanly interact with the world outside of the emulator.

- ## Browsix does this by mapping low-level Unix primitives, like processes and system calls, onto existing browser APIs, like Web Workers and postMessage.
- https://twitter.com/randomdross/status/1062827514597232640
- Browsix is cool. The web is not bound to a particular UX paradigm, but CLI is bound to a particular set of OS semantics.  CLI gets to work on the web too.

- ## [Is this file not available as open source ?](https://github.com/codesandbox/nodebox-runtime/issues/7)
- You can use an extension with Native Messaging to achieve that requirement.

- ## [How to use nodebox-runtime in browser without any online resource's support_202304](https://github.com/codesandbox/nodebox-runtime/issues/34)
- Everything is just static files, but it needs to live somewhere, you can host it on-prem if you want, if you want an entirely offline solution there is only one solution which is native software like Node, Deno, Bun, ...
  - If you want an on-premise setup you will need to reach out us because we aren't allowed to publish the code of the runtime publicly.

- Unfortunately, we did not fully open-source Nodebox for a variety of reasons, some of which are outside of our control. We believe this technology may be the future of improved DX. So, we will continue to explore whether we can open-source it in the future.

- ## 🎯 Introducing Sandpack 2.0 and Nodebox, a Node.js runtime for any browser._202302
- https://twitter.com/codesandbox/status/1626304039251062785
  - Run Node.js in any browser, any device
  - Nodebox is the first runtime that allows you to run Node.js in any browser, any context, and any application 
  - One of the biggest challenges of enabling this was performance. So, we took the time to redesign the Sandpack transpiler using Rust, refined our caching and made many other optimizations.

- ## [Does anyone have a idea how to run Webpack in the browser? : javascript_201601](https://www.reddit.com/r/javascript/comments/40oi1b/does_anyone_have_a_idea_how_to_run_webpack_in_the/)
- 
- 
