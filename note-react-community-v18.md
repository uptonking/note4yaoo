---
title: note-react-community-v18
tags: [community, react]
created: '2021-06-09T10:37:45.741Z'
modified: '2021-06-09T10:38:04.542Z'
---

# note-react-community-v18

# guide

- [A better React 18 startTransition demo](https://swizec.com/blog/a-better-react-18-starttransition-demo/)
  - https://react-fractals-git-react-18-swizec.vercel.app/
  - https://github.com/Swizec/react-fractals
  - 可以增加树的高度和叶节点的数量
  - 给出了调试步骤
# v18-stars
- ## an initial implementation of built-in Suspense cache.
- https://github.com/reactwg/react-18/discussions/25
- The cache is optimized for data that is fetched over an IO boundary. 
  - You wouldn't use it to store, say, controlled text input state or scroll position or other UI-driven state.
- the cache is append-only. 
  - The only way to update an existing entry in a Suspense cache is to refresh and populate a new cache. 
  - So Redux would have to refresh the cache on every `dispatch`, which is not what we designed it for.
  - Refreshes are meant to be pretty rare. Mainly during a navigation, or after a server mutation.
- A good **rule of thumb** is that if it's a type of data that might be preserved when you hit the browser's refresh button, then it can be put into the cache.
  - If the state is lost when you refresh, then it's probably UI state that belongs in a state hook.
- Putting all your UI state into `useState` or `useReducer` is by far the easiest way to ensure that your library will work with all our concurrent features. 
  - (We know there are reasons why people choose not to do this, but we're exploring solutions to address these. 
  - Like making the context API faster to remove the need for subscription-based replacements. Or a new combined context + state API that is optimized specifically for cross-cutting updates that affect many different components.
- If moving ownership of your data store into React isn't an option, you can use `useMutableSource` — which works pretty well for basic cases, but does occasionally de-opt back to synchronous mode. 
  - But `useMutableSource` isn't a cure all. We can prevent inconsistencies (tearing) with `useMutableSource`, but we can't guarantee that that all concurrent features will work perfectly, 
  - because to maintain consistency, we may have to temporarily de-opt back to synchronous rendering.
- Does it mean that when anything new goes into the cache everything else is invalidated?
  - I should have been more precise. By “update” I meant “change an existing cache entry.”
  - Adding new entries to the cache will not affect other entries. You can append as much as you want.
  - It’s only when you mutate something that you have to do a refresh.
- React Fetch keeps data in the Cache (via unstable_getCacheForType) so when the cache is cleared, that data is gone. 
  - This is not specific to React Fetch — any data fetching library integrating with the Cache would work t
# pieces
- ## 

- ## 

- ## 

- ## With time we’ve noticed many bugs had common causes. 
- https://twitter.com/dan_abramov/status/1402937595005386752
  - Some parts of our code were overly “clever” and fragile. 
  - In some places the whole model was flawed and fixing one thing broke the other. 
  - This knowledge led to @acdlite , @lunaruan and @brian_d_vaughn doing two huge refactors.
  - At some point after the refactors rolled out, these bugs just stopped happening. We haven’t had a big one for months by now. But rolling out those refactors was very hard because they could break everything. So we kept two versions of most files, and shipped both as AB test.
- One of these refactors was risky because we replaced a “clever” fast mechanism with a more naïve one. This fixed bugs but AB test showed a significant perf regression. We couldn’t ship it because we didn’t know the cause. We can’t slow down all React apps due to some refactor.
  - We couldn’t guess where the problem is but we were hoping it’s a bug and not a fatal perf flaw. So we reverted the entire refactor and then split it into small individual commits.
  - In retrospect, we should’ve done that from the beginning. It seemed gruelling to redo the work as small atomic changes and AB test each change separately (for at least a week) but finally we found the bad commit. In a small change, the team guessed the issue and the fix worked.
- This refactor unblocked the remaining work which was needed to fix the last significant set of issues with Suspense API that we’ve learned over the two years of using it extensively in the product code. We switched to working on incremental adoption right after in early 2021.

- ## Pitfalls and surprises in data fetching
- https://github.com/reactwg/react-18/discussions/35
- There are a few main concerns that come to mind in terms of data-management and concurrent rendering:
  - Data changes during rendering
  - Lazy-fetching and concurrent rendering
  - Lazy-fetching and offscreen
  - Prefetching and concurrent rendering
