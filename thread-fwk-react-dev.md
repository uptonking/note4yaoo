---
title: thread-fwk-react-dev
tags: [framework, react, thread]
created: '2020-12-05T17:52:28.808Z'
modified: '2021-01-06T14:40:03.364Z'
---

# thread-fwk-react-dev

- 关于react的特殊用法、架构设计、与其他框架的联系区别

# pieces

- ## 

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

- ## Invented a new React pattern I'm calling the "fake child" pattern.
- https://twitter.com/markdalgleish/status/1370951759284162565
  - When making composite components (e.g. `<Select> and <Option>` ) it lets you pass private props (i.e. not on the type signature) from parent to child *without* using context.
  - Note that this also prevents `<Child>` from being rendered outside of `<Parent>` , which is pretty neat given there's no use of context here.
  - https://codesandbox.io/s/dry-surf-jfmzx?file=/src/App.tsx
- This breaks composition though.
  - `const SpecialChild = () => <Child />` .
  - The child component is a dead blob, it can't be bound to state or made dynamic.
  - This is something where imo context should always be used.
  - If it's not clear, the trade-off here is that `<Child>` must be a *direct* child of `<Parent>` , i.e. it can't be rendered by another component.
- Why do you want to avoid using Context here? It seems like a good use case for it.

- I think react-aria has been doing sth similar, but your example is much understandable
- We do this exact thing in React Spectrum for all our collection components. They all share the same `<Item>` “component”, which is just mapped to the appropriate internal element based on the parent
  - Another cool thing about this is it enables virtualized scrolling without changing the API. Rather than passing all children through, we can simply not render some of them until they are scrolled into view.
  - We actually built a whole system for this type of component using generators
  - This does break composition though - ie no wrappers of `<Item>` are allowed. I wish React had a mechanism to query the rendered tree without actually rendering to the DOM.

- Having some feature for this has been on the plans for a while but don’t really have a great plan that isn’t very limiting. Eg server streaming gets tricky if the parent can change the output. This pattern also doesn’t always work well with Server Components...
- Depending on if both or either are client components rendered from a server component. Either the server component parent can observe children that are representations of the client children, not the real child. Or client parent can observe a placeholder for a suspended child.
- Breaking composition has some deep implications.
  - Yeah though in the cases we apply this pattern you wouldn’t ever render the parent in one place and children in another, and I think that’s a reasonable restriction. The children are not real components, they’re just providing data for the parent like any other prop, but via JSX.
  - What about HOC? It’s less of a problem now with lots of libraries going with hooks, but they’re still wildly used. For example Relay pre-Hooks.
    - Generally we recommend placing anything you would have wrapped around `<Item>` inside the item instead which works pretty well. The content is generally what people want to customize anyway.
- Perhaps. That `<Select><Option /></Select>` pattern is commonly great for Server Components though because it allows for highly reusable Client Components so you have to download zero code specific to that usage. I'm sure we'll figure something out though.
- Another option for this is to have a wrapper around both Select and Options that are "Shared" which does the loop over the children and then pass to some client specific implementation detail. The problem doesn't really kick in since the child can't suspend so maybe it's nbd.
  - I think with this API you could put the content inside the Option in a server component instead of the Option itself. Eg `<Select><Option><ServerContent /></Option></Select>`. Makes some sense because the Option itself doesn’t render anything anyway.
  - Could there be a simple useIndex hook that maintained the proper index in the tree and was only readable similar to a ref? In practice, it seems you never need that index on initial render, just things like keyboard interaction.
    - We use this for more than just passing an index through though, eg rendering only some of the items for virtualized scrolling, and mapping to completely different UIs depending on the parent component. It’s more of a JSX replacement for passing a list of objects to a prop.

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

``` JS
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
