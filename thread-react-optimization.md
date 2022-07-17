---
title: thread-react-optimization
tags: [job, optimization, react, thread]
created: 2021-09-24T06:50:13.642Z
modified: 2021-09-24T06:50:31.330Z
---

# thread-react-optimization

# discuss
- ## 

- ## 

- ## helping someone debug react perf got me thinking about a generic high-level approach
- https://twitter.com/_paulshen/status/1441177985512468485
- 👉🏻️ Identify the cause of react rendering. 
  - This is usually some form of `setState` - could be in a lib (eg react-redux). 
  - React isn't going to rerender your app just because it feels like it
- 👉🏻️ Identify why the update is needed. 
  - What state is changing (if any)? 
  - What in the app cares about this change? 
  - How does the UI change and what are the side effects?
- 👉🏻️ Use profiler (or console.log) to see what code is actually running..
  - What components are rendering? Where is time being spent? (use react devtools/chrome perf)
  - What is diff between what needs to run vs what actually runs? 
  - If only parent component reads the state, do its children need to update? Most optimization is making this diff smaller..
- 👉🏻️ Change the code so that less code is running on state updates. 
  - There are a lot of strategies I won't dive into here - memoizing, React.memo, restructuring children, creating smaller global stores (eg redux), moving state outside react's purview, etc..
- 👉🏻️ There are also optimizations around reducing number of React updates. Strategies include throttling and batching (upgrade to React 18 or `unstable_batchedUpdates` )
