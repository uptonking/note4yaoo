---
title: thread-lang-js-nodejs
tags: [js, lang, nodejs, thread]
created: 2021-07-29T15:44:58.716Z
modified: 2023-11-10T07:10:19.089Z
---

# thread-lang-js-nodejs

# guide

# discuss-stars
- ## 

- ## 
# discuss-news-nodejs
- ## 

- ## 

- ## 

- ## Node `require()` is about to be able to load (non-async) ESM. This will solve so many problems.
- https://twitter.com/devongovett/status/1769709489962295414
- if only this could be backported a few versions!
  - It will be backported. Only 18. All previous lines are EOL.

- ## Node.js now has a built-in API for styling text (similar to `chalk` , `picocolors` , etc)
- https://twitter.com/styfle/status/1765458512421814707
- Maybe an API like this could become a standard

# discuss-js-runtime
- ## 

- ## 

- ## 

- ## 一旦度过了冷启动阶段，llrt 的 quickjs 就无法跟 v8 对比了，差距太大
- https://twitter.com/fengmk2/status/1767742512561635462
- 那当然，冷启动和 JIT 二选一嘛
- 感觉正道还是做js的 AOT 编译啊

- ## 🐛 The abundance of js runtimes, each subtly different from each other, makes it a little harder to write code that works across them
- https://twitter.com/threepointone/status/1765656643155423739
  - “feature detection” strategies don’t work that well when you need to detect presence of modules (and the interplay with bundlers)
  - typescript isn’t very good at configuring codebases where different modules run in different runtimes (sometimes multiple)
  - in modern full stack frameworks, a single module might have bits where a function or two might run in a different runtime 
- for websocket clients I would be surprised if there isn’t a wrapper npm package that chooses ws in node and then WebSocket global elsewhere. for websocket servers, not sure what the best approach is today besides Hono. for bun you can use “ws” and it’ll mostly work
- That's why WinterCG exists https://wintercg.org
- I end up with files just to do bundling tricks

- ## AWS has entered the (js runtime) domain
- https://twitter.com/ArrowoodTech/status/1755667431190917577
- Extremely surprised it uses QuickJS and they specifically chose no JIT. It does make good sense for their situation though.

- yet another JS Runtime implementing Node.js compat? Controversial, but when do we call/turn Node.js into a standard?
  - defacto standard at this point
- their firecracker(爆竹，鞭炮; 杰出或激动人心、有吸引力的人或事物) vm is worth looking into if you want to get further back there in the backend and look at infra. i would imagine they are designing something purpose-built for it.
- IMO WinterCG should eventually work on standardizing the subset of the Node API that runtimes can implement to get “enough” compatibility. Maybe not time yet though
# discuss-nodejs-ts ⤴️
- ## 

- ## 

- ## 

- ## Problem: You want to use Node with TypeScript.
- https://x.com/housecor/status/1861890234033766408
- --experimental-strip-types + --experimental-require-module  is honestly my favorite now. No build step, no new dependencies, supported everywhere node is reasonably up to date

- Also worth mentionning @unjsio unbuild : https://github.com/unjs/unbuild

- when you need hot reload, all compiler are ugly and complex, you have to write  more  config and
install more packages. only Bun is zero config, and it is not a compiler, it's runtime environment

- ## [Node.js adds experimental support for TypeScript | Hacker News _202407](https://news.ycombinator.com/item?id=41064351)
- One thing to note is that it is impossible to strip types from TypeScript without a grammar of TypeScript. Stripping types is not a token-level operation, and the TypeScript grammar is changing all the time.
  - Node bundles a version of npm that can upgraded separately, we could do the same with our TypeScript transpiler.

- If Node.js can run TypeScript files directly, then the TypeScript compiler won't need to strip types and convert to JavaScript - it could be used solely as a type checker. This would be similar to the situation in Python, where type checkers check types and leave them intact, and the Python interpreter just ignores them.
  - It's interesting, though, that this approach in Python has led to several (4?) different popular type checkers, which AFAIK all use the same type hint syntax but apply different semantics. However for JavaScript, TypeScript seems to have become the one-and-only popular type checker.
  - In Python, I've even heard of people writing types in source code but never checking them, essentially using type hints as a more convenient syntax for comments. Support for ignoring types in Node.js would make that approach possible in JavaScript as well.

- I personally would very much prefer if NPM modules that have their original code in TS and are currently transpiling would stop shipping dist/.cjs
  - We dont support running .ts files in node_modules, this is one of the main constraints to avoid breaking the ecosystem

