---
title: lib-fwk-tanstack-community
tags: [community, frontend, router, tanstack]
created: 2025-12-16T06:24:30.759Z
modified: 2025-12-16T06:25:32.663Z
---

# lib-fwk-tanstack-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## Is it a good idea to use @tan_stack -store instead of zustand? Will it continue to grow or will be mostly internal library?
- https://x.com/costiniuc00/status/2005194808680497302
- Not only will it continue to grow, but we're actively working on a huge set of improvements with a name you're familiar with
  - TanStack Store is already an implementation of signals

# discuss-news
- ## 

- ## 

- ## 

- ## 
# discuss-tanstack-start/ssr
- ## 

- ## 

- ## why tanstack start made the default in cli? I can't create a bare router project 
- https://x.com/roccosoftware/status/2023485492860436831
- Clone one of the bare router examples from the docs. The builder is being streamlined to support more addons with fewer permutation issues. Also… just start with Start. If you don’t need SSR, turn it off with spa mode. This way if you ever need SSR, it’s just a flag away, 

- Start's entry points are still too tucked away and bare lets you do cool things like this where invalidating the viewer query would propagate deterministically
  - +1. This is one of the biggest issues we're having with start. No way to pass react context to router context

- ## The other night, @schanuelmiller and I refactored TanStack Start's "static" server function mode out of the core and into a server function middleware. _202508
- https://x.com/tannerlinsley/status/1955048427047489801
  - Not only does this mean that our middleware system is awesome, but it was also one of the best times I've had pairing programming in a LONG time. A great reminder that AI's are YES-monsters. No pushback. No resistance.
  - @schanuelmiller forces me to be a better developer and I won't exchange that kind of interaction for AI any time soon.

- ## You did not need another opinion on this but Tanstack Start is really nicely put together.
- https://x.com/aboodman/status/1912571470946971743
- Works great w/ Zero btw. Custom mutators slot right in as an API endpoint.

