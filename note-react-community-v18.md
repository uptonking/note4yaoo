---
title: note-react-community-v18
tags: [community, react]
created: '2021-06-09T10:37:45.741Z'
modified: '2021-06-09T10:38:04.542Z'
---

# note-react-community-v18

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

- ## 

- ## Pitfalls and surprises in data fetching
- https://github.com/reactwg/react-18/discussions/35
- There are a few main concerns that come to mind in terms of data-management and concurrent rendering:
  - Data changes during rendering
  - Lazy-fetching and concurrent rendering
  - Lazy-fetching and offscreen
  - Prefetching and concurrent rendering
