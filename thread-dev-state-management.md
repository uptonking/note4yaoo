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

- ## what's the difference between @sveltejs store and context?
- https://twitter.com/lihautan/status/1385027049673269253
  - Store allow multiple components to share the same value, and get updated when the value changes
  - Context allow components under the same component tree to share the same value, where is the component placed decides the value the component gets
  - [Svelte Store: Store vs Context](https://www.youtube.com/watch?v=p4GmT0trCPE)
- so how should I decide when to use store, context, or both?
  - Here's the 2 dimensions you can think about:
  - static or dynamic - can the value be changed by the user?
  - global or local - is the value the same throughout the entire app, or depending on where the component is used?
  - use store - 💡 if the value needs to be dynamic
  - use context - 💡 if the value is local to where the component is used
- static + global
  - define the constant in a file
  - import the constant from anywhere
- static + local
  - define the constant in a context
  - depends on where it's used, the context value will be different
- dynamic + global
  - define the store 📦 in a file
  - import the store 📦 from anywhere
- dynamic + local
  - define the store 📦 in a context
  - depends on where it's used, the store 📦 from the context will be different

- ## ref
- [RTK Query comparison](https://rtk-query-docs.netlify.app/introduction/comparison/)
- [React Query vs SWR vs Apollo vs RTK Query](https://react-query.tanstack.com/comparison)

# pieces

- ## 

- ## XState is built to orchestrate side effects - but you can get lost if you don't know how to use the primitives.
- https://twitter.com/mpocock1/status/1388040079004864513
  - [XState: Should this be an action, or a service?](https://dev.to/mpocock1/xstate-should-this-be-an-action-or-a-service-2cp0)
- We’re approaching the limits of my Xstate knowledge now.
  - Say you needed that data that your fetch() returned, you would recommend putting any processing of that in an action fired onDone?
  - With the separation of implementation and logic with the actions, I’m always struck how annoying it is with services to have functions in my machine definition. No way around that?
  - You can give them names: `invoke: { src: 'getData' }` and define that in the options you pass to useMachine? If you want to define them locally.

- ## Announcing the alpha release of Lucy, a new DSL for finite state machines and statecharts that compiles to XState machines. 
- https://twitter.com/matthewcp/status/1386030120838877187
  - What CSS does for styling, Lucy aims to do for runtime logic.
- The object syntax used by xstate always tripped me up. This looks much nicer. 
  - Sorry about that! Ironically, one of the reasons that XState has an object syntax is to serve as a low-level output format for something exactly like Lucy.
  - it’s great to have something as a foundation for higher level tools (DSLs, visualizers, etc).
  - XState is CloudFormation, Lucy is CDK
  - XState Builder (when I finally finish it) is Pulumi, (different than the visual creator, which is like... Whimsical)

- ## I’m pretty proud of this level of commenting I did recently for a UI where you can drag and drop "layers", and one of them might be selected.
- https://twitter.com/erikras/status/1384440999200571392
  - This is an "assign" action in an #XState machine

- ## I wanted to write an article called "Why do we need state machines, anyway?" 
- https://twitter.com/DavidKPiano/status/1383096040065269764
  - but it can be summed up in a tweet:
  - State machines & statecharts provide a precise, visual, and universal "language" for describing all kinds of logic.
  - They let you move faster without breaking things.
- Ask 10 developers how they handle logic in their apps and you'll get 15 different answers.
- State machines help you answer "how does this app work?" without looking at 50 different click handlers and boolean variables scattered in random places

- ## You know, the world of enterprise SAAS react could really use a router that behaves similar to a state machine, 
- https://twitter.com/tannerlinsley/status/1382736036304867332
  - is strongly typed for known combinations of routes+searchParams, 
  - and first class search param support eg. default params, synchronously stateful, synchronized to URL
- I might not have state machines but I just released a package to control query params as regular state !
- Bespoke routers are bespoke. Would love to see names given to the various parts I could use to build up my router. For example maybe I use iframes and part of my pathname is actually controlled by the app inside the iframe and postMessage

- ## What GraphQL is for API's, XState is for application logic.
- https://twitter.com/mpocock1/status/1381980661209300992
  - What was previously random, arbitrary and diverse becomes predictable and introspectable.
- Everyone still doing CRUD with GraphQL is still killing basement rats in the tutorial area.

- ## Announcing XState Catalogue 0.1.0
- https://twitter.com/mpocock1/status/1379385435919646723
  - Take the guesswork out of modelling state. 
  - Bootstrap your application logic with professionally designed state machines.
  - https://github.com/mattpocock/xstate-catalogue
- XState Catalogue's next machines:
  - Payment checkout
  - Shopping cart
  - Video/audio playback controls
  - Websocket connection with retry logic
  - Role-based access
  - Web-based video call with controls (muting/unmuting)
  - Data grid
  - Advanced search area with pagination
- This might be one of the coolest oss projects I've seen in a while. Like a UI lib but for logic!

- ## For the last ~2 months I’ve been using Redux with a game engine, and for the last week with Preact. 
- https://twitter.com/orta/status/1378983491250106369
  - I’ve been constantly impressed by how thoroughly documented Redux is, and the useSelector API is absolutely stunning design. Great work.
  - I’m now reasonably convinced that a lot of the criticism I’ve seen of Redux comes from how people use it in their codebases vs instead of anything intrinsic to the abstraction.
- btw, you might be interested in the main discussion threads where we designed the React-Redux hooks API. Lot of technical constraints and design choices for something _seemingly_ simple!
  - [The History and Implementation of React-Redux](https://blog.isquaredsoftware.com/2018/11/react-redux-history-implementation/)
- I found it difficult to explore selectors in large code bases, as they are just global functions rather than getters that are listed by autocomplete.
  - We struggled with proper encapsulation, parametrized caches and polymorphism (for different kinds of dialogs provided by modules).
  - From my memory, we had performance problems with selectors that returned arrays which are passed as props to a react component, especially when these selectors depend on props of the react component.
  - We never had these kind of problems again with mobx.
- A lot of prior criticisms I had heard:
  - Hard to type
  - Verbose API
  - Forces all components to go through redux APIs
  - Doesn’t scale well
  - It’s likely that these all had some validity pre- react hooks, and pre redux-toolkit.  Coming in fresh today it’s worth re-evaluating

- ## I don't recommend any global state management now, 
- https://twitter.com/dogetoge/status/1377097524490641415
  - because there are too many state management libraries. They are all the same. 
  - With the development of react concurrent, we tend to build state management into the framework. 
  - React itself is also a state management, isn't it?
- It's funny that before React it wasn't a thing. 
  - Part of that because state wasn't respected enough, conflated with the Model in MVC, or the libraries were reactive in MVP with their own primitives. React created the space where we got this new tool.
  - Patterns like reducers, and state machines are all possible with provided primitives. 
  - Although until Context is performant enough to recommend in all cases this will not come to pass because React's state management is tied to the component system which has consequence.

- ## RTK Query vs React Query - which to use in what scenarios?
- https://www.reddit.com/r/reactjs/comments/mggpr7/rtk_query_vs_react_query_which_to_use_in_what/
- In general, the main reasons to use RTK Query are:
  - You already have a Redux app and you want to simplify your existing data fetching logic
  - You want to be able to use the Redux DevTools to see the history of changes to your state over time
  - You want to be able to integrate the RTK Query behavior with the rest of the Redux ecosystem
  - Your app logic needs to work outside of React

- ## Having a sudden deep temptation to rewrite my whole side project to strip out Redux and try out React Query and React Context. This would be a biggish undertaking.
- https://twitter.com/TkDodo/status/1348542727860989953
- I still really value a lot of the things that I originally liked about Redux - the fact that it encourages stateful thinking about your application and making its behavior deterministic.
  - But it does entail a lot of boilerplate overhead and being able to strip that out would be really satisfying.
- I haven't had the need to use context alongside of react-query. 
  - if you have some state left that is not server state _and_ truly needed everywhere (darkmode toggle is a classic example), context serves nicely.
  - But often, not many "complex" things are left that warrant useReducer
- if you like #redux but also appreciate the data fetching ideas that #ReactQuery offer - try out #ReduxToolKit with #RTK-Query

- ## Pardon my stupidity but what are your thoughts on running Redux in a separate thread/worker?
- https://twitter.com/agusterodin/status/1375569680300040193
- It's absolutely doable, and there's multiple articles that talk about it.
  - However, I don't see any benefit to doing so in almost all scenarios. 
  - Reducers are rarely a perf bottleneck - updating the UI is more expensive.
  - you should minimize main thread work, but DOM updates have to happen there, so in most cases the logic does too.
  - But realistically most apps probably aren't perf sensitive enough to where they would even have to consider that sort of thing.
- [Off-main-thread React Redux with Performance](https://blog.axlight.com/posts/off-main-thread-react-redux-with-performance/)

- ## Did you know that a reducer is like a single-state finite state machine (and vice versa)?
- https://twitter.com/erikras/status/1374381386476396563
- [A reducer is a single-state state machine](https://erikras.com/blog/reducer-single-state-machine)

- ## I don't like the proxy based update strategy, because it involves the magic of runtime and the fatal flaw of deconstruction. Coarse grained update is always good, whether it's block level or component level.
- https://twitter.com/dogetoge/status/1373828122269732866
- You don't need proxies to do fine-grained. It just makes the experience a bit smoother(other than destructuring). Use functions instead. You maintain explicitness, don't have destructuring issues, and get to keep performance too. Although I'd give up destructuring for proxies.
- Why give up destructuring? Proxies can do destructuring.
  - The deconstruction of Proxy is a value rather than a reference, which will lose its reactivity.

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
