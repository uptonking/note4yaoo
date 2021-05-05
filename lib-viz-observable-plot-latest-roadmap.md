---
title: lib-viz-observable-plot-latest-roadmap
tags: [observable-plot, roadmap]
created: '2021-05-05T07:44:41.621Z'
modified: '2021-05-05T07:45:07.226Z'
---

# lib-viz-observable-plot-latest-roadmap

# guide

# roadmap

# breaking-changes

- ## Announcing a new open-source JavaScript library for exploratory data visualization: Observable Plot!
- https://twitter.com/mbostock/status/1389611128339144704
- this will play nice with React?
  - Observable Plot is built on the standard DOM API. Whether web standards play nicely with React is up to React; I don’t want to write framework-specific libraries when I can write to standards
- My own understanding is that D3 is really about very specific low level data manipulation (not even viz specifically) while this new library aspires to be more declarative (gimme a scatter plot ASAP!)
  - D3 is like a “stdlib” for vis: low-level, decoupled components with little opinion on how they are put together. D3 is for bespoke visualization or as a foundation for higher-level tools (including Vega-Lite and Plot). Plot is for exploring data quickly.
- It'd be awesome to have a standard JS module distribution so this can work directly in browsers with no tools. Does D3 have a modules distribution?
  - It’s a nontrivial task but we’re actively working on it, and as soon as D3 adopts type = module so will Plot.
  - That said you can already consume D3 or Plot as ES modules in browsers using Skypack as described in the README.
- Have y'all considered a standalone dataframe library? I'm surprised ops like group are Plot operations.
  - Try using Observable Plot with Arquero! The integrated transforms like group aren’t mandatory — they’re just convenient.

# changelog
