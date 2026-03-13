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

- ## the more I look how all javascript runtimes implement garbage-collection, the more I lose my hope in humanity. it’s a surprisingly hard task with too many edge cases.
- https://x.com/yagiznizipli/status/2000728248607486172
- Don't worry about it, we have the following package.json script before running any command.

```json
{
  "node:memory:128gb": "cross-env NODE_OPTIONS='--max_old_space_size=131072 --max_semi_space_size=256'"
}

```

- If it runs only once and exits, you don’t need any garbage collection 🤪

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
# discuss-js-runtime/solutions
- ## 

- ## 

- ## 

- ## Announcing Hermes-node: Hermes can now run as a standalone CLI with Node.js-compatible APIs - no C++ embedding required. _202602
- https://x.com/tmikov/status/2024609186936660170
  - Technically, hermes-node is a Node.js API compatibility layer for Hermes. It ports Node's native bindings (fs, net, http, child_process, etc.) to Node-API and reuses Node's original lib/*.js files, allowing standard Node.js programs to run on Hermes instead of V8. 
  - It vendors libuv, c-ares, llhttp, Ada, simdutf, etc to provide the same networking and I/O stack as Node, and runs as a standalone CLI binary.
  - This is still a work in progress, though surprisingly functional. More Node modules coming, source will be published soon.

- Did you do this via implementing v8’s C++ API similar to node-jsc?
  - My goal wasn't to drop-in replace v8 in Node, so I went in the opposite direction. I am porting and partially re-implementing Node C++ bindings.
  - So, instead of putting Hermes in Node, I am adding Node modules to Hermes, so to speak. This gives me better control over the architecture and more "ownership" over the result.
  - I am pretty excited about adding sound typing to the Node modules and compiling them natively. End result is potentially almost everything written in typed JS, with very little C++.
- What is the perf impact of using modules to interface. Any penalty

- Will this also work with static Hermes somehow? I.e. can we AOT compile Node.js bindings? (Are they even well typed enough?)
  - I developed it in my free time. Yes, compiling typed .js is very much part of the plan.

- int32, int64, float32, float64, shared memory multithreading, static memory layout objects. Small list left for the greatest lang ever.
# discuss-deno
- ## 

- ## 

- ## 

- ## 
# discuss-bun
- ## 

- ## 

- ## 🐛 Claude Code 一定程度上带火了 Bun。Bun用来装 npm 包是极快的，用来当做 CLI 的运行时也不错，但是千万不要拿来做长时间运行的服务，比如 API 之类的。
- https://x.com/austinit/status/2032448694382125318
  - 我使用了 Bun 做 API Server 一年左右，发现它在运行期间会一直吃内存，而且几乎只吃不释放，后来我发现这就是 Bun 处理内存的方式。几乎每次都从刚运行的几十Mib内存占用，慢慢在数天内吃到 2Gib，然后稳定，或者在某一刻继续增长，直到OOM了。
  - 后面随着 OOM 次数增多，我把这个项目运行时换成了 Node，数周运行下来发现，内存从 bun 的 2Gib 占用到了 node 占用的 80 Mib，真是离谱，以前我还以为是我业务量太大导致的。

- 应该是bun本身设计导致的，包括数据库连接数，bun一上来都是直接吃满的，为了性能。本来我还准备接下来在生产环境试试bun，感谢大佬的分享，求稳还是看node

- 本来用的很好的，结果发现在一些非常古老的CPU上是用不了的……

- ## Bun 才是最激进的，Zig 自己都没 Stable 
- https://x.com/RaySong19184922/status/2025411031775019378
- bun用的zig是自己魔改的定制版本，有些语法和zig主分支都不一致了，这不仅仅是激进，主要是zig老在breaking change

- 这并不算激进吧， 用最新的 stable 版本是常规操作。 我们都是用 CI 自动更新的，一发布 CI 跑过就升级了。 用 unstable 版本才算是激进
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [LibJS JavaScript Engine | Hacker News _202203](https://news.ycombinator.com/item?id=30857705)
  - https://serenityos.github.io/libjs-website/

- What is the draw here compared to other JS engines (either v8/JSC/spidermonkey on the big end or something like quickJS/duktape on the small end)?
  - All those other engines are cross-platform, whereas LibJS is UNIX only and actually very dependent on SerenityOS libraries (so not really a portable UNIX library), but that's apparently the intended design.
- To be fair both JavaScriptCore and V8 heavily rely on the base C++ libraries that are part of Chromium and Webkit.

- ## Looks like LibJS from @ladybirdbrowser is currently the most complete implementation of the JavaScript language according to test262
- https://x.com/awesomekling/status/1862516765642686637
  - https://test262.fyi/
- Major vendors are extremely competent! Our score is mainly higher because we implement new language features eagerly when they are specced, and we enjoy improving our spec compliance by tracking down random edge cases and fixing tests

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
