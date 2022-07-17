---
title: thread-fwk-react-dev
tags: [framework, react, thread]
created: 2020-12-05T17:52:28.808Z
modified: 2021-01-06T14:40:03.364Z
---

# thread-fwk-react-dev
- 关于react的特殊用法、架构设计、与其他框架的联系区别
# discuss-stars
- ## do you know why we need @reactjs ? why not build an app using only DOM API directly?
- https://twitter.com/sseraphini/status/1379547345130565632
- For me it’s the declarative way to define how your UI and data behaves and not having to care about the necessary dom changes to do that.
- Componentization leads to code reusability.
  - Unidirectional data flow is easier to reason about.
  - VDOM makes it performant and robust.
  - Huge ecosystem and community.

- ## Which React component API do you prefer for complex reusable components (such as a table)?
- https://twitter.com/housecor/status/1405916713707884554
  - Option 1: Config object
  - Option 2: Compound component
- For complex and re-usable components i would not recommend react at all. There is a reason why enterprise grade widgets won't get created with react or angular (e.g. ag grid, bryntum).
  - I would say the reason they're not made with React is so they can address a larger audience. If one already has React, using it's paradigm = less code, and the ability to compose other React components inside.
  - The benefit of using React is I can reuse lots of child components. This reduces the bundle size and complexity of the complex component.
- Trust me, if you have components which rely on 50+ state vars, React is the wrong tool. For this, you need a class config system and powerful state management logic. This is actually my field of expertise
  - https://github.com/neomjs/neo
  - neo.mjs enables you to create scalable & high performant Apps using more than just one CPU. 
  - No need to take care of a workers setup, and the cross channel communication on your own.
- For #1, This way I can take json data from an api call and pass it through to the Table component
- Unpopular opinion - 1 
  - Composition is great when it comes to homogeneous data 
  - I always find config object easier to work with. 
  - JSX just adds a lot of verbosity. 
  - Also config object allows you to apply filters & transforms easily. 
  - Also with TS config objects are more predictable
- In that table example, the compound components is about to get SUPER ugly as soon as the data is dynamic and needs some transformation from the server to what your display interface expects
  - IMO you can generate the shape config expects using elegant javscript functional programming. Using jsx, you are going to have a lot of extra syntax and mixing of js and jsx to accomplish the same thing
  - I will concede that the autocomplete experience is better with a config object in TypeScript. 
- Tables are already implemented in HTML as "compound" elements, ie: `<thead>`/`<tbody>` are children of a `<table>`, 
  - also HTML is extremely well documented so I don't have to go read the implementation to use them. 
  - If these were more than just wrapper components I'd take #1.
- Config object make thinks harder when you want a custom table in one place. You’ll end up having keys that are function that render component
- If data is dynamic then I think 2nd option us not suitable and 1st option is preferred
- The second option is a lot more simple and easier to work with while preserving readability (e.g. passing in an array of data with .map)
- #2 all day- harder to set up initially but worth it for power & flexibility

- ## When creating reusable React components, prefer compound components over config objects.
- https://twitter.com/housecor/status/1405512541846052871
  - Compound components are more flexible and offer a more natural API.
  - Use React's context to pass props down to child elements as needed.
- Replies: "The config object is type safe and enforces consistency". 
  - That's fair. Compound components are a tradeoff. 
  - Arguably a Select is too simple to justify this pattern. But it really shines with complex components like a table
- They are indeed more flexible, but they are also easier to abuse. You can validate config objects but you can't really validate children.
  - agreed. I see 2 core downsides to the composite component pattern:
  1. More work to implement
  2. More flexibility = more risk of reuse
- I feel like Typescript encourages you to avoid this pattern for good reason, because CCs rely on children, which can't be typed strongly enough to avoid having to read the implementation. I like letting TS suggest props and catch my mistakes. Config props all the way for me! 
- We’ve started following this approach for new components in our internal library, and it’s definitely a fine balance when trying to ensure people don’t deviate from the branding guidelines. But I can confidently say it helps us solve more problems than it introduces
- This is a huge topic of mine. I've been promoting this along with React Context to get super clean APIs.
# discuss
- ## 

- ## Is useReducer the only client state manager that can closure over props / server state? I don't  think you can do something like this with zustand, xstate or others. You probably can with redux, but only if all your state lives in redux.
- https://twitter.com/TkDodo/status/1533528718064361474
  - I meant reading something / having access to something from the outer scope, in this case, the `amount` . I think it would've been clearer if I inlined the reducer in the example instead of currying it.
- This isn't a closure though; this is a new reducer being created on every render. React's keeping track of the previous reducer's state and using it for the new reducer, which seems bug-prone but just so happens to be fine for a contrived example like this one.

- ## In hindsight the JSX transform that ships with TS is very much not general in many ways:
- https://twitter.com/fabiospampinato/status/1533413033892098049
- 1. The new automatic runtime function gets passed the "key" as its third argument, React cares about keys, Solid doesn't need them at all, they are just useless there.
- 2. Children are called before parents, this works in React but breaks Solid entirely, arguably this is just conceptually wrong.
- 3. Props are created before the h function is called, this makes other things that React doesn't care about impossible.

- ## React opinion: most context providers should just be singletons instead.
- https://twitter.com/jamonholmgren/status/1534295833562075136

```JS
// e.g. not:

<RootStoreProvider store={rootStore}>
  <App />
</RootStoreProvider>

// but this:

let _store

function useStore() {
  if (!_store) // initialize it
    return _store
}

const App = () => {
  const store = useStore()
}
```

- Primary issues brought up in replies seem to be:
  - SSR: I do React Native, but yeah
  - Mocking: I dislike mocking, but if you have to, probably need context
  - Component and storybook snapshot tests: I avoid those tests, don’t find them all that useful myself
  - But if those things are important to you, then yeah, use context. I am able to avoid it often myself.

- The singleton pattern is anti pattern for good reasons… This does not work well with testing or storybook for example. Or server side rendering. Context is really a beautifull way to write SOLID code without the usual boilerplate of OOP.
  - Hooks aren’t SOLID at all you’re completely subverting dependency injection (props) when you use context

- The advantage with the context provider is that tests can easily supply a different value when testing which makes things much easier than having a singleton.
  - Also for apps that run on Web and do SSR, we wouldn't want to use a singleton for values that can user-specific data.

- Providers are react way for inverse of control. It gives you much more testability and flexibility. Enclosing state provider in singleton would be the same as accessing global variable directly - works, but easy to break and hard to test.

- ## I'm toying around with using a custom React renderer that doesn't actually do any rendering (all components return null) just so I can use hooks to manage effects.
- https://twitter.com/ccorcos/status/1514437514722873350
  - I noticed that even when pulling state out of components, those components still aren't pure because of useEffect.
  - Now all components do is render HTML and I can test all of the state/effects logic (like fetching data, etc.) in complete isolation without needing the DOM...
  - Is anyone else doing something like this? 
  - I tried writing effects just as a state machine, but React hooks really are quite convenient and composable!
  - https://github.com/pmndrs/react-nil

- ## unless mitosis uses custom elements builtin extend, there's no way to translate React into WC
- https://twitter.com/WebReflection/status/1514631499961847810
  - At that point, a fast/thin layer like uhtml would be a much better target/outcome (or uland with hooks!)
  - not only tables, options, LIs, and others are problematic, current WC as target produces even more bloat than React would produce by itself!

- ## Poll: When do you create a custom React hook?
- https://twitter.com/TkDodo/status/1504200942069194753
  - 1. When it’s reusable logic
  - 2. When it’s reusable logic or an async call (fetch)
  - 3. When it’s reusable logic, an async call (fetch), or feels complex
  - 4. For all logic and state. My components only contain JSX.
