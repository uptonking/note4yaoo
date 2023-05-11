---
title: lib-excel-tanstack-table-community-v8
tags: [community, tanstack-table]
created: 2021-04-30T17:53:42.566Z
modified: 2022-08-21T10:19:58.756Z
---

# lib-excel-tanstack-table-community-v8
- [Making Tanstack Table 1000x faster with a 1 line change - JP Camara](https://jpcamara.com/2023/03/07/making-tanstack-table.html)
  - [[v8] Improve grouping performance on large clusters of values_202210](https://github.com/TanStack/table/pull/4495)
# guide

# discuss
- ## 

- ## Inspired by @shadcn 's data table, I made a version using React Aria Components
- https://twitter.com/devongovett/status/1656100596406157312
- Important to note: if you just wanna display some data and it doesn't need to be interactive (e.g. selection, sorting), then an HTML `<table>` is perfect! 
  - Data tables with interactivity should implement the ARIA grid pattern for a11y (e.g. via React Aria).
- It's fine to use a normal table even with sorting right? `aria-sort` is usable afaik

- ## what's your experience of react-table between firefox and safari
- https://twitter.com/KevinVanCott/status/1650890320555524097
- Firefox always has border issues with table elements, which have to worked around.
  - But a bigger issue this week, I'm going to have to deal with a bug that only happens in Firefox when Firefox is not at 100% scaling.

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
# discuss-issues
- ## [Auto-size column width v8](https://github.com/TanStack/table/discussions/4179)

# discuss-architecture
- ## [Easy way to modify/extend features like Visibility.ts in v8](https://github.com/TanStack/table/discussions/4067)
- Not sure if its an anti-pattern or not... but you can add your own `state` and `setState` functions to the `table` instance with some typescript trickery (and some ts-ignores)
  - I store a bunch of that state and the setStates right on the root of the instance here

- ## [Possibility to create custom features](https://github.com/TanStack/table/discussions/4403)
- not yet

- ## [Declaration merging makes typing per-table meta difficult](https://github.com/TanStack/table/discussions/4220)
- This would require a return to the insane generics. I doubt the benefits would outweigh the increased friction on types.

- currently, I just add more props to meta, but I have no way to understand which types are related... 
  - I do think adding a generic for meta is the solution here

- [Possibility to type `meta` prop in `ColumnDef`](https://github.com/TanStack/table/discussions/4104)

- [I define a custom meta type for columns, but VsCode is not inferring type](https://github.com/TanStack/table/discussions/4072)
  - Due to generic limitations, This meta object must be typecast to the correct type before usage.
# discuss-performance
- ## 

- ## 

- ## 

- ## [How to properly use memo to optimize rerender in v8](https://github.com/TanStack/table/issues/4227)
- When columns change, their data models could have also potentially changed. 
  - Changing column stability/reference will trigger the table to rerender and this is good thing, otherwise your table would never update when columns change.
- useReactTable is a hook that tracks state for the entire table. When that state updates, the entire table must update. This doesn't mean that everything will be repainted, but it will be rerendered. 
- Optimize your table to be rerendered often.
Columns must remain stable they are changing. Use useMemo to stabilize them between rerenders or move them out of the render function

- [OnRowSelect rerender all components in table](https://github.com/TanStack/table/issues/4092)

- ## [RT 8 GroupBy Performance](https://github.com/TanStack/table/issues/4551)
- I was able to get a 20% improvement by optimising based on the fact that functions on each row are defined adhoc (and therefore allocated) for every single row, with no sharing.