- My only two gripes with it are
  1. I do not like vinxi layer, I always have some odd errors with vinxi that are hard to debug. Hopefully they'll remove this soon
  2. I do not like createRoute api to create routes. I understand why it's done that way, I just really prefer remix's api (it's clean and simple)
- Docs say they are removing vinxi before v1 release

- ## @tan_stack Start is a bit confusing what runs on the server? what runs on the client?
- https://x.com/tannerlinsley/status/1928169539344420917
- It's actually pretty easy. Everything runs on both server/client by default. This is called isomorphism. 
  - If you want something to *only* run on the server, use `createServerFn` , `serverOnly` , or `createIsomorphicFn().server()` . 
  - If you want something to only run on the client, use `clientOnly()` , `<ClientOnly>` or `createIsomorphicFn().client()`

- beforeLoad is a router thing, so it runs all the time, but you can create a server function that is called in your before load function .
- when a server function is called on the server, is making s request to itself? Like an actual http request?
  - It doesn’t make a request. It creates a request though, sends that request straight to the handler to be executed, then returned. Same flow as on the client, just sans fetch() and server routing

- Is this like the old getInitialProps from nextjs?
  - Similar in timing yes

- If I use a hook or a browser api, does that only run on the client?
  - Hooks will run as normal (no effects on server though) and browser APIs will need to be accessed only on the client. You can do that by conditionally looking for document, using an effect, or mounted flag, or even our own utils like `clientOnly(), <ClientOnly>, or even createIsomorphicFn().client()`

- ## [Start BETA - Tracking _202411](https://github.com/TanStack/router/discussions/2863)
- 202411: v1.83.0 - Changed export variable renamed from Route to APIRoute
- 202505: Devinxi Alpha
  - npm uninstall vinxi ; npm install vite
  - API routes have seen a huge improvement and we're now calling them "Server Routes".

- ## Introducing a new package that automates SSR dehydration/hydration and streaming between TanStack Router / Start and TanStack Query.
- https://x.com/schanuelmiller/status/1953941380121739485
  - with this integration, if you execute a query on the server during SSR, the query data will be sent to the client automatically next to the SSR HTML. this works for queries that block the SSR requests as well as ones that resolve later.

- What are situations where this is extra beneficial?
  - whenever you don't want the client to refetch the queries the server performs during SSR. also to prefill the client query cache that are not immediately rendered.

- Does this replace react-router-with-query then?
  - yes

- ## 🤔 [Does Tanstack Start use rspack and rsbuild by default? · TanStack/router  _202410](https://github.com/TanStack/router/discussions/2582)
  - Does Tanstack Start use rspack and rsbuild for file-based routing by default?
- TanStack Start is vite only since Vinxi relies on vite-specific features for its bundling.
  - TanStack Start is a framework on its own, so the bundler option isn't opened to the user. Unless Vinxi, opens up switching their bundler to something else, I don't see this changing anytime soon.

- ## 🏠 [Devinxi by tannerlinsley · Pull Request · TanStack/router _202505](https://github.com/TanStack/router/pull/4111)
  - Remove vinxi dependency

- [Start BETA - Tracking · TanStack/router · Discussion](https://github.com/TanStack/router/discussions/2863)
# discuss-tanstack-router
- ## 

- ## 

- ## 📡 [Parallel Routes (named Outlets) Feature _202305](https://github.com/TanStack/router/discussions/605)
  - I was wondering if there were plans to introduce parallel routes similar to what exists in Next.js which allows for matching multiple routes in the same segment but being independent chunks and with a different data URL.

- Start is still only RC. It’ll be a bit l longer, but soon 

- ## [Best way to migrate a large app from (old) React Router to Tanstack Router _202510](https://www.answeroverflow.com/m/1443596813851427007)
  - At Mastodon, we are looking into migrating our router from the old-style React Router (v6, using the v5 APIs) to Tanstack Router.
- At work on a pretty large codebase (250+ routes) I just finished a react router v5 to tanstack router migration, while making them co exist
- We found the same limitation as you, at least with RR 5. Tanstack router would two way sync with the url, but RR 5 no, but we found workarounds, and two strategies worked for us:
  - strangler fig like pattern: take the top level of the app, and have it render by TSR (TanStack router) in a catch all route, and we would migrate top level routes progressively.
  - faking RR 5 history and location api: this ended up helping us having both react router api and tanstack api work, with one tradeoff: we had to switch all route rendering with TSR. RR 5 uses context to populate the history, params and location api. We found a way to have it rely on TSR state, meaning that all RR api where getting and updating tsr state directly

- We shotgun approached it at my work (180 routes) and it took about 3 months to do. The main abstraction was custom withRouter and hooks that mapped the TSR style to RR style.

- ## With TanStack Router and Start gaining popularity, React Query may become optional.
- https://x.com/YBenlemlih/status/2002846358609256932
  - You can now load data directly in the router using a loader function. So you get built-in loading and error states.
  - So should you load the data in React Query or TanStack Router?
  - Bonus: you can combine both to get the best of both words.
  - Using loaders also unlocks prefetching, i.e. faster navigation/loading times.
- In Start you also unlock isomorphic features: 
  - the page is initially rendered on server (instant UI thank to ssr) and SPA-like smooth navigation (client side subsequent navigation)
  - better SEO: custom head fields based on the loader result 

- query still gives you a whole suite of tools for mutations, revalidation, and optimistic updates. router loaders are great for initial fetches, but not a full replacement
  - yep, I just use query in loader for initial fetch, then can do extra stuff with it if needed in actual function

- use the two to get the best result. So loader function fetches the data while loading the page on server side, then I pass is as initialValue to TanstackQuery to handle refresh, invalidating, etc on the client side.

- How will you handle the case when you need same data over different routes? route loaders are good for some specific cases but react query is good for almost all the cases.

- Same was for server components and loaders in remix/react router. But if you need data fetching on client, react query is still the way to go

- ## [Why TanStack Router Requires Manual Route Tree Configuration : r/reactjs _202510](https://www.reddit.com/r/reactjs/comments/1o210lp/why_tanstack_router_requires_manual_route_tree/)
- Get the vite plugin
  - It’s for file-based routing; I want to use code-based routing instead.

- Cause tanstack router is unaware of the structure of your tree, it's just like the same thing with react router, declarative, only difference is you're not using JSX.
  - I think what you're looking for is the file based routing, similar to NextJS app router. Tanstack Router can also do that, just search for it.

- Routing is a developer concern, not framework's responsibility. It's hard to do programmatically things that devs know better.

- ## I’ve said this before, and I’ll keep saying it. Parallel routes and component routes will be massively powerful in TanStack Router. _202505
- https://x.com/tannerlinsley/status/1928654398114214360
  - Just need to get this Start thing launched. Routing is far from solved.
- Parallel route State in next is not stored in the URL. When you refresh or share the URL, any non main slots are reset back to their fallback content

- What are parallel routes?
  - when you visit a `/a/b/main_child` route, its parallel route such as `/a/b/parallel_1`  and `/a/b/parallel_1` will also be rendered in their specific outlet port.

- What do u mean component route?
  - Components as nested routes.
# discuss-tanstack-db
- ## 

- ## 

- ## 

- ## Is @tan_stack DB a new ORM, like Prisma or Drizzle?
- https://x.com/jherr/status/1954942206688805231
- It's not quite an ORM, but more of a data-fetching and caching solution.  Think of it as a powerful bridge between your database and UI.

- It's less an ORM, more a data-fetching layer with potential to reshape how we interact with databases.

- ## 🔁 How does TanStack DB, Store, and Query fit together? _20250806
- https://x.com/penberg/status/1952995106966958316
  - DB is the reactive client store using differential data flow to provide live queries. 
  - Query is a general purpose data access interface to bring data over (for example, from REST API or database). 
  - But what is store? And how do sync frameworks like Electric fit the picture -- they seem to integrate with DB, but not query?

- Store is a lightweight signals implementation thats framework agnostic - perfect for react where there is no built in signals system for storing and computing application state.
  - DB grew out of our investigations into how to integrate sync with Query...
  - sync breaks the normal 'optimistic state while fetching” that Query supports into ‘optimistic state until we see the firm state come back through the sync’. Making that work with Query was complex and we couldn’t find a good DX. 
  - We also found that with sync you want to sync the normalised tables, rather than a pre-joined data structure. To do that you then need a way to construct the expressive structures that you want for the UI on the client.
  - 🤔 We also found that real applications often have many different datastore that are used to build the front end, you need a sync capable store that can join with non-synced data, and that store can’t be tied to a single sync engine. Hence DB was born.
  - So while we are the main contributors to it, the intention is that the on rap is via Query and then to *any* sync engine. It’s very important to us that thats the case and we will help and support anyone building a sync engine integration.

- https://x.com/penberg/status/1953102852974350423
  - I switched my example project to use TanStack DB with the Turso serverless driver, and the UI is now incredibly responsive and slick

- ## Why is @tan_stack DB a database?
- https://x.com/samwillis/status/1996216487204315412
  - It's both something new, but also very much based on the architecture of any traditional database.
  - All the same parts are there, and data flows through it in the same way.
  - Only difference is it can load data from anywhere...

- what's your answer to the split-brain problem à la CAP theorem?
  - The remote database is the single source of truth. Dataflow is unidirectional, with a thin optimistic layer applied locally that is removed on confirmed writes being seen back on the sync path.

- Will it ever support FTS
  - The index system is pluggable, so all possible. We're working to make custom query operators an options too.
  - I have my eye on https://github.com/Michael-JB/bm25 in WASM as way to do FTS with DB...

- i'm a huge fan of this project so this is coming from a place of love but when i think database i think this part. the rest (what ts db does) is super important and most of what the application touches though, so others may not have the same idea
  - 🛢️👀 Yep, and I get it. There is enormous call for local persistence in DB. It's on the roadmap. That for many will be when we can finally convince them of the name. 
  - I like to think of DB a little like Neon, separate storage and compute. We've been building the concept part.
  - In-memory will always be the default, with persistence as an opt-in.
# discuss
- ## 

- ## 

- ## 

- ## 
