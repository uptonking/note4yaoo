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

- ## 🆚️ [Why use Redux over Facebook Flux? - Stack Overflow](https://stackoverflow.com/questions/32461229/why-use-redux-over-facebook-flux)
- Redux is not that different from Flux. Overall it has same architecture, but Redux is able to cut some complexity corners by using functional composition where Flux uses callback registration.
- Flux makes it unnatural to reuse functionality across stores. 
- People have been rendering on the server fine with Flux
  - In traditional Flux, stores are singletons. This means it's hard to separate the data for different requests on the server. Not impossible, but hard. 
  - This is why most Flux libraries (as well as the new Flux Utils) now suggest you use classes instead of singletons, so you can instantiate stores per request.
- Redux just goes further: there's just a single store, and you can read its current state, or create a new store with a new state. Each request gets a separate store instance. Read more about server rendering with Redux.

- ## 🤔 [Redux - multiple stores, why not? - Stack Overflow](https://stackoverflow.com/questions/33619775/redux-multiple-stores-why-not)
- 单个store 容易维护，修改，读取。
- 单个store 易于 rollback 或 undo
- 单个store 容易一次更新全部, 数据是共享的，flux 的多个store, 当store A 依赖store B, 就需要waitFor()

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

- ## 🚀 [Introduction to Facebook's Flux architecture | Hacker News_201502](https://news.ycombinator.com/item?id=9095023)
- Everytime I see the Flux architecture I wonder what does it bring to the table that a reactive programming library like RxJS or Bacon.js don't? It seems Flux is just hacking together well-defined concepts in these libraries.
  * Stores could use Observables instead of EventEmitter
  * Components become Observers by subscribing to Observables which is extremely similar to setting up Listeners.
  * Instead of Actions through a Dispatcher, Actions become Proxies (or Subjects in RxJS terms or Buses in Bacon.js terms) that Stores subscribe to and Components push to.