- I think extracting to a custom hook only for reusability is a bit limiting. I have many custom hooks that are only used once, in one component, co-located to that component. Why?:
  - to give it a name and a clear #typescript interface, which communicates intent.
  - to encapsulate other hook calls. It can often become a black box to the using component what the hook depends on.
  - to separate concern
  - to make the tests easier to write (no need to look at the generated DOM)

    - I don't usually test hooks in isolation, but the components that need them with either cypress or testing-library. react-query doesn't have a single hooks-test

- If you want to unit test your hooks logic, you need to make it a custom React hook; otherwise, you can't unit test function components that contain hooks.
  - With classes, we could gain access to the internal methods, but with hooks, you need custom hooks to do that.
- It’s called extract method, so just for code clarity

- ## If I'm not wrong, in simple terms, Remix-Router = ReactQuery + ReactLocation.
- https://twitter.com/ShajanSheriff/status/1506972204457627651
- They are very similar in their data fetching goals. Even with all of the data loading, boundaries, and even built in mutations (which RL does not have), RR still lacks a robust search param API like RL. In practice, this is the most important feature to me right now, too.
- If Remix/RR had
  - ‘search: val | updateFn’ in useNavigate and Link components
  - search filters
  - structural sharing
  - library wide inverted control of search param encode/decode, etc
  - RL wouldn’t even exist. The async stuff was important but I would have been willing to wait.

- ## When I build libraries for React, ironically, I don't really use hooks like useState, useReducer, etc. 
- https://twitter.com/tannerlinsley/status/1504854824952610818
  - One of the best perks (and footguns) of managing your state *outside* of react is that you get to have full control over when a component should rerender.
- A great use case for this is when you need to call a bunch of state altering functions in succession. There's no waiting for your updates to come down the react pipeline, so you get up-to-date values immediately in your private state.
  - Then, when you're finally ready to commit them to your component state, you can send your private state to your component usually by saving it to a ref (don't forget to trigger a rerender!) or by using setState. Okay... so I usually have at least *one* of those two hooks ; )
  - **Rule of thumb** here is that once you take responsibility for managing state outside of react, you need to be extra aware of batching, unintended overwrites, and especially mutating your component state during render 😬
  - Either way, it's a powerful pattern to learn and master.
- Here, useTable creates the table instance with the rerenderer as the subscription. Since we are returning the instance itself (which manages its own state), we can just use a ref. Then, on every render, we send through the options again to the let the table instance update.

- Diving into the internals of many popular 3rd-party React hooks/libraries, I'd think many developers are in tacit agreement with this.
  - "Update a ref and force a rerender" feels so dirty but also so nice. And `useSyncExternalStore` helps here too.
  - 🙋‍♂️ Agreed. Like…state could even be managed in a framework agnostic outside library. 🤔
