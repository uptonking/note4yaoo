---
title: lib-state-mobx-community
tags: [community, mobx, state]
created: 2023-04-07T03:10:07.950Z
modified: 2023-04-07T03:10:33.378Z
---

# lib-state-mobx-community

# guide

# discuss-author
- ## 

- ## 

- ## The world converges to 2015's #MobX reactivity system in the end
- https://twitter.com/mweststrate/status/1704870011850887589
  - in turn inspired by Meteor Tracker & Knockout. But the object model, and semantic guarantees (topological sorting of deps, strict separation between observables, derivations and effects, sync push dirty state + lazy value pull, transactions), where all introduced then iirc

- Incremental computation and FRP have been around for ages, we’re all reinventing/remixing stuff from decades ago. None of the JS frameworks really invented the core concepts at play here. That’s fine! Each JS framework adds their own take and helps the field move forward.
  - Yeah it is not a complaint :) Frameworks will do it better as they have more lowlevel control which MobX doesn't have over React. But the convergence in propagation semantics is very interesting.

- i think propagation semantics is still changing though, Ember/Starbeam/Signia are all using a variation on deferred notification and logical clocks rather than pushing "dirty" events

- ## 💡 mobx-react vs signal
- https://twitter.com/mweststrate/status/1628893187665285127
  - every observer component tracks it's entire render function like a `computed` and subscribes, if the output of the computed changes it merely "ticks". 
  - Since they are also memo-ed and observable objects are stable, nodes that pass down observable objects don't render.
  - Note that MobX doesn't use setState at all, it is independent of React and also works with Angular, Lit etc. It's only the `observer` utility from mobx-react bindings that are React specific
- 👉🏻 The primary thing that MobX offers over signals is that it provides transparently a full JS object model: arrays, maps, objects, class instances, every property in there will automatically become a signal, making complex data graphs trivial to read/write & observe with same perf
- My question is: When MobX detects a change, how does it notify React to re-render? And is it able to notify independent components in React? (Or does it just notify the root React component?)
  - Independent. Ilnot related to root or render tree shape at all. It works the other way around, rendering becomes a local derived signal which only the component itself subscribes. signal itself updates through the normal reactive tracking, and only triggers if used signals change
  - Yes, it's able to notify independent component in React and other libraries (redux, zustand...) can do that as well.

```JS
// simplified
const fc = observer(functionComponent);

const fc = memo(() => {
  const [render, setRender] =
  useState(functionComponent())
  useEffect(() => {
    computed(() => functionComponent()).subScribe(setRender)
  })
  return render
})
```

- Why aren't all signals implementations based on mobx? Is everyone reinventhing the wheel?
  - I suspect cause MobX looks overwhelming if you are only looking for the reactivity model. 
  - It is the reactive object model that makes the reactivity shine, but also the what makes the API surface and implementation big (but was written for 2015 browsers, can be smaller now!)

- MobX is awesome! I am a big fan! It would be great if we could just use something like MobX out of the box in Qwik but the serialization and tree shaking requirement put a special constraint on us.
  - Theoretically it should be quite doable, as dependencies / dependents are pointer arrays that could be serialised as atom id's, but never took a stab at it.

- _Every_ state management library that interacts with React ultimately does some form of `setState()` inside of a component to trigger a re-render
  - (exception would be something like preact/signals that bypasses React rendering to update the DOM directly)
# discuss
- ## 

- ## MobX now supports standard decorators! 
- https://twitter.com/mweststrate/status/1724428973063700705
  - 👉 Clean (no constructor code)
  - 👉 30% less overhead
  - 👉 Works out of the box in TypeScript
  - 👉 Some cool news around MobX & signals!

- ## #MobX decorators are 32% faster when using standard decorators, compared to legacy decorators. Yay for standardisation!
- https://twitter.com/mweststrate/status/1719828168075366452

- ## dan_abramov, BlueSky uses Mobx.what are your thoughts on using Mobx now?
- https://twitter.com/acemarke/status/1695569310498914357
- it seems to be primarily used as sort of a cache for the fetched server data. i think i’d prefer to work with plain objects for this kind of use case but i don’t actively mind it. i might explore alternatives if it starts getting in the way somehow
- Components as signal trackers with render effect

