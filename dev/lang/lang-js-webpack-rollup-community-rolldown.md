---
title: lang-js-webpack-rollup-community-rolldown
tags: [community, rolldown, rollup, webpack]
created: 2024-12-21T13:36:25.532Z
modified: 2024-12-21T13:36:48.616Z
---

# lang-js-webpack-rollup-community-rolldown

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 🤔 Rolldown's wasm build just got significantly faster in browsers
- https://x.com/youyuxi/status/1869608132386922720
  - One challenge of native bundlers is that they have to ship and run as wasm in browser environments. Some bundlers like rspack doesn't even support this due to the complexity it involves.
  - the biggest perf advantage of native bundlers comes from parallelization, but in browsers we'd have to simulate threads using web workers. Without proper optimization, native bundlers can end up being slower than JS bundlers in browsers!
  - For example, I was surprised to find out that esbuild's wasm build is actually significantly slower than Rollup in web containers. This may have to do with Go wasm compilation and de-optimized parallelization.
  - Rolldown suffered from this too, and we've been wanting to tackle this since the very beginning because we know we want it to run fast in every use case.
  - our friend @Brooooook_lyn finally solved this by implementing proper worker thread pooling / reuse in napi-rs.

- Do you think you can use wasm on @nodejs too? How slower it is compared to native? Considering all the problems and bugs of native addons, it would be great.
  - Yes, this is actually running through WASI of StackBlitz’s version of Node. Haven’t tested it against local Node but it should work too.

- Will this increase the speed of Vite?
  - That’s the whole point of Rolldown

- 
- 
- 
- 
- 
- 
- 
- 
- 

- ## Bootstrapping achieved! Rolldown is now bundling its JS CLI with itself _20240524
- https://x.com/youyuxi/status/1793938789968351646
  - Currently it's transforming TS using a simple esbuild plugin. 
  - With OXC TS transforms landing later this year, TS transform will become built-in and no longer require plugins.

- ## Rolldown is open source! The Rust-based bundler designed for the future of Vite. It is still a work in progress, _20240308
- https://twitter.com/youyuxi/status/1766014404666245582
  - but it's now in a state that we are happy to share with the community and welcome contributions.

- @rolldown_rs & @vite_js the Rollup's hashing algorithm ammends hashes of unaffected VUE files each deploy. Is there a chance that rolldown will have a different/better hashing algorithm?
# discuss-perf
- ## 

- ## 

- ## 
# discuss-features
- ## 

- ## 
