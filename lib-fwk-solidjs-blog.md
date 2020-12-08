---
title: lib-fwk-solidjs-blog
tags: [blog, lib, solidjs]
created: '2020-12-05T07:11:47.041Z'
modified: '2020-12-08T13:27:35.701Z'
---

# lib-fwk-solidjs-blog

## blog-solidjs

### [Introducing the SolidJS UI Library_202003](https://dev.to/ryansolid/introducing-the-solidjs-ui-library-4mck)

- SolidJS is a declarative UI library for building web applications, much like React, Angular, or Vue. 
  - It is built using brutally efficient fine-grained reactivity(No Virtual DOM), an ephemeral(短暂的、只流行一时的) component model, and the full expressiveness of JavaScript(TypeScript) and JSX.
- These are the 5 reasons you should be at least aware of SolidJS.
- It's the fastest
  - It's been at the top of the JS Frameworks Benchmark with the most optimally hand-written plain JavaScript implementation. 
  - This includes surpassing the fastest low-level Web Assembly implementations and this is with a declarative UI library.
  - Solid is now the fastest on the server as well. Using the Isomorphic UI Benchmark it has pulled out in front of competition.
- It's the smallest
  - While it won't win size in toy demos and benchmark where everything happens in a single Component, that honor probably goes to Svelte, 
  - when it comes to larger actual applications， Solid has almost no overhead on Components (more like a VDOM library rather than a Reactive one).
  - For example, SolidJS currently is the smallest implementation of the renowned Realworld Demo
  - Solid's compiler does a great job of managing tree shaking, its codebase built off the same powerful primitives as the renderer make the runtime small and completely scalable.
- It's expressive
  - Solid apps are built using JavaScript(TypeScript) and JSX. 
  - The compiler optimizes the JSX but nothing else.
  - You are not limited to premade helpers and directives to control how your view renders (although Solid ships with some). 
  - You don't get to rewrite v-for the way you write a component.
  - There are ways to write custom directives or precompiler hooks, but in Solid it's just another component. If you don't like how `<For>` works, write your own. 
  - Solid's renderer is built on the same reactive primitives that the end-user uses in their applications.
  - Solid's reactive primitives manage their own lifecycle outside of the render system.
  - This means they can be composed into higher-order hooks, be used to make custom Components, and store mechanisms. 
  - It is completely consistent whether working in local scope or pulling from a global store.
- It's fully featured
  - Solid still considers itself a library rather than a framework so you won't find everything you might in Angular. 
  - However, **Solid supports most React features** like Fragments, Portals, Context, Suspense, Error Boundaries, Lazy Components, Async and Concurrent Rendering, Implicit Event Delegation, SSR and Hydration(although there is no Next.js equivalent yet). 
  - It supports a few things not yet in React like Suspense for Async Data Loading, and Streaming SSR with Suspense
  - React clones like Preact and Inferno would require significant changes to their VDOM core to offer the same so it has been a much longer road. 
  - And the same is true with new directions React has been doing in its experiments as async rendering and multiple roots are trivial with Solid.
- It's familiar
  - Solid doesn't stand out when it comes to API's or developer experience. 
  - If you've developed with React Hooks before Solid should seem very natural. 
  - In fact, more natural as Solid's model is much simpler with no Hook rules. 
  - Every Component executes once and it is the Hooks and bindings that execute many times as their dependencies update.
  - **Solid follows the same philosophy as React with** unidirectional data flow, read/write segregation, and immutable interfaces. 
  - It just has a completely different implementation that forgoes(放弃、弃绝) using a Virtual DOM.
- Solid has been in development for over 4 years. But it is still in its infancy when comes to community and ecosystem.

- I've been using this library for a big project at work and I much prefer it to React.
  - SolidJS has a cleaner API (though similar) than React.
  - It's reactive computation model is clean, simple and efficient.
  - It's easier to integrate 3rd party libraries with SolidJS than with React

- I wonder how it compares to lit-html
  - I've separately done benchmarks where I've shown even out of non-compiled tagged template approaches Solid's tagged template version is faster than libraries like lit-html lighterhtml etc
  - lit-html is a library designed to handle rendering and doesn't worry about components and state management so feature sets are not equivalent. 
  - Lit-html has close relationship with Polymer and supported by Google so already a huge leg up

### [Why SolidJS: Do we need another JS UI Library?_202006](https://dev.to/ryansolid/why-solidjs-do-we-need-another-js-ui-library-1mdc)

