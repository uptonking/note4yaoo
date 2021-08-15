---
title: thread-dev-engineering-stars
tags: [engineering, thread]
created: '2021-08-10T03:50:40.299Z'
modified: '2021-08-10T03:51:01.891Z'
---

# thread-dev-engineering-stars

# discuss

- ## 

- ## 

- ## 

- ## Poll: How does your team do daily app development?
- https://twitter.com/housecor/status/1426893559056240645
  1. Call a shared dev environment database
  2. Call a dedicated database for each developer
  3. Call mock APIs
- #1 is common and the obvious default. But it's rarely the right answer.
- Why #2 or #3 are worth setting up:
  ✅ Stability
  ✅ Autonomy
  ✅ Faster iteration and feedback
  ✅ Supports fast, reliable APIs, which leads to fast, reliable tests 
- I'm not surprised simply because 1 is the default. 2 and 3 require extra up-front work, so you've gotta sell management on the need.
- #2 and #3 have an ongoing maintenance cost to take into account (#3 more so than #2) to keep feature parity. But still worth considering as its likely offset by the advantages you mentioned
- I use SQLite locally and move to sql server for production.
- I prefer a static dataset since it’s stable and can be augmented as we find edge cases we need to cover via tests.

- ## How I pivoted from an object-oriented programming style to a functional programming style
- https://twitter.com/housecor/status/1426191017968119813
  1. I stopped attaching behavior to objects. My objects are merely data structures.
  2. I create pure functions.
  3. I pass primitives/plain objects (with no behaviors) to these functions.
- I also do this in conjunction with my shift to "vertical slice" type architecture (vs the old n-tier/onion approach).

- ## If I want to create animations for video (nothing too complex: animated diagrams, simple illustrations) should I go straight to After Effects or are there more scoped-down tools to learn instead?
- https://twitter.com/steveruizok/status/1424799618559320068
- https://github.com/remotion-dev/remotion
  - https://remotion.dev/
  - Remotion is a suite of libraries building a fundament for creating videos programmatically using React.
  - Leverage web technologies: Use all of CSS, Canvas, SVG, WebGL, etc.
  - Leverage programming: Use variables, functions, APIs, math and algorithms to create new effects
  - everage React: Reusable components, Powerful composition, Fast Refresh, Package ecosystem
- PPT -> Video ?
  - not a bad option
- Really depends on what you mean by complex... sometimes Keynote is enough for me
- Rive also exports video and png sequences.
