---
title: lang-js-webpack-rspack-community
tags: [community, rspack, webpack]
created: 2024-01-03T16:14:34.162Z
modified: 2024-01-03T16:14:53.804Z
---

# lang-js-webpack-rspack-community

# guide

# discuss-stars
- ## 

- ## [RFC: Lazy make for reexports in side effects free barrel file · web-infra-dev/rspack _202508](https://github.com/web-infra-dev/rspack/discussions/11273)
  - barrel file: a file that imports modules from other files and exports the said modules
- https://x.com/rspack_dev/status/1952577747706142927
  - Rspack v1.5 will introduce an experimental optimization that skips building unused reexports in side-effect-free barrel files.
  - This reduces the build time of `import { Button } from 'antd'` from 528ms to 82ms.

- ## I just discovered that nearly all bundlers(rspack webpack rollup esbuild) handle module externals incorrectly(or not following spec).
- https://x.com/hardfist_1/status/1889287024743723053
  - It seems impossible to do it right unless bring lots of runtime code and bring ugly output result.
- defer import may help solve this problem
  - Module declarations could also solve it.
- keep esm ordering semantics is really hard and will introduce extra cost, it actually not only cause problems for external but also cause problems for advanced chunk optimization like code splitting and bundle splitting

# discuss-internals
- ## 

- ## I just realized that OXC's AST transfer is similar to TC39's binary AST proposal
- https://x.com/hd_nvim/status/1911838244498559139

- ## Currently, for performance reasons, we interpret JavaScript regular expressions literal as Rust regular expressions _202502
- https://x.com/hardfist_1/status/1886376769122652230
  - and don't meet too much problems, what if we interpret more JavaScript syntax as native syntax ?

# discuss-author/news
- ## 

- ## 

- ## 

- ## Rspack 1.4 will introduce Wasm build, allowing browser-based bundling in StackBlitz and other web environments. _202404
- https://x.com/rspack_dev/status/1912713947133981046

- ## Do you know Rspack can compile codes on demand just like Vite _202505
- https://x.com/Soon_Iter/status/1920088131363086447
  - `lazyCompilation` with preloading, build the code onHovering the link, seamless refresh 

- ## I originally thought that bundler was  CPU-bound, but on some platforms(enterprise macOS), the I/O overhead is far greater than the CPU overhead during make phase(generate module graph). 
- https://x.com/hardfist_1/status/1904140063338054110
  - Reading files takes significantly more time than parsing files
  - Don'ts guess, just profile!

- ## 🦀 @rspack_dev pick Rust just because @rspack_dev needs super complex js binding which is not easy for Go( binding between two gc language is hard)
- https://x.com/hardfist_1/status/1899502014935290162
  - reason 2: @rspack_dev needs minifier & transformer
  - if not limited by these, we would also choose Go to port Rspack(maybe called gopack).
- There're so many good parts of Go for porting existing Javascript code
  * much faster compile time(no need to release for an hour)
  * good support for cross compile(no need to get every machine or every docker image)
  * GC is much easy to use and debug than Rust Arena
- forgot to mention SWC

- https://x.com/hardfist_1/status/1899493638436245782
  - A key reason @rspack_dev chose the webpack architecture is the composability of loaders.
  - This architecture decouples filtering and transformation logic while enabling flexible configuration through module.rules, allowing developers to easily replace transformation logic for specific files without affecting other parts which seems not easy in Rollup or esbuld(try to replace the transform logic of vite-svgr-plugin without modify its code). 
  - If a faster TypeScript loader (e.g., ts-loader) with type-checking capabilities emerges in the future, users could seamlessly replace the builtin:swc-loader with the new faster ts-loader to meet their type-check needs.

- However such flexibility does come with a higher difficulty to configure TS properly to provide correct type for each import.
  - that's why we build rsbuild

- https://x.com/hardfist_1/status/1899578913472549138
  - If a rust parser is still much faster than ts-go parser, I think it's still useful. A faster rust transformer is not that appealing like before

- ## the @rspack_dev project originated from the @LynxJS_org project.
- https://x.com/hardfist_1/status/1898512395854811166
  - We started using Rollup to implement Lynx Build tools (2020.03), which initially only supported MiniApp DSL. However, we quickly encountered performance issues in large projects (2020.11).
  - Later, we rewrote Build Tools using esbuild to solve the performance issues (which is called speedy and can actually support run on webpack & rollup & esbuild), and added support for SFC and ReactLynx(2021.07). 
  - The reason we did not use Vite is because Vite not have good support for environments that do not support ESM and Bundleless. Later, we tried to use Speedy on Mobile Web Framework (2021.11), but the lack of good splitting support cause performance regression for users and HMR performance degradation caused by too much JS plugins forced us to reconsider whether Esbuild was a good choice
  - Therefore, we considered rewriting Esbuild & Rollup in Rust (2022.3). At this time, 3 infrastructure teams merged with various frameworks (libraries, mobile web, pc web, Lynx, microfrontends ..) and thousands of old webpack projects to support. 
  - we also encountered some limitations in the Rollup API (such as filter support and transform composability), so we decided to unify the build tools and solve the performance issues together with easy migration path, which leads to Rewrite webpack in Rust (2022.8) . And you know the rest of the story.

# discuss
- ## 

- ## 

- ## 
# discuss-perf
- ## 

- ## 

- ## 

- ## [Slow re-build time when changing JSX structure in React component _202401](https://github.com/web-infra-dev/rspack/issues/5315)
- Should been fixed _202402

# discuss-features
- ## 

- ## 

- ## [chore: support devServer.proxy _202212](https://github.com/web-infra-dev/rspack/pull/1329)
  - add devServer.proxy support
  - add function config support

- [devServer.proxy 不支持cookieDomainRewrite](https://github.com/web-infra-dev/rspack/issues/5469)
  - 我用你这一小段配置试了下 cookieDomainRewrite 是能正常工作的