- ## years later MobX still makes people go home early by keeping complicated projects scalable and fast
- https://twitter.com/mweststrate/status/1696571664601936181
  - the trias politicas of observable > derived > effect has become so much the de-facto mental model, that it has become the standard way of doing reactivity/signals
- It feels to me, like the React team don't have enough experience with libraries as MST/Ember Data, because after you use them, everything else feels so bureaucratic

- ## I hope all of this fervor for signals is helping us finally realize that mobx is by far the most underappreciated state management library for React
- https://twitter.com/Steve8708/status/1628916464781787136
- The problem with MobX is "proxy" and "class" centric - not friendly for some people.
  - 👉🏻 it is by no way class based at all you can make any primitive including arrays observable. We‘re not using a single class in our huge codebase. mobx serves us so well in a big codebase we even built our own orm on top of it and it’s framework independent not sure why signal all of the sudden is such a thing when it has bern there for years!
  - it feels like it could really benefit from a rewrite of some of its api. Such as HoC, which isn't the way react is going and yet

- Love MobX. Although I often see it abused, fees like mobx apps are easier to do “wrong”. I think solid’s approach kind of solved a lot of the issues with MobX by encouraging unidirectional data flow and making the api thinner and simpler.

- Valtio is simplest yet so underrated

- Love MobX. We have deeply nested data and immutability just doesn’t seem worth it. Normalizing it also seems silly.

- ## MobX is on an interesting fine line between the two approaches, 
- https://twitter.com/mweststrate/status/1631200668194152450
  - still running full component bodies, but it typically avoids for most of the manual hook optimisation labour and avoids dependency arrays without being prescriptive where / how the rendering logic is written.
- There is a common trap: forgetting to mark a component as 'observer' (cq. passing observables to non-observers). It's the result of deliberately not shipping an own view library, but rather building top of React.
- 👉🏻 MobX abstracts away the signal model by largely pushing it into the object model, so that optimisations come for free or with very little overhead, without requiring a lot of syntactical sugar or surprising semantics (imho). (And without needing a compiler step)
  - My expectation is that **signal based solutions will eventually evolve into nested signals (signals containing signals) which will be either a bit clunky, or land on a Vue/MobX like object model**.

- capture was a common source of problems for me, not because it was inconsistent but because there were nuances in my code that I didn’t really have to think about with other models (eg dereferencing an observable in a loop, dereferencing in a callback)
  - These are all signposted(路标; 指向标) in the docs, so just part of the learning curve, but there were a few long debugging sessions that relied on me knowing what to look for. Also so many accidentally stashed(隐藏) proxies
- Interesting, I generally think of it like quite the same as normal closure capture. An example at hand by any chance? We might not ehh.. capture this well enough in the docs yet.

- It's probably circular. We were really heavy on proxies(we call the Stores) early days and Signals were advanced API. But after Hooks and there was this shift in our community hard to them.
  - This is why I stopped working on React Solid State. It was basically indistinguishable from React Hooks.

- a barebones signal is basically like a mobx boxed observable 

- ## vue3的响应式和mobx的响应式存在同样的问题，即在使用proxy的情况下，对数组的修改操作不是原子的，一次shift可能会产生多次proxy的set操作。
- https://twitter.com/wulianwen1/status/1691810099738677532
  - 因此mobx自己在内部写了一套数组的操作，保证数组的api只产生一次reaction。
  - 有没有更好的方法呢
- 我理解的 batching 一般是将用户的多次修改合并为一次更新，而这里是 shift 是一次修改触发了多次 effect

- 不确定是不是和我写的这个有一丢丢关系，vue 的 reactivity 这个底层包是没有做 reaction 的 batch 的，但是上层 runtime-core 是封装做了的
  - 你是对的，微任务把之前的同步操作隔开了，所以连续多次的set操作不会同步触发watchEffect，而是在下一个微任务到来的时候触发一次reaction
  - effect 和 watchEffect 的差别应该就是一个同步跑的，一个加了 schedule

- Vue3's update has a flush queue, it provide a batch update ability.

- 无解的，只能照着实现一下了
  - 做了一个尝试，在get里面把数组原来的api hack掉，在Reflect.set执行完成之后进行reaction。目前work well，不知道有坑没
  - 感觉大家倒腾 Proxy 的思路都差不多... 这个倒是没啥问题，等你需要对数组里面的元素也做递归的 observable 时，还有更刺激的问题在后面
