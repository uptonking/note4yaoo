---
title: lib-utils-codesandbox-community-webcontainer-nodebox
tags: [codesandbox, nodebox, wasm, webcontainer]
created: 2023-04-11T12:33:49.507Z
modified: 2024-01-25T13:32:35.137Z
---

# lib-utils-codesandbox-community-webcontainer-nodebox

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-stackblitz
- ## 

- ## Today marks a big milestone: you can now self-host all of @StackBlitz . _20240125
- https://twitter.com/ericsimons40/status/1750539087675785670
  - [Announcing StackBlitz Self-hosted _20240125](https://blog.stackblitz.com/posts/stackblitz-self-hosted/)
  - We’re excited to share today that StackBlitz Enterprise Server, a self-managed build of StackBlitz, is generally available to any team

- ## If laptops keep getting faster, cloud based developer tooling is going to become less appealing. 
- https://twitter.com/ericsimons40/status/1719473082459378041
  - These machines are so powerful that most of the value add can run locally. 
  - Maybe we'll get a hybrid model, SaaS running locally, but it's clear where things are heading.
- This is a core reason why we bet big on Wasm building http://WebContainers.io. Unlocks SaaS experiences powered entirely by (ever increasing) client side compute. 

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
