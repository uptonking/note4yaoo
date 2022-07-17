---
title: lib-state-redux-community-stars
tags: [community, redux, state]
created: 2021-06-09T01:08:31.499Z
modified: 2021-06-09T01:09:55.241Z
---

# lib-state-redux-community-stars

# discuss-stars
- ## React-Redux Roadmap: version 8.x, React 18, and TypeScript
- https://github.com/reduxjs/react-redux/issues/1740
- most likely React-Redux v8 will:
  - Keep the exact same primary public APIs we have now (`useSelector` and `connect`)
  - Update the internals to be built around `useMutableSource` as an integration layer to provide better compatibility with Concurrent rendering. (It's also possible that we could look at context-based approaches again if React finalizes a "context selectors" API and makes that available.)
# discuss
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
