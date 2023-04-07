---
title: lib-state-redux-community
tags: [community, redux, state]
created: 2021-06-09T01:08:15.547Z
modified: 2021-06-09T01:09:47.648Z
---

# lib-state-redux-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Mark createStore as deprecated
- https://github.com/reduxjs/redux/issues/4325
  - We don't want anyone using the core createStore method directly in their apps today. 
  - We want them using configureStore from RTK instead.

- ## Is there a performance benefit on using Context API vs Redux?
- https://stackoverflow.com/questions/57841048
- Use-context with Use-reducer to replace redux is not a good practice. 
  - Context will cause reloading of the pages, this will be identified if we look into the profiler provided by react dev tools, where as redux won't do that. 
- I'm actually concerned with the performance, not the differences or when to use it.

- ## Concurrent Mode
- https://github.com/reduxjs/react-redux/issues/1351
- The short version is that it's going to be up to the community to experiment and see exactly where the incompatibilities are.
  - Suspense transitions would likely be problematic, because you'd end up with cases where the Redux store is already updated from a dispatched action and thus trying to display "new" UI, whereas Suspense would want to still be displaying "old" UI.
  - The other major issue is "tearing", where new Redux actions might be dispatched during the pauses in rendering, and thus cause different parts of the tree to read different versions of the store state during the same render pass. 