- It's one reason to consider a switch to Deno or Bun, but at least to maybe at least check JSR before NPM these days. The ecosystem for server-side ESM exists and is growing at a rapid pace

- ## [Roadmap for experimental TypeScript support · Issue · nodejs/loaders _202407](https://github.com/nodejs/loaders/issues/217)
- Step 1: Initial implementation
- Step 2: Decoupling
- Step 3: Make it fast
  - We could vendor SWC in Rust, build our own wasm, or compile it to static libraries that we could use in core, c++ rust FFI, etc.

- ## ✨ [module: add --experimental-strip-types · nodejs/node _202407](https://github.com/nodejs/node/pull/53725)
- It is possible to execute TypeScript files by setting the experimental flag --experimental-strip-types.
  - Node.js will transpile TypeScript source code into JavaScript source code.
  - During the transpilation process, no type checking is performed, and types are discarded.
- 🤔 Why I chose @swc/wasm-typescript
  - Because of simplicity. I have considered other tools but they require either rust or go to be added to the toolchain. 
  - @swc/wasm-typescript its a small package with a wasm and a js file to bind it. Swc is currently used by Deno for the same purpose, it's battle tested. 
  - In the future I see this being implemented in native layer. Massive shoutout to @kdy1 for releasing a swc version for us.

- Not supporting extension-less imports is by-design

- users should write their import specifiers with .ts extensions, like import './file.ts', and there’s typescriptlang.org/tsconfig#allowImportingTsExtensions allowImportingTsExtensions to support this via tsconfig.json. Such behavior also aligns us with Deno.
# discuss-scaling-nodejs
- ## 

- ## 

- ## 

- ## Node.js doesn't have a predictive way to manage traffic spikes, so over-provisioning for peak loads isn't optimized for the stable periods that follow. We've all faced this issue.
- https://x.com/matteocollina/status/1853393504807846207
  - This is why @Platformatic is simplifying multithreading in our Node.js app server.
- Node.js applications are usually deployed as single-threaded: ↳Each instance operates as a single process. ↳Organizations overprovision to handle traffic spikes. ↳This leads to wasted resources and increased costs.
  - Additionally, heavy computations can block the event loop, causing performance and user experience issues.
- What’s clear is that we need to rethink our approach to infrastructure. This is why @platformatic ’s Watt app server now supports service replication. By starting multiple workers, you can now fully utilize all the CPU cores available on your server, providing the best possible user experience.

- 🆚️ How is this different from pm2 ?
  - Wattpm is designed to run only one application at a time, typically inside Docker/Kubernetes. pm2 is designed to run multiple apps on a vps.
# discuss-perf-nodejs
- ## 

- ## 

- ## 

- ## [通过执行字节码来优化node启动速度 - 知乎 _202408](https://zhuanlan.zhihu.com/p/712684270)
  - 很多解释型的语言为了更快的解释开发者编写的源码时就可能会引入字节码，比如java、v8
  - 因为一般生成的源码不是树就是图，这种数据结构比较好理解，但也非常松散，而且遍历时速度不如意，毕竟机器执行连续顺序紧凑的结构有助于寄存器的缓存。
  - 执行的前两步：编译源码 -> 生成字节码 -> 开始解释 （当然还有什么机器码什么的这里就不写了）
  - 所以直接生成字节码给解释器解释不更好？

```JS
// node如何生成字节码
const bytenode = require('bytenode');

async function main() {
  let compiledFilename = await bytenode.compileFile({
    filename: 'out-old.js', // 需要生成的文件
    output: 'out.jsc', // 生成文件
    compileAsModule: false // 最终生成的是脚本还是模块
  });

  console.log('编译成功:', compiledFilename);
}

main()

// 如何执行字节码

// const script = new vm.Script(javascriptCode, {
//         produceCachedData: true
//     });
// const dummyBytecode = compileCode('"ಠ_ಠ"');

const bytecodeBuffer = fs.readFileSync(filename);

// runBytecode(bytecodeBuffer);

const context = vm.createContext(sandbox);
const script = generateScript(bytecodeBuffer);

script.runInContext(context);
```

- bytenode本身是一个第三方库，封装了一些生成的逻辑，其实就是使用了node的vm模块来保存字节码。
- 这里需要注意的是sandbox，因为最终生成的代码是在一个vm里执行的，vm可以理解为一个干净的v8环境，而我们需要使用node的很多内置模块就只能通过sandbox来注入。
  - 上面的部分代码也来源于bytenode库，我只把执行的部分拿出来了，并加入了sandbox的逻辑。。

