---
title: lib-state-signal-community
tags: [community, signal, state]
created: 2023-04-07T04:09:44.063Z
modified: 2023-04-07T04:09:54.488Z
---

# lib-state-signal-community

# guide

- tips
  - signals和immutable的mental model有很大不同
  - 实现协作的案例更多基于immutable，但基于proxy的实现也有，如o-spreadsheet
  - [介绍 Preact Signals - 掘金](https://juejin.cn/post/7144373510016598023)

- preactjs-signals的实现不基于proxy
  - tldraw-signia也不基于
  - [Signal Boosting | Preact](https://preactjs.com/blog/signal-boosting/)
    - Turns out Preact's signals are not Proxy-based (as Vue's refs), they are get/set based. 
    - I guess that's because they are not deeply reactive. 

- mobx
  - [By default, MobX uses proxies to make arrays and plain objects observable](https://mobx.js.org/configuration.html)
    - [Object.defineProperty and useProxies: "ifavailable"](https://github.com/mobxjs/mobx/issues/2876)
    - [Proposal: MobX 6: drop decorators,😱unify ES5 and proxy implementations](https://github.com/mobxjs/mobx/issues/2325)

- immer-core/plugin都基于proxy
# discuss-stars
- ## 

- ## Here is a little demo I whipped up using Preact Signals - can be used without a framework!
- https://twitter.com/wesbos/status/1650589973215584260
  - Here is a little demo I whipped up(匆匆做) using Preact Signals - can be used without a framework!

```JS
const createState = (s) => {
  const ls = new Set();
  const n = (k, v) => { ls.forEach(l => l(k, v, s)) };
  const subscribe = (l) => { ls.add(l); return () => { ls.delete(l) } };
  const p = new Proxy(s, {
    set: (t, k, v) => {
      t[k] = v;
      n(k, v);
      return true;
    }
  });

  return { state: p, subscribe, listeners: ls }
}

// no need for setState()
const state1 = createState({ ilhan: 42, deniz: 10 });
state1.subscribe((k, v) => { if (k === 'ilhan') { console.log("ilhan set to", v) } })
state1.state.ilhan = 44; // ilhan set to 44
state1.state.deniz = 11; // nothing
```

- ## React mobx is still observable but the way its set up feels a bit like signals. Is that right?
- https://twitter.com/grunin_ya/status/1638614039659003905
- No, Mobx's observables are signals.
- Mobx Author: Correct, MobX is signal based, using the term observables has created quite some confusion :) (as people pointed out at the time! but in the literature I was basing upon it were called observables, which was a moot(有争议的问题) point, lesson learned)
- On the upside, the term signal didn't exist at that point yet at that point (and atoms was of my own making iirc), so MobX is basically signals-avant-la-lettre :) 前卫的
  - The meaning of AVANT LA LETTRE is before the letter : before the (specified) word or concept existed.

- ## what are the blockers/downsides that are preventing you from using/trying Vue?
- https://twitter.com/0xca0a/status/1567846559655632896
- signal is not new, it's lie mobx valtio et al, the interesting bit and why it went viral is because it cleverly hacks the reconciler. i wouldn't want a proxy near a big project, and i wouldn't want a framework to conform around one. i want react to be immutable that's all.

- ## Why @preactjs, @solid_js and @QwikDev recommend using Context API to share Signals/Stores?
- https://twitter.com/_aantipov/status/1634832927556276226
  - Why not simply export/import them similar to Zustand and deprecate Context?
  - for instance, Vue seems to work just fine with exported/imported reactive data.
- SSR and testing. It's easier to pass a mocked thing via context than to make a side-effecting import.
- Do you SSR? The concern mostly around leaking global state across requests (different users). That being said if one were not allowed to write to it during SSR it'd be fine. But then it couldn't hold the data you fetched during SSR.
- What is exported (es module) can not be deleted whereas a context can be cleaned up.
  - Hmm, the context object itself is usually created and exported as well. Also, if you use Context to hold global state and define on the top of the tree, then it will always be there. Same as with exported Signals. Zustand seems to work just fine with exported atomic stores.
- I use both methods in Svelte depending on the use case.
  - Context is decoupled since any parent can define its content.
  - Importing is hard coupling which makes sense when you have complex logic in a separate file.

# discuss
- ## 

- ## Why are people so obsessed with signals right now
- https://twitter.com/m1nd_killer/status/1629530182636781568
- It is same technology that we had 2 years ago, as immer, just in new format
- Immer is amazing, but pretty different. Mobx on the other hand (by the same creator) would be the much closer comparison
- I mean both technologies let you make mutations with Proxy under the hood. And signals just a new way to solve the same issue.
  - But mobx more about observables and huge stores.
  - Anyway, mutating with proxy let make code easier to read

- ## I don’t think Vue 3 refs should be used as an example of “Proxy based reactivity” - only deep access is tracked using Proxies
- https://twitter.com/youyuxi/status/1635416467645829120
  - the .value itself is a simple getter, very much like Preact / Qwik signals. 
  - The shallow version of it (shallowRef) is identical to signals
- Why have proxies a bad rep. Seems like people don't like to have all the reactivity based on them, any reason for this?
  - Performance.

- ## I keep wondering if there's some way to speed up React-Redux via signals/proxies/etc.
- https://twitter.com/acemarke/status/1628103434577510400
  - @dai_shi had a POC PR that added a `useTrackedState` hook a while back
- Immutability and signals are like water an oil imo, they don't mix well together.
- The primary speedups come from lazy subscriptions and diff bypass. It might be possible to get the former, but very unlikely the latter.

- ## Signals are cool but don't be fooled, 
- https://twitter.com/PeerReynders/status/1568754562739195906
  - they are observables and have been used by client-side frameworks on the web for *at least* 12 years if not longer. If you look at their implementations they are more or less the same.
- Knockout.js (2010) is the most frequently referenced.
  - Knockout (2010) adopted the overloaded function style (from overloaded C++ accessor/mutator methods) to represent a reactively updated value (because IE didn't support getter and setter object properties) which was created by the `ko.observable` factory function.
- "java.util. Observable" was part of Java 1.0 (1996)
- Observables are more like streams because they emit events/values at specific points in time. 
  - Signals can be always be queried for their latest updated value. 
  - (in ReactiveX only a BehaviorSubject caches that last emitted item) 
- 💡 In the Observer Pattern the `Subject` is only capable of invoking `update` on the `Observer` which mirrors how a ReactiveX (2011) `Observable` invokes `next` on `Observer` ; neither is query-able (while signals are).
  - An Rx `Observable` supports at most one `Observer` though.

- ## Today's vibe: Mutable data structures are 💯. 
- https://twitter.com/tannerlinsley/status/1648722093222273024
  - I can sympathize with some decisions to go immutable (esp around React's change-detection evolution), 
  - but the deeper I get into performant/predictable/simple code, the more I resent the abstraction, hence Signals 

- Any time I'm in my framework-agnostic layer for @tan_stack , I just get so sick of all of the indirection around reactivity and state. 
  - So often it ends up getting the way of writing performant code, as seen from the article he commented on in his stream the other day. 
  - That specifically was a section of code that was historically written in/with React and when we made the move to framework agnostic it slipped through the cracks and didn't get migrated to our mutable state approach. 
  - It sadly still "worked", but that small goof(愚蠢的错误) literally cost a TanStack Table user 1000x  perf on the row grouping logic
- ag-grid: Running into similar things over here! The majority of our code is framework agnostic and we have to be careful not to leak immutability restrictions out of the framework specific sections that require it. I am definitely looking out for any spreads that I come across now!

- An interesting exercise I like to do: remove the assumption of satisfying the framework's reactivity paradigm and think of how you would accomplish the same thing with as little memory/cpu overhead as possible. Mutation is a sharp ⚔️, but not forbidden.
  - I mostly have beef when immutable contracts get in the way of writing performant code, which is all too easy to find these days.
- It's funny how you and I have come to appreciate mutability, both with performance concerns but very different contexts.
  - I'm over here trying to get 3d spaceships to fly around with realtime networking at 60fps.
  - Updating mutable refs outside the React render cycle go brrrrrrrrr
- https://twitter.com/mweststrate/status/1631200674313641984
  - My expectation is that signal based solutions will eventually evolve into nested signals (signals containing signals) which will be either a bit clunky, or land on a Vue/MobX like object model.
  - MobX abstracts away the signal model by largely pushing it into the object model, so that optimisations come for free or with very little overhead, without requiring a lot of syntactical sugar or surprising semantics (imho). (And without needing a compiler step)
- It's probably circular. We were really heavy on proxies(we call the Stores) early days and Signals were advanced API. But after Hooks and there was this shift in our community hard to them

- The problem with immutability in modern fws is that JS doesn't have intrinsic support for it. Hence when using immutability with JS we get more overhead and less benefits. That said, the biggest problem with signals is that JS doesn't have intrinsic support for reactivity either.
- How would you imagine such intrinsic support for either immutability/reactivity?
  - In the case of immutability, I don't need to imagine it. For the Web we've already got it in Elm or Reason. For JS there's the Records & Tuples Proposal, but it's really just a patch.
- It may be a pipe dream, but a reactivity primitive in JS would be so cool. I get whiffs of that feeling when I use tools like @observablehq and its `viewof/mutable` decorators.
  - I don't think just adding a reactivity primitive in JS would be enough. I don't see how it would be better than Solid's implementation, except for making Ryan's life easier in the long run. To be truly reactive JS itself would need to change, kind of like what Svelte is doing.

- The issue with immutability is when it leaks scopes. I recall spending a lot of time with this in jquery golden years (not jquery fault). No one was too worried about this back then.
- Mutation is perfectly fine if you know when and how to use it.
  - When: almost never, mostly when performance is absolutely critical 
  - How: in a totally isolated manner. don't pass around an object that needs to be mutated in multiple places

- I'm going to argue that the key benefit of immutability is the contract. 
  - So as long as your mutation can be contained and that there are explicit controls, then you get most of the benefit, forgoing(弃绝；放弃) the base overhead cost of constant cloning.
- Absolutely this. Mutability seems great until you're staring at a variable with bloodshot eyes at 3am screaming "WHO CHANGED YOU?"
- Can/should `Object.freeze()` and `defineProperty()` be used more to protect against mutation? I know they're there, but I don't use them or see them used.
  - Potentially. Funny enough Solid's Stores use proxies which are readonly so they actually guard against direct mutation. I've seen solutions do `Object.freeze` in dev and not in prod. Apollo for example.

- ## I'm very interested to see where the Rx/Signal interop goes in Angular. 
- https://twitter.com/RyanCarniato/status/1643107003655667713
- To be fair it isn't new technology. Probably the longest running library still in use today is MobX.  They call their Signals, Observables (not to be confused with Rx Observables). But this is a pretty thorough explanation.

- ## It's interesting seeing React devs calling signals "the future" since they've been around in frontend frameworks for quite a while - in fact, over a decade! 
- https://twitter.com/youyuxi/status/1604727769916588034
  - They were called observables in Knockout.js, and refs in Vue Composition API.
  - In today's context, the term "signal" seems to also imply fine-grained view updates bound to signals. This is something Vue is moving towards as well.
- While this concept has been around in different forms for a long time, it's undergoing a renaissance due to being elegantly incorporated into Solid and Preact in a way that is newly emphasized ans coherent, causing it to gain more popularity than it had previously.

- 🤔 Is it similar to what RxJs does?
  - They are somewhat related but not really the same thing. In RxJS the term has special implications of emitting values as events over time.
- RxJS can be used for fine-grained reactivity, but I don't think it's ideal. Angular is exploring a new reactive primitive.
- rx is mostly for push based reactivity, what Evan is describing is called either push pull reactivity or pull based (either though it's not pure pull based which is a different thing).
  - Push pull reactivity is generally more performant and DX is somewhat different.

- Preact's implementation looks exactly like Vue refs. Not sure if there are any underlying differences? I also like that the examples use count.value in the JSX, avoiding the unwrapping confusion of Vue refs. Omitting .value in Preact seem to improve performance though.

- ## I don’t know what Signals are but I wonder if it’s like mobx observables.
- https://twitter.com/seojeek/status/1641628197048524801
- It is. In MobX it is `observable.box` .
- Our solidjs components don't rerender. Only the expressions that change. It's like a MobX-first framework. It is optimized with reactivity in mind. No VDOM, no component level change system.
- Yup, difference with MobX is that you don't need to call it, you use the value directly
  - When using objects. Primitive values like  observable.box in mobcx have a .get function that is called. Just a necessary thing in JavaScript.

- ## Found a great writeup by @tldraw about signal! 
- https://twitter.com/ewind1994/status/1631613275124412416
  - It argues that MobX, Recoil and Jotai all implement signals, just in different ways.
  - Fully agree that for signal, it's reactivity that matters, and its mental model is a framework agnostic win.

- ## I hope all of this fervor for signals is helping us finally realize that mobx is by far the most underappreciated state management library for React
- https://twitter.com/Steve8708/status/1628916464781787136
  - I have no clue how we would've built @builderio without it

- We are also huge users of mobx and mobx-state-tree at @builderio , and mobx influenced @QwikDev ’s state/signals system as well

- The problem with MobX is "proxy" and "class" centric - not friendly for some people. 
  - But I agree with you, it underappreciated. 
  - Also, it the first(?) state manager which have a strict framework on top of itself - mobx-state-tree. It has "flow"... We all will recreating this soon.

- finally someone mentions it. mobx serves us so well in a big codebase we even built our own orm on top of it and it’s framework independent not sure why signal all of the sudden is such a thing when it has been there for years!

- wasn't a big fan until i heard linear was using it thoroughly and looked more into. still like the magic of swr on certain simple projects - see the need though!

- The only reason I did not used it is because it's bundle size

- ### It is worth pointing out Qwik does not use Signals the way Solid does. 
- https://twitter.com/RyanCarniato/status/1604708328952565760
  - Qwik has an amazing hydration story. However, it does not leverage Signals in the same way for render or update performance in the browser.
  - It's a VDOM that uses Signals to trigger component re-renders. Think Preact + Signals, or Vue, or MobX + React etc..

- ## framer motion had signals five years ago 
- https://twitter.com/steveruizok/status/1635197073078513664
  - `MotionValue` provide reactive composable atomic state that provided a second channel for data that didn’t cause React to re-render (essential for animations). They can be computed via “transform” hooks.

- I wonder what @mattgperry you’ve learned after this time with such a system? Has MotionValue matured, any changes to its API that came out of long use?
  - These have roots in the Popmotion value API which as you can see in the opening summary "A multicast reaction that tracks the state of a number and allows velocity queries" I wrote when I was shitfaced on Rx
  - The API has remained the same since day 1. Easily my favourite part of Framer Motion and imo the most underused power feature. No notes
  - The only thing that's changed is I occasionally add a "naughty" method to make my life easier somewhere like `setWithVelocity`, which I basically use to force a new value and velocity to transfer a value from WAAPI back to the main thread. 
  - It would be great to have signals that you could pass straight into React's style but honestly I trust my render loop/render functions to be optimised for this

- This is the reason for stuff like animated.* out of react-spring.
  - Something I've wanted between signals & concurrency is a way to accumulate per-frame changes and apply them synchronously outside of React's scheduler. This is something I'd do in a game engine or renderer as mutating shared or WIP GPU memory can have severe perf ramifications.
- Exactly this, non of these data models efficiently support constant changing of values ala game engines from physics, game play, and AI control. Double goes for multiplayer except for netcode style. The rate of change and amount of entities would break all of the de jour app state/reactivity solutions. Rejecting simulation/emergent change isn't the not the end game.
- We’re halfway there with Theatre’s “signals” implementation. It’s a few years old but battle tested at this point.

- react-spring has had this for a long time as well,  `SpringValues` are observables that can omit events to their animated nodes.

- ## I realized recently that Framer Motion values are actually signals. 
- https://twitter.com/devongovett/status/1658573125125312512
  - They update outside React's render cycle. 
  - Good for performance, but I find the API a bit cumbersome compared to plain React. 
  - Hoping the React compiler finally enables animations without special wrappers.
- The challenge is locality of reactivity. Like components are the thing that changes. It makes easy bounds but is at odds with the cross-cutting independence you want. A compiler can "fix" this but only through masking the decoupling. Hooks already suggest this solution
- I think framer motion exists before "signals" were named that way so perhaps signals are motion values ; ) But yeah they work in a similar fashion

- ## Introducing Preact Signals: a reactive state primitive that is fast by default._202209
- https://twitter.com/_developit/status/1567209440843022341
  - feels like using plain values
  - automatic updates when values change
  - updates DOM directly (fast!)
  - no dependencies arrays

- What makes Signals unique is that state changes automatically update components and UI in the most efficient way possible.
  - Signals provide the benefits of fine-grained state updates regardless of whether state is global, passed via props or context, or local to a component.
  - You can use them inside or outside of components, unlike hooks. They also work great alongside both hooks and class components.

- For folks using React, there's a version of Signals for you too!
  -  we built Signals for Preact, but it works in React too - even the fancy granular text updates!  

- How are arrays supported? Mobx uses a proxy to catch any array operations which is pretty nice
- https://twitter.com/marvinhagemeist/status/1567276588042952705
  - MobX is great! Was a heavy user of it. 
  - 💡 We decided against intercepting built in objects as there are too many of them and too many ways to mutate them. 
  - Always using a signal and reading from it via .value felt more consistent and simpler. So we went with that

- 🤔 How does that work for signals that capture large object trees, that are rendered by different components (e.g. classic todo app)? One big signal would over render, creating many small signals would be cumbersome from DX?
  - You'd create the more granular signals yourself. **We nudge folks to subscribe as late as possible vs MobX proxies which set up subs eagerly**. Wouldn't say one or the other approach is better, just a different tradeoff.
  - You can build the same MobX-style Proxy API on top of signals
- Could you elaborate on the "sets up subs eagerly"? I'd say MobX does it late as well, but maybe we're referring to something different
  - Reading my tweet again I could have phrased it better. I meant that in the ideal case we want the renderer to set up subscriptions. With proxies or object getters it's too early as just accessing obj.foo usually sets up the subscription already.
- But that happens only during rendering, so sounds the same?
  - The difference is that it allows us to bypass virtual dom updates entirely and bind to the underlying dom node directly.
  - If you pass a signal as text in an html element for example then the component it's in is unaware of the subscription. Instead the text node sets it up.

- Does that mean that Preact uses a compiler now? So it's like Svelte 
  - Nope! This would be a fantastic primitive for compiled output, but our goal is always to deliver as much value as possible without compilation. 
  - People do all sorts of amazing things with Preact that require runtime and introspection.

- What's the advantage vs mobx?
  - Automatic rendering that bypasses VDOM diffing, 
  - integration into the framework, 
  - automatic memoization of components that use signals for state. 
  - Every form of state management has been done a thousand times, the unique thing here is the integration.

- its a similar concept. there are hundreds of implementations of this concept, we built one that has implementation details that are specifically optimized for VDOM and necessary to achieve our goals.

- is there any examples of doing async updates? If I hand batch an async function or return a promise will it wait for it to resolve, for example
  - batching is sync-only, so if you want to skip updates you'd need to store them somewhere that isn't already wired up to rendering. You can use a signal for this, or even a computed that you temporarily disconnect.

- It looks same as @vuejs ref
  - we've also explained it as "like a ref, but reactive"

- Great Work! Anyway, I may miss the point of how it is different for any external store that re-renders only subs components. Using just forceRerender without useSyncExternalStore, do we may have well-known issues like zombie child or tearing? 
  - Everything is synchronous, so there is no tearing. This also doesn't use forceUpdate, in React it generates components that update using hooks.

- https://twitter.com/marvinhagemeist/status/1569246610105765892
- Should the computed example in the Guide then not access todo.completed.value to work as intended? Would we need to mark each property of a todo as a signal, or can we just do signal(todo) to make all its properties observable a la MobX?
  - We don't do deep observability by default like MobX.
  - There is an addon called preact-signal-store that turns all object properties into a signal
