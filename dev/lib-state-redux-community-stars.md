---
title: lib-state-redux-community-stars
tags: [community, redux, state]
created: 2021-06-09T01:08:31.499Z
modified: 2021-06-09T01:09:55.241Z
---

# lib-state-redux-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## 🤔 [Sagas should rather be totally autonomous · redux-saga/redux-saga](https://github.com/redux-saga/redux-saga/issues/8)
- You have to consider the source of truth according to what you will want to record / replay and how the derived source of truth should behave after code change.
- 👉🏻 state sourcing
  - If you consider state as a source of truth, then you can record state and replay them in the same React app.
  - If you record only state, you don't have the event log and then if you change a reducer the state history will remain the same: you can only hot-reload React views
- 👉🏻 event sourcing
  - If you record events (or actions) of what has happened, then you can replay these events into redux reducers to recompute the whole history of states, and replay this state history into React to show something. 
  - If you change a reducer, then you can compute a new history of state: this is how Redux hot reload works. However you can not modify the event log.
- 👉🏻 command sourcing
  - If you choose to record the commands (ie the user intent) then you can recompute an event log from the intent log, and then a state log from the event log. 
  - The intent is generally translated to events in actionCreators and jsx views where we transform low-level dom-events to Redux actions.
  - Command sourcing would permit to hot-reload the interpretation layer too and would replace the "WentLeft" by a"Jump" in the event log before computing the state log and before injection states in React. In practice it has not much interest and may be more complicated to do (not sure but maybe ELM is doing this no?)

- ## [Redux is half of a pattern (1/2) - DEV Community](https://dev.to/davidkpiano/redux-is-half-of-a-pattern-1-2-1hd7)
- the article completely misses the point about Redux being an event store that implicitly leverages several good patterns that are seen in highly-available distributed systems.
- it forces you to separate your write model (dispatch) from your read model (props). this is known as CQRS.
- the reducers are actually referred to as projections in event sourcing.
  - reducers/projections are just aggregate data accumulated from events and are considered part of the read model. 
  - the strategy of doing the reduction on each event allows you to present aggregated data in "realtime". 
  - the alternative would be to iterate through large sets per read or write. it's a per-event, "realtime" .reduce()
- Redux + Thunks was terrible. 
  - But Redux + Sagas more closely represent event sourcing as you see it in distributed systems. 
  - with events thought of as streams (or aggregates in the Domain-driven Design world). 
  - Sagas are actually referred to in the event sourcing world as either process handlers or sagas and are responsible for complex stream handling.
- event stores and blockchains use roughly the same structure conceptually: Append only File
- most databases under the hood actually have a very similar event sourcing structure referred to as WAL -- write-ahead logging.
- the typical event payload is the same in all these systems {eventType, metadata}
- Just take a look at Redux w/ Sagas, Greg Young's Event Store, any blockchain, and even Kafka. They are all fundamentally similar. And since they all source from a log file, they can all replay state.

- Redux is absolutely not event sourcing (I used both extensively)
  - The only thing in common is that there are "events", something extremely common and found in pretty much all codebases (and the dreaded DOM)
  - No frontend keep all the events from last week around for the logged user, it's slow enough as it is. If you don't keep all the events, then it's not sourcing, just event driven (like almost all UI paradigms from the last decades)
- "Event-driven" does not mean "event sourcing".

- ## What are people using these days for React state management?_202308
- https://twitter.com/ccorcos/status/1689440157781606400
  - I’m talking more about UI state as opposed to backend/data stuff.
  - useState: plumbing can get annoying
  - Redux: too much boilerplate
  - MobX: popular but I fear complexity
  - Zustand: looks like what I'd build myself
  - Recoil: doesn't have garbage collection?

- Relay has client side schema extensions for local state

- https://github.com/theatre-js/theatre/tree/main/packages/dataverse
  - Dataverse is the reactive dataflow library Theatre.js is built on. 
  - It is inspired by ideas in functional reactive programming and it is optimised for interactivity and animation.
- Kind of looks like you're re-inventing React hooks though with the effect stuff.
  - Yeah that was intentional because I felt hooks are a nice escape hatch from the pure/functional paradigm while keeping the code looking functional. 
- I like Jotai and Signia. 
  - Signia is the closest to Notion state but it’s more correct. Has transactions. No proxies. Used by @tldraw , pretty nice.
  - Annoying thing about Jotai is using it outside React components was annoying like 2 years ago when I played with it.

- tldraw and Notion are already built around lightweight in-memory databases implemented in Javascript.
  - You can adopt TLStore + Signia in your own app, I did it to manage state in my Electron guy

- I've moved on from the whole idea of "app state as a reactive relational database". 
  - You can do that right now with tuple-database but I've learned that statically defining the entire state tree and manually garbage collecting it is a pain and doesn't add much value.
  - Just imagine a complex UI like Notion: dynamic lists of objects with arbitrarily nested popup menus based on the type of block. You don't want to have to structure all that state in a single global database. I've tried and its just a waste.

- We created Zedux for exactly this - it's heavily based off Jotai/Recoil but with real cache management (inspired by React Query), fully controllable outside React.

- I think mobx can get really ugly with types. Out of the ones you listed, recoil/jotai are probably what I’d lean toward, although there’s a lot of local first sync libraries like replicache, aphrodite, etc that also do state management

- Honestly good old class components are still my favorite
  - My favorite thing about class components was the ability to subclass your own class that uses different methods with reactivity baked in. That's what we did at Notion. Composition of hooks is pretty great too though.
- I never subclassed much, but it is nice. My main problems with hooks are 1. inspectability / can be hard to follow what's going on 2. sneaky perf issues (easy to mess up, eg with useCallback, even with linters) 3. things that are easy with class components can be hard with hooks

- Proxy kind of seems like overkill here.

- mobx is fantastic and not too complex.
  - I do think in larger team settings you need to align on and enforce your own patterns for use though. 
  - It's pretty unopinionated about how you structure your state objects.

- mobx-state-tree
  - pros are patches, normalization with references, and zod-like schema validation
  - cons are types are buggy and performance overhead over mobx
# discuss
- ## 

- ## 

- ## 

- ## React-Redux Roadmap: version 8.x, React 18, and TypeScript
- https://github.com/reduxjs/react-redux/issues/1740
- most likely React-Redux v8 will:
  - Keep the exact same primary public APIs we have now ( `useSelector` and `connect` )
  - Update the internals to be built around `useMutableSource` as an integration layer to provide better compatibility with Concurrent rendering. (It's also possible that we could look at context-based approaches again if React finalizes a "context selectors" API and makes that available.)