- 编译为字节码还有一个好处就是保护源码，要不别人直接拿到源码修改修改就可以二次打包
  - 还有一种优化方式是关于快照的，不过这种方式相对来说更麻烦

- ## 最近工作中手上有一个后端 API Server, 一开始我是拿 Node 写的, 特征是一个请求进来我得 fan out 50+ 个请求出去
- https://x.com/strrlthedev/status/1897127153642430817
  - 性能总是不行, 本地跑批开 600 个 client 就全 hang 住了, 一卡 20 分钟
  - 迫于实在是不会 profile node 所以今天干脆拿 go 重写了一部分; 性能 10x 了, CPU 使用率也上去了

- 最近我们也遇到不少node的问题 找profile一看 相当多时间片都在 gc

- 感觉不是语言问题，是架构问题？

- 这个问题我司之前拿来做内部pk 一堆go的遥遥领先最后被一个优化得极优秀的nodejs给干掉了 核心原理是 如果远端是同一个或者少量的server 那么 减少建立连接的次数 能复用就尽量复用 就可以保证性能足够好
  - 当然 用go的话随便写写性能就很好了 用node多少还得认真点 多花点心思想清楚细节
# discuss
- ## 

- ## 

- ## 

- ## node 写服务端或者说写前+后，纵使有千般不好，万般不是。 但一个仓库一个语言一个框架一个编辑器一次解决问题，这一点就够了。
- https://x.com/wwwgoubuli/status/1844569476257427554
  - 这个趋势不会变的。node 就是会吃下越来越多的“靠前的后端”。
  - 来我们公司前真的怀疑过所谓全栈框架 next, nuxt 之流是否真能写后端，但我们还真就是直接用 nextjs 写后端撑起百万的月活。

- 确实，而且这样有一个好处就是在monorepo的开发模式下，types.d.ts可以共用，彻底解决前后端API对接时的类型同步问题

- 但是量化不得不用py
  - 所以说嘛，它可以处理也擅长的是比较靠前的那部分后端。我这两年其实越来越少说后端，我比较喜欢说服务端。因为有很多时候，一些模块或者服务和前端是没有任何交互的，他们只操作队列或者数据库。同样的，前端也应该尽量只操作这些数据源。和后端的耦合不应该是过多的增删改查。

- 太绝对了，风水轮流转，ASP、PHP 何曾不是那么流行过？

- node 无非是工具罢了。

- ## How do you debug @nodejs ?
- https://x.com/matteocollina/status/1844694356160028954
- VS Code and its JavaScript Debug Terminal or by recording a @replayio if the code execution problem is more complex and hard to diagnose

- ## 🆚️ undici.request is MUCH faster than Node's built-in fetch (also backed up by undici).
- https://x.com/mattpocockuk/status/1841781998622314583
  - The extra overhead of fetch needing to be compliant with web standards really slows it down.
- On one of @matteocollina ’s twitch streams some time ago, he said the perf can be improved to be on par with more investment. It’s not that one is inherently slower than the other. I think some of this is due to underlying web streams implementation

- Seems neglectable overall. Nginx is doing 50K to 80K requests non-clustered from what I found and given node is used for much heavier tasks, this bench seems acceptable. I would take standards over this perf win any time.
- So, if I've got my maths right, undici is about 32 nanoseconds per request faster. The instant you add real network latency onto that then that number becomes meaningless. Ping times to my WiFi router are about 8ms, which is 250x more than the 32ns speed gain from using undici.

- Matt, this is just very actively harmful content. Really. You are saying "thing is slow because it's standard". That is blatantly untrue. There is nothing in this example that has to be slow because a spec says so. Which is why it's blazing fast in many runtimes other than Node.
- if you use Bun with fetch you’re still at least 20x faster

- Fetch API in general isn't that great for server side use. You'll easily end up with chains of copying and creating responses. For browser it's fine though.

- ## I've rewritten the Node.js task runner (node run --test) in C++. 
- https://twitter.com/yagiznizipli/status/1781682054393966900
  - It's 50% faster than the JavaScript implementation.

- ## 🌰 With fs.readFile I can't easily determine the mime type in Node, right? (I don't want to use a libary.)
- https://twitter.com/_mql/status/1759890585949720687
  - We need it as fallback for "default" assets (like icons) that are not overridden in the database. So I guess in this case I can keep the mime type mapping in sync.

- you can't
  - you can probably approximate if the file is binary or not — reading first N bytes and see if there's a 0-byte there, which is not something you can find in text files
  - otherwise, yeah, need to you use libmagic (this is a lib name) probably

