---
title: thread-lang-js-datatype
tags: [data-type, lang-js]
created: 2024-03-16T14:11:24.927Z
modified: 2024-03-16T14:11:57.461Z
---

# thread-lang-js-datatype

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## This is a way better default than using `Number.parseInt` directly.
- https://twitter.com/cpojer/status/1768807456782876808 
-  I’m using `Number.isFinite` though.
- What‘s the advantage over checking for a finite number or !isNaN?
  - For me it’s forgetting to check for NaN because it’s typed as number. Returning null forces me to deal with it at every call site.
