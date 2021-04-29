---
title: page-engineering-dev
tags: [dev, engineering]
created: '2021-04-29T13:16:29.483Z'
modified: '2021-04-29T13:16:52.333Z'
---

# page-engineering-dev

# guide

# pieces

# blogs

## [Exploring Codebases](https://bypaulshen.com/posts/exploring-codebases)

- Which file do you open first? App.tsx seems like a good starting place.
- Rather than random walk through the codebase, I find it useful to have a goal, even if artificial. 
- I come up with a statement — there MUST be a place where X happens — and then try to find it.
  - In React, there must be a place where it manipulates the DOM, probably with DOM APIs (appendChild? innerHTML?). How does it decide what DOM manipulations to perform?
  - In this app, there must be a place where it fetches data from the server. Maybe a fetch call? GraphQL? or some other abstraction.
- Why does this line of code exist?
  - Maybe there are useful comments nearby. Maybe the associated commits are well structured. Or the code is well structured.
- Jump to definition and find references are table stakes language service features at this point. 
- What are other useful language features for reading code?
  - Trace the code： flamegraphs
  - Documentation
  - contributors
  - Tooling
