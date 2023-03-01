---
title: thread-pm-base-presentation-ppt
tags: [pm, ppt, presentation, thread]
created: 2021-04-19T14:51:21.033Z
modified: 2021-08-16T06:59:32.581Z
---

# thread-pm-base-presentation-ppt

# guide

- ppt的技术方向侧重图形编辑器，依赖计算机图形学

- ppt的方向不要投入过多精力，很多大厂意识到ppt经常浪费资源，逐渐转向word

- products
  - design-to-code
  - code-to-design
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## we want to build a layout, so we have a designer mock it up in Figma, using the box model.
- https://twitter.com/steveruizok/status/1596886646066393088
  - then, we ask an engineer to implement the spec, done by hand, again using the box model.
  - this handoff process usually takes days/weeks. yet in theory doesn’t need to exist
- steveruizok
  - First, Figma acquired the very talented Visly team a few years ago, I imagine they’ve been working on something in design to code handoff.
  - My worry would be that creating a better handoff product would make Figma a worse design product
  - Even scoped only to layouts, production layouts often contain much more information than designs. That’s okay—it’s too much to expect a design to anticipate every edge case in a responsive layout, locale and accessibility setting combinations, etc
  - The outcome is that the design will never be a source of truth for a production application unless it is the only source of truth; ie an app like framer or webflow, where the app anticipates this in every feature
  - Those sites solve a very different problem than “engineers have to rebuild designs in code”
  - 👉🏻 because code export problem is imo not an actual problem. Rebuilding layouts from figma in html/css is an extremely minor and entirely acceptable redundancy in the product pipeline; pulling in generated code would create more problems than it would solve
