---
title: thread-dev-state-management
tags: [dev, state, thread]
created: '2021-02-28T07:28:44.040Z'
modified: '2021-02-28T07:29:07.622Z'
---

# thread-dev-state-management

# repeat

- ## The motivation I develop global state libraries is to avoid selector interface that are only required for render optimization.
- https://twitter.com/dai_shi/status/1373607985033871363
  - It depends on object ref identity which is a hard concept for beginners.
  - This shows some comparison among use-context-selector, jotai and proxy-memoize.
  - #ReactTracked and #Valtio are not shown, but they have the same idea.

# pieces

- ## 

- ## 

- ## today I'd use Redux Toolkit, hooks, single-file "slice" logic, no hand-written actions, and probably not bring in Redux-ORM unless I had _very_ relational data.
- https://twitter.com/acemarke/status/1373296162082553862
  - Ecosystem: hooks, CRA abs path changes, Semantic-UI unmaintained, Redux-ORM had a lot of API changes.
- In other words, _principles_ are still the same, vs specific lib versions and APIs.
  - feature folders, optimizing re-renders, selecting data in children by ID, reducer patterns, techniques for modals, etc.

- ## Counter examples: zustand vs. valtio vs. jotai
- https://twitter.com/dai_shi/status/1372705718764068865
  - https://codesandbox.io/s/zustand-valtio-jotai-counters-my6np
- Can we also have speed/performance comparison between those libraries?
  - Performance is hard to discuss. Main concern in React global state libs is extra re-renders and all there basically deal with it. Other than that, it depends on requirements and app code. Zustand is thin, so if app code is optimal, it'd be best. Valtio might work better otherwise

- ## Some people that watched my Records & Tuples talks were interested to discuss the benefits for Redux/Reselect ecosystem.
- https://twitter.com/acemarke/status/1370417763366354949
  - IMHO it has advantages and can optimize some selectors more easily than Reselect
  - Maybe the impact of R&T may be smaller for the Redux  ecosystem once useContextSelector land?
- Really not sure how much benefit it's going to have.
  - The real point of memoized selectors is _derived_ data, ie, `todos.map(t => t.text)` - both avoiding expensive recalculations, and returning same references if inputs haven't changed.
  - Eyeballing it, it seems like R&T _might_ help with the _comparisons_ of those (even deeply). But it wouldn't help with _avoiding_ the calculations in the first place.
  - Also, I don't see as much benefit for updates, given the existing of Immer and its use in RTK.
- if you filter() and it does not filter anything, or map and it does not transform anything, with a record it can return the same array. 
  - I think it can have some advantages to bail-out earlier of some further computations, including React re-renders but not only
  - I like Immer but would be quite happy to replace it with this https://github.com/tc39/proposal-deep-path-properties-for-record

- ## I find the term "global state" a bit dated, which is why I use server-state and client-state. 
- https://twitter.com/TkDodo/status/1368198159223111684
  - client-state can bel local (useState) or global (zustand, redux). 
  - server-state with react query is always global - accessible everywhere via the right query key.

- ## starting to think this "derive transformed data while rendering instead of storing the transformed data in state" needs to be a blog post.
- https://twitter.com/acemarke/status/1367332072063455232
- I think the realisation that we can just derive most state instead maintain and sync it was one of the AHA moments I had with react.. would love to read your take on it
- [Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it)
- [Don't over useState](https://tkdodo.eu/blog/dont-over-use-state)
  - An example
  - Fetch some data from a remote endpoint (a list of items with categories) and let the user filter by the category.
  - We have no predictable way of telling what "categories" are.
  - The page loads, categories are X
  - User clicks the button, categories are Y
  - If the data fetching re-executes, the categories will be X again
  - Maybe this is not so much about `useState` after all, but more about a misconception with `useEffect` : It should be used to sync your state with something outside of React. 
  - Utilizing `useEffect` to sync two react states is rarely right.
  - Whenever a state setter function is only used synchronously in an effect, get rid of the state!
  - We've reduced complexity by halving the amount of effects and we can now clearly see that categories is derived from data. 
  - A single source of truth.

- ## Literally never ever use redux on a new project under any circumstances. 
- https://twitter.com/tannerlinsley/status/1365834060161900548
  - Most projects are served just fine with context, hooks, and something like useSWR(). Beyond that you should look at something like relay.
  - It’s a fine way to express a state machine but (1) plain state machines don’t really help you with common problems that much and (2) it’s easy to express plain state machines in modern react
- Ironically, "state machines" aren't even the primary use case for Redux
- The best reasons to use Redux are:
  - Writing as much logic as possible as pure functions
  - Moving logic outside the component tree
  - the DevTools
- Have you seen typical React code that doesn't have a state management tool that helps with structure? Most of the time, it's an absolute mess.
  - Excessive amounts of useState() per component, ad-hoc logic and validation in event handlers/callbacks instead of some centralized place, state in context causing unnecessary, large rerenders, race conditions due to async logic in useEffect(), etc.
- The hooks that React provides don't afford any guidance towards any notion of organized structure, and trying to implement ad-hoc state management with the hooks creates performance problems more often than not.
  - Yes and this is exactly why redux is such a problem.
  - It provides some structure and it gets way overused. 
  - And it creates so much code that you have to maintain. 
  - And so much indirection that’s hard for newcomers to follow. And it’s not aware of life cycles. Etc
  - And the branding is really good so people think you need to leverage more and more of the ecosystem, which creates a lot more indirection for, imo, very little benefit (I’m thinking especially of redux thunk)
  - Yeah, I agree with you on redux thunk but, to be fair, the side-effect story with React isn't much better. The useSWR/useQuery/etc. hooks definitely help, but have specific use-cases (async logic isn't just data fetching/caching).
- I often think that the future of apps is built on state machines where React plays a very minimal role in our application state/business logic. It's not going to take much more for the tooling and ecosystem attitude to catch up and realize this future.
- I used to think this too until we tried to use just context and usereducer in a non-trivial app. My God the unnecessary renders and performance issues 
  - I think there's still a valid use case for redux
- I would really like to know what you think of @pmndrs three tools: zustand, jotai and especially valtio. 
  - Zustand for flux, jotai for atoms and valtio for proxy, they all reduce to the smallest principles.