- Of course, React + concurrent features work best when it manages *all* state using its own mechanisms (hooks), but that's simply not how the real-world works. Apps tend to rely on external data that can arrive at any time, & frameworks need to be able to handle this reliably.
- React is not "reactive" in the traditional sense (especially granularly). If it was, integrating it with external pub/sub/actor style data sources would be both natural and likely more performant.
- [TL; DR of Why React is Not Reactive](https://www.swyx.io/reactrally/)
  - React could be fully push-reactive
    - I later realized this is basically the default state of things if you write any JS user interface with no scheduler.
  - But then you run into problems with backpressure, where you need batching, and expensive renders (eventually causing the need for time slicing and other async rendering techniques).
  - The solution is to push updates (reacting to external events) into a queue, but only pull views on demand.
    - This is also known as scheduling. It’s possible to implement this inside of an Rxjs-like paradigm, but it would be so finnicky that you’d basically be rebuilding push-pull reactivity inside of the scheduler anyway.

- useReducer is def more direct since useState is built on it 

```JS
function useRerender() {
  return React.useReducer(d => ({}), {})[1]
}
```

- what I meant to ask is whether you use these hooks *only* to re-rerender, with "dummy" state, or if you actually put something useful into the state ever, as a way to "sync" or smth
  - “It depends” Usually its a ref.
  - a ref + this kind of dummy state setter to rerender?
  - Yeah
- This is actually pretty neat. useRef to store state + useState to force rerenders is something I’ve never used, but seems incredibly flexible.

- Another reason to use Solid - this is the default behavior with hooks

- useRef is just useState({current: initialValue })[0] so you are technically still *inside* of react hahaha. And yea if you mutate that state directly then it is instantaneous. But seriously I wonder what are the benefits of doing it on your own as opposed to asking react to do it
  - The difference is the ability to change mutable, persistent state without also triggering a rerender.

- I feel like half of my library code is usually just pubsub logic
  - And the other half of mine are Monotonous Typescript Generics Incantations

- Can you give Example ? Please
  - #ReactQuery, #ReactTable, #ReactCharts

- You also get leaner components and the ability to swap your DOM manipulation library easily, i.e. to simply opt-out of React altogether with minimum effort if need be.
  - For super generic libraries that aim to bind to more frameworks in the JS landcape, this pattern is a must.

- ## jsx: What would you like it to "translate" to if this was native JS? DOM API constructs? Native VDOM? Something else?
- https://twitter.com/devongovett/status/1501972169458425861
  - Objects like React.createElement returns: { type, props, children }
- But then the nodes are opaque, and you can't traverse them without executing the functions. For example, it's useful to be able to access props from a node object, or traverse into children. JSX represents a tree, and I think it's useful to expose it as one.
  - FWIW, this introspection(内省/反射) is basically deprecated in React in my mind. It blocks essentially all optimizations we could do and very rarely used. We just have to provide suitable alternatives.
  - That's unfortunate. We use it extensively to implement natural APIs for collections. We need to know all items up front e.g. for keyboard nav, but don't want to render them all to the DOM (virtual scrolling) or use some post-render registration pattern.
  - Not sure there's another way to implement that at the moment. What optimizations does it prevent?
  - Server Components passed to a child resolve eagerly. So the type goes to React. Node. Static optimizations like inlining or call-through without global reasoning (for perf). Lowering JSX inline to custom low-level DOM element creation. Etc.

- ## If I were to rebuild Inferno again today, I'd go down the path of making it a "hooks only" compiler designed framework. 
- https://twitter.com/trueadm/status/1498515284877058052
  - I'd also create two templates for each component - one dynamic and one static. 
  - This would give the equivalent performance of Solid, whilst being tiny in size.
  - Many of my previous ideas were conceptualized in the React Compiler project I was hacking on.
  - https://github.com/trueadm/react-compiler

- ## React (and React based frameworks) have an uphill performance battle.
- https://twitter.com/zachleat/status/1489612637008805890

- ## It's time for the React Router v6 mega thread!
- https://twitter.com/mjackson/status/1436117485808349204
  - We are on the home stretch; the last 10%. This is the hardest part of any project
- Things on my short list of TODOs:
  • Add better animation primitives
  • Allow `<Link>` to link to external origins
  • Low-level renderMatches API (complements matchRoutes)
- Still would like to see middlewares implemented, I made my own router to get that feature. But happy to see new things nonetheless
  - What are you doing with your middleware?
- https://github.com/aposoftworks/react-complete-router
  - side effects (SEO)
  - guards (prevent route from being viewed but does not trigger a redirect, for example auth), this is pretty good with switch
  - inject extra values and calculations
  - bind router externally to other fw (redux, etc)
  - This basically exposes an API for the user to write code to further extend the router without having to alter the router source code. Giving tools for incredible new things.
 
- The router is fairly low-level. I'm pretty sure you can do everything you mentioned with React hooks. For example, side effects when the location changes are just:

```JS
const location = useLocation();

React.useEffect(() => {
  // side effect goes here
}, [location]);
```

- The same thing can be said from backend middlewares, they can be declared within controllers, but somehow it's much better to do it with middlewares.
  - I think coupling those things into react are unnecessary, since they do not work with react. Making it harder to test or debug. 
  - Another example is that the router algorithm itself can be overridden because it can be a middleware.

- In my opinion, React hooks *are* middleware. They are like stateful middleware. React Router v6 gives you a LOT of hooks that should allow you to do just about anything you want. You can hook into any piece of state that you need.
  - it feels wrong to control things like this, routing should be handled by the routers and routes. And creating a component only to handle this would pollute the vdom in a unnecessary way (one of my main problems with styled components)

- ## svelte even supports web components
- https://twitter.com/passle_/status/1433019029766148096
- I mean, yeah, React is even worse, its not just silence, its feigning to be working on it until someone else does it for them.
- I've extensively consumed WCs in a Svelte app and only had minor issues. AFAIK it's just the compile-to-CE feature that's buggy -- a nice-to-have, but nowhere near as essential as basic WC compatibility.
- tbh, reading that issue as someone who knows React but not WCs, the impression I got was that no one on the WC side could come up with a clear explanation of how React _should_ handle the seemingly dozens of nuances(细微差别) in data passing behavior WCs can apparently have
- It’s a very difficult design space because there are many ways to do WCs, and also because **React is “pulling” into the SSR direction while the WC community doesn’t have a cohesive story around it yet**. I think Joseph has done a fabulous job integrating feedback from all sides.

- ## Can someone please open source a package which takes a list of file path strings (like Remix, Next) and convert into React Router route object.
- https://twitter.com/dev__adi/status/1432310439254261764
  - Vite's glob import already solves the other half of File Based Routing.
- My setup is wild because I dislike file system routing (it introduces so many silly constraints for what amounts to a highly subjective DX boost). So I have some code that turns a route config file into file system routes as a pre-build step, so that Next.js can be kept happy.
  - I do agree Next.js file based routing is very limited partly because it lacks nested routing support. But since Remix is built on top of react-router I feel that it can handle most of the situations. Have you checked it out?
- The biggest issue is the awkwardness when it comes to co-locating page-specific modules, 
  - because most of these systems either don’t allow non-page modules in the pages dir, or force you to use an awkward prefix (like Gatsby’s underscore). But there are some more niche issues too.

- ## Any good examples of doing Error Boundaries with Next.js?
- https://twitter.com/leeerob/status/1410452498402398208
1. No changes needed to keep the dev overlay.
2. For handling errors on the server, you can create a custom 500.js page
3. For handling errors on the client, just React Error Boundaries
4. For reporting, either stdout logging or your favorite exception monitoring tool

- ## The most underrated feature of @Reactjs Server Components: There's no API - just the filename.
- https://twitter.com/swyx/status/1341535594543910912
  - When you add `.server.js` you get:
  ✅Zero bundle impact
  ✅Auto code splitting
  ✅Direct backend access
  ✅No waterfalls
- the secret to this, of course, is that "the API" is swept under a figurative rug:
  - React bundlers/servers now must handle the filename correctly
  - React I/O libraries hide the caching impl
  - lets not talk about the SECRET HOOKS we found during livestream
- @Shopify is using React Server Components (and @tailwindcss !) to build fast, fully customizable storefronts

- ## I've been thinking about React Compat in reactive libraries wrong. 
- https://twitter.com/trueadm/status/1408567234306453504
  - There are projects trying to remove the VDOM from React but that is proving really hard.
  - What if instead we view a reactive primitives as the building blocks, and React Compat like a Virtual Machine built on it?
- I think there's also a blur between what is VDOM and what is not. 
  - I don't regard VDOM to be a a JS object mapping of DOM nodes, 
  - but instead I regard it more a structure that stores intermediate values for a template that represents the UI.
- while checking out my compiler project that I worked on a few years ago. It basically compiles React components to what you see above. It extracts out the metadata as static templates and keeps components as functions that only return the dynamic values.
  - It won't win things like the JS framework benchmark, because it's not optimized to clone HTML elements (which should be banned IMO), but in real-world the metrics were light and day. It was over twice as fast as Inferno in complex, heavy real world examples.
  - In the real world, you rarely have enough to warrant a clone. Cloning is only effective if you have enough static content to warrant it. I've found that it's either the case that the children are very dynamic (another composite component), or all the props are dynamic.
  - Not to mention it adds complexity around things like event handling, fragments, stateful elements, and animations/transitions. I explored all this in-depth with Inferno back in the day, hell we even did element recycling which was a major benchmark hack haha.
- I wish the JS framework benchmark diversified enough to be more real-world, i.e. more components used and more dynamic content. Its simplicity makes it far too easy to game. In fact, there are libraries built around only that benchmark, and fail for other trivial things.

- ## If I were to make Inferno today, what would I have done differently.
- https://twitter.com/trueadm/status/1407086342559997955
  - I wouldn't use React's API
  - I would make it formally use an ahead-of-time compiler design
  - Wouldn't abstract over HTML and instead build around abstractions
- Furthermore, 
  - It wouldn't have its own event system
  - It would use a partial virtual DOM system
  - It would have accessibility baked in as a first-class citizen, including focus management
  - It would have a hooks-like API and wouldn't use classes
  - It would have streaming SSR
- I love the ahead of time idea. I bet JSX would be faster if components transpiled into 2 or 3 flat arrays:
  - components
  - children count
  - props(?)
  - children counts could be pooled from a preallocated Uint32Array
- Check out my compiler project I played around with a few years ago
  - https://github.com/trueadm/react-compiler
  - you'd actually improve performance not using a Uint32Array, purely for the fact you can re-reference template arrays that commonly appear.
- Wouldn't abstract over HTML and instead build around abstractions. What do you mean with this point? Any good prior art to share?
  - React Native Web, cc @necolas . If you get it right, you can solve so many problems. `<div onClick={…} />` should never been allowed to happen.
  - Is even argue that `<div>` shouldn’t have happened. Look how SwiftUI tackles this. 
  - We default to HTML because we are accustomed to it, not because it’s the right abstraction.
- Oh I think I follow. It’s about providing solid primitives instead of driving users towards (mis)using HTML directly. Does that sound right?
  - Pretty much. HTML is a free for all.
- you don't need to know about the underlying host with react-native-web. it reduces down to building blocks, a div on some host that happens to be the web is a View there i think and that makes it x-platform. no opinions on if that's good or not, but the idea was interesting.

- ## A key philosophical difference between Next.js & @blitz_js is that Blitz is all about giving sharp knives to developers. 
- https://twitter.com/flybayer/status/1406722174505918464
  - But Next.js is opposite. They seek to keep you from cutting yourself, which often comes at the expense of power and flexibility.
- Genuinely curious about how you manage this tension when Blitz is built on Next?
  - All tension was resolved once we forked Next.js! 
  - Once I finish the migration from our custom compiler to our additions in nextjs core, Blitz will technically be a fork of Next instead of being built on it. Finishing this is the last big thing before 1.0
  - Currently we plan to always keep up to date with Next.js. We benefit greatly from all the work that goes into it!

- ## The perf goal for this Hot Module Reloading implementation is 60+fps. 
- https://twitter.com/jarredsumner/status/1403748267188396034
- That means < 16ms to:
  1. detect changes on disk
  2. push updates to clients
  3. rebuild
  4. client performs update
  - Not sure yet how possible that is. At the very least, 1-3 is something the bundler controls
- basic websocket echo server works, next steps:
  - binary protocol
  - when HMR is enabled, convert export to var & generate default callback function that updates each var
  - runtime that registers module and a callback
  - wire up file watcher & websockets to protocol

- ## Thinking about React Fast Refresh next, but there are many dependencies.
- https://twitter.com/jarredsumner/status/1403283485389844485
- React Fast Refresh depends on:
  - Hot Module Reloading
  - JavaScript Parser hooks that hash code and annotate fn calls, hooks, exports
- Hot Module Reloading depends on:
  - WebSocket Server + small runtime api / client 
  - Filesystem Watcher (detect changes)
- Filesystem Watcher is platform-specific.
  - macOS: FSEvents || Kqueue
  - Windows: watch dirs but not files
  - Fortunately, Zig makes using platform-specific APIs pretty easy. 
- I’ll probably DIY the Websocket Server implementation
  - I’ll first try just giving each websocket client it’s own thread. 
  - That should be okay in a development context where you don’t have thousands of clients. 
  - Probably another thread for listening and responding to fs events
- I’ll probably do the websocket part before the filesystem part. 
  - Worried about the build perf impact of React Fast Refresh — hashing a lot of stuff is slow due to all the copying.

- ## A reminder that React `StrictMode` silences `console.log` on the double renders. This is the reminder I wish I'd read two hours ago 
- https://twitter.com/mattgperry/status/1389946417993687043
- I’m still struggling to understand how concurrent mode works exactly.
  - I think the "easiest" way to think about it is we're used to render => commit. Whereas in concurrent mode this often happens but the renders could happen any time and the commit may happen/may not happen/may happen later.
  - My least favourite gotcha as a result of this is renders can't *read* from *any* mutable source. Not just useRef, but classes/objects etc. You can read those in effects, but not in the render body. As a function that accepts props, good luck discerning those
- It’s still crazy that there isn’t an option to turn them back on especially for library authors.

- ## Do you know the state reducer pattern in React?
- https://twitter.com/matiasfha/status/1389583745632673800
  - Is a design pattern that enable the user of a component to manipulate or manage the inner state of it by using a reducer pattern.
  - [The State Reducer Pattern with React Hooks](https://kentcdodds.com/blog/the-state-reducer-pattern-with-react-hooks)
- The State Reducer Pattern (an idea an implementation by @kentcdodds for downshift) is a form of Inversion of Control where your component enable the user of it to control internal behavior through the API.
- React hooks made the implementation of this pattern slightly simpler and idiomatic by using the useReducer hook.

- ## Really don't understand React devs who don't like @tailwindcss (I mean, use what makes you happy ofc).
- https://twitter.com/swyx/status/1385573418158891014
  - React components localize state and side effects. 
  - Tailwind localizes styles and responsive design. 
  - They are fundamentally, philosophically aligned.
- DX of styled components/emotion is just so much better. Its much harder to read components larded up with utility classes from bootstrap and tailwind
- Because they don’t know that an asset with a URL is better than injecting different style tags on ever render.
- The string-based API makes it hard to re-use, hard to derive those styles and hard to maintain.
- Because tailwind is not Javascript ? Remember React is just javascript.
- Utility-first and token-based styling is the probably the right approach for most teams. 
  - However, utility classes in the form of magic strings is the wrong abstraction. 
  - Better to use a more type-safe, component friendly approach—there are plenty these days (stitches, fela)

- ##  `import React from 'react';` will go away in distant future
- https://twitter.com/dan_abramov/status/1308739731551858689
  - use ` import * as React from 'react';` instead.
  - https://www.reddit.com/r/reactjs/comments/iyehol/import_react_from_react_will_go_away_in_distant/
- what is the problem with default imports?
  - It complicates our ESM story, doesn’t work by default with TypeScript, and was mostly necessary for JSX anyway. 
  - Now that JSX doesn’t need it, it doesn’t make sense to have so many different ways to import React.
  - I’d say it would’ve been annoying if we still often needed React to be in scope (because "* as" is more to type) but with the new JSX transform it would not be as useful.
- What is the purpose of this？
  - When you need to import everything from a file that has bunch of exports in them then you can use (import * as React from "react), which makes more sense as you are importing everything from it, every export it has.
  - While, on the other hand (import React from "react") is a default export which means there has to be a default export named "React" in that file. Something like. export default React; On of the biggest reason for this switch is (tree shaking).
  - 能够使语义更明确

- ## Thread See new Tweets Conversation Lee Robinson @leeerob What is Incremental Static Regeneration (ISR) with Next.js?
- https://twitter.com/leeerob/status/1382400399949271040
- Incremental Static Regeneration (ISR) is a new solution allowing you to update static content instantly without needing a full rebuild of your site.
- let me explain why ISR exists.
  - If you've tried to build a large-scale static site, you might be stuck waiting hours for your site to build. If you double the number of pages, the build time also doubles.
  - Next.js allows you to create or update static pages after you've built your site. 
  - ISR enables developers and content editors to use static generation on a per-page basis, without needing to rebuild the entire site.
  - Next.js can define a revalidation time per-page (e.g. 60 seconds). Initially, we'll show the cached page.
  - Any requests to the page after the initial request and before the revalidation period are cached and instantaneous.
  - After 60 seconds, Next.js will show the cached page and trigger a regeneration in the background to fetch the latest data from your CMS.
  - Once the page has been successfully generated, Next.js will invalidate the cache and show the updated info
  - ISR is just one feature of Next.js' hybrid approach. Developers are empowered to pick the correct solution for their needs (e.g. SSG, ISR, SSR)
- If there is an error generating the page, it will *not* invalidate the cache and instead continue serving the existing static file. No downtime!
- Could you expand on what you like about incremental builds?
  - ISR is really useful for data changes/caching. For code changes, you want something similar. 
  - Gatsby's incremental builds only rebuild pages with changed dependencies/code. My Gatsby rebuilds take about 20-60 seconds, compared to Next.js's 15-20 mins.
- You have control over the initial build. As a developer, you get to make the tradeoff for faster build times or to statically generate more pages

- ## Pages in Next are just components and it pre-renders all pages at build time by default (aka static-site generation aka SSG)
- https://twitter.com/benmvp/status/1382119271766003713
  - When a page's data must be retrieved at request time (likely user-specific), we can render using OG server-side rendering (SSR) by swapping in `getServerSideProps` .
- "On-demand rendering" combines the best of SSG (cached pages) & SSR (dynamic pages) to enable dynamic cached pages
- One way is by creating fallback pages w/ `getStaticPaths` that caches dynamic routes (eg `/post/<id>` ) on request instead of pre-rendering them upfront
- The other way is thru "Incremental Static Regeneration" using `revalidate` . It makes static pages seem dynamic by regenerating them often (up to once a second) w/ updated data

- ## Redux was only ever added because the old context api was a trash fire.
- https://twitter.com/_developit/status/1382078110041059331 
  - It's in the process of being phased out in favor of useReducer/modern context api.
- That's interesting. New context API still has performance issues if not used carefully. 
  - Redux 6 actually moved to it and quickly reverted back in Redux 7 for that reason. 
  - The problem is if using hooks directly in the provider you are tying your updates to further up the tree.
- My whole area of work has been looking at how we can use granular techniques to optimize update boundaries independent of components. 
  - It frees the enduser from needing to worry about structure when it comes to performance. 
  - This has application on client and server rendering.
- In the end components become little more than just a function call. 
  - They don't own their own state, and props are just things passed through them instead of bound to them. Still colocated in creation, just not owned.
  - So that's what I mean when components are just function calls.
- would you consider the vue-style nested function to be part of this? or is your goal to fully extract any form of state from rendering
  - I'm not exactly extracting it outside. It's just the boundaries are the control flow rather than the components. Components are for the developer, but the framework flattens things down to control flow boundaries.
- Inside a conditional it doesn't matter if there are 1 or 10 components, things are only going to be released if that condition changes. Things are only going to be updated if they granular depend on what changes. Components are just organization mechanism.
  - sounds like the approach we've been discussing too. subscriptions trigger updates, components are just a way to create subscriptions or register side-effects.
- I developed this system accidentally creating Solid. 
  - I built it without components at first. I was focused on performance and thinking one day I'd just stick them into WebComponents. For convenience I adopted JSX Components syntax which compiled to `Comp(props)` .
  - I was focused on the client, but then Marko team approached me, having realized that removing the components could let them with stateful primitives and analysis do subcomponent hydration. Actually break hydration along control flows as well.

- ## React Server Components are all about APIs.
- https://twitter.com/RyanCarniato/status/1381640821510873089
  - When you keep state in the client you are sending the data over one way or the other, there is no escaping it. Below the navigation fold you need to present new information. Only MPAs never are going to need the "static" parts
  - Now there are plenty of ways to lazy load that information. We can defer hydration. Use things like Intersection Observers. But if you ever return to the same route you will at some point you will be sending some serialization of the data/markup.
  - So where are the savings? Well framework is there anyway, the interactivity/stateful stuff needs to be in the browser, and below the fold the template is coming one way or another. It's avoiding pulling in JS libraries to process data. Lodash, Markup, etc
- So breaking it down, RSCs are a couple things really.
* An approach to Progressive Rendering
* Autogenerated Component-Level RPC API
* A way of orchestrating the whole thing
- This is great and really innovative way to approach SPAs. I hope to see more of this in the future. 

- ## Is there a special name for @reactjs components whose sole purpose is to execute custom #hooks?
- https://twitter.com/TkDodo/status/1330492854628708364
  - I use them for "conditional" hooks when information is not available at the top level
  - I call them headless components, not sure if that's a thing though
- The term "headless components" was used to refer to components that handled logic, but inverted control of the view to the user (render props). They're not really needed now thanks to hooks.
- The pattern I wanted to show is about a component that doesn’t render anything but only executes side effects
- react-nil calls them null-components or logical components in their readme

- ## I didn't realize that I could use RTK for generating reducers/actions with React.useReducer.  
- https://twitter.com/SquishyDough/status/1380592058411388935
- Yep, I've done that several times myself - works great! After all, a reducer function is just a reducer, no matter what you used to write it

```JS
const counterSlice = createSlice({
  /* usual stuff here */
})

// later
const [counter, dispatch] = useReducer(counterSlice.reducer, 0)
```

- ## Confession: 80% of what I enjoy about @sveltejs could be built atop React/Preact. 
- https://twitter.com/dan_abramov/status/1377302931096154112
  - I think it'd greatly improve the DX for devs struggling w/ React's extreme lack of opinions.
- I think it’s worth noting we *are* starting to have opinions about some things. E.g. data loading. Routing is related to that. 
  - We just don’t do it only because some solution is popular. We do it where the whole strategy depends on it. There are downsides and upsides to this.
  - What we want to avoid is picking a solution because it’s common (but not because of some first principle reason) and then realizing it doesn’t work with things that we actually *do* have opinions about that come from first principles.
  - The frustrating thing about our approach is that it’s slow and takes a long time. The nice thing about it is that each of the pieces play together well as a cohesive whole and integrate in a deep way. And each new piece informs constraints for the next pieces.
- Like, how could we have opinions on routing before Server Components? It would be a shame to standardize some approach and then have to backtrack because it doesn’t work with the paradigm that’s actually built from first principles. But now we have the constraints for next steps.
- Think about feature intersections. What happens at intersection of code splitting and server rendering? Data fetching and animations? Loading states and streaming rendering? Routing and cache invalidation? “Convenient” solutions may solve individual aspects but fail to compose.
- I agree with @heystevenyung it was great that ecosystem could innovate. But the next step isn’t to cement the current state. It’s to learn from it and upstream the lessons into the architecture. Our current focus is data loading, server rendering, and code splitting.
  - We learned that we shouldn’t put all the logic on the client. 
  - We learned that initial HTML should stream instead of waiting for all data. 
  - We learned that large blocking JSON blobs are bad. 
  - Waterfalls bad, but colocation good. 
  - Loading too much is bad, loading too late is also bad.
- These are all problems of most mainstream solutions. Both in React and other ecosystems. 
  - That’s clearly not what we need to standardize on! 
  - Instead, we need to provide composable primitives that let the ecosystem default to good outcomes. 
  - That’s been, and still is, our focus.
- One huge benefit for everyone with React adopting these approaches is platform support returning. Perhaps unsurprising but many platforms/services down't support streaming back responses and always been an unfortunate barrier. React's clout should help here.
- I haven’t seen that Marko article by Patrick before. 
  - @acdlite just said a few days ago he was surprised BigPipe did not end up influential, and seemed largely forgotten with SPAs. But the article references BigPipe. 
  - Our new streaming server renderer is inspired by BigPipe too.

- ## If you've ever tried to use multiple React renderers in the same app (like `react-dom` , `react-kanva` , and `react-three-fiber` ), you may have noticed Context doesn't cross renderer boundaries.
- https://twitter.com/acemarke/status/1376659560920928256
  - There's a neat `useContextBridge` hook that should help that
- In particular, this might pop up as the classic "can't find store in context" error from React-Redux, when you've got a Redux-connected `react-konva` or `react-three-fiber` component nested inside a React-Redux `<Provider>` in a ReactDOM app, since it can't access the context.
- I think it actually got worse, when experimenting with reacts new reconciler modes every now and then I'm bumping into a new error that states react detected that a context is being read from two renderers which "isn't supported" 

- ## I stopped using React professionally right before hooks were released. 
- https://twitter.com/AdamRackis/status/1375484819891752961
  - Getting back into that game now and my fucking god this shit is hard. It is shockingly easy to mess things up in subtle, hard to debug ways.
- They just wanted to diversify the wider framework ecosystem. 
  - Hooks were their way of telling people it was ok to use reactive primitives. 
  - In a way, I thank React hooks for Vue and Svelte 3 even if the core principles in those libraries precede them. React made them brave again.
- Spoiler: every framework has issues
- Hooks only exist because React wants to run a render() multiple times and throw away the results, for concurrent mode. 
  - That can only happen if render() is pure though, hence getting rid of the possibility of using state external to what React gives you.
  - Yep, and all external state management tools are facing a bit of a crisis now.
  - And I've yet to see any real benefit to CM or suspense. Suspense is basically a PoC when it comes to features, UX and DX, and CM is trying to turn a runtime into a VM.
- Yeah in a sense the worst thing that happens with tearing is we lose our async consistency guarantees and fallback to how things are today. It settles the same in the end. I had more concern about MobX synchronous side effects during render. But seems they aren't concerned.

- ## React is great for websites, wizards etc but it’s still incredibly hard to build really fast and interactive (drag&drop, shortcuts etc) applications.
- https://twitter.com/jorilallo/status/1375216746081173512
  - Not sure what this would require but there’s an opportunity for something new
- Tools like zustand, react-spring and react-use-gesture provide tools that fit this problem really well, by leveraging refs, subscriptions, imperative mutations.
  - Feels like writing imperative code but with all of react's good parts
  - Future needs something that’s more native, not just gobbled together. We already do this and it’s too complicated
- have you use use-gesture? there's nothing cobbled together or complicated about it, it's a clean abstraction of what a gesture is.
  - if react had fast updates nothing externally would change, it would all just be technical details for libraries to implement.
- Completely agree with this -- we're building something highly interactive and made the deliberate decision against using React for exactly this reason. Seriously wish JQuery UI wasn't abandoned in 2016.

- ## The html `...` alternative to JSX is 🔥, as it allows React without transpiling. But there's no TS checking on components in the literal
- https://twitter.com/giltayar/status/1371443623573749760
- It's a problem I really really hope the TS folks find a solution for - right now it would require implementing a complete XML parser in TS Types. There are some demos, but they make my head spin and I have no idea how they could be feasibly generalized (v slow).
- The current recommendation is basically that, if you are working in an environment like VSCode where TS types are super helpful, you should author in JSX and transpile to HTM. The transpile process can be extremely fast, but we haven't released a pure token-based approach yet.
- Whenever I see such a discussion about this general topic, I'm kinda sad we don't just use JSON to create the VDOM
  - Tagged template literals were designed specifically for embedded languages. I think TS growing to be able type-check them w/o plugins is a great way forward here.

- ## In React Router, a URL is just *part* of a Location. So you can have many locations at the same URL.
- https://twitter.com/mjackson/status/1371533569785356289
  - Each location may have its own state, and has its own entry in the history stack.

- ## Looks like React Native's Hermes JS engine is finally shipping with Proxy support
- https://twitter.com/acemarke/status/1370515928300027909
- What’s almost shocking for me is that they’re shipping no iOS as well

- ##  Preact Server Components
- https://twitter.com/marvinhagemeist/status/1370041302935560194
- Here is a quick prototype that fetches components that were rendered on the server. 
  - Need to sort out some implementation details, but so far I like where this is going 
- I’ve seen preact’s implementation of server components and can confirm they are doing it _right_. 
  - As always with this team, such a clean execution of quite a complicated concept. I don’t even like SSR but am so very nearly sold.

- ## I’ve been waiting to see what this PR (Fizz) would look like for a couple of years by now
- https://twitter.com/dan_abramov/status/1369624574065803264
- I'm so excited! I've been out here implementing similar features the way that made sense to me, but have been dying to see how you all were going to do it.
- still related to server components?
  - It’s all part of the same picture. This one in particular relates to streaming HTML renderer, which is complementary to Server Components.
- When you render React on the server today it's a synchronous process, it all happens in one go. This means you have to do all your data fetching ahead of time, meaning it cant live inside of React itself. It also means that a single slow data fetch will block your entire page.
  - This PR is the initial parts of a new asynchronous server renderer. Besides being a game changer for how we can do data fetching on server rendered React apps, it can also stream the parts as they become ready.
  - This means a single slow fetch wont block the user from receiving the page, they can get the parts that are ready early.
  - Note that this isn't the full vision on data fetching on the server, there is also a separate but very related concept Server Components.
  - Just to be clear though, this isn't something you need to learn or understand right now, it's just laying foundation.
  - You are also unlikely to interact with the parts in this PR directly, this will be abstracted away for you by frameworks like Next.js.

- ## Lots and lots of libraries are having to build React wrappers for otherwise-portable Web Components because React is bad at DOM. 
- https://twitter.com/slightlylate/status/1368418750161055747
  - [3 Approaches to Integrate React with Custom Elements](https://css-tricks.com/3-approaches-to-integrate-react-with-custom-elements/)
- Just in case it helps, carbon-web-components package ships React components auto-generated from the corresponding Web Components
- In the year of our lord 2021, years after all browsers came to support WC natively, and after React broke back-compat guarantees which might have prevented the library from getting good at DOM, folks still have to do these dances
  - I'm not saying React is the new IE XX, but tooling-space would, perhaps, benefit from thinking of frameworks as runtimes in this way.

- ## react is x-platform. 
- https://twitter.com/0xca0a/status/1367523451561512968
  - it renders on the web, desktops, mobile, vr, ar, webgl, canvas, sketch, figma, console, tvs, watches, etc.
  - you use the same components across platforms. 
  - this is how it looks when you use react-spring for instance on a native shell
- As of version 5.3.x react-spring is now universal/platform independent. 
  - It can animate *anything* on *any target*, from react-native, react-blessed (see screen-cap), to your fridges touchscreen if it had a react-renderer. 🙀 For anything other than dom point it to dist/universal
- this is how it looks when you use react for webgl and games 
  - that isn't just shared knowledge bc these are all components, 
  - it's using the same react libraries you'd rely on with the dom: react-router, redux, etc 
- preact is a web framework. it renders divs and spans. 
  - react is preparing for a future in which anyone can create for any platform, and where platforms share the same libraries and components. 
  - well, actually, not just preparation, that's where we are right now.
- preact is a web framework. 
  - That for me is one of the biggest advantages of Preact, not a downside...
  - Since React started trying to target more and more platforms it got bigger and bigger and it's codebase and code model got very complex.
  - well, that's not really true is it. people forget that react is 2kb. it got smaller and less complex (hooks). it didn't grow bc of x-platform. but react-dom could really need a face lift, i wish it was smaller so much is certain.

- ## I've wondered for a while what the technical reasons are for so many people using react over preact. Are there any?
- https://twitter.com/_developit/status/1367514064289730565
- there are a dozen reasons. 
  - react is moving forward, constantly innovating and breaching into spaces a web framework like preact does not dare go. 
  - concurrent mode, suspense, hooks, reconcilers, the new event stuff they're working on, it's always react leading.
  - doesn't mean no point using preact, there is, but it's easier take an idea and make it smaller, but preact is not the one going forward, fighting for unity across platforms. 
  - you save a few of bytes, but you also miss out on mostly everything that's happening in reacts eco system.
  - exactly, though you do have hooks in preact. 😃 but you just can't do things or express yourself in the way you could in react, there's just so much missing. that to me is worth more than a few kb i guess.
- So technically, it's more about the advanced or experimental features than any major functionality. I would love them to support Web Components as well as Preact does!
  - the new things are major though. 
  - suspense will change how we think of async matters. 
  - concurrent mode will make it rival native performance in ways web apps never could. 
  - web components are bugged and broken. 
  - i don't think that's what most people care about.
- FWIW preact has its own design process and leads in many areas, my guess is that they're just the areas you're not personally interested in.
  - things like: framework interoperability, pluggable component architectures, partial and mutative hydration, unkeyed diffing, tagged templates as JSX output, state graph integration into VDOM, etc.
  - i don't doubt it. i am referring to a particular segment of innovation, see unification across platforms, reconciling native and non-native.
  - or things like suspense, which change how we handle async matters. these are all user-facing, groundbreaking inventions.
- "state graph integration into VDOM" Face with monocle this sounds intriguing, any further reading available?
  - I wish! that's the one we're furthest out on, it's only roadmapped at this point. 
  - Though FWIW Vue is already doing something like it, and Vue 3's performance is great partly as a result.

- ## Do you have a really interesting use for inline reducers? 
- https://twitter.com/acdlite/status/1364250190279045126
  - Like where you pass a closure to useReducer. Or, you swap out different reducers at runtime.
  - In the class world, an equivalent is accessing the second argument (props) of a setState updater.
- Personally, I dont see a use case for an inline reducer because it is a function of state and action. 
  - If I need to access props, I pass it as action payload.
- Opposite viewpoint: I strongly believe that reducers never need to be swapped out. 
  - App logic can always be factored so that the same reducer is used for the lifetime of the component.
  - Contrived example - you wouldn't do this: `useReducer(asleep ? sleepingReducer : awakeReducer, ...)` .
  - You should have this instead: `useReducer(humanReducer, ...)` .
  - Where `humanReducer` handles both being asleep and awake.
  - What’s your position on passing a function to setState? Why is one ok but the other isn’t?
  - I personally never do it, and I think that it's an implicit "event" which is better handled by a reducer.
  - In other words, setState + functional updates = an implicit, decentralized reducer.
- Yeah, this is a very useful for inline cDU which doesn’t exist in hooks land
  - Right but do you have a representative example that instantly convinces people why it’s useful? That’s what I’m looking for
  - Validating form a with something async, get the validated state and latest values in the callback
  - Invert control so that the caller of the  imperative function has ability to abort or alter the effect at the call site

- ## can I virtualize an array of @reactjs components?
- https://twitter.com/sseraphini/status/1362502418781642755
  - I'd like an API like this:
  - `<Virtualize> {arr.map(a => <Item key={a.id} a={a} /> </Virtualize>`

- What do you mean by virtualize?
  - I’d like to stop rendering them on DOM to make the page light
  - For offscreen elements? Or something else?
  - Yep, offscreen ones
  - Offscreen elements are deprioritized in React. But that would be a great challenge, since you'd end up destroying and recreating elements every time it left the viewport.
  - But that would be a interesting feature for React.
  - We could check for an element position in the viewport, and check if it's inside it. And not render elements outside that viewport. But that would make the components mount/remount every time.
- replace react-window/virtualized with react-virtuoso
  - removed a lot of boilerplate code!

- ## Does anyone else add `console.log()` or `debugger;` to their components in the middle of a debugging session so that Fast Refresh picks it up?
- https://twitter.com/dan_abramov/status/1362549600511483917
- I sometimes add a console log so I can look at it's arguments in the debugger because it's easier than looking at a massive list of props

- ## One of the challenges of building React component libraries is to not impose any specific styling solution to the App code.
- https://twitter.com/pomber/status/1362125599607820290
  - My approach is to use a `classes` prop
  - That makes the component interoperable with almost all styling solutions.
  - 本已有10种方案，作者又提出了一种，于是有了11种方案；更应该参考大公司方案
- I like this approach a lot, I have this same problem with my company’s component library used in multiple apps with different styling solutions, 
  - I initially used Tailwind but ended up ditching it and providing behavior only components without styles

- ## I envy the mental capacity of folks who can be productive prototyping with single-file components.
- https://twitter.com/dan_abramov/status/1361792509601607685
  - React lets me write garbage code (for prototyping) and I love that. 
  - Got a single 1K line file, ~10 components, changing their names/structure all the time. 
- I'm not sure what the difference is here. At least in Vue, single-file components allow you to do the very thing that you describe for prototyping:
  - Everything in one file? Check.
  - Define multiple components in the same file? Check.
  - As a React and Vue user I can relate
  - With Vue SFC I really have to plan the components in advance; 
  - sometimes I get it right, sometimes I get it wrong, 
  - but refactoring them is painful. 
  - Meanwhile with React I can just refactor them like normal functions
- It's exactly the opposite for me - I split into smaller files to navigate more easily. 
  - I envy the technical skills of people who are able to navigate 1K line file productively
- A big file doesn't mean your code is garbage. 
  - You will know its boundaries better after a while and you can split it up and give it good names. 
  - But that's usually the path towards good code. 
  - Premature organization by arbitrary rules can make it harder to see better patterns.
- I prefer react style allowing me to compose multiple components in one file, especially when it's something like a drop-down component, or something where I may not reuse some of the other components.
  - I like embers conventions for structures and uniformity, and then I like svelte for the simple and fast dev process.

- ## how to debug @reactjs components?
- https://twitter.com/sseraphini/status/1361300393544855554
  - console.log props and state
  - console.log inside useEffect
  - console.log
- How to debbug JS:
  - Old school - alert
  - New Kids on The Block - console.log
  - Bonkers - debbuger; 
  - Noobs - Dev tools
- I prefer debugger, or debugger statements, which is basically flexible console.log
- Break points (debugger) is the only way I debug anything in any language.
- Devtools. Breakpoints
- useDebugValue to custom hooks

- ## I smell an antipattern.
- https://twitter.com/erikras/status/1361606811971952641
  - I’ve got two third party custom hooks that want to give me a ref to give to an element so that it can do fun stuff to the element.
  - The problem is I want to give both refs to the same element. 
- Libraries should almost always accept, not create, refs IMO
  - How do libraries know when these refs resolve?
  - The same way we all do? In a useEffect.
- This is a good reason to stay away from react-hook-form and instead embrace the glory that is react-final-form!
- mergeRefs utility function to the rescue.

- ## What are the major changes to the ecosystem since 2018?
- https://www.reddit.com/r/reactjs/comments/lg92yi/what_are_the_major_changes_to_the_ecosystem_since/
- Biggest things:
  - React hooks changed how we write components, along with increased use of the new Context API (which has also led to confusion over when and how to use Context effectively)
  - Redux is still most widely used state management tool, but there are many other good options
  - Redux Toolkit and React-Redux hooks drastically simplified writing Redux code
  - New libraries like React-Query and Apollo that focus on "data fetching/caching" instead of "state management"
  - Next and Gatsby joining CRA as major "React distributions"
  - Switch from Enzyme to React Testing library and more "integrated" component testing
  - Widespread use of TypeScript (>50% usage in the React community at this time)

- ## 3 Rules for Keeping Components Organized
- https://www.seancdavis.com/blog/three-rules-keep-components-organized/
- Rule #1: Separate Source Files into Logical Buckets
  - I prefer to separate components by the role they play within the larger application.
  - Even though layouts, templates(container), and blocks(comp/element) are (or could be) all technically a type of component, I like keeping them separate from one another. 
  - some frameworks — Jekyll is one example — are more opinionated about where you place your components without some custom configuration. 
  - (With Jekyll, components are more like partial templates, which they call includes). 
  - In cases like this, it's usually a good idea to use the framework's defaults.
- Rule #2: The Top Level is for Shared Components Only
  - Many times a component is only used in one place, by one other component. 
  - In that case, it isn’t necessary for that component to be exposed right in the primary components directory. 
  - Instead, it could be nested within the directory of the component that uses it.
  - the top-level of a directory of components should be in use either by more than one other component or by some other type of component.
- Rule #3: Supporting Files Live Alongside their Component(s)
  - Knowing that all supporting files are in a directory along with a component saves me a lot of digging around.
  - Supporting files include stylesheets, client-side scripts (for server-side components), or utility files (like adapters and transformers).
  - I have found it much more efficient to group a component with all its supporting files rather than grouping types of files together. 
  - I've found it easier to locate pesky issues by keeping styles and scripts decentralized and closer to the thing they are affecting.
  - That said, this requires some additional diligence on your part to ensure you're scoping those supporting files in such a way that they're only affecting the necessary component(s).

- ## The browser is the source of truth when it comes to the URL. 
- https://twitter.com/mjackson/status/1356713777526263808
  -  Any time you read it and put it into memory (like Redux) you risk getting out of sync. 
  - Your Redux store is not the source of truth when it comes to the URL.
- Remember: the user can change the URL without you ever knowing about it. They can either:
  - hit the back button or
  - manipulate the address bar directly.
  - You can't stop them. Once they do, the URL has changed. If your source of truth is Redux, you're now out of sync.
  - The only thing you can do is react to a change in the URL.
  - To effectively "prevent" navigation, you must be able to undo the navigation they just did. This is not easy to do, but it's possible in most cases using histry pkg
- i think the main appeal to copying any sort of external state into redux was so that you can join it with other data already in redux (in mapStateToProps) but i don’t think this is necessary anymore given hooks. makes it much nicer to compose state at the component level
- one can also say the the url is just a side  effect of being in the current state. Kinda like saving a bookmark. Now source of truth is your app, and in state X it sets url Y and renders DOM Z

- ## One interesting thing we found when researching my last article is that every framework's version of this React code logs different things when you click the button
- https://twitter.com/RyanCarniato/status/1353801009844240389
  - Which are more correct
  - React: "0 0 0"
  - Vue 3: "1 2 0"
  - Svelte: "1 0 0"
  - Solid: "1 2 2"
  - [5 Ways SolidJS Differs from Other JS Frameworks](https://dev.to/ryansolid/5-ways-solidjs-differs-from-other-js-frameworks-1g63)
- well a major difference between the svelte version and the react one is that with the react code everything has to pass through the whole update cycle, whereas in svelte count is just a variable and ++ mutates it in place, or rather at the next ; 
- Imho, react has made the best decision here because it takes care of the worst case scenario(Multiple state changes are batched into one state change preventing multiple rerenders).
  - Also, This behaviour is noted well in the docs and is mostly associated with event handlers.
- I work in React almost exclusively now, but I have to admit that classes add a lot of clarity to state in components.
  - *However* having worked on the Angular team, particularly in the engine/compiler, I can tell you that classes are a double-edged sword because of inheritance.
  - People subclassing subclassed components. 
  - Class-based components in web frameworks tend to have some static traits. 
  - There's a lot of dancing around how to propagate that through inheritance in a way that makes sense.

- ## How do you decide when to split up a component? 
- https://twitter.com/MichaelThiessen/status/1165241262494167043
- TL; DR: when you need to, but not before.
- I generally split into list and listItem components so every v-for iterates over listItem components. Because there is always this moment when you need a computed value for these list items.
- When I feel a component does more things than it should, when a component gets too big (200+ lines), when a component has too many props

- ## What are some React anti-patterns that you encounter often? Why are they dangerous?
- https://twitter.com/TejasKumar_/status/1214259916376027137
  - Code mutates props.
  - Code modifies state directly.
  - props.key is read inside a component.
  - Keys duplicated among siblings.
  - Event handler returns false to prevent default.
- Putting too much logic in event handlers. This goes for any framework, though.
- Putting too many responsibilities on a single component. This is often represented by too many states, too many props, large render function, or too many instance functions.

- ## why use react for threejs?
- https://twitter.com/0xca0a/status/1282999626782650368
  - same reason you use it for the dom.
  - three arguably is even more unruly than the dom as every "thing" is wired into everything. 
  - the snapshot is from my react-europe talk, a simple search for "cube" (yellow) reveals the difference  
- threejs: cube affects *every* aspect of the app: setup, state, view, resize, events and render, it is not re-usable at that point. 32 hits. 
- react: a re-usable self-contained self-cleaning component and one invocation.
- this is not a dig at the dom or three. these are imperative systems and im glad they don't add high level features, because that's not their domain. react simply expresses sth imperative in a declarative way with a common ground that makes management and sharing much easier.
- r3f does the same for three that react-dom does for the dom, updates or not. you can write small-ish vanilla dom apps relatively clean, in three that is less likely bc a "thing" always has to reach everywhere to function.

- ## the magic of react has always been that
- https://twitter.com/0xca0a/status/1353659846202159109
  - if you eliminate the technical hinderances, then you can transfer an idea to the screen directly, you can worry about the things that actually matter, be it design or otherwise.
  - https://codesandbox.io/s/cell-fracture-forked-3rjsl
- https://twitter.com/0xca0a/status/1341811710081044483
  - a tutorial on working with @glTF3D in @threejs_org & React.
- vue/svelte/ng were made for the document object model. 
  - vue now has renderers, svelte, i don't ... think so? 
  - react saw it coming and anticipated for a future where renderers transcend(超出；胜过) platforms many years ago.

- ## Use `React.useMemo` instead of multiple `React.useCallback` s to create an object of handler functions in a custom hook. 
- https://twitter.com/kyleshevlin/status/1352639659147456512
  - [memoizedHandlers.js](https://gist.github.com/kyleshevlin/08a2deb904b79077e46966567ccabf06)
  - Makes it super simple to make a whole bunch of methods stable, preventing unnecessary rerenders

```JS
function useBool(initialState = false) {
  const [state, setState] = React.useState(initialState)

  // Instead of individual React.useCallbacks gathered into an object.
  // Let's memoize the whole object. Then, we can destructure the
  // methods we need in our consuming component.
  const handlers = React.useMemo(() => ({
    setTrue: () => { setState(true) },
    setFalse: () => { setState(false) },
    toggle: () => { setState(s => !s) },
    reset: () => { setState(initialState) },
  }), [initialState])

  return [state, handlers]
}
```

- But why not just call setState? It's not normally getting redefined, is it?
  - The purpose of the hook is to expose an API.
  - We don’t want the consumer to be able to do just anything with setState, such as pass it a non-Boolean value in this case.
- Definitely really nice. It’s type safe and prevents inline functions to be used. I just replaced every bool state in our new project at work with that pattern 
- Nice little pattern right here, never thought about callbacks this way before. Not even sure why `useCallback` is favored over `useMemo(() => …)`. The former seems to cause more confusion than the problems it solves.
- Neat. I'd still `useCallback` for functions with non-overlapping dependencies. 
  - Otherwise, other callbacks would get recomputed unnecessarily.

- ## re: context vs redux debate
- https://twitter.com/dai_shi/status/1351351537751126018
  - If one would compare useReducer+useContextSelector vs React-Redux, it would clarify what Redux and its family offer.
  - Note use-context-selector no longer depends on any hacks, it just uses ref+subscription, like react-redux.
- By the way, we could use Redux in React without Context.
  - Just like zustand, a react hook could subscribe to a Redux store directly.
  - My reactive-react-redux v5-alpha follows this pattern with experimental useMutableSource.

- ## new trend in react: there's a sizeable community within react that fears state managers, and they go through hot hell to avoid one.
- https://twitter.com/0xca0a/status/1350731142480146435
  - 批判使用多个context造成wrapper hell，而不使用类似redux管理状态
- the root cause was most likely redux 
  - people think dealing with state is complex because they're facing volumes and volumes of information. 
  - and it sure piled on when they went the "zen of state" route.
- to make it clear, this isn't about libraries giving you a provider for theming and so on. 
  - they're using context as it should be used. 
  - this is merely about app-state and splitting up what normally would be fields in your state model into multiple providers to avoid re-render.
- Struggling to see what's materially wrong with this pattern? Other than deeply nested things looking unsightly. I think calling this out as a mistake is incorrect.
  - split state up, app becomes slow, rigid, hard to refactor, once state A relies on state B you get into real trouble, if B also relies on A you face an impossibility. 
- Yeah I got pretty frustrated with using context for sharing state in a performant way. Pretty happy with Zustand.
  - I just use context for delivering non-changing instances which I guess what libraries are doing too.
- Though Provider is helpful for implementing server side rendering, where it makes sense to have a store per request, rather than a singleton store

- ## But first be able to explain why you don't like passing props multiple levels
- https://twitter.com/markdalgleish/status/888213730265153538
- Also, explain why you're creating so many component layers when a single component will do just fine.
  - From experience, it's probably because their components import their own child components directly rather than accepting children as props.
  - I think it has to do with your approach. I fell into the trap at first of trying to make a neat little component for every box on the page
  - Nowadays I always start with a single component and take the top-down approach. Don't create a new component until I absolutely need to
  - Having lots of small components for page layout is amazingly expressive, they just need to be composable, accepting children as props.

    - Building out a living style guide of React components is a great way to force this architecture.
    - I've been working on something like this these last of couple months and it is an amazing workflow.
    - With well thought out component APIs, updates are a breeze. I absolutely love it.

- This is why I love the render prop on Route so much. No need for extra components just for URLs
  - I've been thinking on this angle for glamor/ the css prop/ programming workflow in general. when it's make it work -> make it right.
  - I tend to get to prod faster, but if I try to make my abstractions before making *something* work, I tend to have a bad time. 
  - Exactly. Problem with Just JavaScript is our tolerance for big classes is way less than big templates. Have to fight the abstraction urge.
