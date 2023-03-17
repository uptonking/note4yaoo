---
title: lib-net-ajax-react-query-dev
tags: [ajax, lib, react-query]
created: 2020-08-06T10:23:53.305Z
modified: 2023-03-05T08:55:03.696Z
---

# lib-net-ajax-react-query-dev

# guide

- [用react-query解决你一半的状态管理问题](https://zhuanlan.zhihu.com/p/351280149)
  - 将服务端状态(缓存数据)从全局状态中独立出去
  - 使用通用的hook处理请求中间状态 isLoading, isError
  - 多余请求合并
  - 统一的缓存更新/失效策略
- [Use react-query but no react](https://github.com/tannerlinsley/react-query/discussions/790)
  - https://codesandbox.io/s/magical-bush-gbsk7
# discuss-stars
- ## 

- ## 

- ## I'm building a react-query-like library but for specifically tuple-database backends. 
- https://twitter.com/moonriseTK/status/1636536122711867393
  - Its super early, but I really like how I setup these tests. 
  - By using a deferred server, I can render the hook, make any assertions, respond to the request, then make any assertions afterward.
  - Building this for an app I'm working on. The real benefit is that you basically never have to refetch...by subscribing to the key, the server just tells you when to update. So the implementation becomes a lot simpler than something like react-query which is very generic.
- it seems similar to evolu.  crud to local firstly, then sync
  - Yeah very similar. I will have to dig into their implementation, i wonder if they do subscription or just refetch.

- ## React Context  is a lot closer to props than it is to state. To me, it's just prop drilling without having to write that code explicitly.
- https://twitter.com/TkDodo/status/1627586506402537473
- That's why it's okay to put data from React Query into context. It's not state syncing. It happens synchronously. The single source of truth remains the Query Cache.
  - It's the same as doing: `<Comp data={data} />` a bunch of times (data coming from useQuery)
- It has the same trade-offs as explicit prop passing compared to calling useQuery again in a deep child:
  - no fine grained subscriptions (select). probably irrelevant for most apps.
  - no refetches on mount events (there is none)
  - component becomes "coupled" to parents
- It also has the same advantages:
  - data cannot be undefined if you've checked for loading / error up top (yay, no ?. needed)
  - no additional observer created (has a non-zero cost). probably irrelevant for most apps.
  - "easier" to test
- Truth to be told.. Loved this thought...context api ia just solving the dependency management problem, but not the state management problem...
  - Absolutely. I wanted to phrase it without "dependency" and "injection"

- ## While I could probably refactor #ReactQuery to use middleware too and get the meat-and-potatoes bundle down to around where SWR is, it would ultimately require users to add a bunch of middleware to get it back to today's 100% functionality, bringing it right back up where it is 
- https://twitter.com/tannerlinsley/status/1433154450600853505
  - Would it be worth it? Meh.
  - To be clear. We are not doing this.
- Where can I see what middleware are for libs like react query (without having to learn and write swr)? The only middleware I know are from redux or from server side (express, fastapi)
  - Middleware usually just describes a user defined function that wraps the original functionality of the caller.
- very interested to see a smaller react query, but the effort can be too much indeed 🥲
  - i think what i'd like to see is more alternatives flourishing, it gives more control over size vs feature set.
- Glad that you're now thinking of it this way. 
  - There're things that SWR *can* have, but we've decided not to add aggressively (just like your opinion on middleware). 
  - To be clear: supporting middleware doesn't mean SWR will "shift a lot of core features into the user's hands".

- ## React 18 and the future of async data
- https://swizec.com/blog/react-18-and-the-future-of-async-data/
- React 18 is shipping with `<Suspense>` and `startTransition` for deferred component rendering, but not data loading. 
  - To explore that future, I built a side-by-side comparison of current best practice – React Query – and future `<Suspense>` for data fetching.
- The demo shows a New York Times best seller list.
  - Its name and publication date come from an API call. 
  - The list of books comes from another API call. 
  - You get a cascading spinner effect. Need data from the first call to make the second.
- Suspense coordinates those loading states for you and shows 1 spinner. Nothing renders until everything's ready.
  - But the true benefit is how Suspense simplifies your code.
- Look at the WithoutSuspense branch of my demo. 
  - First you have the low-level data loading. An async helper that calls the fetch() method to load data from an API.
  -  You await the fetch(), then you await the json() parsing, then you return the result or throw an error.
  - Second you have a helper hook that loads your data. You should use React Query or similar for this part.
  - **To avoid re-fetching the same data for every component, libraries like React Query and ApolloGraphQL use an internal global cache**. The shared cache leads to ridiculously snappy UI.
  - Third you have to handle loading states everywhere.
- · turns async states into first-class citizens of React. You don't have to think about it. 
  - You'll need React 18.x and a suspense-enabled library like `react-fetch` . The library would rely on suspense `<Cache>` internally.
  - Any component inside `<Suspense>` can say "Halt! Don't render me yet". React waits until every "halt" is resolved to render the children.
  - While components resolve, React shows the fallback.

# discuss
- React Query is for managing server state, not client-only application state. 
  - For that, feel free to keep using redux or react context.

- about GraphQL
  - A lot of apps are not as graph-like as we imagine
  - Deep querying/transport is handy, but not worth the savings unless you have massive amounts of relationships or truly need deeply relational querying clientside.
  - If that's the case, and waterfall-querying/transport-size becomes a problem, you can easily add relationships and field-masking to a REST api (eg. JSON schema, pre-GQL api, custom) or finally implement GQL (I wager this would never happen for a lot of apps)
  - The benefits of GraphQL are often thought of as native to GQL itself, but most of the benefit felt comes from libraries like Apollo and Relay. I'm more of a believer in these libs (and their architecture) than I am in GQL.
  - Subscriptions in GQL seem to be pretty wild-west still, and fall on the user (or a lib) to implement however they want. Some libs implement them very well, some don't. They also raised questions in me about what exactly subscriptions should be transporting (queries vs events)
  - This is what initially inspired me to build React Query. I loved these tools, but ultimately we didn't go with GQL. I found that the great experience I associated with Apollo and missed had more to do with its opinions and architecture than GQL.
  - https://twitter.com/tannerlinsley/status/1211749083863384064

- move to react-query
  1. Stop trying to cache your #react server state in {globalStateLibrary}.
  2. Move it all to React Query
  3. Realize your "global state" is now TINY.
  4. Stop using {overPrescribedGlobalStateLibrary} for that TINY state and just use useState/Reducer/Machine + Context.
- Stop using “global state” tools for Server State! 
  - Queries
  - Prefetching 
  - Caching
  - Optimistic Mutations
  - Background Fetching
  - Paginated/Infinite Queries

- So how does react-query solve the issue of global state?
  - It solves it by making you /not need one at all/. 
  - Rather than keep the data in some "store", which is a representation of data from the server anyway...
  - Just keep a cache of the query's response.

- I saw a PR of yours explaining how you're not planning support websockets in RQ.
  - Well, it's not about "support". 
  - It's about integration, which is already there. 
  - You can set up sockets however you'd like (I use pusher, usually), then send events to users to "invalidate" queries on the front-end. 
  - This cuts down on message size and also let's the client be smart
  - Bottom line is that if data is async, I'm storing it in React Query. 
  - My recommendation for CRUD like apps that use sockets is to not transfer objects in the payload, only events. If you have a truly real-time app like chat/game, totally different.
  - So for an app that needs real-time data, I guess the solution could be a custom hook that handles websocket events and invalidates RQ to store the most updated data in cache

- Looking at @tannerlinsley's react-query, it seems nice and useful as well as @zeithq's swr. But, they are both Hooks-oriented. 
  - My journey is to find and create a new Suspense-first API. 
  - react-suspense-fetch is a primitive library and react-suspense-router is built with it.
  - Could there be a non-router based API? How does it look like? That's my recent question.
  - Also, although react-suspense-router is for Render-as-You-Fetch, initial data fetching is Fetch-on-Render. Can it be Fetch-Then-Render? I 
  - Data fetching hooks and suspense oriented apis are definitely not mutually exclusive. Id say they are more related and synergistic than anything. The only missing piece is performing rollled-up prefetching automatically based on route which you’ll def see in the coming months.
  - react-suspense-fetch: 
    - it's still a fetch-as-you-render paradigm, it all just comes down to the mechanisms for discovering the data a route needs. 
    - In this case, you use a separate route.data import which is cool.
    - However, it's still highly opinionated and relies on an up-front routing config being declared and knowable before rendering into a routes component. I can't think of any other ways to do this yet though, so we'll see what happens there.
    - Thanks for the comment! Yeah, this router-base approach requires route config defined in advance. That's something I'd like to tackle. No idea yet. It won't look like ordinary hook based APIs. Not even sure if such APIs are acceptable to developers. Hope to come up with something
    - https://twitter.com/dai_shi/status/1234815419208200194

- React Query Research question. If you have a `useQuery` instance rendered on the page, and you render another identical `useQuery` instance on the page, would you expect the second instance mounting to trigger a backround refetch? Or just subscribe?
  - https://twitter.com/tannerlinsley/status/1232703154854256640

- Is the approach of React Query to forgo(放弃) a global state and instead have local states for each component and its children?
  - Not quite. React Query has its own global state internally that is built specifically for handling async resources and handling their caching/defining/invalidation/refetching lifecycles. You use it in your components much like you would local state, but much better for async data
  - I also want to investigate if useMutableSource could make things better for react-query as well.
  - It would probably improve some performance. Right now it just uses a pub sub setstate pattern.

- Lots of what we call "Application State" is actually just a client-side cache of server state. 
  - And just with any cache, invalidation is a hard problem.
  - Interestingly, I don't think many apps really consider this, but it's pretty important.
  - For example, when a user updates some data, most apps I've seen (and built) will make a request to make the update, and when it's successful, they update the state (client-side cache) as well. Sometimes the order is switched in optimistic UIs.
  - In either case, how do you know that the rest of the data you have in your cache is still current? 
  - Maybe another user changed data in another entity (or even a different property of the same entity).
  - In your app, if the application state on the server got updated, how long would it take for the client to have those changes reflected in the UI?
  - (Let's exclude your app's chat feature for this. I'm asking about regular resources here.)
    - on browser refresh
    - on navigation
    - on polling interval
    - other
  - This is why I'm increasingly interested in simpler libraries like react-query which simply invalidate entire queries and rerequest everything on mutations (and even when the user refocuses the app) rather than libraries like Apollo which try to stitch together state changes.
  - It's all trade-offs (consistency/correctness vs resource management). 
  - But I think more apps could be made simpler and provide a better user experience by favoring correctness.
  - https://twitter.com/kentcdodds/status/1228727040238473216

- All apps have two types of state: UI State and Server Cache. 
  - Put all your server cache in react-query 
  - and the rest of your state is pretty simply managed within React state/context.

- Do you have any guidance on how to integrate with websockets for realtime updates? 
  - If you are pushing the entire payload, you can use the `queryCache.setQueryData` to update the entity anywhere it is used in your cache. 
  - If you are pushing notifications (my recommended approach), you use those to trigger refetches for queries that use the entity.
  - IMO unless you are 100% sure that the client needs an asset immediately, then pushing an entire payload to the browser produces a lot of waste. 
  - With a notification and refetch, you ensure that only queries that are in use (or at least recently used) get updated.

- If I throw a new error in the root of the query function, it will get stuck on "status: loading".
  - If I return the error, the status will be "success", and the error object will become the data.
  - Right, because:
  - 1 - By default, react-query will retry a query by default 3 times before actually failing and going into the status === 'error' state.
  - 2. - When you catch an error, the outer function is no longer in a throwing state. A return === success. You should rethrow

- How does it replace redux state management?
  - It replaces the management of *server state/cache*. 
  - So if you are like a majority of app developers, a vast majority of your "global state" is server cache. 
  - Once you put that into React Query, what you're left with is usually a tiny bit of app state that you can manage via React

 

- RQ handles your server state and what’s left is usually a small bit of auth and actual UI state, both of which require nothing more than useState/Reducer + context. 
  - There are use cases for Recoil and Redux, but they are the exception, not the norm like everyone’s been taught.

- If you have a slow render, memoize the computation inside of that component.
  - If you still have issues, then split your state/dispatch, then split contexts. 
  - You can go soooo far with just React. 
  - There are so very few (real) cases where I would ever suggest using Recoil or Redux.
  - Even without memoization, this is still fast as long as your renders are fast. 
  - I can rerender every component in a react chart instance with a single context at near 60 FPS. 
  - Unnecessary renders are only a problem if you’re writing slow components or rendering 10000’s at once.

- I feel like I need to clarify something that seems to be going around.
  - SWR did not inspire React Query. 
  - RQ was born long before SWR was publicly release or known of.
  - What is more accurate is that they had similar release dates & have influenced each other in positive ways.
  - Competition is good.
- App state is really not that big. Theme, UI state like a sidebar being open. 
  - Then there’s routing state. 
  - Still all dwarfed usually by server state.
- So, there are no actions with React Query. It's all subscription based. So 99% of the time, if you move data fetching from Redux to React Query, you'll end up deleting ALL of your reducers, actions, selectors, etc for that data.
- I feel like the whole idea of presentational vs container components has fallen by the wayside with hooks. 
  - In the project I work on people just embedding logic and data into any components with hooks.
  - This is a shame, this separation of concerns works so well.
  - For me, "containers" simply got split up. Some stayed as "routes", most became custom hooks. I think the part that people may still be missing is the "custom hooks" part. It's dead simple to do.
  - I didn't like having a container for every single component, now what I do is have a "PageComponent" that has a custom hook - this is entry point and contains all the stateful logic.
  - All of the components below this tree are presentational
- Having a client for your API is great and IMO suggested. 
  - It's a great "separation of concern". 
  - React Query for instance, isn't concerned with *how or where* you get your data from, only that you get it.
  - Think of it this way, a client could be the best place for authentication, type origination, deserialization, REST/GraphQL DSL
  - And in parallel React Query handles caching, timing, stale data lifecycle, garbage collection, invalidation, etc.

- do you have a folder structure with #ReactQuery in mind? or if you can point me to a project that's using it that would be helpful.
  - I just create a custom hook for each query and put it in the hooks directory. Eg. hooks/usePosts.js
  - Does your custom usePost hook also contain mutational functions such as createPost and updatePost? If so, do you return multiple states for the different mutation and query from the same hook?
  - Nope. Those are different hooks. usePost.js, useCreatePost.js, etc.
  - I create a custom hooks for each query and mutations, like Tanner, but I put queries and mutations in two different subfolders, as for a big project you could easily have 50+ of this hooks. So apiHooks/queries and apiHooks/mutations.

- [talk about React Suspense and data fetching](https://twitter.com/tannerlinsley/status/1281143594544328707)
  - Lots of talk about React suspense today. I’m very excited about it.
  - However, I feel like the patterns I’ve seen in #ReactQuery (and friends like SWR) have alone been more transformative for my own dev process and users and have even prepped me for suspense in a lot of ways.
  - The biggest thing that suspense is going to do for me is just one thing: avoiding that flash of loading/placeholder for newly mounted components. Suspense doesn’t fetch, it doesn’t codesplit, it doesn’t preload for you and it doesn’t cache for you.
  - It’s really only about smoothing out the experience of moving from state to state without seeing a loading placeholder. And I am all for it! I hate those loading flashes. 
  - But if I’m being honest, I think caching and prefetching are WAY more important than that UX quirk.
  - The fact that suspense will depend on data loading, prefetching, caching, etc to be used to its fullest potential is the most curious piece of it all. We’re all waiting for suspense to happen. It will. 
  - But then what? At that point everyone will be reaching for three things:
    1. Automatic code and data splitting.
    2. The ability to prefetch that code and data in a reliable way.
    3. Data caching layer.
  - I’m working from the bottom up with #ReactQuery. And already getting so many benefits without even thinking about suspense or code splitting. 
  - I’m also using Next.js from the top down to take care of as much code/data splitting and prefetching when I need it.
  - If it’s that important, prefetch it earlier! Don’t need suspense for that.
  - You don’t need anything more than we have already to start caching, prefetching, code/data splitting, etc.
- When we say “Suspense for data fetching” we don’t mean “the Suspense component”. 
  - That’s been done over a year ago. We mean an integrated and flexible solution that lets you write code in that paradigm.
  - This solution includes: a way to read data anywhere in the tree, a consistency guarantee (if parent and child both read some data for new ID, you don’t show old+new mixed up), a cache layer to avoid waterfalls, an invalidation strategy, plus a code splitting integration.
  - You can’t implement parent/child consistency well without Suspense. `<Parent id>` and `<Child id>` read different data by id and id prop changes. If your solution shows a mix of old and new data while both are refetching, that’s the problem Suspense *as a paradigm* solves.
  - But Suspense as a paradigm also introduces new problems *because* it solves consistency (without consistency you can ignore them). Such as — if you were looking at something, and now it’s refetching, sometimes it’s bad to replace already fetched content back with a big spinner.
  - Now this isn’t some minor UX thing. This is a pretty major expectation for a user that the content they’re looking at doesn’t suddenly disappear. Like if you paginate with “load more” you don’t want existing items to go away.
  - This is why “declarative and consistent loading states” were not attempted before. You get the “blowing content away” problem and you can’t solve it without framework-level support. Concurrent Mode is a solution to that problem. Because it can render next screen “in memory”.
  - So I think stating spinners are a “minor thing” is misleading. If you have declarative loading states and also solve consistency then spinners become a major problem. That’s why we don’t recommend people to use Suspense for data fetching in stable releases. Without CM it sucks.
  - Now if we talk about Suspense+CM then it already works. Relay Hooks works and the whole new website is built on that. People can try. But not everyone is happy with Relay as a solution. So the remaining part is a cache implementation that doesn’t encourage waterfalls.
  - The waterfall problem is interesting. It’s a direct consequence of (1) wanting colocation and (2) wanting consistency. If Parent and Child must be consistent, Child can’t render until Parent is ready — means we don’t know there’s a nested request. This is very slow at scale.
  - Yes, you can get around it by manual prefetching. That also doesn’t scale. It works for a small app but it doesn’t work for hundreds or thousands of components, each of which may want to read some data. If we don’t solve that scale, it doesn’t count.
  - Relay has a scalable solution. It avoids waterfalls automatically by composing queries at compile time. So the root query always “knows” what children are going to want before their code even loads. But Relay isn’t for everyone. So we want to build a more generic version.
  - The easiest way to avoid client waterfalls is to move them to the server. Low latency. This is conceptually exactly what GraphQL does, but you don’t need GraphQL for that. It’s just a single server endpoint behind which may several different APIs for different components.
  - That also gives you ability to code-split based on *data*. Why load LogedOffNavbar if user is logged in? Why load GifCommentImage when the comment did not include a GIF?
  - If you centralize data fetching on the server then its response can include *code* chunks. Code is data.
  - I just found the framing a little misleading (“Suspense is just declarative loading states”). It’s more that it’s everything else that makes this possible without big sacrifices.
  - I’d also say that consistency between async data in the tree that’s requested by different components is vastly underappreciated. That’s the core new benefit of that paradigm but people miss it largely because not much else (except Relay) offers anyting similar today.
  - By visual consistency I mean that you shouldn’t ever have a situation where A display data from oldId but B displays data from newId. Or the other way around. They should always be consistent with each other as siblings, just like React guarantees for synchronous rendering.
  - In this situation, you are correct. **React Query would potentially show old/new data mixed, depending on raced conditions.**
  - Now imagine hundreds of components. Each doing its own data fetching requirements without coordinating with others at every level. Inconsistencies at that scale would lead to very jumpy UI and crashes from mistaken assumptions (eg some prop from parent didn’t match child’s data).
  - I just wanted to be clear *that’s* the problem we are working to solve. On that scale, consistency isn’t nice-to-have but it’s table stakes. Everything breaks down without it.
  - ReactQuery is doing the best it can do but React needs to empower it to be able to do more.
  - I just want the “suspense is a thing to not show a spinner” meme to die a little bit. That’s not really what it is.
  - Which, to be fair, is our fault for introducing it this way! Spinners seemed like a catchy way to describe it but it’s **more about read data anywhere without screwing(弄坏，弄乱) up the UI**.
  - **How many apps don't need anything more than route-level data fetching**?
    - The latest @ReactPodcast about  @remix_run basically came to this conclusion. 
    - But then the "route-y" boys think everything is about routes. (and they're right)
  - But for the ones that do need more and run into the waterfall requests, do you envision most if not all of those apps jumping for Suspense for Data + CM when it's released? Like... is the pain that bad? Clearly it was for FB. But what does your research say for everyone else?
  - Sure! A lot of those apps might not even benefit from React itself much. I think overall `Promise.all` is a good indicator.
  - It’s not an unavoidable problem. When you run into it you hoist data fetching up. That ends up not being efficient (not the whole child tree has to wait for all data) but hey, it works. There’s a reason people `Promise.all` over the place.
  - How many React apps have Promise.all?
  - I mean the kinds of apps that fetch all data at route level could often be better written with a Rails-like model. Just a regular old style web app! This is something we also want to make easier to do using React in the future.
  - As I said earlier, the only thing I wanted to clarify is that Suspense is not a thing to avoid “spinners” but something different.

- do you use react query as your source of truth for state or do you hold state in react or elsewhere as well?
  - For 99% of async and server state, React Query is the source of truth. 
  - For anything that truly lives on the client or "app state", I have a tiny useReducer + context.

- 1. Cache space is negligible in most apps. If you are running into cache size issues, you're probably holding on to things too long or not garbage collecting unused cache. A big tradeoff for something that rarely is an issue.
- 2. You can do this with RQ, it's just not automatic, and for good reason. Its often that index/list calls for assets only show a part or summary of the entity, and your single crud calls will show all of it. I realize that this one of the things that fragments are for in GQL.  
  - but at the end of the day, is it really that difficult to just invalidate your queries? Active stuff on the screen refetches (would happen on a refresh anyway) and anything unused would get refetched on next use. Again, a harsh tradeoff with a lot of edge cases IMO
- 3. Bandwidth does have some shallow concern with refetching all the things all the time, but then again, what if your users were to refresh the page? At that point, you would be in the same position needing to refetch all the things anyway. At the end of the day, the tradeoffs just don't seem worth it to me. Even after using Apollo and building my own Redux powered normalized cache, it was all so much work for such tiny and often underutilized ROI.
- There's also a plethora of interesting situations that normalization puts you in. My favorite is when a mutation on a single object inherently changes its position in a list that was generated server-side. You don't know that order, so you can't perform the normalized update.
- To know that order, you would have to know all that the server knows... and that right there is enough to sell me on never using a normalized store for async assets again.
- In most applications, React Query would replace Redux anywhere that you are fetching data from a server (async state). So anywhere you're traditionally using redux-thunk or redux-saga, you'll just use React Query.  For other state that isn't asynchronous, you can keep using redux

- Do you know what the “builder pattern” is when referring to Typescript Types?
  - I think the name is leading people in the wrong direction. It’s more about using function chaining like `registerPlugin(plugin).registerPlugin(...).registerPlugin(...)` to build up complex generics where arrays and reducers are limited.

```JS
can(2020)
  .beTheYear()
  .thatWeStop()
  .making(apis && libraries)
  .thatLookLike(this)?.please;
```

- (or am I the only one who doesn't like overused builder patterns?)  
  - For as much as we talk about making libraries and JS bundle sizes smaller, a lot of you sure love this un-tree-shakeable pattern.
  - I dislike it a lot too! But then I also dislike the "config object" pattern because you can't minify the keys 😳
  - Curious if there's an alternative xstate API that wouldn't force to give unminifiable names to states themselves. Understand if it's not a priority (I guess prod introspection is useful). But I wonder if other takes on this that use plain variables (for minification) exist.
  - I was a little cheeky, just pointing out the difficulty of visually parsing inside-out: `uppercase(toString(add(mult(2, 3))))`
  Versus left-to-right:
 `mult().add().toString().uppercase`

  - The pipe operator is one way to get the readability, without the builder pattern (fluent api).
  - When working with a team, I prefer this:

```js
const multipledNum = mult(2, 3);
const addedNum = add(multipliedNum, 42);
const stringAddedNum = upperCase(toString(addedNum));
```

  - Clarity > conciseness (plus this minifies well enough)
  - Also, I don't hate the builder pattern/fluent interfaces completely, I just think they're sometimes overused when more idiomatic alternatives can be used.
# survey: how to fetch data
- [What do you use to fetch data in your web app?](https://twitter.com/kentcdodds/status/1243657342278758401)
  - fetch/axios/other
# survey: where to put app state
- [Where does a majority of your app state truly live? Where is its source of truth? ](https://twitter.com/tannerlinsley/status/1282810546270597121)
  - in memory
  - session storage
  - local storage
  - indexeddb
  - server-side/db
  - url queries
  - in the dom
  - I think what’s actually insightful here is that that not all state is created equal. 
  - The rate of access, modification, scope, persistence, etc is very fluid depending on needs and might even change over time, but also determines the tools you use to consume it.
# comparison
- [react-query vs swr vs apollo-client](https://react-query.tanstack.com/docs/comparison)
