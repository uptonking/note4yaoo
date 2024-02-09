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
# discuss-js-runtime
- ## 

- ## 

- ## AWS has entered the (js runtime) domain
- https://twitter.com/ArrowoodTech/status/1755667431190917577
- Extremely surprised it uses QuickJS and they specifically chose no JIT. It does make good sense for their situation though.

- yet another JS Runtime implementing Node.js compat? Controversial, but when do we call/turn Node.js into a standard?
  - defacto standard at this point
- their firecracker(爆竹，鞭炮; 杰出或激动人心、有吸引力的人或事物) vm is worth looking into if you want to get further back there in the backend and look at infra. i would imagine they are designing something purpose-built for it.
- IMO WinterCG should eventually work on standardizing the subset of the Node API that runtimes can implement to get “enough” compatibility. Maybe not time yet though
# discuss
- ## 

- ## 

- ## 

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
