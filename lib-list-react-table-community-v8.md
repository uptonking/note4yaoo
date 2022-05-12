---
title: lib-list-react-table-community-v8
tags: [community, react-table]
created: '2021-04-30T17:53:42.566Z'
modified: '2021-05-13T02:54:14.171Z'
---

# lib-list-react-table-community-v8
- v8分支参考
  - https://github.com/HebleV/react-table/tree/beta
    - beta-20201109
    - https://github.com/XiaoyueCai/react-table/tree/beta
  - https://github.com/schuchertmanagementberatung/react-table/tree/next
    - next-20200525
# discuss-stars
- ## 

- ## 

- ## 

- ## After a lot of research and even implementation, I found requestIdleCallback scheduling is not the right performance tradeoff for the CPU/Memory load of #ReactTable. 
- https://twitter.com/tannerlinsley/status/1524128427229335552
  - Web workers could be more promising, but for now, async table-ing is on hold. #tabbit-hole
- The problem is that when you break up a memory-heavy block of synchronous work into chunks, that shared memory has to be stored across tasks. I'm not super familiar with the low-level memory strategies/thresholds for JS engines, but I'm assuming this chunking has negative effects
  - Totally, super agree with the problem of serialization as well. Once we can pass large amounts of structured data around its over for other platforms. Here's the API I was thinking of. Not sure if it fits this use case but could be fun to noodle on

- Y'know, this actually mirrors what the React team found with using `requestIdleCallback` for scheduling

- I found this web worker demo interesting. No performance time improvement, but leaves the main thread unblocked, just like you are looking for.
  - https://afshinm.github.io/50k/
  - Exactly. We don't necessarily need to make things faster. We're doing that already. We just need a way to unblock the UI for large tasks in a framework agnostic way.

- I would suggest looking at how @Microsoft did for excel cloud, it s unbelievable what they did there, full porting of excel.

- ## So far, I've been unpleasantly surprised at how much longer the *total* time of a long-running task is when you break it out into multiple scheduled tasks (via requestIdleCallback) vs just running the task synchronously.
- https://twitter.com/tannerlinsley/status/1524100159176511488
  - Am I wielding useIdleCallback wrong?
- I used to work on a 3D modeling program where we did some long running tasks. Breaking it up did indeed make it way slower. Ended up doing it in a webworker and using transferable objects.
  - This could very well be a solution. The tasks I'm performing are not necessarily as CPU intensive as they are memory intensive. Instead of a single op never leaving something like lower level hardware caches, they probably get moved out to RAM between the tasks.
  - Maybe idle callback fits a CPU intensive task set better than a very CPU + large memory intensive task?  My experience has had results of like 5-7x time when dealing with constructing/manipulating large data structures (~1million)
- that's expected with requestIdleCallback. Overall time will be bigger, the advantage is that your browser will not freeze while doing the calculation as it can take some breaks to do something else every now and then. You can try to play with the timeout or switch to workers
- Do you provide the timeout option? It's highly recommended, as without it can take several seconds before the callback gets fired.

- ## Finally got #ReactTable working well with React's strict effects.
- https://twitter.com/tannerlinsley/status/1523719550381944832
  - Turns out having your own scheduler can make that pretty easy... did I mention that the core has its own scheduler?
  - TLDR: I have built my own scheduling and memoization system into the ReactTable core
- Then you are using refs and controlled rerenders, I know, well, I guess
  - Indeed
- I wouldn't say "easy", but the strict effect have a purpose: idempotency. Strict effects act on effects by running them multiple times, the design of the library should follow then (just execute the cleanup, and next time rexecute).
  - Yep
- Niiice, @ScriptedAlchemy and I have been writing some of our own as well. Using the event loop to schedule main thread work is awesome. Assuming you are using the event loop, ha!

# discuss
- ## Hopefully in the future, I can make #ReactTableUI a reality. 
- https://twitter.com/tannerlinsley/status/1507082151967150084
  - This project would essentially be a "batteries included" approach to React Table with highly performant opinions around all of the hard parts of table UI like:
  - virtualization
  - column pinning
  - filter/sort/column UI
  - grouping / Pivoting UI
  - faceting
  - etc.
  - I have good ideas on how to keep the UI implementations relatively "topless" (one step away from headless? 😂) too, to allow a similar amount of flexibility that you get with react-table when it comes to styles and markup control.
- If you want inspiration, I think Ariakit is currently the best headless UI library in the game right now in terms of API design, extensibility, and how its internal code is laid out.
  - 🚀️ Reakit > Ariakit

- #ReactTable v8 alpha updates:
  - Row expansion
  - Expansion Example
  - Grouping/Aggregation Example
  - Better filter performance
  - Better grouping performance
  - General bug fixes

- ## Column resizing is going to be even more powerful in @tan_stack #ReactTable v8. 
- https://twitter.com/tannerlinsley/status/1504576494940528640
  - As per usual, you can implement all of the UI however you like, but you'll have new tools like "onChange" and "onEnd" resizing modes and a unified markup-agnostic sizing model.