- The dispatcher really is just a simple pub/sub mechanism.
  - The thing that Flux helps define is how to manage data. We don't have models, but it gives you a coarse structure for your data, with which you can do stuff like data dependencies (derived data), only rerendering part of your UI when parts of your data changes, etc.
  - How events are used within all of this could certainly be re-purposed with Rx (I've repurposed it as channels myself). You are not wrong, but flux is a bit more formalized with a few more things.

- Is there a way to get rid of flux boilerplate? I don't want to write three different files (a file with actions, another file with constants, and the actual store).
  - Sure - just use what you want. Outside of the dispatcher, flux is mostly a design specification for clientside information flow. Actions, stores, etc aren't native to flux - they're just approaches for accomplishing the desired information flow. Check out the examples closer - they aren't react classes.
  - That said, my personal opinion: the deeper you get into a big project the more you'll see the incredible value of the approach. The breakeven between the overhead of learning the approach vs the productivity 
  - With a lot of software, the more I get deeply into a project the more I feel I'm battling the artificial constraints of the tools I'm using. Flux is exactly the opposite. The deeper I get in, the more I feel it's working for me (and I'm not even using their dispatcher - since I had written my own initially before flux came out

- Reflux is a Flux library without the dispatcher boilerplate.

- alt is very small and removes boilerplate, but still isomorphic.

- So... a global message bus? That will quickly become spaghetti in a large code base.
  - The whole point of it is to eliminate spaghetti code. Traditional large frontend apps often end up with very complex chains of information dependency and it can become unclear as to what changing a piece of code will affect. 
  - Flux tries to prevent this by enforcing a uni-directional data flow, meaning working out what a certain component affects/is affected by is much simpler.

- Don't people realize that returning HTML instead of JSON will solve their problem for 80% of the use cases?
  - However, returning html fragments isn't the solution for all use cases. Consider native apps for Android/iOS/OSX/Windows. They will need data to be delivered via an API. 
- HTML fragments are a (very) poor solution to real time websites. Applications that use streaming data sets tend to use the data for more than just presentation
  - Even if the client doesn't need the data, HTML fragments suck for practicality.
  - Even if you solve the problem of consistency and applying fragments to the DOM, chances are you will be left with performance problems. You will need to batch updates to control repaints.

- ## [Facebook Flux – Application Architecture for Building User Interfaces | Hacker News_201407](https://news.ycombinator.com/item?id=8097776)
- looking at Flux libs like Fluxxor and it seems overly and unnecessarily complicated to me. Why is it so complex?
  - Seems like actions were designed to encapsulate update logic that doesn't belong in the store (e.g. update ordering when multiple stores are involved). A pubsub event queue wouldn't make this very easy.

- This looks very interesting, and if I'm not mistaken, slightly reminiscent of how apps are built with Om (using core.async for dispatch and atoms for storage).

- ## [Flux Application Architecture | Hacker News_201405](https://news.ycombinator.com/item?id=7719957)
- I really like this architecture - it's clearly based on lessons learned from the same types of pains that I myself encountered w/ non-trivial jQuery, and the unidirectional data flow makes it a lot easier to reason about the code. It's very similar to what I'm doing with my own micro mvc framework Mithril

# discuss
- ## 

- ## 

- ## 

- ## [Application Architecture with React: Rethinking Flux | Hacker News_201509](https://news.ycombinator.com/item?id=10213905)
- With each next article about React (and more generally javascript) it's more apparent that the final result is a mongo/rethink like db in the front-end with a transparent sync to the server
  - Maybe something like PouchDB, lazily synced with a CouchDB instance on the server ? I'd love to see a better integration, where for example global state would be automatically saved in PouchDB. You'd get pub/sub, history and synchronization for free, at the cost of PouchDB's performance

- If you're going to borrow every idea from ClojureScript and Om, why not simply switch to these technologies instead of relying on so many libraries?
  - Many companies will simply not use ClojureScript, it's too niche and too hard to find developers for at the moment. It's much easier to find JavaScript developers.

- I feel like every new architecture for flux lately comes at the cost of a lot of code complexity. The global state is becoming extremely common too, and it feels like a big anti-pattern. Not really a fan. I do like the more pure-flux Alt at the moment. I felt quickly put off from Redux after going through docs for a while.
- Only the states that can be global need to be global. It's not an anti pattern to manage state inside the component.
- 👉🏻 databases are global state (The design pattern here is separation of code from state. OOP couples code (methods) and state (members))

- ## [UIs are not pure functions of the model (2018) | Hacker News_202207](https://news.ycombinator.com/item?id=31979347)

- ## [Xilem: An Architecture for UI in Rust | Hacker News_202205](https://news.ycombinator.com/item?id=31297550)
- I think the Redux pattern is similar enough to Elm that I didn't feel a need to make a finer distinction.
- Elm also predates both Redux and Flux, even being referenced in Redux's Prior Art page
- redux architecture is just a global scan(). more or less what the elm architecture is as well.

- ## [the whole React-Redux boilerplate mess... is the the result of an entire generation of code monkeys and job seekers who didn't design their technology stack with any real engineering consideration | Hacker News_202002](https://news.ycombinator.com/item?id=22264381)
- Redux was a simple and elegant implementation of the unidirectional data flow (aka the Flux pattern). 
  - It came out during the time when the state of the art was Angular 1.x (aka AngularJS)'s two-way data binding, requiring a lot of dirty checking. 
  - Redux might or might not (the story is moot) have been influenced by Elm, which has exactly the same concept of actions, state modifications in response to actions, and re-renders in response to state modifications; all as pure functions; and Elm developers are finding this approach enjoyable and predictable. 
  - But even Elm aside, the pattern that redux is using, i.e. communicating via messages (actions) and subscribing to state changes in connected components, is a variation on the age-old, battle-tested event sourcing and pub/sub. 
  - What's so bad about that?

- ## [How to optimize React applications that use Redux | Hacker News_201707](https://news.ycombinator.com/item?id=14706430)
- This doesn't really explain why it has to be that way. I'm not really a fan of "it is because it is" design. It doesn't seem like there's any particular reason that a state reconstruction algorithm needs to be more expensive than O(1). What kind of advantages does this design have that an append store wouldn't give?
  - Redux was built as an implementation of the Flux Architecture. In Flux, you have different "stores" for different types of data (such as a UsersStore, PostsStore, and CommentsStore). One of the key concepts of Redux is that instead of having separate stores for each type of data, you can have separate "reducer functions" that are responsible for initializing and updating those data sets, and write another function that combines all of them together into a single object state tree. 
  - So, the standard encouraged approach is that the root reducer function delegates the work of updating each "slice" in the state tree to smaller functions, and so on ad infinitum. That way, each individual slice reducer function can be written and understood in isolation.

- ## [A Farewell to FRP | Hacker News_201605](https://news.ycombinator.com/item?id=11667523)
- When ELM came along with its signals, im like, meh, why not Rx?
  - Just like when Flux "came out". They just rebranded Event Sourcing in the client UI.
