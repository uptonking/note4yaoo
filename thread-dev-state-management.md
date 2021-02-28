---
title: thread-dev-state-management
tags: [dev, state, thread]
created: '2021-02-28T07:28:44.040Z'
modified: '2021-02-28T07:29:07.622Z'
---

# thread-dev-state-management

# pieces

- ## 

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
