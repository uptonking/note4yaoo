---
title: lib-fwk-solidjs-blog
tags: [blog, lib, solidjs]
created: 2020-12-05T07:11:47.041Z
modified: 2020-12-08T13:27:35.701Z
---

# lib-fwk-solidjs-blog

# guide

# blog-solidjs

## [SolidJS · Reactive Javascript Library](https://www.solidjs.com/guides/reactivity#how-it-works)

- Solid is made up of 3 primary primitives: Signal, Memo, and Effect. 
  - At their core is the Observer pattern where Signals (and Memos) are tracked by wrapping Memos and Effects.

- Signals are event emitters that hold a list of subscriptions. They notify their subscribers whenever their value changes.

- The trick is a global stack at runtime. 
  - Before an Effect or Memo executes (or re-executes) its developer-provided function, it pushes itself on to that stack. 
  - Then any Signal that is read checks if there is a current listener on the stack and if so adds the listener to its subscriptions.

## [Building a Reactive Library from Scratch - DEV Community](https://dev.to/ryansolid/building-a-reactive-library-from-scratch-1i0p)

- [A Hands-on Introduction to Fine-Grained Reactivity - DEV Community](https://dev.to/ryansolid/a-hands-on-introduction-to-fine-grained-reactivity-3ndf)
- [Finding Fine-Grained Reactive Programming - JavaScript inDepth](https://indepth.dev/posts/1269/finding-fine-grained-reactive-programming)
- [Exploring the state of reactivity patterns in 2020 - JavaScript inDepth](https://indepth.dev/posts/1280/exploring-the-state-of-reactivity-patterns-in-2020)

- Fine-grained reactive systems execute their changes synchronously and immediately. 
  - They aim to be glitch-free in that it is never possible to observe an inconsistent state. 
  - This leads to predictability since in any given change code only runs once.
- Fined-grained reactive libraries use a hybrid push/pull approach to maintain consistency. 
  - They are not purely "push" like events/streams, nor purely "pull" like generators.

```JS
// singals core contains a getter and setter 
export function createSignalCore(value) {
  const read = () => value;
  const write = (nextValue) => value = nextValue;
  return [read, write];
}
```

```JS
// Signals are event emitters.

// a global context stack that will be used to keep track of any running Reactions or Derivations
const context = [];

// bi-reference between runningContext and signalSub
function subscribe(running, subscriptions) {
  subscriptions.add(running);
  running.dependencies.add(subscriptions);
}

// Signals consist of a getter, setter, and a value. like a Subject object
// Reactions, also called Effects, Autoruns, Watches, or Computeds, observe our Signals and re-run them every time their value updates.
export function createSignal(value) {
  // each Signal has its own subscriptions list.
  const subscriptions = new Set();

  // auto subscribe when read
  const read = () => {
    const running = context[context.length - 1];
    if (running) subscribe(running, subscriptions);
    return value;
  };

  const write = (nextValue) => {
    value = nextValue;

    // clone the subscriptions list so that new subscriptions added in the course of this execution do not affect this run
    for (const sub of [...subscriptions]) {
      sub.execute();
    }
  };
  return [read, write];
}

export function createEffect(fn) {
  // running context that will be stored to global; like a observer object
  const running = {
    execute,
    dependencies: new Set()
  };

  const execute = () => {
    // clean up the previously registered context
    cleanup(running);
    // This allows us to dynamically create dependencies as we run each time. 
    context.push(running);
    try {
      fn();
    } finally {
      context.pop();
    }
  };

  execute();
}

// Every cycle we unsubscribe the Reaction from all its Signals and clear the dependency list to start new
function cleanup(running) {
  for (const dep of running.dependencies) {
    dep.delete(running);
  }
  running.dependencies.clear();
}

// usage
const [count, setCount] = createSignal(0);
createEffect(() => console.log("The count is", count()));
setCount(5);
```

```JS
export function createMemo(fn) {
  const [s, set] = createSignal();
  createEffect(() => set(fn()));
  return s;
}
```

```JS
const useReducer = (reducer, state) => {
  const [getState, setState] = createSignal(state);
  const [getAction, dispatch] = createSignal();
  createEffect(() => {
    const action = getAction();
    if (!action) return;
    state = reducer(state, action);
    setState(state);
  });
  return [getState, dispatch];
};
```

- There are two main things we are managing. 
  - there is a global context stack that will be used to keep track of any running Reactions or Derivations. 
  - In addition, each Signal has its own subscriptions list.
- These 2 things serve as the whole basis of automatic dependency tracking. 
  - A Reaction or Derivation on execution pushes itself onto the context stack. 
  - It will be added to the subscriptions list of any Signal read during that execution. 
  - We also add the Signal to the running context to help with cleanup
- Finally, on Signal write in addition to updating the value we execute all the subscriptions. 

- This is how libraries like KnockoutJS from the early 2010s worked.

- 🎤️ discussions

- I understand the idea of reactive value, but how the updates on DOM are performed, does the framework subscribe to the changes via effects or some unexplained magic is happening?
  - That's it. DOM rendering are effects. More precisely nested effects as to only retrigger the closest change.

- I've been wondering why people like representing a reactive state in `[get,set]=data` instead of `S.data` 🤔 Is it because React introduces it that way?
  - There is the single getter/setter function: state()表示get，state(value)表示set
  - KnockoutJS popularized this approach but it becomes pretty ambiguous once you leave local scope. 
  - 语义不够明确
  - `get+set` This is how it works in MobX, and Svelte 2
  - The thing with tuples are you can name them exactly as you want. 

- Using Observer Pattern terminology the "signal" comes from the "subject".
  - By using "getState" the "observer" not only "gets the state" of the subject but also implicitly subscribes to updates to the subject's state. Similarly "setState" triggers the machinery necessary to update anybody who's interested in the updated state.
- 

- In this scenario(with `createMemo`) where there is only a single observer that has no other dependencies this will effectively execute the same number of times (as without `createMemo`).
  - The main benefit of `createMemo` is to prevent re-calculations, especially expensive ones. 
  - This is only relevant if it is used in multiple places or the thing that listens to it could be triggered a different way which could also cause re-evaluation.
  - This is actually one of the reasons I personally like explicit reactivity. A lot of libraries/APIs sort of push this memoization on you by default or hide it in their templating. It's excellent for update performance but you end up with higher creation costs.

- running code from the article i found that nested effects will create new subscription everytime outer effect runs, without cleaning up previous subscriptions, causing zombie inner subscriptions to appear.
  - Yes, an actual reactive system is more complicated. I'm missing cleanup on nested effects, but to be fair most reactive libraries do. Mobx and the like. They expect the user to handle final cleanup. Solid is special in that we build a hierarchical ownership graph to do this ourselves and this works really well with our rendering system, but it is far from the norm.

- Why use context stack?
  - Nested reactivity. Generally you can nest effects or derivations inside themselves. This is important to how Solid renders but I suppose wasn't needed for this simple example.
  - If you try to subscribe after the inner effect it doesn't track. 
  - Keep in mind this is just a simple approximation. I don't actually use an array in my libraries and instead just store the out context and then restore it.

- I'm basically backlinking the signal because on effect re-run we have to unsubscribe from all the signals that it appears in their subscription lists.

- In the code above effect's dependencies are being added but not really used anywhere except for cleaning itself

- why do we need to cleanup in general?
  - The observer pattern is inherently leaky. Signals don't need cleanup but any subscription does. If the signal outlives(比…活得长) the subscriber it will have no longer relevant subscriptions. 
  - At minimum we need to mark the subscriber as dead. The fact that we dynamically create and tear down subscriptions on each run has us doing this work anyway.

## [Super Charging Fine-Grained Reactive Performance_202212](https://dev.to/modderme123/super-charging-fine-grained-reactive-performance-47ph)

- I've been working on a new fine grained reactivity libary called Reactively inspired by my work on the SolidJS team.

- Let's explore some of the different algorithmic approaches to fine grained reactivity

- Reactivity is the future of JS frameworks! 
  - Reactivity allows you to write lazy variables that are efficiently cached and updated, making it easier to write clean and fast code.
- Fine-grained reactivity libraries have been growing in popularity recently. 
  - Examples include new libraries like Preact Signals, µsignal, and now Reactively, as well as longer-standing libraries like Solid, S.js, and CellX.
  - Using these libraries, programmers can make individual variables and functions reactive. 
  - Reactive functions run automatically, and re-run 'in reaction' to changes in their sources.

- Reactive libraries work by maintaining a graph of dependencies between reactive elements. 
  - Modern libraries find these dependencies automatically, so there's little work for the programmer beyond simply labeling reactive elements. 
  - The library's job is to efficiently figure out which reactive functions to run in responses to changes elsewhere in the graph. 

- Reactivity libraries are at the heart of modern web component frameworks like Solid, Qwik, Vue, and Svelte. 
  - Reactively comes with a decorator for adding reactive properties to any class, as well as prototype integration with Lit.
  - Preact Signals comes with a prototype integration with React

- The goal of a reactive library is to run reactive functions when their sources have changed.
  - Efficient: Never overexecute reactive elements (if their sources haven't changed, don't rerun)
  - Glitch free: Never allow user code to see intermediate state where only some reactive elements have updated

- Reactive libraries can be divided into two categories: lazy and eager.
  - In an eager reactive library, reactive elements are evaluated as soon as one of their sources changes. (In practice, most eager libraries defer and batch evaluations for performance reasons).
  - In a lazy reactive library, reactive elements are only evaluated when they are needed. (In practice, most lazy libraries also have an eager phase for performance reasons).

- MobX is an eager reactive library
  - MobX uses a two pass algorithm, with both passes proceeding from A down through its observers. 
  - MobX stores a count of the number of parents that need to be updated with each reactive element.
  - MobX stores a count of the number of parents that need to be updated with each reactive element.

- Preact started with the MobX algorithm, but they switched to a lazy algorithm.
  - Preact also has two phases, and the first phase "notifies" down from A, but the second phase recursively looks up the graph from D.
  - Preact checks whether the parents of any signal need to be updated before updating that signal. 
  - It does this by storing a version number on each node and on each edge of the reactive dependency graph.

- Like Preact, Reactively uses one down phase and one up phase. Instead of version numbers, Reactively uses only graph coloring.
  - Ryan Carniato describes a related algorithm that powers Solid in his video announcing Solid 1.5.

- Current reactivity benchmarks (Solid, CellX, Maverick) are focused on creation time, and update time for a static graph. 
  - Additionally, existing benchmarks aren't very configurable, and don't test for dynamic dependencies.
  - We've created a new and more flexible benchmark
- 
- 
- 
- 
- 
- 
- 
- 

## [Why I'm not a fan of Single File Components - DEV Community](https://dev.to/ryansolid/why-i-m-not-a-fan-of-single-file-components-3bfl)

- The crux of the problem with restricting files to a single component is we only get a single level of state/lifecycle to work with. 
  - It can't grow or easily change. 
  - It leads to extra code when the boundaries are mismatched and cognitive overhead when breaking apart multiple files unnecessarily.
- Most libraries even non-SFC ones, don't support nested syntax though. 
  - React for instance doesn't allow nesting of Hooks or putting them under conditionals. 
  - And most SFCs don't really allow arbitrary nested JavaScript in their templates. 
  - MarkoJS might be the only SFC one that I'm aware of supporting Macros(nested components) and inline JS, but that is far from the norm.

## [Introducing the SolidJS UI Library_202003](https://dev.to/ryansolid/introducing-the-solidjs-ui-library-4mck)

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

## [Why SolidJS: Do we need another JS UI Library?_202006](https://dev.to/ryansolid/why-solidjs-do-we-need-another-js-ui-library-1mdc)

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

## [Future Reactivity Design - HackMD_202305](https://hackmd.io/@0u1u3zEAQAO0iYWVAStEvw/rJCOaC_Z2)

- I want to focus on 2 key mechanisms that I believe central to moving to lazy reactivity. 
  - This document will layout ideas on how they could work.

- Root-Scoped Effect Queues
  - One of the biggest benefits of lazy pull based reactivity is that we can defer work until we need it. 
  - Idea 1: Merging with Existing Roots
- Async Transactions
  - Idea behind this is starting from the root of a change no changes are applied until all pure calculations are resolved.
- Async Primitive
  - Option: Async Components
  - Option: Fine-Grained Blocking
# more
- [Comparative study of reactivity across frameworks and implications for Resumability_202308](https://www.youtube.com/watch?v=vf1v7n2ApHI)
  - It has my favorite visualization of the differences between Signals and Observables and a great example to show the difference between reactivity in frameworks.

- [Designing SolidJS: Components](https://t.co/JBBZSaanu1?amp=1)
- [Designing SolidJS: JSX](https://t.co/Y3MQ34um1R?amp=1)
- [Designing SolidJS: Reactivity](https://t.co/P9aD3WHBZe?amp=1)
