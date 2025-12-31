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
# discuss-internals
- ## 

- ## 

- ## 

- ## 

- ## 
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
