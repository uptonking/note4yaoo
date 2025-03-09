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

- ## 

- ## I just discovered that nearly all bundlers(rspack webpack rollup esbuild) handle module externals incorrectly(or not following spec).
- https://x.com/hardfist_1/status/1889287024743723053
  - It seems impossible to do it right unless bring lots of runtime code and bring ugly output result.
- defer import may help solve this problem
  - Module declarations could also solve it.
- keep esm ordering semantics is really hard and will introduce extra cost, it actually not only cause problems for external but also cause problems for advanced chunk optimization like code splitting and bundle splitting

# discuss-internals
- ## 

- ## 

- ## Currently, for performance reasons, we interpret JavaScript regular expressions literal as Rust regular expressions _202502
- https://x.com/hardfist_1/status/1886376769122652230
  - and don't meet too much problems, what if we interpret more JavaScript syntax as native syntax ?

# discuss-author
- ## 

- ## 

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
