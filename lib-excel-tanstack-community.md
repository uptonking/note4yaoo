---
title: lib-excel-tanstack-community
tags: [community, tanstack]
created: 2023-03-01T13:00:08.556Z
modified: 2023-03-01T13:00:27.664Z
---

# lib-excel-tanstack-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

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