- ## I love React hooks, but today I find myself writing my own edge-case memoization/performance optimization system. 
- https://twitter.com/tannerlinsley/status/1476239050927329281
  - With hooks I would need to compute all of the possible (and very expensive) outputs of this system using useMemo, even if they're not used
  - In my custom approach, these computations are just fns that lazily track user and internal dependencies to return a memoized value. This way you only pay for what you use, instead of computing the universe on mount or even when a few deps change.
- Don't misunderstand me
  - Hooks are the 💣-diggity 99% of the time.  
  - The biggest reason I am doing this is because I have libraries (like #ReactQuery and #ReactTable) that pack some serious logic into very simple hooks eg. useQuery/useTable
- That's what always worries me with hooks. I feel out of control. You keep computing variables even if you don't need them. This is why I use refs sometimes. They are way more readables but I think that classes gave us more control.

- ## [20220102] A quick snippet of an early ReactTable v8 table that renders!
- https://twitter.com/tannerlinsley/status/1476778803045167106
  - I like the API look so far! Similar enough to existing v7 to be a reasonable migration path, and I can see the logic behind the changes for type purposes already.
  - https://gist.github.com/tannerlinsley/c63cd35cdba2189f31d211ee2f2cafb3

- #ReactTable V8’s core is built in vanilla JS and uses getter fns for just about everything now… and since adopting this pattern I can’t help but see the silhouette/echo of @solid_js every time I work on it.
- https://twitter.com/tannerlinsley/status/1477342367585751040

- ## [20210430] I'm so tired of trying to make a TypeScript plugin system for React Table v8 
- https://twitter.com/tannerlinsley/status/1386903354769477638
  - that I'm about to slash(大幅削减；砍) the entire plugin system altogether and just build a monolithic(完整的) utility. 
  - Everything included, all the time.

- We got it working! This is one of the biggest wins I’ve ever had with a TS plug-in system. 
  - I won’t say I’m happy about the gotchas/limitations that held back my previous attempts, but at least I know now!
- React Table v8's new plugin system will officially be fully typed, even for developers writing plugins!

- I thought you'd gotten it working?
  - It was so close. But apparently generic maps just don't have the support they need yet. Either the inferred generic syntax needs to land or named/optional generic slots need to land. Without either, it just won't work without increasing the LOC required by plugins by like 10x 
- Typescript FAILS when the effort to 'type' variations of arguments and overrides becomes  *more work* than writing the actual library code. I then revert to 'any' or 'unknown'.
  - That last 20%of typing properly is not worth the mental anguish(痛苦，苦恼) just to deliver extra 'insight' that will be rarely used.
- Yes. Everyone has a different answer, none of them have been comprehensive.
  - I might have some higher expectations from TS (eg. I refuse to declaration merge)

- ## [20210224] I think I've built a type-safe plugin system for #ReactTable v8.
- https://twitter.com/tannerlinsley/status/1364251586956943361
  - Not only typed for app devs, obvi, but also fully typed for plugin authors as well.
- You can customize just about any part of the core React Table functionality that you want, 
  - encapsulate all of that logic into a single object, then ship it around your app, the internet, etc
  - Pretty typical plugin system. It's the fact that it's fully typed that's special.
- Why is static typing so important in plugin systems?
  - Plugin systems are traditionally very difficult to type if they involve changing the public API of the thing which they are extending, especially with TypeScript.
  - Types themselves offer a myriad(无数，大量) of benefits to any system. There's ample amount of blog posts on TS out there.
- React Table v8 is coming later this year with fully native types. Sponsors will see an early private alpha soon.

- ## [20201117] #ReactTable v8 #TypeScript Plugin System Update
- https://twitter.com/tannerlinsley/status/1328410205734858753
  - 未push到github
- This is the current status of how it looks like to build a (contrived) React Table plugin.
  - Provide your Instance
  - Opt-in to decorate specific generics, allow others to default
  - All types are inferred during implementation
- Just cleaned up #ReactTable's new `useTable` function's #TypeScript generics and inference 
- Anything specific that you can recall that made things click? Still trying to push through on understanding how to write more advanced types.
  - Types are really just functions
  - Generics (T, etc) are just variables
  - Utility Types (native and custom) are the bread and butter of powerful type inference. Study them, create your own, etc
  - Still learning more myself
- I think the worst thing to type in apps would be around context providers. 
  - Providing typings for a theme when you use many themes requires multiple tsconfigs to resolve module overrides in different ways

- ## [20201029] #ReactTable v8 (alpha) is shaping up to be much leaner. 
- https://twitter.com/tannerlinsley/status/1321521377644408832
  - Core: 3kb vs 6kb
  - All Plugins (more than v7): 12kb vs 15kb
- Sounds like you came up with a viable path for implementing plugins in TS?
  - Nope. I'm decided to keep the current system and just type as much of it as I can, incrementally making it better.

- I helped write Jimp's plugin system with strict TS typings
  - https://github.com/oliver-moran/jimp
  - 源码是js，类型声明在单独的.d.ts文件
  - An image processing library written entirely in JavaScript for Node, with zero external or native dependencies.
