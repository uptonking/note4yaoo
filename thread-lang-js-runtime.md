---
title: thread-lang-js-runtime
tags: [lang-js, runtime, thread]
created: 2024-03-30T05:55:36.744Z
modified: 2024-03-30T05:55:54.349Z
---

# thread-lang-js-runtime

# guide

# blogs

## [Building runtime-aware JavaScript packages - CodeSandbox _202306](https://codesandbox.io/blog/building-runtime-aware-js-packages)

- With the addition of import paths mapping in Node version 16, we can define a dependency to use determined by whether the module is running in the browser or Node.

- While bundling projects, it's a common practice to use process.env. NODE_ENV to create different builds for production and development
  - if we import the process from `node:process`, then the bundlers and CDNs that build these packages will detect the usage of built-ins and polyfill them accordingly.
  - Note: This is only handled in CommonJS and is generally discouraged! 
  - It is suggested to use conditional exports and imports for branching rather than relying on code analysis.
# discuss-stars
- ## 

- ## 

- ## 🤔 Porffor: Compile JS to native code ahead of time. No need for V8.
- https://x.com/mattpocockuk/status/1841549046772547840
- So there's no need for a JS runtime? It's a self executing binary?
  - Yes, that ends up being insanely small compared to the binaries produced by Deno/Bun. 90mb -> 15kb sort of difference (was shown in the talk Oliver gave)
  - There are some big challenges, like they haven't implemented GC yet. But they have some independent funding so they have a bit of runway to work with.

- 🆚️ how does it compare to what Static Hermes is doing?
  - Similar ambitions I guess. Both look to be using static types to make optimisation decisions. Both target WASM: SH does so via LLVM, Porffor directly targets WASM. I suspect Porffor will have very nice zero-overhead FFI features over time. It's early days for both projects.
  - And I suspect more interesting differentiation will happen a level above when someone builds a runtime above these projects (Node.js : V8 :: ??? : Porffor :: ??? : SH)

- quickjs does not compile JS ahead of time? it interprets. you can bundle it with JS but that isn't actually compiling JS
  - qjs, yes, but its also bundled with qjsc, a compiler
- that still isn't actually compiling JS though, it's just bundling the engine with source/bytecode
  - fair point, but you can strip out eval for a tiny binary with no js parser

- Still, I guess that will require custom packages that implements servers and stuff. Current ones depends on the v8 interface.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Graal.js is a JS engine, implemented in Java, executed on GraalVM. 
- https://x.com/birch_js/status/1804430816010973518
  - It allows you to efficiently run JS code, and even implements the entire Node.js SDK (as it embeds the Node.js C++ codebase).
- it is very heavyweight and warms up quite slowly.
- curious how it compares to NodeJS Mobile https://github.com/nodejs-mobile/nodejs-mobile
- there is also es4x which runs on vert-x/jvm. this does pretty well on techempower benches.
- Truffle is an Olympic accomplishment in the engineering world. Ahead of its time even.
- Sure it works great , oracle actually have a node server with graal js as engine and not v8
- Graaljs in openjdk is very much different from graaljs in graalvm

- ## JavaScript 的生命力来源于去中心化。虽然基础很草台，但是因为浏览器五花八门，没有一家垄断，导致没有一个厂商可以独立为其增加特性或者大刀阔斧地修改。
- https://twitter.com/xicilion/status/1773619873488191937
  - 而对于开发者，因为有那么多浏览器需要兼容，谁也不敢随意尝试一两个厂商支持的新特性。最终达成了目前的行业共识。
- 微信小程序就敢加，只是现在技术能力还不够。
- 小年轻，没人用浏览器。
  - 国人不用不代表全世界人不用
