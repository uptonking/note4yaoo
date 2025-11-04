---
title: lang-js-toolchain-devtools
tags: [devtools, lang-js, thread, toolchain]
created: 2024-03-17T15:24:08.363Z
modified: 2025-04-09T02:49:16.372Z
---

# lang-js-toolchain-devtools

# guide

# discuss-stars
- ## 

- ## 

- ## 你混淆过的JS代码将和“开源代码”没区别，ChatGPT可以轻松将你混淆后的代码还原。
- https://twitter.com/HeySophiaHong/status/1769238857286086886
  - 编译过后的代码也不安全，现在已经有研究能反编译二进制了

- js的混淆并不是主要为了安全
- 如果是前端，做什么加密混淆都意义不大
- The purpose of Uglifying is just to minify the size of the js file.

- 想靠“加密”前端代码来获得安全方面的保护，本来就是自欺欺人的做法。 拆穿这个假把式有益帮地球省点能源。

- 这星期刚试过，真的看起来可行，虽然也可能存在一定幻觉，但是可信度不低，拿来还原80-90%的逻辑能节省不少工作量

- 反编译这项工作的确适合AI做，各种混淆器再厉害也架不住AI的大数据训练。
# discuss-testing
- ## 

- ## 

- ## [Best test framework for Node in 2022? : r/node _202209](https://www.reddit.com/r/node/comments/xhb4bi/best_test_framework_for_node_in_2022/)  
- We use Mocha with Chai for tests - works perfectly. 
  - We use c8 for coverage, which is a drop-in replacement for nyc which doesn't (or didn't when we switch) support `import` . 
  - We then use husky for managing git hooks, such as ensuring all tests pass to allow a push (which can be forced through if needed).

- Mocha and Chai are a terrific mixture. Chai offers a plugin system which may help with testing. I think it's worth mentioning.

- One thing that Jest has — both for better and for worse — is a module mocking mechanism. With your mocha + chai setup, do you ever find that you need to mock out a dependency of the module that you are testing? If yes, how do you do it?
  - Sinon if you have to. Restructuring your code so you don't have to mess with imports when you need mocks is a better move, though.

- Chai is an assertion library; it is meant to facilitate writing assertions. You want to use Sinon for anything spy related.
- Jest is okay but still very FB and React-oriented. On the front end, with a React project, I would use Jest only if required. Jest is not better than these three.
- The combination (Mocha, Chai, Sinon) covers all types of tests. You are never let down.

- We use node-tap at work which is similar to the new experimental nodejs test runner. There is also AVA which is also popular. I tend to lean more towards test runners that don’t pollute the globe namespace, that have a reduced api and rely less on mocking. If you write pure functions, then testing becomes much simpler and not much need for mocks.

- I maintained Mocha for 5 years and added parallel execution support.
  - Jest has certain limitations that you should be aware of when testing Node.js code or ESM in particular.
  - You can test just about anything with Mocha, but not out-of-the-box. Module mocks can be handled by something like rewiremock. Snapshots with other plugins; often these are plugins for assertion libs. OTOH if you’re using ESM w/o transpilation, mocking modules is much more painful due to limitations of the spec.
  - node-tap and ava work great. node-tap is especially well-written.

- ## [Jest or Mocha for testing Nodejs Application : r/node _202110](https://www.reddit.com/r/node/comments/q55mh2/jest_or_mocha_for_testing_nodejs_application/)
- A thousand times jest, because it gets coverage right, which mocha doesn't.

- The only reason to use jest is to support React component testing, and that's still not a great reason because there are solutions to this problem now that use mocha. Mocha is soo much faster and less complicated. The testing support that Jest provides that Mocha does not can be added in through the use of Sinon and other packages if needed. Jest tries to support too many test needs and does none of them well. I'll never use jest in a project again. Mocha is always the right choice.

- mocha and native assert
# discuss-compiler/tsc
- ## 

- ## 

