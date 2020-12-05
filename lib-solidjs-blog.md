---
title: lib-solidjs-blog
tags: [blog, lib, solidjs]
created: '2020-12-05T07:11:47.041Z'
modified: '2020-12-05T07:12:20.836Z'
---

# lib-solidjs-blog

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

## ref