- The number of times I've asked myself that over the years is staggering(大得惊人的; 令人吃惊的; ).
- I only started promoting it because it had already achieved the goals I had set out for it. 
- Understand that this is a personal journey so it is one full of personal bias.
- I love React. I didn't always though.
  - In 2014, I didn't see the point. I was very happy with KnockoutJS.
  - I missed using function components and easy composition patterns based on primitives.
  - I watched the first 2 years of React dev debate over the right store mechanism 
  - and I kept on thinking why is this even a thing? 
    - Change propagation and composition patterns are something I took for granted 
    - and now I had to use classes and figure out which flavor of Flux fit my mood.
- If instead of parsing DOM nodes like Knockout, I could just read in a text file and parse the string to create my own HTML-like DSL. 
  - I played with this for about year and decided it wasn't bad. 
  - I still had this obstacle though that at this time all the performance benchmarks were based on re-rendering full pages from data snapshots. 
  - And while my experiment updated quickly these were a mess. 
  - I decided that Proxies were going to be key and changed my experiments to focus on that.
- However, React was changing rapidly during this time.
  - Batching updates, Function Components, HOCs for composition. Slowly by slowly React didn't seem so bad. 
  - IDE support and tooling made developing much nicer than my string templates.
  - The only thing I missed was the code organization I had in my libraries. 
    - I really missed my data being declarative. 
    - By that I mean with Knockout I'd describe a thing and all its behavior in one code block and then I could encapsulate it. 
    - React HOCs weren't quite the same. The declarations and the behavior were still separate generally.
- And then I stumbled across a library. Surplus
  - It was easy to cross reactive scopes and props were a mixed bag of Signals and data you always needed to check what you were getting. 
  - with the JSX it was able to just let the JS statements pass through. 
  - I had various JavaScript like DSLs in my String Templates, sort of invented my own language 
  - but I was hitting a place where I wanted to bring in JS parsers anyway. 
  - I liked the state objects in React and I saw object proxies being the solution to doing diffing so that this approach could compete in any scenario that a VDOM could.
  - However, Surplus' compiler optimizations wouldn't detect them so I had to artificially wrap reactive expressions in {( )} to artificially fool it.
  - Over time Adam, Surplus' creator, had less and less time to spend on the project and I decided to take my own shot. 
  - Building something similar on Babel, but proxy friendly
  - This was great but it felt foreign. React had gotten everyone to feel like they were using plain objects. 
  - I couldn't land on how I wanted to box primitives. Should I use a getter/setter, or function form like Knockout, or explicit get/set like MobX? These were all ugly. 
  - The pattern was amazing but realistically I felt no one would really get over their preconceptions here.
- I never had much interest in Vue.
  - I saw their reaction to React Hooks, deciding to expose their own reactive primitives and I got excited.
  - It did eventually land as the Composition API.
  - However, in my (very subjective) opinion, it lacks the clear finesse of React or even Surplus. 
  - It was sort of like a modern Knockout which I think is exactly what what they are going for. 
  - Tooling and DX is improved, but the mental model hasn't moved forward as much. 
  - It has that easiness of use but I was concerned the approach was setting it up to repeat many of the patterns that caused reactive libraries to fall out of favour before.
  - React had already impressed on me the value of uni-directional flow, immutable interfaces, and explicit updates
  - Vue has all the makings of the reactive titan we want, but they are only starting to embrace their true identity. 
- For Svelte, There were 4 main points being made that I felt were suspect, if not misleading.
  - No Runtime
    - obviously JavaScript executes at runtime, so was he saying he doesn't reuse any code?
  - Virtual DOM is Pure Overhead
    - If you think it's expensive creating a tree of JS Objects, how expensive do you think it is to do the same traversal and wire up a bunch of event listeners. 
    - This feels every bit as suspect as the old VDOM is faster than the DOM.
  - Benchmarks
    - the benchmarks that Rich chose weren't even remotely good ones.
  - JSX as a DSL
    - the benchmarks that Rich chose weren't even remotely good ones.
    - but the insistence that it wasn't an option for Svelte seemed odd
- React had all the strong principals, and vision but the implementation incompatibility would likely never be bridged.
- Vue is a large library that has to cater to people of all backgrounds.
- If you are interested in a library that has the discipline of React, transparent implementation that doesn't cut corners for easiness, and all the performance to back it up, maybe SolidJS is the library for you.

## ref

- [Designing SolidJS: Components](https://t.co/JBBZSaanu1?amp=1)
- [Designing SolidJS: JSX](https://t.co/Y3MQ34um1R?amp=1)
- [Designing SolidJS: Reactivity](https://t.co/P9aD3WHBZe?amp=1)