- ## ts-node monkeypatches `require.extensions` (a internal that should not have been exposed and has been deprecated since Node.js v0.10) which conflicts with Node.js type stripping and boom
- https://x.com/satanacchio/status/1902715349021204845
- not many dependencies rely on require.extensions to know if ts-node is loaded, we are opening a bunch of issues and sending patches

- ## Do any TypeScript compiler nerds out there know if there's anyway to create a TS server plugin asynchronously?
- https://x.com/justinfagnani/status/1847699545658184114
  - I need to import some standard JS modules into my plugin.
  - I might need require(esm) to land in VS Code

- Use workers to import the esm module  into the worker and atomics in the main thread and worker to wait on this synchronously.

- ## [How to compile a specific file with tsc using the paths compiler option - Stack Overflow](https://stackoverflow.com/questions/44676944/how-to-compile-a-specific-file-with-tsc-using-the-paths-compiler-option)
- what you can do is overwrite the include property of your tsconfig with something like this: `"include": [ "src/root/index.ts" ]`

# discuss-tsgo
- ## 

- ## 

- ## 

- ## [When "tsgo" is released, will it be able to execute typescript directly like ts-node, or will executers like ts-node and tsx be updated to use it? : r/typescript _202506](https://www.reddit.com/r/typescript/comments/1l6l8nh/when_tsgo_is_released_will_it_be_able_to_execute/)
- `tsgo` is a replacement for `tsc` . It'll do what tsc currently does. It also replaces the custom `tsserver` with a standard LSP interface.

- No, tsgo won't execute typescript code just like the current tsc doesn't. 
  - It will compile it to check for errors and optionally emit JavaScript, and provide language server protocol services.
  - I would expect that yes execturos like ts-node and tsx will either be updated to use it, or tsgo will be merged into the main typescript project so that it just works and the executors start using it without even knowing they're using something different.

- It's substantially slower than the swc based alternatives and Go is much harder to use as a "plugin" due to its poor FFI capabilities so it's unlikely it will be used by tools as a type-stripping back end.
  - That said, Nodejs has TypeScript support built in now (swc backed) so ts-node, tsx and such are effectively redundant. It's also much better than tsx/ts-node because it doesn't have leaky transforms.

- probably not. that is not really typescripts job
  - ts-node exposes you to the trouble of runtime node.js esm resolution, and cjs/esm incompatibility, which is frequently troublesome, so this is indeed common what you are seeing
  - tsx helps by using a bundler, esbuild, under the hood. the bundler basically removes the need to do runtime esnext/nodenext module resolution, since it is all just bundled. can be helpful for cases where cjs vs esm is causing trouble 
  - you should consider using node with --experimental-strip-types. it replaces 90+% of reasons ts-node or tsx is needed. it is more similar to ts-node than tsx in spirit, as it does do normal runtime module resolution, no 'bundling', it just removes ts types so that it can ingest .ts files

- these tools do different things. tsgo is for type checking. People typically don't check types when using something like tsx to execute code. You just do that in your IDE / CI.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 💡 Pro tip: always do deps installation at the start of your dev script, like `pnpm i && vite` . It will save you nerves during branch changes / pulling.
- https://x.com/artalar_dev/status/1949184081498894788

- ## I'm wondering whether bundler & compiler should keep following Node.js new features like `module-sync` , 
- https://x.com/hardfist_1/status/1843292473046781963
  - It seems tools should be runtime agnostic, so why should we keep following Node.js specific new behavior other than Deno's or Bun's. I hope JS0 can solve these things
  - Node.js behavior shouldn't be treated as tooling's standard. We need a tooling standard

- ## JavaScript compilers today are fixated on compiling individual modules. 
- https://x.com/trueadm/status/1806470121604419969
  - That is a sensible and deterministic property but really the true power of compilation is cross-module.
  - You could even argue that there would be no need for something like RSC as a highly intelligent compiler could do all that work for you and remove the limitations by refactoring your code to make it work.
  - The drawback is always going to be the debugging experience. The more the compiler does work that the developer doesn’t expect, the harder it is to reason about some bugs. This is solvable though, as has been shown in other languages.
