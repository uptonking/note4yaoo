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

- ## 
# discuss-author
- ## 

- ## 

- ## 
# discuss-start
- ## 

- ## 

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

- ## 

- ## I’ve said this before, and I’ll keep saying it. Parallel routes and component routes will be massively powerful in TanStack Router. _202505
- https://x.com/tannerlinsley/status/1928654398114214360
  - Just need to get this Start thing launched. Routing is far from solved.
- Parallel route State in next is not stored in the URL. When you refresh or share the URL, any non main slots are reset back to their fallback content

- What are parallel routes?
  - when you visit a `/a/b/main_child` route, its parallel route such as `/a/b/parallel_1`  and `/a/b/parallel_1` will also be rendered in their specific outlet port.

- What do u mean component route?
  - Components as nested routes.
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
