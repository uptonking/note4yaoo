---
title: thread-dev-state-management
tags: [dev, state, thread]
created: 2021-02-28T07:28:44.040Z
modified: 2021-02-28T07:29:07.622Z
---

# thread-dev-state-management

# repeat

- ## [The new wave of React state management | Hacker News_202207](https://news.ycombinator.com/item?id=31959289)

- ## Believe it or not, most my effort in @ReactJS global state libs is to _avoid_ selectors that are only required for render optimization. It just didn't feel a good abstraction.
- https://twitter.com/dai_shi/status/1428155847536873479
- for redux: reactive-react-redux, proxy-memoize
- for context: react-tracked, jotai
- for module state: react-hooks-global-state, valtio
- use-context-selector and zustand are out of this category.
- While, at the same time, I learned people like "selectors" abstraction very much.
- btw, react-tracked is not only for context, it provides an API for react-redux and zustand too.

- valtio/mobx/vue are based on proxies. 
- jotai is based on atoms, which is "just functions" like React.

- ## The motivation I develop global state libraries is to avoid selector interface that are only required for render optimization.
- https://twitter.com/dai_shi/status/1373607985033871363
  - It depends on object ref identity which is a hard concept for beginners.
  - This shows some comparison among use-context-selector, jotai and proxy-memoize.
  - #ReactTracked and #Valtio are not shown, but they have the same idea.
- selector can lead extra re-renders, even if num1 and num2 are not changed, because it creates a new object.
- (be careful with)Selectors. Relying on memoiztn for perf is more like an antipattern when comprd with reactiveness. 
  - On huge projcts it's always a pain to write perf rdx due to one of the related selectrs in relesct not maintaining referential equality and breaking memoisation

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

- ## Redux fundamentally has two problems that RTK can't solve (currently)
- https://twitter.com/DavidKPiano/status/1395541811402268677
  - Effects aren't declarative. Reducers may be pure, but effects are hidden in middleware and very much impure 
  - Global, atomic store isn't always the ideal architecture
- I think that's actually the point David's making: that global state has weaknesses, and that in many cases it _isn't_ the right tool for the job.
  - but that's not a problem with Redux itself. It's a specific tool.
