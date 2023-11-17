---
title: pattern-arch-flux-community
tags: [architecture, community, flux, redux]
created: 2023-11-17T10:27:15.910Z
modified: 2023-11-17T10:27:28.695Z
---

# pattern-arch-flux-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🤔 [What do you mean by “Event-Driven”? | Hacker News_201702](https://news.ycombinator.com/item?id=13593683)
- Event-sourcing implies CQRS, but the reverse is not true.

- I see CQRS as an implementation detail orthogonal to ES, but which dovetails nicely as they both work well with distributed systems. ES has immutable events (monotonically increasing), and CQRS implies a distributed system and allows for more efficient retrieval, leveraging ES's immutability.

- I think that most of the time event-sourcing will impact your model/business-logic layer, because you often want to capture the intent of changes, rather than calculating a naive combined delta of all changes that occurred in memory.

- A good summary. However too many choose to view it only as Event-Sourcing/CQRS, a silver-bullet applicable to a minority of applications.
  - Event-Driven as an architecture that is based on recording changes to a baseline state, should be applied only where really suited.

- ## 🤔 [Why did you reinvented Event Sourcing, a concept that had existed for almost a decade, and renamed it to "Redux" instead of keeping the original name?_201607](https://github.com/gaearon/ama/issues/110)
- Redux is JS library inspired by Flux, Elm and Om. **Both Flux and Elm are inspired by event sourcing**. Redux is not called EventSourcing.js (is this what you propose) for the same reason Flux and Elm are not called EventSourcing.
  - PS. Redux is actually somewhat different from event sourcing (see all those discussions) but again, I’m not claiming it’s somehow better, or that Redux is a pattern.

- ## 🆚️ [Flux Comparison by Example | Hacker News_201502](https://news.ycombinator.com/item?id=8989495)
- Anyone tried doing isomorphic (server/client) flux? 
  - Most implementations rely on the flux stores being singletons which can't work for multiple requests on the server. 
  - The only one that's isomorphic is yahoo's but that one feels terribly verbose.
- I've been making an app based on yahoo's dispatchr (part of fluxible) for about 4 months now, and I hardly spend time with the "verbose" part of my app. All the real work is in data fetching, view rendering, business logic, and so on.
- I am using Yahoo's fluxible app and it is quite good. Doesn't feel verbose at all in every day use.
- Which part of Fluxible feels verbose?
  - dispatching and listening to actions. you need to pack your action with a magic string and a param object then unpack the params again in every listener. 
  - dealing with asynchronous data fetches: 3 actions for every async data action
  - the service api: too many optional params
- It would be cool if there was a nice way that you could wrap an action with a function to generate that boilerplate for you

- Alt has isomorphic support but there are some trade offs such as you're unable to use actions on the server. But you can still keep your stores as singletons and have them be concurrent. I'm still juggling on different ways to tackle this problem to offer more flexibility.

- My experience is also that it's almost impossible to make isomorphic apps with singleton based designs. Too bad the original Facebook version used singletons and everybody copied it. Big mistake.
- I haven't understood why this pattern hasn't been the default all along. Singletons are not a pattern used very often in JS so I'm not sure why it caught on in Flux.
- the original Facebook example used singletons and everyone followed their lead.
# discuss
- ## 

- ## 

- ## [How to optimize React applications that use Redux | Hacker News_201707](https://news.ycombinator.com/item?id=14706430)
- This doesn't really explain why it has to be that way. I'm not really a fan of "it is because it is" design. It doesn't seem like there's any particular reason that a state reconstruction algorithm needs to be more expensive than O(1). What kind of advantages does this design have that an append store wouldn't give?
  - Redux was built as an implementation of the Flux Architecture. In Flux, you have different "stores" for different types of data (such as a UsersStore, PostsStore, and CommentsStore). One of the key concepts of Redux is that instead of having separate stores for each type of data, you can have separate "reducer functions" that are responsible for initializing and updating those data sets, and write another function that combines all of them together into a single object state tree. 
  - So, the standard encouraged approach is that the root reducer function delegates the work of updating each "slice" in the state tree to smaller functions, and so on ad infinitum. That way, each individual slice reducer function can be written and understood in isolation.

- ## [A Farewell to FRP | Hacker News_201605](https://news.ycombinator.com/item?id=11667523)
- When ELM came along with its signals, im like, meh, why not Rx?
  - Just like when Flux "came out". They just rebranded Event Sourcing in the client UI.
