---
title: lib-viz-vega-dev
tags: [d3, lib, vega, viz]
created: 2021-05-13T16:09:11.557Z
modified: 2021-05-13T16:09:35.947Z
---

# lib-viz-vega-dev

# guide

# discuss
- ## How did you decide to use Vega-Lite? There are a number of options in the JS visualization space (Plotly, Highcharts, chartJS, etc.)_202103
- https://twitter.com/ghalimi/status/1372119435272589314
- Because Vega-Lite is the only library I know that provides the right abstraction level. All other libraries end up hard-coding features for specific charts. Vega-Lite does not. It knows nothing about line charts or bar charts.
  - It just knows about what a chart is, and what marks like line and bars are. From there, you construct your own chart with meta-data. And this abstraction is itself built on top of Vega, which goes beyond charts and maps and can support diagrams.
  - The layering of abstractions from Canvas/SVG to D3 to Vega to Vega-Lite is very, very powerful. No other framework comes even close to that. And the level of configurability is unmatched, not to mention the level of interactivity brought by Vega-Lite 5.0.
- Vega and Vega-Lite are not as easy to use as other frameworks though, especially Vega. Their power comes at a cost
- when we first used it, Vega-Lite did not really exist. So we spent a year building something like Vega-Lite on top of Vega. And what we ended up with was about 5% of what Vega-Lite does today.
- This experience taught me three things:
  1. Vega-Lite is really clever.
  2. The Vega-Lite codebase is really clean.
  3. The Vega-Lite folks are true geniuses.
- But even Vega-Lite was not sufficiently abstract for us. If you try to develop a canonical UI for Vega-Lite for which you directly expose all concepts offered by Vega-Lite, you will end up with something that is not really useable.
  - This is not a negative critic about Vega-Lite. It is just a reflection of the fact that it's level of abstraction remains relatively low. Higher than Vega's and much higher than D3's, but still too low.
  - Furthermore, all three layers (D3, Vega, and Vega-Lite) lack a critical piece of the puzzle: a robust data typing framework. This is what we bring to the table with Principia Data
