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
