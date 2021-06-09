---
title: lib-state-redux-community-stars
tags: [community, redux, state]
created: '2021-06-09T01:08:31.499Z'
modified: '2021-06-09T01:09:55.241Z'
---

# lib-state-redux-community-stars

# pieces

- ## 

- ## 

- ## 

- ## 

- ## Concurrent Mode
- https://github.com/reduxjs/react-redux/issues/1351
- The short version is that it's going to be up to the community to experiment and see exactly where the incompatibilities are.
  - Suspense transitions would likely be problematic, because you'd end up with cases where the Redux store is already updated from a dispatched action and thus trying to display "new" UI, whereas Suspense would want to still be displaying "old" UI.
  - The other major issue is "tearing", where new Redux actions might be dispatched during the pauses in rendering, and thus cause different parts of the tree to read different versions of the store state during the same render pass. 
