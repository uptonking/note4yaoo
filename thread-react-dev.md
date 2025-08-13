---
title: thread-react-dev
tags: [react, thread]
created: 2020-12-25T15:22:27.224Z
modified: 2021-01-06T14:40:11.360Z
---

# thread-react-dev

# guide
- [Using Generators in React Components](https://blog.tomaszgil.me/using-generators-in-react-components)
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Today I learned you can pass generic type params to react components and I almost vomited
- https://x.com/joshmanders/status/1919524052022014416
- It is even more useful when the type inferred and the end user doesn't have to think about it, the props are just *magic*

- ## useCallback 实际上是 useMemo 的一个特殊形式，useMemo会自动调用函数并且返回值，而 useCallback 是不调用直接返回函数
- https://x.com/wulianwen1/status/1865416582102704181
  - 这两个函数在 react 源代码中的实现非常一致，窃以为 react 团队单独实现 useCallback 的原因是语义化和减少函数调用的这一步性能开销，

- 就函数声明那点开销几乎可以忽略不计。useCallback 的目的是因为 useMemo 里的计算可能开销很大，由于 useMemo 里的计算可能会依赖于函数，所以没办法只能把函数也缓存起来。

- ## 活久见，使用 useRef 缓存过的 VDom，居然还会触发重渲染，而且重渲染使用的还是缓存时的 props。
- https://x.com/YuTengjing/status/1803435159645200623
  - 一直以来的认知都是只有父组件重新染，setState, context api 会触发重渲染，没想到这里 vdom tree 上的一个节点由 null 变为缓存的 vDom 也会触发重渲染
- 组件被卸载了又挂载肯定会执行render的
  - 除了 props 还有 hooks 呀，hook 可能包含副作用的

- ## TIL React changes a component in a Suspense context to `display: none !important` until data fetching completes.
- https://x.com/cpojer/status/1798912741383844237
  - Quite unexpected in my case where the transition from being offline to online triggers a data refetch, not an initial load, and makes all content on the page flash.

- ## React Compiler 开源了，这次 fb 是搞了个真 compiler 
- https://twitter.com/unixzii/status/1790948056244101557
  - IR、SSA、optimization passes 都是按照正统编译器来设计的。
  - 底层用 Rust 编写，passes 用 JS 编写，可扩展性很强，感觉想学编译器的话可以用它入门了。
- 至今没懂 SSA 究竟是干啥的
  - 简单讲就是剔除变量的重复赋值，会让控制流、可达性等代码分析更容易
- 全是JS写的，rust 只是放在那，没有用
- 如果是生成的虚拟机指令的话还行，生成的却是js代码，怪不得很多web页面性能这么差，也不完全是chrome本身的问题。

- ## Slots are such a cool pattern for composition in React Aria. 
- https://twitter.com/matt_stobbs/status/1773482640768700464
  - They allow you to share data between parent and child components but still give you the flexibility of choosing what the child components are and how they should be laid out

- ## 💫 In React, how would you fix the performance of this black bar animation that's dropping frames when the new page renders?
- https://twitter.com/ryanflorence/status/1769374265873441229
- This can be handled by using CSS-only solutions, outside of React. When something can be handled by CSS only, I tend to prefer that solution. It frees up the main event loop to focus on interaction & the browser’s CSS layout engine is vastly more performant.
- Handle the animation outside of React. So many React performance problems can be handled by taking it outside of the React render cycle
- Just get rid of the animation.

- ## 🤔 Am I going crazy or is this a legit way to avoid hydration errors? 
- https://twitter.com/TkDodo/status/1741068994981826947
  - Basically abusing `useSyncExternalStore` to safely read server snapshots on the server and on the first client render, and then falling back to the client snapshot.
  - The good thing is that on client side transitions, the client snapshot will be read immediately.

- I’m glad you like this pattern but which part of this feels like a hack to you? Preventing hydration mismatches is exactly what the `getServerSnapshot` argument is designed for
  - The hacky part is imo subscribing to "nothing". There is no external store here and nothing to sync. 

- Yeah that’s how React Aria’s `useIsSSR` hook works

- UseSyncExternalStore is a criminalky underused hook, that solves so many SSR issues.

- ## Avoid mixing business logic with your React components.
- https://twitter.com/_georgemoller/status/1739644203867464091
  - Instead create abstraction layers that communicate with them.
  - 提供了动画示例
- Makes a lot of sense. This design is more maintainable and instead of fetch I usually use SWR or React Query for further scalability as it provides faster fetching, caching and other features out of the box.

- ## Very interesting to see the battle between react-merge-refs (my package) and merge-refs
- https://twitter.com/theKashey/status/1739045763857199194
  - I ask @reactjs , could you please add an official utility for this? It can't be implemented perfectly by third-party.
  - [Non referentially stable refs cause multiple updates](https://github.com/gregberge/react-merge-refs/issues/5)
- There are a lot of different versions of this pattern. Almost every project came with something similar:
  - react-hooks.org/docs/use-fork-ref
  - mitchellhamilton/apply-ref
  - theKashey/use-callback-ref
  - mui-org/material-ui@9bd4277/packages/material-ui/src/utils/useForkRef.js

- ## Not enough people, me included, understand how suspense works
- https://twitter.com/TkDodo/status/1727806048910651628
- What seems to surprise people the most is timing though. I get asked a lot how dependent queries work with suspense and the answer is: they just do, because it fires the first query, then suspends, then fires the second. It just surprised me that people have been using suspense for quite some time but don't know this because it means they've had unintentional waterfalls ...

- ## I often group related props into an object.
- https://twitter.com/housecor/status/1723706241048809898
- Advantages:
  ✅ Less code, so easier to read
  ✅ Clarifies the relationship between related fields
  ✅ Makes it easier to pass the data around
  ✅ Don’t need to change the component’s API when properties change
- But be careful, you might need to useMemo to avoid rerenders.

- ## Thanks to `flushSync` , you can finally manage focus in React again. (but I will always love this.setState)
- https://twitter.com/ryanflorence/status/1722358755499913582
- setTimeout won't always work, and adds some gross flashing and gross UX for assistive tech too
  - if it was noticeable maybe a requestAnimationFrame. But that may not work either depending how updates are batched. I'm really curious if it's a micro / macro / event loop task with flushSync. Yea UX with assistive tech could get weird with jumping focus so rapidly
- Nifty! So it essentially "flushes DOM updates synchronously", I'll have to keep this one in my back pocket.

- ## React tip: stop using forwardRef() for your custom components. 
- https://twitter.com/DavidKPiano/status/1720874496427446770
  - Just name the `ref` prop something else in your custom component (like `inputRef` ) if you can.
  - Key phrases here: "your custom components" and "if you can".
  - A ref is just an object. Passing it *through* a custom component shouldn't be anything special.

- I don't think this is good advice. Most libraries and frameworks work on the assumption that 'ref' is the name of the prop (e.g. HeadlessUI for focus management).

- Is forwardRef() deprecated from now on?
  - It is not, but I believe it will be removed in the future.
  - yes but the goal is to allow you to pass a vanilla ref prop directly so teaching people to not do that should probably come with a note that the goal is to enable exactly that

- ## If you want cleaner event handlers in your jsx in React you can use currying
- https://twitter.com/_georgemoller/status/1720237969087373716
- The problem with this is if handlers are passed around, folks will eventually forget to call the function. I had few hard to debug problems like that when a curried function was used as event handler - compiler is happy but the handler is not being called.
- Just because you can, doesn't mean you should. Personally, I find this harder to read.
- why don't you skip all of that and simply do this: `<li onClick={setSelectedItem} />` ?
  - sometimes you need to put extra logic

- ## Avoid using conditionals to render views in React
- https://twitter.com/_georgemoller/status/1719150019918418421
  - Instead use Maps/Enums
- Nice approach. Also i think that in these examples might worry adding dynamic imports to only import the component to be render es. This way you have both boosts: maintanability and performance.

- ## Using a key prop to reset @reactjs components is a great technique. 
- https://twitter.com/aarongarciah/status/1719297001714487507
  - It resets the state *and* re-creates the underlying DOM elements. 
  - 👉🏻 Sadly, lots of devs are not aware that the focus gets lost when it's contained within an element inside the component whose key is changing
  - IMO managing focus is one of the most challenging problems in complex web apps

- ## Q: Does RSC still use fibers (just one render)?
- https://twitter.com/sebmarkbage/status/1716927877915275640  
- No.
  - react-dom/client is implemented using Fiber (for now)
  - react-dom/server is implemented using Fizz
  - react-server-dom-webpack is implemented using Flight Server/Client/Reply Server/Reply Client.
  - 6 separate implementations.

- ## I've used useCallback maybe once or twice in the last 3 years, never useMemo 
- https://twitter.com/samselikoff/status/1712826463706075209
  - always-rerender is the beauty, heart & soul of React
- In react-native they quickly become needed !
  - Rendering cost in RN is much higher. While browsers are ultra optimized for js and dom changes, it is not the case with RN.
- Quick check on current project (roughly 50k lines of Next.js frontend and custom component library).
  - One useMemo, which is possibly unnecessary.
  - 30 useCallbacks. Mostly related to debouncing and some form input horrors, plus few UI obscurities.
  - Purely in application code (not the component library), there's one, and that relates to setting up some kind of polling with setTimeout. Which is kind of horrible but probably necessary right now.
- Many devs don’t have a good sense of what’s an expensive computation. Most computations don’t need useMemo—Same for useCallback. They have their uses in rare scenarios, but 95% of the time it’s better to just render.

- ## 个人觉得比较理想的非受控表单验证和定义
- https://twitter.com/__oQuery/status/1711301515707810123
- 非受控会不会存在很多校验逻辑都得手动处理
- 非受控的场景太局限了，日常开发中占比百分之 10 都不到。

- ## In React, I group related state into one useState. Here’s why
- https://twitter.com/housecor/status/1711362678696874369
  - ✅Requires less code.
  - ✅Makes it easy to send to the server.
  - ✅Can create a single onChange handler that sets the relevant property.
  - ✅Clarifies the relationship between fields, which makes the code easier to understand. These values represent something. What is the name of the "thing" they represent, together? Grouping state answers this important question.
- Just one tiny step away from useReducer
- 如果 react 中有多个状态需要存储，为了简单省事，我一般都是用简化版 useReducer

- I personally dislike that approach because it makes updating the state more complicated. You must always remember to include or spread the other properties, and you lose the built-in React feature that prevents re-rendering when the state remains unchanged.

- Also using this, although it seems this pattern is not super popular People either use multiple useState, or one useReducer. I use useState with objects all the time and I'm fine.

- ## How many React perf problems are in this block?
- https://twitter.com/jasonlaster11/status/1697740863588417641
  - setState inside for-loop of useEffect
- Alright I’m seeing two: the dependency array obviously and the fact that if your run in StrictMode you’re going to dispatch twice. What else am I missing ?
  - You got it. It’s also super scary.
- What’s the right way to do something like this
  - multi dispatch in an effect with no dep array is bad

- ## Is the tuple returned from useState referentially stable?
- https://twitter.com/TkDodo/status/1694608330063245510
  - do I need to go through destruct valueAndSetter, do useMemo that creates value & pass that?

```typescript
const valueAndSetter = React.useState(initialValue);

<MyContext.Provider value={valueAndSetter}>
```

- useState on rerenders calls useReducer, that calls useReducerImp and this is the only return statement in this function, it returns a fresh tuple each time
  - updateReducerImpl
  - https://github.com/facebook/react/blob/main/packages/react-reconciler/src/ReactFiberHooks.js

- So it means in order to put a state value and its getter into the same react context and have it stable, I need to destruct, useMemo to create another tuple or object, and then pass that? Seems a bit tedious

- The getter is not. I wrap it in useMemo every time. 
  - The setter is but if you pass them like that I think it’s gonna be recalculated. You need to do exactly what you said.

- ## React could significantly improve by including a built-in `useDescendants` hook. 
- https://twitter.com/diegohaz/status/1689699208238923776
  - This would operate much like `useContext` , supporting SSR, but bottom-up. 
- The existing userland solutions are far from ideal.
- Generally, the current solutions require a register function that is passed down. Descendants then invoke this function using useEffect, which means it doesn't execute on the server.
- Additionally, maintaining the correct order of descendants is challenging. For example, if a new element is lazily inserted in the middle of the list, it will be registered last. You must either re-register all descendants with each render or inspect the DOM order.
- In Ariakit, the issue is resolved by passing a register function down and comparing the DOM order. This is what the `Collection` component does

- Yes! This is one of the hardest problems for library developers in React. Last I heard @sophiebits was thinking about the problem space.
  - https://github.com/reach/reach-ui/tree/dev/packages/descendants

- Unity basically works like this, I agree it's much better than the current context situation.

- I've come to terms with the situation that it'll never be supported and I just have to pass content as props so the component can do whatever it wants with the prop and then render. not clean but no magic

- 
- 
- 

- ## Do you know of a resource that demonstrate when #React Hooks / ref callbacks are called and in what order when: [mounting/ unmounting], [suspending, resolved], 
- https://twitter.com/SCooperDev/status/1686793459942780930
  - And same with StrictMode. 
- [Timeline of a React Component With Hooks](https://julesblom.com/writing/react-hook-component-timeline)

- ## I just spent a few hours debugging an issue and the root cause surprised me: React replaces the `value` setter on `<input>` with an (intentionally) incorrect implementation.
- https://mastodon.social/@developit/110753572938750564
  - `node.value = toString(getToStringValue(value));`

- ## Today we run into a fun case with concurrent React 18.
- https://twitter.com/oleg008/status/1679857963714899970
  - We had a useEffect that was sometimes not running. 
  - Turned out by throttling CPU it can be made reliably reproducible.
  - Turns out you can't rely on useEffect dependencies to run something. 
- Yes, that's why they do flushSync in v4 of react-use-websocket
  - Basically it's a feature, not a bug, it batches setState by default so you can't rely that you setState will cause a re-render
  - [Introduction to React v18 automatic batch updates and flushSync | by Uday Hiwarale | JsPoint | Medium](https://medium.com/jspoint/introduction-to-react-v18-automatic-batch-updates-and-flushsync-9ab9e6c76f0d)
- 
- 
- 

- ## Situation: Multiple teams are collaborating to create a single, big React app. How would you handle it?
- https://twitter.com/housecor/status/1659618313624797186

- ## TIL: console.log in React render doesn't mean a component will be really rendered. Put console.log to useEffect to check whether a render happens.
- https://twitter.com/evoluhq/status/1608253814099820544

- Did you know? useReducer and useState behave differently in React 18. So, preferring useState that can optimize more makes sense when useReducer isn't necessary. useState works for most cases even with _reducer_ 
  - https://twitter.com/dai_shi/status/1534170089981100032

- ## 💡 React tip: I think most implementations of `usePrevious` will write to a ref in an effect and return it, but the rules of react advise us to not read refs during render.
- https://twitter.com/TkDodo/status/1653418107103264774
  - I know it looks weird, but calling `setState` during render (guarded by an `if` to avoid infinite loops) is actually the recommended way.
- React will instantly stop the render cycle when it sees a `setState` and will re-run it. This only works for updating state from within the same component. It's better than `useEffect` because the render hasn't been committed to the DOM yet.
- Why you shouldn't read from refs during rendering is also documented
  - Do not write or read `ref.current` during rendering, except for initialization. This makes your component’s behavior unpredictable.
- It is so counter intuitive to use setState in render ... Like, it totally breaks the pure functional concept of "UI as State". It is really hard to reason about that
  - Agree, but it's probably better than the alternatives. We might need to unlearn a bunch of things though, and we shouldn't need this regularly. @dan_abramov also suggests to not hide these in custom hooks

- second implementation adds extra re-render, while the first one is not or am i missing something? this could be serious difference for heavy/repeated components.
  - Yes, they instantly stop and restart rendering shallowly, so they are not for free, but better than calling setState in useEffect b/c that re-renders everything way too late.
  - The ref solution is "wrong" because it reads from refs during render, which is "forbidden" in terms of react component purity. Things might get unpredictable with concurrent features if you do that.

- I didn't think about this closely, but you might want to consider:
  - const [[curr, prev], setState] = useState<[T, T | null])([value, null])
  - Yeah you can put it into one state object or array, but since updates are batched together it doesn't really matter much imo
- Also, an overengineered version replacing two `useState`s with a single `useReducer`

- i’ve come to see this Hook as a bad idea. what does “previous” mean exactly? it depends on what the code is trying to do. is it the previous value seen by the component? previous value seen by the user? i suggest removing usePrevious altogether and writing it plainly.

- 
- 
- 

- ## Problem: You want to reset React state when a component’s props change.
- https://twitter.com/housecor/status/1652641989773410306
  - Solution: Change the component’s `key` when the props change. 
- Why not use useEffect?
  - Because resetting state via useEffect is error prone. As new state is added, someone may forget to update the useEffect call.
  - Warning: If the component tree is expensive to render, consider resetting state via useEffect instead.

- ## React Suspense should have a minimum delay (~250ms) before showing its children if they're not resolved immediately to avoid fallback flashes.
- https://twitter.com/diegohaz/status/1648585529716269056
  - What's the current solution for this issue?
- This is actually a bug in React currently. 
  - React will throttle the content from appearing for 500ms after showing a fallback but because of the bug it doesn’t do this if there are no more fallbacks in the rest of the tree. Should be fixed soon.
- Oh, nice! Although I think 500ms may be too much.
  - Apparently backed by some user research at Facebook, but I feel like there are always gonna be scenarios where you wanna tweak it
- css [Fix flicker on search by gaearon](https://github.com/bholmesdev/simple-rsc/pull/2)
- 
- 
- 

What's the current solution for this issue?

- ## Next version of @preactjs DevTools will display which exact hook caused a component to update. 
- https://twitter.com/marvinhagemeist/status/1632341790073270276
  - Previously it would just display "Hooks changed" and not say which of them did.

- ## snapshot lifecycle is still missing after all these years, keeping classes on unnecessary life support
- https://twitter.com/mattgperry/status/1610957981956427781
- Could u give a example that only snapshot can do while hooks can't? 
  - Any layout animations are impossible without this lifecycle method
- I was wondering if the new useInsertionEffect hook could be used for this? As it runs before any DOM mutation.
  - No this would be very unsafe. The problem is this hook is intended for inserting CSS. So mutations are actively taking place and then interleaving a bunch of reads in there so you’d be triggering layout thrashing for a bunch of potentially incorrect measurements
- 
- 

- ## for years i needed a setState that affects the view without causing render.
- https://twitter.com/0xca0a/status/1602037455577817091
- Seems like useSignal react doesn’t have (yet?)
  - prob the same, a transient binding into a view. i wish they'd see how important it is, but fear they'll go off the mark. every time it came up, the discussion steered into upcoming animation primitives, but has little to do with animation. i hope they're not overthinking it.
- why not just `ref.current` ? because refs don't have reconciling knowledge. for instance 0 => "0px" is something the reconciler knows how to do. tools and eco systems can only exist around features like this if they're platform neutral.

```typescript
const [bind, set] = useTransientState(0)

useEffect(() => {
  let r = () => (
    requestAnimationFrame(r), 
    set(v => v + 0.1)
  )
  r()
}

<div style={{ left: bind }} />

```

- ## Has anyone ever investigate the cost of React context "at scale" - e.g. if most components are wrapped in Context is that a performance pitfall?
- https://twitter.com/al_hinds/status/1535399948812173312
  - I'm exploring imposed constraints disallowing events/className/style/ref as component API for DS composition either explicitly (render props) or implicitly (clone element). Some API would still exist for necessity of consumer API (ref/events) but the DS wouldn't use.
- I can see the use of context being relevant for certain props like an appearance. But wholesale unsure.

- ## React tip: if you have an effect that needs to be executed when your app starts, it's definitely okay to execute it *outside* the component, and *not* in useEffect().
- https://twitter.com/DavidKPiano/status/1533798980596940800
  - This is especially true if the effect should only execute once, which is an unavoidable constraint sometimes.
  - 将effect逻辑写在 if( typeof window !== undefined) { auth() }
  - Note: this is a viable option if you are using React. StrictMode and/or you have start-up effects that need to run once and only once. 
  - You can make this self-contained and a bit more testable by wrapping it in a function
- Im not sure I like this, useEffect seems decent for executing side effects.
  - The side effect outside the component feels a lot less isolated and something that could leak into the rest of the code
- This is only true for root component, which is a very specific case. For the sake of consistency I'm not sure it's worth having a specific way of handling on-mount effects differently for root and non-root components.

- ## We want div ref prop to accept both `Ref<Div>` & `Ref<Element>` .
- https://twitter.com/sebastienlorber/status/1533799595045789698
  - Use setters/getters instead of an object attribute 
  - This gives the opportunity to "split" the ref type into 2 distinct types: one covariant and one contravariant
  - The div ref prop could then accept `ReactRefSetter<HTMLElement>`

- ## So what’s the today way of code splitting React components with beefy dependencies? Like if I have a component that uses mapbox and that I don’t want that to be part of the initial bundle size
- https://twitter.com/steveruizok/status/1534067957441171457
- You can wrap it in a component and then make that component lazy - you can also use dynamic imports on the module itself you're wrapping

- ## Did you know? useReducer and useState behave differently in React 18. 
- https://twitter.com/dai_shi/status/1534170089981100032
  - So, preferring useState that can optimize more makes sense when useReducer isn't necessary. 
  - useState works for most cases even with _reducer_ 
  - https://codesandbox.io/s/jolly-haibt-qqykok?file=/src/App.js

- One thing that’s notable is that useReducer is strictly more powerful (which can lead to fewer optimizations). It can do something that no third party nor useState can. It can respond to changes to a parent in the same batch, has already been queued or happens at higher pri.
  - Yes, some of my libraries extensively use such useReducer feature, namely use-context-selector and jotai.

- Interesting! Is that a difference in @preactjs since it uses useReducer for useState internally?
  - You can implement useState using useReducer since semantically it's a subset. However, I think preact doesn't implement this particular semantic because the reducer is eagerly evaluated so updating the reducer's input in the same batch doesn't work in preact.

- ## Here's how useAbortSignal is implemented. This is possible because React no longer warns about setting state of unmounted components.
- https://twitter.com/dai_shi/status/1529413104505073664

- ## We've told people for _years_ not to put non-serializable values like class instances into Redux, b/c it may cause issues with the DevTools + other problems.
- https://twitter.com/acemarke/status/1530191105836335104

- What are your issues exactly with unserializable data in this case?
  - Specifically: Replay's codebase is 80% a copy-paste of the FF DevTools. 
  - This uses classes as abstractions for DOM nodes and displayable values - `NodeFront`,                                                                     `ValueFront`,                                                                     `Pause`, etc. 
  - We currently parse JSON and instantiate those classes, _then_ put them into Redux.
  - The Replay codebase started with very legacy Redux patterns (hand-written reducers, etc), and no Redux DevTools integration. When I added the DevTools setup, that began to choke on the class instances. So, I had to sanitize those out from being sent to the DevTools.
  - I've been modernizing our reducers to RTK's `createSlice`, which uses Immer. Immer recursively freezes all values by default. Unfortunately, those `SomeFront` instances are mutable, and _do_ get updated later. This now causes "can't update read-only field X" errors
  - As a hack workaround, I had to pre-freeze the top-level array of items being put into the reducer, so that Immer won't recursively freeze the values inside.

- Alternative: onSubmit in your component, have it do your http://axios.post or fetch or whatever, and have the callbacks from it dispatch actions.
  - Best practice: treat everything as immutable. Create new structs/objects/types whenever you want to change something inside it.

- How would you model an abortable async call with only serializable types in Redux?
  - Include a `signal` option in your fetch from an AbortController. Attach an event handler to your signal which dispatches an action when/if it's cancelled.

- Yep! Treat redux like a REST api. Same rules apply. If you need fancy class stuff, pass the serialized values into the constructor of said fancy class when you need it.
  - Bonus: way more flexibility as you can pass those values to many different types of fancy classes. You’re not stuck with that one implementation and instance.

- Time for [Symbol.serialize], [Symbol.deserialize], [Symbol.comparator] and [Symbol.hash] to be added alongside [Symbol.iterator].

- ## Does it make sense to use the new useInsertionEffect() in React-Helmet to update doc title/description?
- https://twitter.com/sebastienlorber/status/1530180431475265537
  - It’s unclear how it’ll interact with offscreen atm and it would likely mean that it gets inserted early for optimistic rendering which would update the title before you got there. In general I’d recommend everyone to not use it, unless it’s a `<style>` insertion library.

- ## Syntax Highlighting - I have found this to be the easiest for syntax highlighting in react
- https://twitter.com/theadamaho/status/1527753778384064513
  - You can create your own theme as well. Then just pass the component to the MDXProvider as the `pre` component.

- Big fan of this package! Changing the theme is as easy as copy-replace a css file and there are tons of themes to choose from (most popular VS Code themes included)
  - https://github.com/FormidableLabs/prism-react-renderer/tree/master/src/themes

- ## I really like React. I think it's a perfectly capable UI rendering library that can interact with my app logic (data, states, transitions, effects, etc.) that I keep *outside* of React as much as I can.
- https://twitter.com/DavidKPiano/status/1525880368221589509
  - Yeah, I feel that too. React is more like a UI programming language, it's too low-level to do everything in it. We need proper design patterns that work on top of it for easy app development.

- ## React tip: if you need to access an element ref during render, use useState instead of useRef.
- https://twitter.com/diegohaz/status/1525478538580676608
  - 用state中保存ref要深入分析利弊
  - This is a valid approach for those who are asking. It's especially helpful when you need to fire effects for conditionally rendered elements. This wouldn't work properly if we were using useRef.

- ## It's been *very* annoying to debug certain things with React. StrictMode on. 
- https://twitter.com/tannerlinsley/status/1525120888777060352
  - It's wonderful for catching concurrency weirdness, but the fact that it suppresses console logs (yes, you read that right) is next-level gaslighting.

- ## where can you cause side effects
- https://twitter.com/DavidKPiano/status/1523396827529490432
  - The best "solution" to all of this is to follow the React doc's advice:
  - Put effects in event handlers
  - Render-as-you-fetch using Suspense
  - Only use the useEffect() hook as a *last resort*, or for synchronization

- ## React hooks tip: Prefer primitives in dependency arrays. Doing so helps avoid needless re-runs.
- https://twitter.com/housecor/status/1522914348695445505
  - The dependency array declares when a useEffect should re-run. So if I pass an entire object into the array, the useEffect will re-run anytime that object's identity changes.
  - To fix, I pass only the string I need as a dependency to useEffect.
- Is it recommended to use optional chaining in the dependency array? Like [user?.name]
  - No since it only depends on name in this case
- Good tip ! we can also directly use the destructed `name`

- ## I'm thinking about adding State components to Ariakit. This actually makes a lot of sense, given that all modules expose both component and hook APIs. What do you think?
- https://twitter.com/diegohaz/status/1521387103455744000
  - Downside: you often need to access properties from the state value (like `combobox.matches` ). 
  - The state component could support render props (just as other Ariakit components). But that would be a worse DX, I think.

- ## Using `useReducer` to manage one-way boolean state has become one of my favourite tricks lately.
- https://twitter.com/markdalgleish/status/1521304112738217984
  - const [isEnabled, enable] = useReducer(()=>true, false)

- const [on, toggle] = useReducer(s => !s, false)

- ## when you compose into components. Which one looks better now?
- https://twitter.com/RyanCarniato/status/1519461122390118400
- React wins all the time, by virtue of not requiring to learn another “language” (yes, there’s JSX, but it’s much thinner than the rest). It’s just too bad that React’s rendering and reactivity models are so bad. It’s one of @solid_js ’ appeal: feels like React, but very different.

- ## in react, i often find myself wanting a non-reactive way to access a value. 
- https://twitter.com/_paulshen/status/1519711253739933698
  - what if there was a stable getter for the last committed state?
- react-usestateref does just that 🙂

- ## useSyncRef: this is a react hook util i use a lot in my code. let me know if there's a better way!
- https://twitter.com/_paulshen/status/1519911984170381312
- What's the difference between using `useLayoutEffect` and just using `ref.current = value` here ?
  - iiuc, `ref.current = value` isn't safe for concurrent features because render != commit
- Something minor that you or others may encounter with `useLayoutEffect` instead of `useEffect` is that React will warn you during server rendering (because it assumes that the visual result might be broken without invoking layout effects immediately after the markup is painted).

- ## In React's development mode, when a memoized callback is passed via props (e.g. onPointerMove), React will still create a new event listener each time an event fires. Why?
- https://twitter.com/steveruizok/status/1521123775491756032
  - All but the most recent of these listeners can be garbage collected, so it's not adding new listeners each time. )(And yeah, I know I shouldn't have the performance tab open while in development mode.)
- in development mode react uses a technique of raising a fake event (and immediately handling it) to wrap user code (like handlers and renders) so that if it throws, the browser reports it as an uncaught error despite it being technically caught. at least from what i remember
  - those fake event listeners are immediately removed but will show up in profiling so like you said, profiling in development mode won’t be representative
  - specifically this preserves the DevTools “pause on uncaught exceptions” feature despite us technically catching the error. 

- ## To avoid React 18's mount, unmount, remount in Strict mode, @niallcrosby created a small useEffectOnce hook.
- https://blog.ag-grid.com/avoiding-react-18-double-mount/
  - React 18 introduced a huge breaking change, when in Strict Mode, all components mount and unmount, then mount again
  - this means a useEffect() with zero dependencies will be executed twice.

- ## what are the main advantages of Radix UI compared to Headless UI ?
- https://twitter.com/danigonlinea/status/1488863027898236943
  - More Components 
  - Better API imo
  - Radix was actually easier to style with TailwindCSS
- The only thing that was not on Radix UI was a Transition component
  - what are you doing that required the Transition component? keen to understand use-cases that our Presence component (for CSS animation) doesn't handle.
  - Our toast component used to mount on DOM with a transition, now I hide and show it with an animation. I’m not sure whether attributes like `aria-live` makes sense as this component is in the DOM always. And I also like props like enterFrom for transitions which accepts classes

- https://twitter.com/haritssr/status/1474743842540691457
  - The coolest part about headless libraries is how well they can work together. Opinionated styling limits your possibilities whereas using something like radix and headlessui together feels like they were made for each other.
  - So you combined Radix UI primitive with Headless UI Transition ?
  - Exactly

- ## React + TypeScript tip: No need to import DOM event handler types
- https://twitter.com/sebastienlorber/status/1512420374201446405
- Please, NO. This is bad... Use typescript to express the type with pick, and not repeat onChange 4 times. Adding a new props is also trivial!
  - This is tkind of the same, both have use-cases. Sometimes you need the type for an individual hander, not as props (cf meme in the 2nd tweet with const handleChange)

- ## The debate atm is trying to figure out how to design a hooks API that supports fetching multiple items within one component in parallel, without it turning into a waterfall accidentally.
- https://twitter.com/acemarke/status/1507741160839786502
- U need to read a batch to trigger a batch request (to avoid waterfall) or start requests elsewhere and only suspend in your hook
  - that's how we do it, too. for instance useTexture in drei
  - another possibility is preload

- ## This is how I wish react hooks worked. Dep tracking built in and the ability to opt out is manual.
- https://twitter.com/tannerlinsley/status/1502116674689925123
  - 尝试去掉deps array
- you driving React with Solid's "signals" logic?

- ## react elements的props传递写法
- https://twitter.com/tannerlinsley/status/1499773428739416068
  - `<Comp1 { ...{ ...defaultProps, foo, bar, ...overrideProps } } />` 展开语法
- This opinion is going to be even more divisive, but you can't convince me it's not even better:
  - React.createElement(SomeComponent, { ...defaultProps, foo, bar, something: true, otherProps: someValue, ...overrideProps })
  - It's better in regards to the props, but way worse when you start nesting those calls. JSX, like XML, provides excellent readability for nesting IMO.
- It lacks some type-safety, though. If you spread props, you can pass any extra fields, even if they aren't valid.
- Svelte def got this one right.

- ## We're considering using React Elements as properties. Any downsides of doing so? 
- https://twitter.com/wcandillon/status/1500037309185540098
  - In terms of element creation/identity/performance. It seems to be the same. 
  - What are your thoughts on such API style?
- React is nothing but functions and functional composition
  - React functions take only one argument, i.e. object, with props and children as its properties.
  - Using children prop one can access children components in an array, if you dont want to name them.
  - So, I think both are same
- Quite common for us i would say. Mostly used for overriding default components or when to try to place the child at a specific spot.
- I discovered svelte and the "slots" which does that in a named way

- ## ReactNode TS type is too loose
- https://twitter.com/sebastienlorber/status/1496170761249296391
  - Suggests to create a userland StrictReactNode type 

- ## are there tools for manipulating the AST of code interactively? i'm converting `function MyComponent` to `const MyComponent` and would love to record AST operations like vim macros
- https://twitter.com/brian_wtLau/status/1494410666202984452
- What are the potential benefits of converting `function` to `const` ?
  - needed to wrap a react component with `memo` or `forwardRef`

- ## In React (and other UI frameworks), we spend a lot of time deciding where state should live.
- https://twitter.com/acemarke/status/1486359294127792131
  - Found a post that suggests using "lifetime analysis" (inspired by the Rust compiler) to decide what components own what data
  - [From Rust to TypeScript: Lifetime Analysis for React Component Architecture](https://valand.dev/blog/post/from-rust-to-typescript-lifetime-analysis)

- ## [The how and why on React’s usage of linked list in Fiber to walk the component’s tree](https://indepth.dev/posts/1007/the-how-and-why-on-reacts-usage-of-linked-list-in-fiber-to-walk-the-components-tree)

- ## I wish we could use Rust in React Native (instead of C++) but supporting Rust cross-platform has such a long tail of infrastructure issues to work out. And more popping up...
- https://twitter.com/sebmarkbage/status/1213199159840260096
  - We have a list of other blockers before we can use it. So it's not the only reason. However, if it was the only reason it would still be a blocker for quite a while longer. Who knows if it's temporary or a similar issue will happen later. Maybe one day it'll hit critical mass.
  - Any non-Apple alternative cross-platform language has to deal with Apple issues. That comes with the territory of a cross-platform ecosystem. If we, that like Rust, don't find workarounds then C++ wins in the end.
- A cross platform route could be to compile Rust to Webassembly and either embed a standalone Webassembly runtime since JavascriptCore lacks support or compile the .wasm  back to .c with wasm2c.

- ## All I want for Xmas is for React devs to stop copying props into state with useEffect.
- https://twitter.com/acemarke/status/1474221514400616502
- But should we useMemo everything instead? Or is that the same as useEffect? It's not exactly clear to me when deriving data on each re-render is worth it and when it isn't. How expensive does the calculation need to be to useMemo?
  - That's up to you to decide. Similar to use of `React.memo()` : start by just writing the code "the right way" first. Then perf profile once it's working, and see _if_ you need to optimize further.

- ## Before creating a new state variable, make sure it can't be calculated from the existing state.
- https://twitter.com/asidorenko_/status/1483473130383450114
  - "But why?" 
  - By creating a redundant state variable, you introduce a new source of truth. 
  - Now you have to maintain it to make sure it's always in sync with the other state. 
  - It's a common source of bugs. 
  - By computing data from the existing state, you avoid this problem altogether.
- Bonus points is you useMemo to derive that value
- This is a common mistake. I've seen instances of this mistake in our codebase also. We tend to introduce a new state because of the controls that come with it, but we ignore the cost it brings. If it can be derived, then derive it!

- ## Question every useEffect that tries to sync state between different states in react 
- https://twitter.com/TkDodo/status/1483888488059752452
  - be it between two useStates like here, or e.g. between local and global state / server state. 
  - That code is more complex and more error prone at the same time. It is not what effects are for!
  - i also prefer to only add primitive types to useEffect arrays. So `objProp.fooColor` instead of the whole `objProp`

- value derivated of state → useMemo (or manual calculation). what's cool in Vue (for comparison) is that the api is crystal clear (data for state, computed for memos)

- ## Today we are releasing react-freeze
- https://twitter.com/swmansion/status/1454086713719070726
- https://github.com/software-mansion-labs/react-freeze
  - Prevent React component subtrees from rendering.
  - This library allows for freezing renders of the parts of the React component tree using Suspense mechanism introduced in React 17.
  - The main use-case for this library is to avoid unnecessary re-renders for parts of the app that are not visible to the user at a given moment. 
  - It is important to note that while frozen component subtrees are replaced with a placeholder view, the actual components are not unmounted and hence their React state and corresponding native view instances are retained
  - The most prominent use case is navigation in React Native apps, which is typically follows a stack-based approach. 

- ## I don't love React anymore
- https://twitter.com/fabiospampinato/status/1451531510075564074
  - I'd like to try to write an alternative library in the future, I I really dislike that the code I use for my components doesn't look anything like the rest of the code in the codebase, and the performance is too much out of my control.
- Wishlist so far: 
  - no JSX, no compilation step, no custom event system, no className, no VDOM, no (rules of) hooks, ~no dependencies arrays, 
  - yes optional and easy imperative DOM updates, yes mutating state without executing the entire component again, yes tiny bundle size.

- ## React poll ⚛️ Referential equality is important for props attached to host JSX elements (like `<button> <div>` , etc).
- https://twitter.com/itsdouges/status/1430368254715850752
- I don't think so generally, what non-primitive values go onto DOM elements anyways? I can only think of style, not sure if React cares about referential equality for that or not.
- as only styles and events are accepted as “not strings”, with both (I hope) not triggering VDOM comparison and doing only some very local updates.

- ## How One Conditional Can Entangle Your React App
- https://betterprogramming.pub/how-one-conditional-can-entangle-your-react-app-b817aa47718a
  - 如何处理 `booleanCondition && <Comp />` 这类场景
- However, without a solid compositional or architectural plan, the result ended up being a component that could be used in a lot of different contexts, but was ultimately pretty fragile and definitely not flexible.
- Every time the common elements of this component needed to be reapplied in new contexts, additional ternaries, and conditional statements had to be added.
- There are a few different ways to abstract components, but we tend to stick to the main recommendation from the React documentation and use `children` .
- My team now considers “context flags” a code smell. 
- ## React: I keep forgetting that you can use HTML character entities such as &lt; and &gt; in JSX. No need for {'<'} and {'>'}.
- https://twitter.com/rauschma/status/1429409404210843656
- Btw: when authoring JSX I feel like we have to use `&nbsp;` more than it's really necessary.

- ## Has someone made a JSX editor yet where you can “expand” JSX tree nodes into function definitions inline?
- https://twitter.com/dan_abramov/status/1428137070388826112
  - Same for function calls, really. Just give me a nested rectangle with the source right at the callsite. Let me close/collapse it when I don’t care.
  - apparently VS Code has this ("peek definition"), it's just *not* the popup that appears on hover. The hover one is read-only.
- Doesn't VSCode already do this?

- ## Polymorphism is such a headache. So basically, remove support for `as` prop
- https://twitter.com/peduarte/status/1424032229659979778
  - Seriously considering removing it from Stitches components and offer a more explicit way to change the element type. 
  - TBH, it's a fundamental flaw with the `styled` API
  - the `as` prop was introduced as a workaround to change the node tag, since the `styled` function couples the element type with styles...
- I could find some use cases for the dynamic as prop. 
  - One that's very common is rendering different heading level tags based on a prop or context.
  - There are more specific uses like rendering a menu button as a div if it's inside a menu (that is, a sub-menu button).
- My DX is so much more greatly influenced by TS performance than by being able to do run-time polymorphism. Looking through my code, I can't find one case of `as` which I couldn't trivially switch to a static version. (Mostly just use with `Box` to create a `span` )

- ## I've been thinking a lot about the `as` prop for polymorphism lately and wondering why we all went down the road of runtime TypeScript polymorphism. 
- https://twitter.com/jjenzz/status/1423766700885954562
  - It introduces so many unnecessary complexities, bloats error messages and kills TS per
  - It dawned on me that the prop value never actually changes during runtime, we set it and forget it but still pay the TS costs. I've been racking my brain trying to think of a better way... and I think I may have something. Zero-runtime polymorphism.
- Inversion of control. The prop isn’t the problem, JSX typings are absurdly overloaded
  - indeed, when there’s no need to overload them this way. how often do you change the value of the `as` prop via state during runtime? I can’t think of one time that I’ve ever needed to do that
- Today, I think composing hooks (like useDropdownMenuItem, useDialogTrigger etc.) makes much more sense.
  - +1 to that. For the example above, we would compose the hooks for the dialog and menu item to get behaviors we want and use as to set the element as the styled button. Feels much more atomic (to me). And as a consumer, it’s more clear how the end result will look and behave.

- ## React tip: That data you're setting in state in a `useEffect` hook could probably just be derived while rendering instead.
- https://twitter.com/acemarke/status/1365874077177700361
- Similarly: in most cases, you probably don't want to sort or filter data and then put that into state.
  - Instead, store a description of _how_ to sort or filter, and then derive the final updated data while rendering
  - [DejaVu: Caching versus Memoization](https://dev.to/thekashey/dejavu-caching-versus-memoization-298n)
  - [Rendering Lists code snippets](https://blog.isquaredsoftware.com/presentations/react-redux-ts-intro-2020-12/#/34)

```JS
useEffect(() => {
  setUserCanDoThis(calculateUserPerms(user, perms));
}, [perms])

// could just be:

const userCanDoThis = calculateUserPerms(user, perms)
```

- Isn’t this the point of useMemo?
  - No. `useMemo` is an optimization for the pattern of deriving state while rendering. I'm talking about even trying to use the "derive while rendering" pattern in the first place.
- How does it know it needs to render though
- No, this is for computations derived from other state, that does not have any side-effects. An empty array in a useEffect is just for any side-effects you only want to run once.
  - If these are heavy calculations you'll run into perf problems. That's why we have useMemo.

- ## I spend a lot of time squeezing performance from React and react-three-fiber. Some quick tips:
- https://twitter.com/robhawkes/status/1420032462911049728
  - Avoid updating three.js using props
  - useMemo/React.memo are good for you
  - Chrome and React dev tools for debugging
  - Check perf in production mode
  - Try frameloop="demand"
- If you're using react-three-fiber then definitely take a look at the documentation on performance and pitfalls as there are all sorts of neat tricks.
- There are many other things to consider in regards to performance but these should set you in the right direction.
  - In general, you want to be updating things as little as possible (ideally not at all!). There are also advanced methods to explore like instancing.
- It's a myth that WebGL is slow when used with React. 
  - If you take an open mind and learn how to use react-three-fiber/@threejs then you'll be surprised at just how fast you can make things. 
  - There's also an argument that using React for this can make things even *faster*

- ## TIL: Do not use dynamic rendering with React Fragments.  
- https://twitter.com/bruno__quaresma/status/1420090688025374721
  - That makes it harder for the parser to identify what is changing/changed.

- ## redux-saga doesn't play well with Typescript. 
- https://twitter.com/cse_as/status/1418854592129941513
  - You could spend hours adding complex types & still have type errors creep in due to how the middleware works.
  - If the team has been introduced to ReduxToolkit, it might be a good time to consider switching to RTKQuery (ships with RTK)
- RTKQ can completely eliminate all the hand-written data fetching logic in your Redux apps - no more writing thunks, sagas, or loading state for API reqs!
  - RTK Query also integrates with the rest of the Redux ecosystem, including the Redux DevTools, middleware, and reducers.

- ## You can’t use hooks INSIDE callbacks, but apparently you can AS callbacks.
- https://twitter.com/erikras/status/1418481366451302403
  - const refs = http://values.map(useRef); 

- ## Tip: Use `FunctionComponent` in both frameworks to look up types.
- https://twitter.com/rauschma/status/1416372468269428739
  – [React] component: FunctionComponent, result: ReactElement, children: ReactNode
  – [Preact] component: FunctionComponent, result: VNode, children: ComponentChildren

- ## Controversial question: How do you feel about having special `"key"` and `"ref"` values displayed inline within the "props" panel?
- https://twitter.com/brian_d_vaughn/status/1415418485686087681
- "ref" yes. "key" no. 
  - Because the plan is to **eventually move "ref" to just be a prop like any other**. 
  - Where as "key" conceptually is outside the component and belong more to the parent than the child. It's also already displayed elsewhere for that reason.
- Key is related to "rendered by".
- Seeing the key helped me the other day. I appreciated it. We should also be writing functions with names so the components are named correctly in debugger.

- ## has anyone found a solution to this TS generic problem?
- https://twitter.com/sebastienlorber/status/1412784677795110914
  - Was wondering if there was a way to make it work without `any` , despite TS not having covariance/contravariance
- Use a ref function instead of a ref object
- This is just a HTMLElement vs HTMLDivElement mismatch, right?
  - yes it is, but it's on purpose because it's to build a generic hook that should hold a ref for any kind of HTML element.
  - And I don't want to force users to provide that type as explicit hooks generic
- The issue is while *you* are happy to accept any DOM node, React is not happy to have to assign your generic value to a strictly typed $ref arg for each concrete element such as div. 
  - One solution is to mimic this with a function ref 
- One solution is to mimic this with a function ref 
- Unfortunately TS doesn't allow specifying variance of type parameters
- i usually do this if i dont know the type of my component (which is usually passed as props)
 `const ref= React.useRef() as React. MutableRefObject<any>`

- Don’t give it an initial value of null, it’ll work just fine!

- ## React/Preact friends, if you were to use global components (think design system primitives), would you prefer them to be lowercase/uppercase? 
- https://twitter.com/souporserious/status/1411751597135175682
  - Imports aren't required since they are added with a babel plugin.
  - High-level goal is to describe global components that compile to any platform similar to react-primitives. 
  - Biggest difference is relying on babel rather than a reconciler so we can optimize at build time. 
  - Also, playing with no imports since these are special components
- Personally I prefer uppercase because it doesn’t confuse elements and components, but global with uppercase can get messy with tooling.
- I would recommend uppercase (importable), I think even the React team suggests that. This is coming from the TS perspective where adding primitive JSX constructor tags can be somewhat painful.

- ## Simple pattern to reduce the pain of “prop drilling”: Consider using an object instead of separate props.
- https://twitter.com/housecor/status/1410581176914530305
- From my understanding props as objects make components harder to be memoized. Other than that I think this is a good pattern.

- ## I was immediately excited when I saw React. I recognized the pain it would remove. 
- https://twitter.com/housecor/status/1409540502274334721
  ❌ Cryptic runtime errors
  ❌ Proprietary templating syntaxes
  ❌ Manual DOM manipulation
  ❌ Clunky component APIs. 
  - For me, React was (and is) a breath of fresh air
- For what it's worth, JSX was initially designed by Facebook for React. But making it a specification instead of a library was clearly the right move.

- ## Reusable React component design tip: Mimic native HTML APIs.
- https://twitter.com/housecor/status/1409221753738514437
  - Avoid `<Button label="Send" />` .
  - Prefer `<Button>Send</Button>` .
  - there's a tradeoff at play here. 
  - ✅ Accepting children is more flexible & natural.
  - ❌ Children mean less enforcement over how it's used.
  - But in my experience, replacing children with separate props is typically insufficiently flexible, and leads to clunky APIs.

- ## Use ternaries rather than && in JSX
- https://kentcdodds.com/blog/use-ternaries-rather-than-and-and-in-jsx
  - `books.length && books.map(...)` , What would happen with the above code if contacts was `[]` ? That's right! You'd render `0` !
- Because when JavaScript evaluates `0 && anything` the result will always be 0, it doesn't evaluate the right side of the `&&` .
- The solution? Use a ternary to be explicit about what you want rendered in the falsy case.

- ## Devs coming to React from templating languages like Handlebars are often surprised that JSX doesn't have built-in conditional syntax
- https://twitter.com/benmvp/status/1392257887527792640
  - [Conditional rendering in React](https://www.benmvp.com/blog/conditional-rendering-react/)
  - Well, JSX is "Just JavaScript"™ and I've seen 6️⃣ ways we can use JS to conditionally render UI in React components
- Which one should you choose? It always depends, but *in general* I do:
  - only one condition - inline logical `&&` (most popular)
  - `true/false` conditions - inline ternary
  - multiple conditions - element variables
- 1.  Element variables
  - { `resultJSX` }
  - We can conditionally assign JSX to a variable & render that variable. Can use `if-else` or `switch` statement
  - This used to be my preferred way of conditional rendering cuz I liked that it kept the JSX "clean". But I came around to the more popular options
- 2. Inline logical `&&` operator
  - { `condition && <Comp />` }
  - This works cuz the curlies ( {} ) in JSX take any JS expression. When the condition is false React renders nothing. When it's true React renders the UI
- 3. Inline ternary
  -  { `condition ? <Comp1 /> : <Comp2 />` }
  - Depending on how much UI is rendered in the `true` case, it could be hard to figure out where the `false` case starts
  - I’m in the process of swearing off (complex) ternaries. Except in trivial cases, ternaries feel like a smell that you need to extract some sub components or element variables (to at least make the ternaries easier to read). And don’t get me started on nested ternaries.
- 4. Component early return
  - This moves the conditional rendering to a single place when multiple components use this component
- 5. Helper function
  - { `renderResultJSX()` }
  - When multiple variables are needed to calculate a condition or lots of UI is conditionally rendered, we can move it to a helper func to keep everything together
  - you can even make this inline by using an IIFE
- 6. JSX control statements
  - custom `<IF></IF> <Switch> <When>` component
  - uses component syntax to write conditions. It ultimately transpiles code down to ternary statements
  - It likely won't play nice with TypeScript so I'll stick with the other solutions

- ## I haven't reached for an IIFE (immediately-invoked function expression) since the jQuery days, but I've been using it lately for embedding a switch statement into JSX in a React component, and I quite like it
- https://twitter.com/spikebrehm/status/1407102323348942850
  - It's more useful when there's >2 possible values. Much better than a nested ternary IMO.
  - 注意，如果在children的地方直接书写对象字面量，那么每次都会创建一个新对象
  - 讨论的内容大多集中在使用switch语句和多个 `condition && <Comp />` 的优缺点
  - https://github.com/tc39/proposal-pattern-matching
- Great way to workaround the constraints of JSX. Shame you're using it for a switch statement though!
- why not just create a component that returns each case instead of inlining this function which is essentially an adhoc component?
  - Sometimes wrapping isn’t what you want if a parent uses React.children.map
- this is totally a stylistic thing, but I'd rather write separate conditions. I also don't like the switch statement in general
  - I thought of this too, but it doesn’t cover a case where none of the matches have a match. Plus it’s less clear what the purpose is of those conditions. The pattern matching proposal would be dope for this sort of thing though.
  - It's a bit tedious though and using a Switch statement is certainly nicer.
- I'm still holding out hope that "do" expressions get approved

- ## To keep JSX simple, return early. Check for loading, 404s, or other errors first.
- https://twitter.com/housecor/status/1404038972700073984
- returning early avoids the need for nested ternaries, which are harder to read. 
  - And returning early means I don't need to extract the logic to a separate function merely so that I can implement an if/else (if/else isn't supported inside a return)

- ## Thinking through an interesting problem for how to model the components tree in DevTools. 
- https://twitter.com/brian_d_vaughn/status/1400843220041580546
  - The tree currently reflects a filtered view of React's (internal) Fiber tree. 
  - When React commits an update, the tree is updated by adding, removing, or reordering nodes.
  - Adding Server Components to this tree means somehow splicing in a new type of node (no backing Fiber, not part of React's internal tree). 
  - I think these nodes would be added once then skipped over during updates (unless removed via a node higher in the tree).
- There's probably an elegant way to model this but I'm still turning over the problem in my mind. I think it reduces to:
  (1) Merge two trees (client and server) into a single tree (hybrid).
  (2) Sync updates from the client tree to the hybrid tree.

- ## Playing around with a React hook that returns a component with some props pre-applied. Too hacky?
- https://twitter.com/satya164/status/1391513127431385088
- The problem is that component from the hook will reMount on every re-render of the host component
  - It won't. I'm using a ref for the component and it's never updated after the creation.
- I’ve done that for modals. It works great.
- I think styled components does something similar here.

- ## Here are the differences between component render, dom updating and painting the screen in React.
- https://twitter.com/yagopereiraaz/status/1389743940249784324
- Render: 
  - Component render method/body get called, for functional components that means Component() for classes ComponentInstance.render().
- DOM Updates: 
  - Elements instances are created you can interact with them with useLayoutEffect, but you can't yet see them on the browser.
- Browser paints: 
  - The DOM updates are finally painted on the screen and you can interact with the DOM elements via useEffect and on screen, with the UI.

- ## How to implement a zoom bar with react-three/fiber and react-three/drei?
- https://twitter.com/0xca0a/status/1389520530131324932
  - In React components can either be visual or logical, as in, components can return null/nothing. 
  - We're using LEVA here to quickly implement a re-usable zoom component that you can drop in (or out).
  - https://github.com/pmndrs/react-three-fiber/discussions/1308

- ## My favourite thing about React so far is how much time I get to spend thinking about exactly which state variables depend on other variables, 
- https://twitter.com/stevage1/status/1389032093724839943
  - and when it's safe to update them, so I don't get distracted by actually building anything.

- ## Just realised that JSX has a syntax to support generics
- https://twitter.com/wcandillon/status/1386413737263960064

```typescript
type FormValues = {
  email: string
}

<Formik<FormValues>
  initialValues={{
    email: false // TS error: boolean is not assignable to string
  }}
/>
```

- also, generic type parameters can be both explicitly defined (as in your snippet above) or inferred via arguments (props)

- ## Let’s talk about a React performance antipattern that I see in apps sometimes.
- https://twitter.com/iamakulov/status/1385230664648253443
  - Say I have two functions that I want to pass down through a context
  - How would I do that? 
- The easiest way would be with `<Provider value={{signIn,signOut}}>` .
  - this object is recreated every time AuthWrapper is rendered. 
  - Which means the context receives a new value every time.
- The easiest way to do that is to move the object out of the component
  - However, sometimes (eg if `signIn` and `signOut` come from props), that’s impossible. 
  - In that case, wrap the object with `useMemo` .
- Another (future) way to fix this might be `useContextSelector` .
  - useContextSelector is a proposed React API that lets you subscribe to a specific context’s field. 
  - This way, components rerender only when the field changes.
  - And you can use this API today, thanks to the use-context-selector library
- React.memo() (and PureComponent) help to prevent a component from rerendering when its props and state don’t change.
  - However, they don’t work with context. Every context update always rerenders all subscribed components.

- ## Have you used the useCallback() hook? Tell me why. I'd love to hear about your use case.
- https://twitter.com/brian_d_vaughn/status/1174359975600091136
- I'm using it for debouncing an autosave experience

- ## I rarely use these React performance features: `React.memo` , useCallback, useMemo
- https://twitter.com/housecor/status/1358791451665178634
  - If I have a performance issue, I usually find I made a mistake or am using a component that merely needs optimized.
- You generally don't need them unless you have an onMouseMove or onDrag listener, Or scroll/wheel
- What about when creating custom hooks? Using useCallback helps a lot
  - In theory, it can help. In practice, I find it’s typically unnecessary. 
  - If you are ever pass a function to a component you should probably wrap it in a `useCallback` . You never know what that component is going to do with that function and if they put it in a useEffect dependency array it will cause it to fire each render.
- useCallback is almost mandatory when you have to include a function as a dependency of a useEffect and you are not declaring the function inside the effect, isnt?
  - Yep, though I prefer to declare inside the effect.  That said, this tweet is about using it for performance, not identity.
- I’ve never used useCallback as a performance feature, but they carry functional semantics. If I’m defining a function that’s going to be passed to a descendant component that’s not a native element (eg div, span, button), I always use useCallback.

- ## Did you know that getSnapshotBeforeUpdate in React fires before *any* DOM mutations?
- https://twitter.com/sebmarkbage/status/1380539161690640384 
  - I.e. neither siblings nor parents have been mutated. 
  - This is an important property that avoids layout read/write thrash 
  - but if you read it, the layout hasn't been skewed by previous siblings.
  - This is useful for things like layout animations, restoring scroll position and can be used for focus management (e.g. figuring out where to move focus after something is deleted based on where it was before it got deleted).
  - There's a tradeoff though because it requires queuing mutations, which is why most other libraries don't do this. Seems tough to solve these edge cases without it though. Maybe some new DOM API could help. E.g. pausing style recalc for a while.
- So how do you do it with hooks ?
  - There’s no equivalent with hooks. I use this workaround
  - This is probably really dirty, and the definition of a hack, but since getSnapshotBeforeUpdate runs before the commit phase, maybe you could have a combination of an effectfull callback inside a useMemo hook (which also runs at the pre commit phase) and a ref

- ## I found that migration of complex(ish) class components to hooks is a great exercise to understand hooks. 
- https://twitter.com/sseraphini/status/1376892107416338441
  - I have put this as a task in the new developer onboarding process. So we update some old code, new devs to learn hooks and learn the system.
- simple components are easy to convert
  - but hard ones with ref, lifecycles, and singleton can be tricky to get right
  - the only way is to practice to figure it out all the details

- ## React people hear me out:
- https://twitter.com/lmatteis/status/1375557621789384705
  - VSCode plugin that renders components
  - Editable widgets for changing props on any component
  - The widgets are created based on TypeScript info
  - Any changes to widget are synched w/ code
  - Expose a typed style prop for free editing capabilities
- you are describing @storybookjs
  - No, changes to the knobs/controls don't alter the code, just an in-memory preview.
  - I built a POC for this a few years ago. Storybook has a dev server with access to the file system. This is a feature we’d like to add in the future, made more powerful by controls/args

- ## Every time you do async action in onClick handler or running `setState` not under React control - you probably need a batched update
- https://twitter.com/theKashey/status/1373841140860944384
- setState in react will wait for handler to finish before commiting, setState outside has no way of knowing handler, so commits immediately.
- With useState we have entered a way of "glitches" - temporal state inconsistencies.
  - If before we were "trashing layouts", now we are "trashing fibers".

- ## When creating composite React components (i.e. parent + child pairs like HTML's <select> and <option>) you can avoid exposing private props like "index" or "isFirstChild" on child elements by using context.
- https://twitter.com/markdalgleish/status/1370552733590167552
- Forgive my ignorance, perhaps I misunderstand. But what is the benefit to this other than not seeing a prop e.g. "index" as you mention. This seems on the surface over engineered and perhaps, even if a little, incurring a greater performance hit than exposing the prop.
  - If you use cloneElement instead, it means consumers are able to see the private props in the component's type signature.
  - Also, cloneElement prevents consumers from wrapping child elements with another element since you'll be cloning an element without those private props available.
- Yes, please bring more visibility to this. Several big libraries still use clone element and it's frustrating to have things break because I wrapped a component without forwarding all props. Context works great here.

- ## there's a bunch of articles that explain how React hooks are implemented, 
- https://twitter.com/acemarke/status/1369869411901992966
  - and that they're basically a linked list in memory hence the need for identical use order.
  - has anyone actually written about how hooks have "mount" and "update" impl functions internally?
- that's how hooks have differing behavior between "first render" and "all other renders" - it's different internal impl functions being called based on whether the hook already exists or not.
  - Point is I don't think I've seen any articles that try to explain that particular implementation detail and how that relates to the behavior we see externally (like `useState` accepting the initial value, then ignoring what you pass in later)

- ## use `useThemeContext/useCustomContext` instead of `useContext` .
- https://twitter.com/FarazPatankar13/status/1369013998147018752
  - Is there a reason this isn't more widely recommended? 
- When I was doing workshops that's how we taught it, too.
  - It's just the difference between thinking like a library developer or not. How much API do you want to expose?
  - In React Router we don't just give you the whole context, we only give you pieces with multiple hooks
- This plus useReducer has been my goto for state management
- just call it `useTheme` , the consumer doesn't need to worry about it being a Context as long as they are already a child of the Provider
- I personally don't like it in certain cases b/c it makes testing hard + data/logic is coupled and hard to customize.
  - Well, you could export both `ThemeContext` and `useThemeContext` for more flexibility?
- React context/hooks tip: Create a custom hook for React contexts that shows a helpful error.
  - [How to use React Context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)

- ## How would you implement this differently?
- https://twitter.com/kentcdodds/status/1367356862035718145
- Wrote this to confirm there wasn't a better way to implement the calculator component (without changing its API). It's included in my blog post
- Hah, pretty much the same, object lookup using variables is pretty underused syntax but I think it's super elegant and readable
  - Couldn't disagree more. You're adding in an extra, unnecessary layer of abstraction that moves you further away from the implementation

- ## How to write a React Component in TypeScript
- https://twitter.com/kentcdodds/status/1367830594730618885
  - There are plenty of ways to do it, here's how I recommend typing React Components
  - The point is this: there's no real benefit to using `React.FC` , but there are downsides. So don't use it.
  - [How to write a React Component in TypeScript](https://kentcdodds.com/blog/how-to-write-a-react-component-in-typescript)
- Worth mentioning that you _should_ use `React.FC` if you wish for your component to accept a permissive children type (aka any supported children). 
  - It's not common to restrict children types in my experience (although there are use-cases for that).
  - You can use `React.FC` and then add `children` with a different type to your props type and it will override the one from `React.FC` .
- One improvement I’d make is to use `interface` instead of `type` for `CalculatorProps` (or anywhere you’re modeling a JS object and don’t need a union). This is what the TypeScript team recommends.

- ##  `ComponentProps` helper type from React is indeed very helpful
- https://twitter.com/wcandillon/status/1365326333807583234
- ComponentProps accepts a component and gives you back the type of that component’s props
  - In this example his “icon” prop will accept all the values that the FeatherIcon’s “prop” accepts
  - It’s useful because it means you can declare a type that is derived from a component’s props
  - The reason derivation is good is that it causes the correct things to break and stay up to date.
  - If feather icons adds more icons, the name enum will grow and so will your icon prop. Similarly if it shrinks you will get type errors telling about it.
  - A good deal of being efficient with TypeScript is about knowing how to structure your types such that the errors appear in the most useful places!
  - Sometimes an in-line declaration does wonders for “traceability” and other times inline declarations are noise.
  - It really depends.
- Neat! My solution for the same problem was a little more hacky: `name: keyof typeof Feather.glyphMap;` .
- It really is, even if you control the underlying component it saves you having to export its props interface.
  - Gotcha: it can tempt you to use inheritance excessively when it's easy to dig into another component. In this snippet, icon could be a ReactNode instead.

- ## how to trace which component is suspending in React so I can put a Suspense wrapper around it?
- https://twitter.com/fakenickels/status/1364921351820181512
- tired: Suspense wrapper, wired: Suspenders
- debug stopping at every error since suspense is basically throwing a promise from a component?
- I *think* the dev tools might tell you what suspended.

- ## Once upon a time, there was discussion and PRs that tried to add a third "root state" argument to `combineReducers` , so that slice reducers could read other slices if available:
- https://twitter.com/acemarke/status/1363547923963863046
  - But, we finally gave up on that idea. Still feels potentially useful, though
  - [Feature Request: Allow reducers to consult global state](https://github.com/reduxjs/redux/pull/1768)
- There's been at least one time in the past where I wanted two reducers but went with only one because one of them would need access to the other's state. I can't honestly remember the exact situation though.

- ##  `<Context.Provider value={<SomeJSX />}> <Stuff /> </Context.Provider>` .
- https://twitter.com/dan_abramov/status/1363134687250636800
  - Haven’t used this pattern before, but it’s kind of neat? If you want to pass some piece of UI deeply down without passing props themselves. 
  - Sprinkle(撒，洒) useMemo on JSX node to avoid extra re-renders.
- We use this pattern in our design system. 
  - We have a 'linkComponent' prop on the provider so you can customise how links are rendered, e.g. wire them up to your router, add analytics, etc.
  - [BraidProvider](https://seek-oss.github.io/braid-design-system/components/BraidProvider/)
- May be the first time I've read a facebook dev acknowledge that we actually want to avoid extra re-renders.
  - I mean specifically in this situation (pass some context deep down). 
  - I am not proposing that one should micro-optimize every single component, which is how people tend to interpret this.
  - The rule of thumb is pretty simple — if it makes an interaction faster (as measured by profiling) then do it
- We use multiple vue apps, which the equivalent would be provide/inject, but using this makes components hard to reuse sometimes as they depend on data that sometimes isn't there. 
  - Best to keep this down to globals that are relevant to the entire app, not just a specific component.
- We do this at Stripe to make sure the correct legal text gets shown in our various signup flows. It's also handy (with some extra complexity) for implementing ReCAPTCHA.
- Isn't it just equivalent to container or layout component?
  - Yea, pretty much, although that’s usually done with props rather than Context
  - Yes. Basically a replacement of Container components suffering from prop drilling? But a neat pattern, not sure why I never thought it's possible 
- Interesting. Provider which instead of controlling data, controls rendering. 
  - So the client gets baked ui which is black box for him, the only think is to show it where or when we want.
- I have followed this pattern when I created a generic table component (wrapped in a provider). 
  - When using an instance of such a table, the developer can define different types of columns (column displaying a url link, checkbox column, date column...etc)
  - These different types were f columns are essentially jsx components I’m sending back to the table provider which then renders them as content of my `<td>` .
- Creating modals on demand through redux or context, including react elements, callback function etc. I really like it.

- ## Should You Use useMemo in React? A Benchmarked Analysis.
- https://twitter.com/tannerlinsley/status/1362119303793844226
- It's true that useMemo is not free, but IMO this article is somewhat misleading. 
  - The reason the slowdown for initial render gets so large is because this benchmark returns that huge object from useMemo (so it's being stored!) 
  - It's not algorithmic complexity but memory cost.
  - In the example with n = 5000, we have 10000 components, and each of them stores an array with 5000 objects in it. If you look at the Memory tab, this gets our page to 1GB memory usage! At that point it's not that surprising it would slow down.
  - If we return a primitive value from useMemo (e.g. result of an expensive calculation — which is what it's meant for), the perf gap almost disappears in my testing.
  - So yes, useMemo may slowdown because it uses computer memory, and holding onto 1GB might not be the best idea.
  - There is still a broader point about unnecessary useMemo being unnecessary, but the claim that it by itself causes such a drastic algorithmic slowdown on first render doesn't appear to be true. But holding onto large objects — and lots of them — does have a cost, useMemo or not.
- But using useMemo not just for a value or loop but to memoise the children when there's loads that rarely need to rerender would be super beneficial and not covered here? Also (not sure on this) but when fetching data from an API it would help (when not using some other lib).

- ## Is there still no answer to composing forwarded and internal refs in React?
- https://twitter.com/ryanflorence/status/1361519704821538820
- what is the core use case behind needing this? 
  - When you want to use the ref within your component but also want to allow component user to pass a ref
- I always just used callback refs like so.

- ## saw so many tweets about how cm and suspense are useless etc. 
- https://twitter.com/0xca0a/status/1358703189428752384
  - if you have ever tried R3F you know how it simplifies things that otherwise would cost you an arm and a leg. 
  - FE & forms will gets the same benefits, try it if you can, it's a paradigm shift. 

- ## Anyone ever used Preact without using internal state at all?
- https://twitter.com/_developit/status/1356068911263977472
  - Thinking about using an FSM for state management and then just calling `render(<App {state} />, el)` on state changes.
- Main issue is that you'll only ever be triggering whole-app renders. 
  - With state, only the subtree with changes re-renders. 
  - For a state machine approach I tend to subscribe components individually, even if all they do is call `setState({})` on themselves.
- And if you use a non-vdom library, whole app re-renders might even be cheap 
  - That depends on reference equality bailouts same as VDOM though. 
  - In both cases, a top-level rerender with entirely new data is worst-case perf.
  - There should be far fewer such checks in a sparse tree of template bindings than a full vdom tree. It would be less by the ratio of bindings to leaf DOM nodes.
  - true, assuming minimal composition of templates.

- ## I've come to believe that the base React Hooks should always be used inside of a custom hook 
- https://twitter.com/kyleshevlin/status/1354845869246476290
  - to provide encapsulation and context to the concern
  - IME, 2 things are true
  - there’s never a use of useEffect that couldn’t benefit from a good function name
  - Re: the other hooks, they almost always come grouped together, ie if your managing state, you have some callbacks to handle that state.
  - Put ‘em in custom hooks.

  - Don’t worry if the hooks are reusable, that can come later.
    - By putting all the elements related to a concern in a custom hook, you can focus on the API you want your component to use. 
    - You can hide implementation details your component doesn’t need to know.

  - [useEncapsulation or Why Your React Components Should Only Use Custom Hooks](https://kyleshevlin.com/use-encapsulation)
    - A custom hook is just a function and functions are structures we can use to encapsulate the related elements of a concern and expose an API to our function's consumer.
    - Take notice, our Component now only consumes custom hooks. 
    - Another benefit of this pattern is that dependencies quickly become obvious because they end up being arguments to our custom hooks.
    - By adding this layer of abstraction between our component and the standard React hooks, we can change the implementation of our custom hook's API without changing the component. 

- Something that could help writing components like this.
  - The hook can still live in the same file, declare it at the bottom rather than the top with a "function declaration", or attach it a static property to the component.
  - If it becomes reusable, move it to a separate file.
  - Yeah, I would never move it to a new file _unless_ it was intentionally reusable.

- ## Do you push a new history entry onto the stack? Replace it?
- https://twitter.com/tannerlinsley/status/1355570411803602946
  - And on top of all of this, provide an API that feels like setState, a reducer or state machine?
  - I realize that very few apps actually ever deal with this type of router state… But still, why is it so hard.
  - Which brings me to another point, after dealing with dashboard state for a very very long time now, I am very convinced that it most closely resembles a massive tree of deterministic State machines.
  - This begs the question: should the state live in a machine and get synchronized? Or should it live in the URL?
  - From experience, when the state actually lives in the URL, it becomes very difficult to rely on read and write consistency. Then add a router abstraction in the middle?
  - 描述了很多urlstate处理的经典问题，并且没有标准答案

- ## I recently had to implement a feature where the user could download a png of a div. I came across html2canvas which did the trick perfectly
- https://twitter.com/bmullan91/status/1220659214848229378
- We did something similar to download a chart back in 2015, the result was almost the same but It did broke css a bit. 
  - At the end we preserved that approved because it was way easier to do it in the frontend than moving the logic to the backend. I recommended it.
- I did something like this but for code screenshots before I know carbon existed 

- ## Am I right in thinking StrictMode’s second render swallows console.logs?
- https://twitter.com/mattgperry/status/1352000290241859590
- Yeah, I believe they added this to not pollute the console.
- Ye, this is imho actively harmful - duplicated console.logs might be confusing at first but they dont lie and actually incentivize people to think about purity, concurrent mode etc

- ## I’ve seen React libraries that return elements as objects with $$typeof, while others return them with React.createElement. 
- https://twitter.com/jon_neal/status/1351512951337967619
  - Are there performance considerations?
- If you want to be compatible with React and Preact, publish it as JSX and let people transpile your library with their JSX pragma.
- I would be wary(谨慎的，小心的) of both approaches here. 
  - The $$typeof check will fail in environments without Symbol (react uses a numeric constant), 
  - and both could change in a minor version (they're not part of the public API).
- Though I'll say, if you genuinely need to produce cross-compatible VNodes, your codepen is pretty clever. 
  - It will have a potentially large performance impact though, since property access into Virtual DOM elements will become polymorphic instead of monomorphic.
  - Another option would be for the community to standardize on a "vdom provider" package that libraries could import, which users of a library would be required to alias to their desired implementation. 
  - All of these solutions get more difficult when you factor in state/hooks/etc.

- ## Underrated JSX feature; text interpolations without any extra syntax/quotes/whatever. So good.
- https://twitter.com/threepointone/status/1350174511883300876
- I used to hate this, but looking at it from a design perspective, 
  - this makes a ton of sense and like the issue mentions is great for internationalization
- This is something I missed when I tried using Reason React
  - And the fact that I had to google for like a fucking hour to find the correct binding in order to map over my todo list

- ## the React model of All-in-JS components where HTML and CSS live inside your JavaScript module.
- https://twitter.com/horse_js/status/959908677074513921
- HTML is okay... but CSS should not be inside JS

- ## browser's built-in form validation features are surprisingly robust. 
- https://twitter.com/housecor/status/1330871889867264004
  - Declare attributes like required, min, max, minLength, maxLength, and pattern (regex) on fields.
  - Call checkValidity() to validate. 
- indeed! React devs may forget that you don't have to do this all in JS. 
  - and it turns out that it can be quite a lot less code as well!

- ## Frontend Devs, if you were writing a new UI from scratch, would you use @reactjs or @vuejs  and why?
- https://twitter.com/SENDYYeah/status/1247568314492018688
- I'm not saying @reactjs is the best, but more to personal preference. 
  - After tried both of them for some projects, I feel react project is easier to read and to maintain.
  - JSX force us to put everything in a single language, JS, CSS, HTML all in JS, the thing that scares newcomers
  - After months of grieve for the lost of directives in ReactJS, I tried vuejs and maintenance a project
  - I understand that JSX fits me better than Vue approach, 

    - JSX makes me able to read logic easier, 
    - you put everything **explicitly**, any logic, even for CSS styling on your components.

  - With ReactJS, you have to read everything in JS (or TS), no directives, no binding, nothing to hide
  - some vue solutions makes us easier, but sometimes it took longer to code

    - react be like "tell your JS to return a component with this"
    - vue "tell your component to do a JS work and return a new component with this"

- ## I almost get the perception on here that react it's like the new "jQuery" now._202008
- https://twitter.com/CerovacBogdan/status/1299308881521377280
  - Is it assumed that most FE devs know a bit?
- I was on and off and now again a bit on, 
  - but I would not dare to say that it is the new jQuery as it requires much more specific knowledge (JSX one of them). 
  - But yes - Wordpress does use it - and with it's market share - it has the potential to become new jQuery
- When I was starting out, it was the go-to once you knew some fundamentals. 
  - But, it seems people don't spend as much time with libraries now and jump straight into frameworks like React
  - Did JSX pose a hurdle(障碍；栏杆)?

    - Agree :) I try to be vanilla now, jQuery was golden for cross-browser DOM mngmt. and abundance of plugins. 
    - Maybe if we look at React in that light... I see the benefits of ALL-in-JS in complex context that needs code-reusing etc. 
    - but for simpler "doc's" I still prefer raw HTML+JS

- ## list: How do you manage API calls in react_202101
- https://twitter.com/_Adyasha8105_/status/1347978564251963392
  - Using a library like react-query 
  - or your own custom hooks 
  - or just plain fetch/Axios calls in components or inactions? 
  - What's the best way to go forward
- Short answer: react-query
  - Long answer: Axios was my base. 
  - I found state is kinda tricky when there’s too many request or components with CRUD operations (introduced xstate). 
  - then I realized a cache could help to improve UX (added react-query) 🙃. 
  - Start simple then build up
- I also created my own generic http class wrapper so if I want to swap between fetch, axios or something else, I won’t have to change in multiple places. 
  - have not tried React Query but it looks cool...
  - I just always am cautious of abstraction lib dependencies.
- I have not worked much in React But Axios did the work I needed
- I build a gateway per api 
  - so that all calls to the api go through one entity (in case the contract changes) and it extends a class that makes the actual calls with fetch. 
  - I use redux actions to call the gateway method. Will look at react-query though!

- ## JSX is an abomination(令人厌恶的事物).
- https://twitter.com/justinfagnani/status/1246514699341983744
  - You can't write a literal <, because that opens a tag, 
  - but you can't write &lt; either because JSX isn't HTML and doesn't support entities. 
  - You also can't write HTML comments, or use `<template>` .
  - JSX is clearly unsuitable as a general way to write HTML in JS.
- You can't event put a < inside of a string inside a JSX expression
- There are alternative ways of expressing DOM in JS though. For example: domz
- Recently ran into not being able to use `<template>` in React/Angular. 
  - Workaround is to use `dangerouslySetInnerHtml/[innerHTML]` . 
  - After that make sure that the sanitizer does not strip your Custom Elements
- JSX isn’t even made to “write HTML in JS”

- [My 5 Tips in Building a Design System](https://twitter.com/frostyweather/status/1087380930417840128):
  1. Build components without business logic, but hooks for data.
  2. Build UI components for/from products, not in the abstract
  3. Should be easy to onboard/understand
  4. Create code guidelines early on
  5. Strong processes involved = strong DS
  - I would add early and often 'collaboration' with the dev team to stay aligned.

- ## Unit testing a react component is a waste of time in 99% 
- https://twitter.com/oleg008/status/1235358013495676928
- here is why
  - React components are useless without React or a compatible runtime. 

    - You can see components also as "plugins" which together with the runtime make a framework and then an application.

  - React handles a lot of its side effects like hooks and rendering. 

    - Without all those things, most of the component code should be pretty dumb. 
    - If it's not, you should extract that logic into a separate function.

  - Once all your components are pretty dumb, there is no point in unit testing them, because it's like testing a configuration.

    - What you should be testing though if your component works as expected for an end-user.
    - which means you need functional or e2e tests. 
    - Depending on your use case it can be cypress and co, jest with JSDOM  or anything else that renders your component using React and validates the result same way a consumer would do.

  - Snapshot tests are rarely useful because they test only an HTML output of a component, 

    - which is ok if your user actually consumes HTML as a text, 
    - but most of the time this is not the case.
    - Your typical users in the browser see a DOM rendered presentation of your components, which includes all side effects, interactions and transitions and you are not testing those with snapshots.

- Unit tests are useless 99% of the time. It has nothing to do with react
  - I disagree with that. They are great for complicated functions.

    1. Making clear how they are supposed to be used
    2. Ensuring they work for the intended use cases.

  - Obviously no guaranties outside the unit bu thats expected. React components are a special case.