- ## JS isn't for the server
- https://twitter.com/pilcrowonpaper/status/1755569985995358211
- what a was the final straw
  - Issues with bundlers and packages ".node" files - so many help posts on Discord
- JS on the server shouldn't be processed. Bun or Deno should just execute the source. But we need all isomorphic packages to be shipped unbundled. Although it's scary if we start seeing libraries that rely heavily on non-standard runtime built ins (sqlite)

- ## Node peeps, is there something close to attached built-in (no dep needed).
- https://twitter.com/aboodman/status/1753586853415125060
  - I want to launch a child process and emit its output to the console as it happens (not wait for end of process), as well as capture the output to return to caller.
- it doesn't emit stderr. I could pipe that to stdout so that I can use the `for await` but I ideally wanted to write the child's stderr to parent's stderr, not smoosh the two streams together.

- does args.stdio = "inherit" work?
  - That doesn’t emit the output until the child process is done
  - Well we are not emitting it’s output but logging anything that happens from it

- use child.stdout.pipe

- ## 之前一直没太理解AsyncLocalStorage的作用，终于弄了一个好懂的例子了
- https://twitter.com/wulianwen1/status/1746723329359438024

- ## what globals from the browser are missing in Node.js that you want to have?
- https://twitter.com/jasnell/status/1376618110099226626
  - For those of you looking to write cross-environment, isomorphic javascript that works in browsers and Node.js --- other than fetch and WHAT-WG streams
- It would be neat if there were an official require(”vm”) factory to produce a browser-compatible context. Something along those lines might be a nice way to sandbox the sometimes incompatible underpinnings.
- Important: WebSocket + SSE, IndexedDB, FormData, FileSystem, Text{Encoder/Decoder}Stream, Sanitizer
  - Important-ish: WebRTC/Media*/Video*
  - Fun, but not important: Bluetooth, USB, Audio

- ## Today I learned that node's EventEmitter suffers from an issue called "producer interference".
- https://twitter.com/BenLesh/status/1699477675054707149
  - That's where an error thrown by a synchronous consumer (whomever called `on` ) prevents the producer (the `EventEmitter` ) from notifying subsequent other consumers.
  - This is something we had to change about Observable/Subject in RxJS 6 because of discussion about it in the original TC39 proposal and issues we saw it cause in production apps.
  - `EventTarget` (which is on the browser and node) does NOT suffer from this issue.

- I'm pretty sure this is the biggest source of issues in ldapjs. The nature of LDAP makes using an EventEmitter interface the natural fit, but handling protocol vs connection errors gets very ugly. I haven't determined how I'm going to remove EM yet, but I want to

- I discovered a while ago and rolled my own simple event emitter.

- ## Trying Node.js test runner: Gleb Bakhmutov examines capabilities of new built-in test runner that became stable from Node.js v20
- https://twitter.com/forweb_en/status/1646587007399854081

- ## 💡 Node v18 now has compilation of a Node.js script into a single-executable application using `npx postject` .
- https://twitter.com/karlhorky/status/1646421904205463554
- Any idea if they fixed Node's `fetch` leaking?g

- ## An experimental API for command-line argument parsing landed in @nodejs v18.3.0 - the `util.parseArgs` method. Very cool 👌 
- https://twitter.com/simonplend/status/1532304908585779201
  - intended for developers of simple CLI tools, ad-hoc scripts, deployed Node.js applications, and learning materials.

- ## Node.js now has a built-in test runner
- https://twitter.com/rauschma/status/1516456272215826432
  -  import test from 'node:test'; 
  -  import * as assert from 'assert/strict'; 

- ## Node.js: Best way for an app to run itself from the current(!) source on disk?
- https://twitter.com/rauschma/status/1420839210387394564
  - One option: start a new Node.js instance via child_process.execSync().
- Use case: A Node.js script runs for a long time, watches the file system to detect if its own code is changed and then runs itself (recursively).
  - Slightly weird, but makes sense in the context of static site generation.
- You're talking hot reload? There are tools that will do that for you already - just use one of them.
- If using an external tool is ok I'd recommend nodemon, or, I have to mention it, monex (https://github.com/fabiospampinato/monex). 
  - Otherwise spawning a child (of monex) should work. If you need to talk to the child I can recommend jayson for ipc 

- ## I used `fs·watch()` and found out that it always reports two changes whenever I save a file in VS Code. 
- https://twitter.com/rauschma/status/1420739486892191744
  - Consensus on the web seems to be: Avoid it and use other libraries that fix its issues.