- [Discussion: declarative side effects and data fetching approaches](https://github.com/reduxjs/redux-toolkit/issues/349)
- Wondering what is your opinion on something like Redux-Observables? We use it at work and i just don't see the point
  - Haven't used it too much to have an informed opinion, but overusing observables for state management leads to what I call "operator juggling", 
  - where you're just mixing various operators to get the desired result instead of clearly and explicitly specifying logic.

- ## Normalize your data model for writes, denormalize for reads. 
- https://twitter.com/gunnarmorling/status/1660569588608774145
  - All read models should be derived fully automatically from a single canonical write model; 
  - everything else will quickly turn into a maintenance nightmare with (not so) subtle data inconsistencies.
- A bit like CQRS, yes, but in a more general sense. E.g. you application shouldn't write to OLTP DB _and_ search index or DWH at once. I think Event Sourcing is an independent/orthogonal concern to that.
- But in some cases writing at once makes more sense for instance updating the materialized view of _search_index for critical updates such as immediately displaying the deleted flag true or false, as explained in this video
  - Definitely, there's a space for synchronously materialized views. If possible though, they should be derived from the write model ("source of truth"), rather then being "manually" updated by the application.
- Application writes to the database which is the source of the truth, so after successfully writing it can produce to kafka topic, just to avoid going through whole cycle of debezium->kafkastreams->sink connector->Elasticsearch. It'll shorten the path sinkConnector->Elasticsearch

- ## ref
- [RTK Query comparison](https://rtk-query-docs.netlify.app/introduction/comparison/)
- [React Query vs SWR vs Apollo vs RTK Query](https://react-query.tanstack.com/comparison)


# discuss
- ## 

- ## 

- ## 求问万推的各位大佬，现在有个codebase所有的state management都是基于MobX的，state change都是隐默的(cnt++, array.push等)，没有显式的dispatch/setState。
- https://twitter.com/hd_nvim/status/1712312915360190533
  - 希望要改成能兼容vanilla React，不用observer也能用，跪求推上大佬指个方向能怎么改 
  - MobX必须要搭配observer，对接入方有强依赖性。（是一个SDK产品，不能假设接入方的技术形态）
- 也许 immer 可以兼容这种可变的写法
- 后来怎么改的？
  - Observe 所有数据，callback 是force update

- https://twitter.com/hd_nvim/status/1712675288013021571
- 多多所有项目都是基于mobx的状态管理，有什么问题吗
  - 那估计你还没发觉代码里可能出现的问题
- 我们的项目都是线上跑了好多年的，应该不至于有啥大问题
  - 用mobx，list[0].count++ 在observer包裹的component里会重渲染。useMemo在这种情况下会产生stale data

- ## IMO some things cleanly map to state machines, but a lot don’t. 
- https://twitter.com/devongovett/status/1528013087470649345
  - A hybrid approach is probably best where you have a state machine for actual states (ie booleans), and keep the rest separate. Forcing everything into these massive config objects is a recipe for unreadable code.
  - State machines are a good tool, for states. For other things they have Redux level boilerplate (if not more). JS community tends to jump on new shiny things and apply them to everything. I would just urge a more measured approach. There are many ways of centralizing logic.
  - Every example I’ve seen of any sort of complexity has had a lot of boilerplate. I find these configs much harder to read and follow than “traditional” code. Again, I think it’s a good tool, but if it were me I’d avoid context and actions and keep those outside the state machine.

- I think the problem is that it's trying to model something that isn't really a state machine? To me, a state machine has defined states where it can be in one state at a time. A list of todos isn't really that, so trying to model it as one seems like a lot of overhead.
  - That's a good point. Sometimes I just fire up the stately editor to map things out and help me define the states and transitions. Sometimes it's just to share with designers/product owner to confirm we're on the same page. It doesn't always lead to me using a state machine.

- The config objects shouldn't be massive. You should have separate machines for separate concerns. The hybrid approach is a valid approach
  - The big advantage of keeping everything in one statechart is being able to target states directly in transitions (ie: minimize boilerplate by not needing more events).
  - Part of what irks me are not only the massive configs but deeply indented inline closures … in people's code who should know better. IFL Lucy must help both 🎖️ I love XState conceptually

- ## Writing a comparison article - Redux vs XState.
- https://twitter.com/mpocock1/status/1523967853430509572

- ## i made it(zustand) initially bc of problems that redux couldn't solve, after using redux for multiple years i started to dislike the opinionated nature. it's still flux which scales well.
- https://twitter.com/0xca0a/status/1495360284139139074
  - we have it running in a massive application (CAD) with hundreds of thousands of nested state nodes.
- Is it all just one Zustand instance or spread over multiple based on concern?
- one store, multiple factories that create fractions of state, + primed hook selectors: 
  - const foo = useDrawing(ID, drawing => drawing.foo)
  - const bar = usePlugin(ID, plugin => plugin.bar)
  - this way we have split up the state model into multiple concerns.
- What were the problems which Redux couldn't solve? 
  - the big one was that redux is context based for no apparent reason. the app provider it prescribes is useless in 99% of all cases. bc of this it cannot be used between renderers. state in react-dom can not pierce into canvas for instance.
  - opinions like these made it sour among other problems. zustand is redux, but closer to the non-react original and without opinions. if i wanted zustand to propagate via context i can make it so, but it doesn't prescribe any patterns.
  - zustand being @pmndrs also probably is the only state manager in react that holds complex games with ECS (Entity-Component-System) logic and state bound components with 120fps refresh rates. it gets stress tested in ways that go well beyond regular UI, but UI benefits.
- What makes it performant? Most state management trash memory in my experience. Especially if your web app/games have 100s/1000s of constantly changing objects
  - flux state has the benefit of being outside the component tree, it's javascript state, not react state. 
  - hence it can be used similar to react animation libs that go outside of react but that can still bind to objects or components.

- ## Mobx supports concurrent rendering too. But after playing around with valtio, I realized you did implement in your "simple code"  the most important feature of valtio and mobx - it won't rerender if the non-accessed field has changed
- https://twitter.com/terrysahaidak/status/1484881817752772610
  - This is the most important feature. It's that all the other state managers are missing. Also, without it I don't recommend using any of these state managers in react native where rerenders do matter a lot. This is why I don't recommend redux. At all. Never use it in React Native
- Totally agreed here. Actually, I started adding the feature for redux: https://github.com/dai-shi/reactive-react-redux and even created a PR for react-redux.
  - Now, I have React Tracked https://react-tracked.js.org which adds render optimization for any selector based hooks, like react-redux and zustand.

- ## Just released redux-in-worker v0.8.0, a library to run redux reducers and middleware in web workers
- https://twitter.com/dai_shi/status/1434840658292842500

- ## It's always "are you using finite state machines" but never "are you in a fine state"
- https://twitter.com/DavidKPiano/status/1434146478319091723
- Any day im not in a final state, im in a fine state

- ## Finally all done! [7GUIs](https://eugenkiss.github.io/7guis/) challenge for jotai
- https://twitter.com/dai_shi/status/1433804219828490241
  - Usually I define atoms and components in one file, but for this one, atoms.ts is a separate file.

- ## Developers are mostly fine with using finite states, but figuring out transitions between states is where they draw the line.
- https://twitter.com/DavidKPiano/status/1421951111641006080
- developers mostly don’t work with finite state

- ## Really interesting to see how Uber used statecharts (in Java) to model functional business logic and complex fulfillment flows
- https://twitter.com/DavidKPiano/status/1420166879985950728

- ## "Refactor away your useEffects with XState"
- https://twitter.com/mpocock1/status/1407983384509435907
  - Anyone experienced that wonderful feeling where you can chuck away a bunch of useEffects and model them as invoked services?
- TBF I quite like keeping the useEffect simple and letting the machine handle the event itself. If you must use a `useEffect` , at least with `XState` you don't have to put any logic in it

- ## PSA: react-query is Promise based - it doesn't care about network requests, status codes and the likes. 
- https://twitter.com/TkDodo/status/1407343307047452684
  - `Promise.resolve(5)` and `Promise.reject("oh noes")` will do just fine, especially for an issue reproduction
- Would you advise using promises for test mocks as well?

- ## what data do you keep in your store that was not loaded from a backend (and was not received from the URL)? I.e. data that "only" lives in your frontend store? 
- https://twitter.com/nilshartmann/status/1406851122195742720
- SelectedItem, selectedSection, selectedWhatever, step, form data that has frontend validations that need to be checked elsewhere, pristineness...
  - Heuristic: If it's data you'll need in 2 places, why finding an unrelated common ancestor to store it rather than a global state?
  - Some of these selectedX could be in the URL if they nicely map onto UI (ie if the user can define them as part of the link to share with a friend or bookmark).
- Auth data, user details, settings (theme & language), stuff like notification pop-ups, a bit read-only navigation state to access it outside of the JSX routes. Most data in this application is server-side though, so generally it's not a lot.
  - Always depends on the application, but most applications don't have a *lot* of global state. Also depends on architecture of course.
  - That said, it can even make sense to move some "kinda local" state up into the global store to just benefit from an opinionated dataflow, tooling like the devtools or pre-existing libraries like redux-persist. Very subjective and I haven't really found a 100% answer.
- I think more and more previously "classic" UI state is also moved to backend/URL/browser, so that users can for example restore all their settings/inputs etc. on browser reload or share with others
  - Yeah, especially as keeping client-side and server-side state during SSR is a bit of a pain
- Calculator data. Hold up, not the arithmetic ones. The ones with long forms where you play around with inputs and it gives you a result or a bunch of meaningful messages from an API call, like a tax calculation.
  - 类似本地输入框这样的临时数据
- For time-based views like an EPG, storing the current time there is a neat trick as it allows you to speed up things and move forward in time for testing purposes.
- Shared state between different parts of the application - for eg filters that apply throughout the application.
- Custom product configuration state. Color, size, make, model selections for example.  And many derivations of that data.

- ## zustand has a thing called transient updates.
- https://twitter.com/0xca0a/status/1406246841436487682
  - binds components to reactive state w/o causing re-render. you wouldn't want react running a complete component lifecycle 60 times a sec. i hope react figures this out natively one day, until then: zustand.
- In my state-designer lib, I have a “secretly” API (“secretlyTo” for transitions and “secretlyDo” for actions) that will update state without updating React. Great for these kinds of semi-stateful effects.
  - By semi-stateful, I mean depending on stateful information or part of a control flow that also includes stateful changes (eg. if command key is pressed, update position; otherwise, secretly update position)
- This is why I'm glad there are concurrent features instead of a concurrent mode now; 
  - IIRC external state doesn't play well with concurrency in React (useSubscription/useMutableSource de-opts), but it's such a common use-case that I wish it were first-class.

- ## A while back we tried putting together an "action listener callback middleware" for potential addition to RTK. 
- https://twitter.com/acemarke/status/1405695521944223747
  - Use case is "run code after an action", but meant to be lighter than sagas/observables.
  - The PR stalled, but we're still interested in feedback
  -  We'd like to add it, but want to make sure the API is good.
  - [yet another attempt at actionListenerMiddleware](https://github.com/reduxjs/redux-toolkit/pull/547)
- Is there really a meaningful benefit to having actions like "add/remove listener" show up in the DevTools? I've never been a fan of the idea of dispatching actions just to get a logging effect.

- ## Logux State is a tiny (159 bytes!) state manager inspired by @EffectorJS and Recoil, but was created to move logic from components into stores.
- https://twitter.com/logux_io/status/1395068017755705352
  - It can be used without Logux and supports Svelte, React, Vue.
- Logux Client 0.11 uses Logux State to create SyncMap stores, which hide CRDT Map logic inside the store.
- We will support Logux Redux and Logux Vuex for a while, but now the main use case of using Logux is to use CRDT stores build on top of Logux State.

- ## My favourite part of the XState API doesn't involve state machines - it's the invoked callback.
- https://twitter.com/mpocock1/status/1392947622038720517
  - They're concise, type-safe, and exceptionally flexible. If you aren't using them - seriously, try it.
- I wonder if XState is TOO flexible. Here you are describing use cases that I feel could be solved in 10 different ways, WITHIN the XState paradigm and I think figuring out what the right solution is, could be really fatiguing(令人精疲力竭的，令人身心交瘁的).
  - We should offer guides on use cases, example integrations... There is so much ground we can cover.
- Interesting. Why the double function call as the API? Instead of: `({ context, event, send, onReceive }) => { }` .
  - Because (context, event) => something is the general signature for an invoke creator
- "callback" is legacy node for Promise, which is the standard. Not that I like it, I would rather prefer a lazy promise like Fluture.

- ## What is the best way to continuously make requests on react?
- https://twitter.com/LauraViglioni/status/1391083143474647041
  - RJsX Observables?
  - For continuous I mean each n seconds I make an Axios request and update stuff on my page
- Pooling, useInterval or recursive setTimemout
  - Just make sure to wrap it in a hook that cancells it on unmount
- How about using a websocket? It scales better than doing a lot of requests.
- Easy to get get done with React query, checkout the polling/real time example on the docs

- ## I want to write about react-query and TypeScript next, but need some motivation: what do you find most confusing or are struggling with?
- https://twitter.com/TkDodo/status/1391384960918081542
- The best way to type your data once and have it get inferred all the way down. Is it in the fetcher implementation or manually supplied generics? Which is better for different use cases?
  - This is exactly the goal of the form state hooks I'm working on! Infer types from initial values when possible, carry that through to all usage. Pass type params to narrow where necessary.
- How would you incorporate data validation(types enforcement) for incoming data if you do that?

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
