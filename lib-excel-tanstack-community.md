---
title: lib-excel-tanstack-community
tags: [community, tanstack]
created: 2023-03-01T13:00:08.556Z
modified: 2023-03-01T13:00:27.664Z
---

# lib-excel-tanstack-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🏘️ My new form library Formisch is already available for @preactjs , @QwikDev , @solid_js and @vuejs . @sveltejs will follow soon _202508
- https://x.com/FabianHiller/status/1952555778612629507
  - What makes Formisch unique is its framework-agnostic core, which is fully native to the framework you are using
  - It works by inserting framework-specific reactivity blocks when the core package is built. The result is a small bundle size (<= 2.5 kB gzip) and native performance for any UI update
  - This feature, along with a few others, distinguishes Formisch from other form libraries. My vision for Formisch is to create a framework-agnostic platform similar to @vite_js , but for forms.
- As I understand it, TanStack Form is implemented with a framework-agnostic core that has its own reactivity system. This system is then connected to the framework you are using via framework-specific adapters. This differs from how Formisch works under the hood. Is my assumption correct?
  - That's correct

- Does it also cover complex features like nested forms and async validation?
  - For validation we are using Valibot which supports async validation. But besides that you can also write your own validation logic and call `setErrors` to control the form programmatically.

- 🤔 Are there specific reasons behind the lack of support for React?
  - Yes. Most frameworks, besides React, use signals for their reactivity system. Although there are differences between the frameworks, the general concept remains the same. This makes them easy to support. 
  - However, React's reactivity system is based on rerunning components, which complicates building a complex system if you don't want to rerender the entire form with every keystroke. Therefore, supporting React in a performant and reliable way requires a lot more effort.

- Could you add enhance schema validation  by supporting standardschema?
  - No, not right now. Formisch "walks" the Valibot schema to initialize the reactive store of the form, where every state is its own signal. 
- Standard Schema does not provide the functionality to "walk" a schema because every schema library is implemented differently internally and this is almost impossible to standardise. What schema library would you like to use?
  - I want to use @arktypeio and ajv. That's why I asked. Maybe standardschema need to provide a way to walk the schema
- We will probably support them at some point, but depending on a non-modular schema library like ArkType or AJV goes against the idea of a modular form library. 
  - Currently, using Formisch with Valibot adds less than 3.5 kB to your bundle. ArkType would increase this number by four times, and AJV would increase it by more than eight times.
# discuss-author
- ## 

- ## 

- ## 
# discuss-start
- ## 

- ## 

- ## 

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

# discuss-router
- ## 

- ## 

- ## Introducing a new package that automates SSR dehydration/hydration and streaming between TanStack Router / Start and TanStack Query.
- https://x.com/schanuelmiller/status/1953941380121739485
  - with this integration, if you execute a query on the server during SSR, the query data will be sent to the client automatically next to the SSR HTML. this works for queries that block the SSR requests as well as ones that resolve later.

- What are situations where this is extra beneficial?
  - whenever you don't want the client to refetch the queries the server performs during SSR. also to prefill the client query cache that are not immediately rendered.

- Does this replace react-router-with-query then?
  - yes

- ## I’ve said this before, and I’ll keep saying it. Parallel routes and component routes will be massively powerful in TanStack Router. _202505
- https://x.com/tannerlinsley/status/1928654398114214360
  - Just need to get this Start thing launched. Routing is far from solved.
- Parallel route State in next is not stored in the URL. When you refresh or share the URL, any non main slots are reset back to their fallback content

- What are parallel routes?
  - when you visit a `/a/b/main_child` route, its parallel route such as `/a/b/parallel_1`  and `/a/b/parallel_1` will also be rendered in their specific outlet port.

- What do u mean component route?
  - Components as nested routes.
# discuss-store/db
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
# discuss
- ## 

- ## 

- ## 

- ## Looking at the @tan_stack router docs and @tan_stack query docs and I cannot see a way to use both of them together.
- https://twitter.com/isocroft/status/1764279324134277146
  - Or am I wrong. Cos, I am seeing duplicate function here

- They have a small amount of overlap in caching, but for the most part, they go really well together using loaders to preload queries.

- ## What's your opinion on React Server Components right now?
- https://twitter.com/tannerlinsley/status/1687552723875676162
- What do RSCs need to be more production ready?
  - Be released outside of Next
- I have a SSG with freemium model. Not sure about costing in RSC. Also, doesnt it promote bad programming as you can just dump packages at server?

- ## You no longer *need* an external data library to use @Tan_Stack Router. The following are built-in:
- https://twitter.com/tannerlinsley/status/1688679819326926849
  - Loader Data
  - Stale-While-Revalidate
  - Max Age
  - Max Preload Age
  - GC Max Age
- Defaults are set for success regardless!

- Turn on gcMaxAge to something other than 0 for unloaded routes to stick around and get reused for both prefetch and load. Turn down maxAge from Infinity to get auto refreshing.

- Are we able to use TanStack Router in a vanilla JS web app yet?
  - Theoretically yes. But I’m not sure what that looks like. Testing and server env is basically that.

- ## @Tan_Stack Actions just got some upgrades to be on par with TanStack Loaders.
- https://twitter.com/tannerlinsley/status/1678498390873886720
  - This is a smaller, lighter library meant to be used with Router + Loaders.  Think of it like `useMutation` , but more composable, bite-size and less-opinionated.
  - It's really just an extremely tiny state manager special-built for router-based mutation flows

- ## bling: new javascript framework?
- We're currently working on a prototype right now.
- FYI, all of the start code will be in the router repo for now, under a new package
- https://github.com/winter-things/winterkit
  - The primary motivation for this project is to build a foundation for server-side Javascript frameworks. The goal is to provide a set of tools that can be used to build a framework that is easy to use, easy to extend, and they don't have to maintain it
- Why?
  - Each modern framework is slowly adopting the Web Fetch API as the server runtime API along with other Web Standard APIs. This is an awesome direction for the web and an amazing foundation for full-stack Javascript apps to be built on.
  - There is a lot of duplicate work that a bunch of frameworks like SolidStart, Remix, SvelteKit, Astro, QwikCity, Nuxt, Next have done to support the Web Fetch API.
  - The challenge is the variety of Javascript server runtimes available for developers to use: Node (Docker, Fly), deno, bun, Cloudflare Workers/Pages, Vercel Serverless/Edge