- `fs.watch()` is not wrong, like most modern editors, VSCode uses “safe” or “atomic” writes, which do more than one IO operation to save a file (save to temp file, then rename to overwrite original file).
Using another library that abstracts this is useful, though.
- I've written a little comparison between that and chokidar/nsfw/node-watch in the readme too.
  - I'm saying that my package isn't, chokidar is, and nsfw is probably in the middle. It is pretty vague, but chokidar has 1000000x more downloads than mine, I'm basically the only person using mine, so I think that's potentially a significant downside that should be highlighted.

- ## In Node.js, we have awaitable timers built in, with cancellation support.
- https://twitter.com/jasnell/status/1371955481342742529

```JS
import { setTimeout } from 'timers/promises'
const ac = new AbortController()
await setTimeout(1000, undefined, { signal: ac.signal })
```

- ## @nodejs is fast and easy to use. 
- https://twitter.com/matteocollina/status/1381639256842584069
  - The fact that your JavaScript libraries are either (1) buggy (2) slow is not a problem of JavaScript. 
  - Simply put, those libraries are not well written. 
  - Rewriting everything in another language is unlikely to solve either problems.
- Node is also SOOO easy to use in ways that seem fine at first but break in a myriad of strange and surprising ways at scale.
  - Yes, I'm looking at you Streams and your hostile frenemy EventEmitter.
- I'm not sure how fast it actually is, I recently made a couple of libraries for reading files and fetching their stats objects about ~2x faster than what Node itself can do, and those libraries are build on top of Node itself too, this kind of stuff shouldn't really be possible.

- ## PSA: Using Node.js 16+ and want to compare the runtime performance of two functions ... Use `timerify` and `createHistogram` !
- https://twitter.com/jasnell/status/1392589770140774402

- ## in Node.js 16 you can prefix CJS require() and ESM import() specifiers for Node.js core modules with `node:` .
- https://twitter.com/jasnell/status/1385238402149150721
  - for instance `require('node:fs')` instead of `require('fs')` . 
  - This makes it clearer that it's a core module.
- Yeah I like this pattern, it’s worth using for weird cases when you want to ignore any mocking

- ## Did you know that in Node.js 16 you can use emojis as imports and exports names?
- https://twitter.com/NicoloRibaudo/status/1385346663842127873
- And is this useful?
  - Yes! When importing from other languages (e.g. wasm) you might have to import something that is not a valid JS identifier. 
  - My tweet was about emojis, but the actual feature is that you can use arbitrary strings in imports. 
  - I think exports support it just for symmetry.
- when did strings become identifiers?!
  - It's not part of the spec yet, but in practice it's a stage 4 feature (it has consensus from the committee, tests, and it's implemented in 3 major engines)
  - Is it just for WebAssembly?
  - Yeah the main motivation is integrating with other languages.

- ## New JavaScript features in Node.js v16 (compared to the latest v14)
- https://twitter.com/mathias/status/1387023971741315075

➡️ String.prototype.replaceAll
➡️ Promise.any + AggregateError
➡️ logical assignment
➡️ RegExp match indices
➡️ Atomics.waitAsync

- If we compare against Node.js v14.0.0, then these features are new, too!
  - top-level await
  - private methods and accessors
  - WeakRefs

- ## TIL Node.js v15 or higher can generate UUID v4 using `crypto.randomUUID()` ; 
- https://twitter.com/Kikobeats/status/1414661088247963652
  - `crypto.randomUUID([options])` ：Added in: v15.6.0
  - ts-node is a TypeScript execution engine and REPL for Node.js. 
  - ts-node非常适合测试api，内置模块也需要import('fs')或者require('fs')，两者都支持；
  - node版本更新太快，注意兼容性，甚至被删除或不存在

- ## Since Node.js v12, you can do: `import * as fs from 'node:fs';` .
- https://twitter.com/rauschma/status/1419472964496527362
  - Benefit: Can’t be confused with npm-installed packages.
- this also works in TS with the latests versions of @types/node which includes all the `node:` prepended stuff
- I think that’s the main benefit. A related benefit is that it allows adding new modules to Node core even if a package of the same name already exists on npm.

- ## Node.js is terrible at two things:
- https://twitter.com/jevakallio/status/1380073988802670595
  - Traversing big trees
  - De/serializing large strings
  - Also known as: - GraphQL Servers; - React SSR; 
- Serialization in all languages is costly and CPU intensive tasks the same, 
  - but this is a very good opportunity to write some native code in rust to cover those requirements.
- the purpose of event loop do not regards to it's limitation in certain kind of algorithms solving, 
  - because we pretty know that we have C to do this, the nodejs is a multipurpose tool that we use to do abstract things.
