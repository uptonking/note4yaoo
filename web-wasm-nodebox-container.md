---
title: web-wasm-nodebox-container
tags: [nodebox, wasm, webcontainer]
created: 2023-04-11T12:33:49.507Z
modified: 2023-04-11T12:34:16.725Z
---

# web-wasm-nodebox-container

# guide

- tips
  - 让原生程序在浏览器、移动端执行
  - 让浏览器中的文件系统更方便
# examples
- browsix /3.1kStar/MIT/201904/ts/inactive
  - https://github.com/plasma-umass/browsix
  - Browsix is a Unix-like operating system for the browser.
  - outdated. requires node 6 (latest is node 19)
  - Browsix uses `BrowserFS` for its filesystem
  - Browsix makes core Unix features available to web applications (including pipes, processes, signals, sockets, and a shared file system) and extends JavaScript runtimes for C, C++, Go, and Node.js programs so they can run in a Unix-like environment within the browser. 
  - Browsix also provides a POSIX-like shell that makes it easy to compose applications together for parallel data processing via pipes.
  - Browsix enables you to compose the in-browser part of your web applications out of processes. 
    - This process model is implemented on top of existing browser APIs, like web workers, so it works in all modern browsers.
  - forks
    - https://github.com/milahu/browsix
    - https://github.com/SamGinzburg/browsix
# blogs

## [Announcing Sandpack 2.0 and a Node.js runtime for any browser](https://codesandbox.io/blog/announcing-sandpack-2)

- One year ago, we introduced Sandpack, an open-source in-browser bundler that allows you to run live running code examples on your website.
- But in version 1, the big caveat to “any JavaScript application” was that it only worked for client runtime execution. And we wanted to change that.
- Nodebox allows running server-side examples. 

- 💡 Nodebox under the hood
- Nodebox is a high-level abstraction of Node.js. 
  - That means it doesn’t implement some of the small details of Node.js, but we made various tweaks to make it compatible with every browser. 
  - So, Nodebox aims for application compatibility, not Node.js feature parity.
- Performance was also one of our top priorities while developing Nodebox. 
  - 👉🏻 We completely rewrote the Sandpack transpiler using Rust, tweaked our caching and made several other optimizations. 
  - The result? It’s really fast! Our Vite templates, for example, have a hot start time of 500ms.
- We’re shipping Nodebox with out-of-the-box support for Next.js, Vite and Astro, but we’re growing to support just about any server-side framework you can imagine. 
  - However, bear in mind it can’t run napi or any other low-level C++/Rust package you can use in Node.js—only WebAssembly and JavaScript modules. 
  - Postgres, MongoDB and MySQL are also currently not supported because of the lack of raw socket support in browsers.
- Plus, we're currently working on some missing APIs, such as async_hooks, vm, worker_threads, automatic process exiting (users now need to manually call process.exit before the process is exited) and synchronous exec/spawn. 
  - Nodebox works in iOS Safari, but it’s still on beta support due to a browser memory leak. 

- 🆚️ Difference with WebContainers
- WebContainers is a technology that also allows you to run Node.js in the browser. 
  - However, it uses modern browser technologies like `SharedArrayBuffer`, which makes it impossible to run in Safari and requires the user to set additional `Cross-Origin-Isolation` headers on the server to run any code.

- Instead, we implemented Nodebox without modern browser technologies, to make it run in any browser (like iOS and Safari) with minimal setup. 
  - The disadvantage of this is that Nodebox will use more memory when you spawn more threads, and we cannot get full Node API compatibility (for example, we cannot use synchronous fork). 
  - This is okay for Nodebox because it was built to run small projects and examples, which it does really well. 
  - If you want to do full development in the browser, we recommend using our microVM technology instead.

## [Unix in the Browser Tab | Hacker News_202201](https://news.ycombinator.com/item?id=29823022)

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
# discuss
- ## 

- ## 

- ## Browsix does this by mapping low-level Unix primitives, like processes and system calls, onto existing browser APIs, like Web Workers and postMessage.
- https://twitter.com/randomdross/status/1062827514597232640
- Browsix is cool. The web is not bound to a particular UX paradigm, but CLI is bound to a particular set of OS semantics.  CLI gets to work on the web too.

- ## [Open-sourcing for the webplatform ? · stackblitz/webcontainer-core](https://github.com/stackblitz/webcontainer-core/issues/458)

- webcontainer is a compatibility layer for node apps, similar to wine (Wine Is Not an Emulator)

- so were looking for a compatibility layer between node.js apis and web apis
  - some node apis have polyfills
    - https://github.com/niksy/node-stdlib-browser
  - but some node apis are hard to polyfill

- https://github.com/leaningtech/webvm /未开源
  - WebVM is a server-less virtual Linux environment running fully client-side in HTML5/WebAssembly.
  - WebVM is powered by the CheerpX virtualization engine, which enables safe, sandboxed client-side execution of x86 binaries on any browser. 
  - JIT-compiling binaries to WASM = fast

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
