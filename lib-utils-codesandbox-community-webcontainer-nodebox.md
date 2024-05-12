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

# discuss-stars
- ## 

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
# discuss-stackblitz
- ## 

- ## 

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

- ## [Unix in the Browser Tab | Hacker News_202201](https://news.ycombinator.com/item?id=29823022)

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

- ## Introducing Sandpack 2.0 and Nodebox, a Node.js runtime for any browser._202302
- https://twitter.com/codesandbox/status/1626304039251062785
  - Run Node.js in any browser, any device
  - Nodebox is the first runtime that allows you to run Node.js in any browser, any context, and any application 
  - One of the biggest challenges of enabling this was performance. So, we took the time to redesign the Sandpack transpiler using Rust, refined our caching and made many other optimizations.

- ## [Does anyone have a idea how to run Webpack in the browser? : javascript_201601](https://www.reddit.com/r/javascript/comments/40oi1b/does_anyone_have_a_idea_how_to_run_webpack_in_the/)
- 
- 
