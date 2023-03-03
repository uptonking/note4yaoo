---
title: thread-lang-js-ts-stars
tags: [js, lang, thread, typescript]
created: 2021-06-22T11:54:15.957Z
modified: 2021-06-22T11:54:44.506Z
---

# thread-lang-js-ts-stars

# guide

# discuss
- ## 

- ## 

- ## 

- ## I really wish there were Promises in JS that could be evaluated sync. It’s a complex problem.
- https://twitter.com/trueadm/status/1630739165045194752
- For UI frameworks you want to allow the user to pass a promise, but ensure that if it is ready that you can render synchronously. But `T | Promise<T>` doesn’t compose the way promises do, so either you accept a perf/UX hit, create your own alternate async ecosystem, etc.
  - I use a WeakMap for this. Only pass promise. Lookup resolution value sync via weakmap where you want to do this. Still agree though: custom thenables are great and Promise.resolve using them is great, async/await not using them sucks
- This was discussed ad nauseum a decade ago. If you want sync promises try jQuery. Deferred.
- https://github.com/abbr/deasync
  - DeAsync turns async function into sync, implemented with a blocking mechanism by calling Node.js event loop at JavaScript layer. 
  - The core of deasync is written in C++.
- conclure js Using generators instead of promises allows for a LOT more flexibility, including cancellation, sync resolution, and better testing. The API is strictly the same as async/await

- I definitely want eager await that resolves sync if the promise resolves sync. That’s more in the style of callbacks, and allows you to write a single api for both sync and async interfaces.
  - I struggle with this issue in tuple-database. I want to write the same code that works for an async backend or a sync backend. I don’t want to create an intermediate query language…
- My problem is actually pretty specific:
  - For tuple-database, there's an async storage interface and a sync storage interface. 
  - The sync interface is important if you want to use it for application state management and stuff. Or maybe you just want to use local storage...
- Since the lowest level abstraction is either sync or async, it pollutes all the code above it which needs to be written to handle both cases.
  - I looked into coroutines, higher-kinded types, monkey-patching promise... 
  - My solution? Regex lol
- Replicache is designed to be used for application state and it is async. We are religious about 60fps. Promises that resolve immediately *are* slower than sync code but we’re taking microseconds. It works great for 60fps in our experience.
  - We have tons of customers in production using Replicache exactly this way (among them @vercel ) and it’s ~instant.
- Yeah, you can definitely get away with async state management most of the time...
  - I'm curious if that can get in the way of typing into an `<input>` if the input's value is updating async as you type...
- Yes you can. We do this while animating at 60fps.
  - We have many users who back input boxes by @replicache directly. It's a design goal of ours to enable this exactly. Try it out, I think it's an overlooked design pattern.
- 👉🏻 关于架构层sync或async api的设计 
  - The other nice thing about making the api to Replicache asynchronous is that it permits falling back to io as necessary. Many sync systems have this problem where these choose sync apis for perf but eventually data gets large and causes excessive gc.
  - If the core API is async it can be up to the sync system to dynamically manage cache size. Replicache does this, lazily caching data from IDB and paging it out after awhile.
- Getting into the weeds though: on iOS Safari, if you want to call focus() on an element to bring up the keyboard, it must be called synchronously in response to a user action event callback... Now, what if they press a button and you want to open a popup and focus the input?
  - https://twitter.com/ccorcos/status/1631159120043835392
  - In React, at least, you're going to want to update the state, synchronously re-render, and then call focus... This *could* work with a sync state update. Unfortunately, React's move towards async rendering throws a wrench in it. But the problem remains the same.
- I am pretty sure it only needs to be called in the same task (queueing a microtask is fine). So if your data is in memory it will still work.

```js
const foo = await Promise.resolve("foo");

// vs:

const foo = await new Promise((res, rej) => setTimeout(res, 0));
```

- The first runs in *same turn* of event loop as calling code, guaranteed. Second gets queued in event loop.
- Microtasks are crazy fast. All they are doing is delaying a function to run later in the turn of the event loop. No actual IO (to disk, network, whatever) can possibly get between the queuing of a microtask and its execution.
- `setImmediate` is not part of the spec or implemented by browsers, but was meant to queue a task. So shorthand for `setTimeout(fn, 0)`.
- A microtask enqueued from within another microtask would execute immediately I believe, but I bet React's whole rendering model probably has its own considerations for this.
  - I think they were also doing some weird stuff with unwrapping resolved promises.. somehow.. maybe an RFC.

- It’s important to understand that `async` does not mean “yield to event loop”. When the underlying promise resolves in same event loop task, the resolution will also run in same event loop task. This usually happens when the data needed is already in memory, because it’s cached.
  - Mutations don't need to go through useEffect or similar in the first place because they aren't an effect of render, but of some UI event. So the whole cycle should happen in one frame if your data is in memory, even if all the methods are `async`.

- Yeah, but my goal was to just have one system that can work either sync or async... Perhaps, that's not a great goal, but that's where I landed on these problems... If generators could have a typed yield (similar to  await), then my problem would be solved...
- It's worked really surprisingly well for us. I think UI developers have a phobia of `async` because it often means 'network activity' in classic web apps. But that isn't actually what `async` means to the browser. It just means >= microtask.

- This is good news. I’ve done cr-sqlite / vlcn as completely async (and had to part ways with collaborators over that decision) so this gives me some reassurance(肯定，保证).

- ## [Suggestion: avoid `delete` keyword](https://github.com/ianstormtaylor/slate/issues/4425)
  - we could look at swapping set_node to do node[key] = undefined and improve performance instead of using delete node[key].
- While this was once true (delete being slow), I think there's sufficient evidence that it's no longer a primary issue
- I'm not 100% convinced but you're right performance characteristics can change.

- ## The number of times I see this makes me want to cry: `element.addEventListener("click", (e) => handleClick(e))`

- https://twitter.com/RogersKonnor/status/1620437284498870272
  - Youre creating an anonymous function callback which means if this script runs more than once you'll have multiple event handlers.
  - Whereas, if you just reference the function, you'll get automatic deduping.
  - element.addEventListener("click", handleClick)
- Yes, I think it's because a lot of people assume you need an anonymous function in order to get access to the event object

- ## 被javascript 这个setInterval 坑到了，才知道这玩意不是精确按时间执行的，要想精确计时，还挺不容易，递归的方案在手表上又太耗资源。
- https://twitter.com/haozes/status/1620006802451755010
  - 现在华为，小米的手表写的小程序都是用js
  - javascript 那个正常情况下误差非常大，在这破表上，大概一分钟差1秒
- 确实如此，自己定期重刷吧
- 倒是可以用 setTimeout，然后利用执行时的当前时间做一个时间修正

- 可以换个思路，拿setInterval 当作状态更新逻辑，而不是取值计时。

- 这也不是 setInterval 的坑，非实时系统的定时都是不精确的。即便可以通过提高优先级提升精度，恢复到应用场景过程中还是有可能被抢占而丢失精度。
  - 运行时的关系。应该是JS在单线程的事件循环里处理时钟事件，一旦有别的事件阻塞了这个线程，计时就不可靠了。Java和Swift往往使用单独的线程来处理时间。

- [如何实现准时的setTimeout](https://mp.weixin.qq.com/s/ENU93_jSUaAONCkfTQTK-Q)
- while: 想得到准确的，我们第一反应就是如果我们能够主动去触发，获取到最开始的时间，以及不断去轮询当前时间，如果差值是预期的时间，那么这个定时器肯定是准确的，那么用 while 可以实现这个功能。
  - Web Worker为Web内容在后台线程中运行脚本提供了一种简单的方法。线程可以执行任务而不干扰用户界面。
  - 在 worker 中写入一个 while 循环，当达到我们的预取时间的时候，再向主线程发送一个完成事件，就不会因为主线程的其他代码的干扰而造成数据不准的情况。
- requestAnimationFrame() 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。
  - 该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行，回调函数执行次数通常是每秒60次，也就是每16.7ms 执行一次，但是并不一定保证为 16.7 ms。
  - 可以尝试一下将它来模拟 setTimeout
  - setTimeout 系统时间补偿
  - 当每一次定时器执行时后，都去获取系统的时间来进行修正，虽然每次运行可能会有误差，但是通过系统时间对每次运行的修复，能够让后面每一次时间都得到一个补偿。

- ## Promise resolvers are one of my absolute favorite little programming tools
- https://twitter.com/aboodman/status/1619426079399350272

- I've been looking for a name for this pattern for years. IIRC I've used it mainly in tests

- I think some people call this "deferred"
  - https://github.com/ljharb/promise-deferred

```JS
// https://github.com/rocicorp/resolver

import { resolver } from '@rocicorp/resolver';

const { promise, resolve } = resolver();
resolve(42);
await promise; // 42

class LongRunning {
  async stop() {
    this._stopper = resolve();
    await this._stopper.promise;
  }

  async run() {
    while (!this._stopper) {
      // ...complex asynchronous process...
    }
    this._stopper.resolve();
  }
}
```

- ## is it a good practice to use Proxy objects in your app, or I should let that shit to library authors?
- https://twitter.com/hhg2288/status/1602323703198523394
- I don’t like them, they feel a bit convoluted and aren’t that performant either.
  - Greg who made Shelf tried to add them to the Shelf library but found they were slowing things down significantly.
- if the problem can be solved more simply I wouldn’t touch them. I have yet to run into a problem in app code that proxies are the obvious answer for 

- ## I'm not a fan of premature optimisation but if you know a structure is going to be created *a lot* you're probably better off with a class over a factory function.
- https://twitter.com/mattgperry/status/1588479452908060673
  - There's an upcoming Motion PR that makes this switch, leading to 20-25% lower memory usage across all @framer sites
  - With a factory function, everything is created anew. 
  - Whereas with a class, a method is defined once and shared in memory.
  - This has clear ramifications(结果，后果) for memory usage if these structures are being created 1000s of times, especially when, as in our case, the structures are big.
  - This is more of dorky(stupid) interest than something you should account for when making these architectural decisions

```JS
// before
function createThing() {
  return {
    method1: () => {}
  }
}

createThing().method1 === createThing().method1 // false

// after

class Thing {
  /** class instance methods are shared on the prototype */
  method1() {}
}

new Thing().method1 === new Thing().method1 // true
```

- In JSC, classes have a prototype object, a constructor and instances. The instance’s JSC:: Structure is created with a prototype object. The prototype’s functions are allocated once, on the prototype. Reusing the same prototype skips allocating the functions again

- ## ag-grid: Been experimenting further with #TypeScript and seeing what the user experience might be like if I was to create a "generic bag" type builder. 
- https://twitter.com/SCooperDev/status/1556743650394181633
  - Enabling users to provide generic params and not have to worry about providing defaults for all the previous params is intriguing.

- react-table: Genmaps worked well internally, but ended up being cumbersome for user-land types. 
- I finally took 9 generics and:
  - Converted 3 to any
  - Converted 4 to declaration merge-able interfaces
  - Kept 2 as traditional slotted generics
- Users liked it more and DX loss was negligible.

- ## Join @tannerlinsley as he dives into the history of React Table and discusses everything it’s taught him.
- https://twitter.com/tannerlinsley/status/1548730511832387585
- Mapped types are different - it's a method for transforming types.
- Generic maps are when you store generics as an object.
- Oh I see, that's why @tannerlinsley is mentioning it when the function signature changes from many positional parameters to only one, which accepts an object using a generic map.

- any way you could show this concept in a typescript playground? I was also intrigued after I watched the vid but my googling is failing me
  - @prisma is also doing that, it just so happens that I wrote a blog post about that a few days ago. I think the generic `T` in all the examples would be called a Generic Map.
  - [How Prisma adapts Result Types based on the Actual Arguments given](https://pkerschbaum.com/blog/how-prisma-adapts-result-types-based-on-the-actual-arguments-given)

- ## Performance tip: if you need to set a lot of dynamic keys to an object, a Map can give you better perf
- https://twitter.com/Steve8708/status/1508502291170484224
  - In short, JS VMs try to assume a shape of an object using a hidden class. When the shape changes, this can lead to a deopt
  - It's the same reason why setting a property to null/undefined can be faster than deleting
  - A Map, on the other hand, is optimized for this very use case of frequently adding and removing keys (see the "performance" table row here)

- ## How to specified an optional argument in #javascript ?
- https://twitter.com/rauschma/status/1510961319268306948
  - function foo(requiredParam, optionalParam = undefined) {}
  - The `= undefined` doesn’t do anything but it tells people reading the code that a parameter is optional.

- ## Habit: When declaring REST API response types via #TypeScript, I only declare properties for the fields we use.
- https://twitter.com/housecor/status/1495023556358455298
- Benefits:
  1. The type is simpler.
  2. The type contains no noise. All properties are relevant.
  3. The type is handy for mocks. It declares only the properties we use.
- To clarify, generated types are great. 👍 I just don't want to use them directly because they often contain properties I don't need or use. 
  - So, I use TypeScript's `Pick` or `Omit` utility functions to derive my own more narrow types.
- manually defined API types often do not reflect the reality and even if they do now, they can get out of sync real quickly.
  - We've moved to openAPI contract definitions and let the types be generated from that - and I don't want to go back 

- ## FWIW we spent considerable effort exploring whether modern syntax could benefit Preact, and our conclusion was that hand-optimized ES5 is still fastest.
- https://twitter.com/_developit/status/1437429523893600256
  - We did find a bunch of browser bug workarounds for IE11 that were worth dropping though.
- Example - here's the fastest ES20xx JSX factory vs ES5
  - The ES5 version is faster than the modern syntax version - not because rest parameters are slow, but because syntactic rest parameters unconditionally allocate an Array. In the verbose ES5 version allocation is conditional for the two most common cases (0 children / 1 child).
- There are a bunch of these cases:
  - `for..of` : faster than `forEach()` , slower than `for(;;)` syntax
  - `Map` : faster than array pairs, slower than dictionary-mode object
  - `async` : faster than `Promise` chains, slower than callbacks
  - `class` : faster than transpiled ES5, slower than hand-written
- I believe we're sort of at the point where modern JS is fast enough for 95% of things and should be the default, but library authors seeking low-level performance wins still drop down to ES5 where verbosity can better inform VM optimizations
  - Ideally this would reverse itself over time, but that's a chicken-egg problem.

- ##  `setTimeout` is a codesmell 99% of the time
- https://twitter.com/oleg008/status/1436027606302928897
- Today I implemented an UI for copy-to-clipboard button. It shows a "Copied" feedback that dismiss after 5 seconds. 
  - `setTimeout` is a codesmell when it is used to workaround some async operation like "ensuring" a value is updated or waiting an animation
  - It's a codesmell because it's not reliable and you should figure out how to capture the end of that async operation. Like `onAnimationEnd` events for animations, callbacks, etc
- Persistent Browser-Based Games use it for server-side ticks, to alleviate the logistical nightmare of having the client trigger the processing of player data. Maybe it should be 98.9% of the time
- Alternative is async and await?
  - No. Thats not the point. The point is timers are never or rarely needed.
  - One of the few places where it’s really needed is when you want to display a “loading…” text and animate the dots.
  - can do that with css

- ## I used to think I was clever writing code that behaved differently depending on how many parameters a callback was expecting.
- https://twitter.com/erikras/status/1422545745647972358
  - But that’s a terrible API. Don’t do that.
- nless you have explicit function overloading like in Clojure... or perhaps it's more like, pattern matching on number of arguments.
- I discovered jQuery, where every second argument was object
  - I discovered functional programming, where you only always need a single options argument
  - now they force me to write crappy TS code where the "coding standard" is to cram 3-4 args

- ## Question: Do you use an object, or an array of objects?
- https://twitter.com/housecor/status/1420032929829380107
  - Situation: You need to work with key/value pairs. 
- Object advantages:
  - Less code
  - Fast, direct access by key
- Array of object advantages:
  - Easily add another property if requirements change
  - Can document each property with a comment above the property in the type declaration
  - More obvious what the code means at a glance
- The point is, it all depends on requirements. 
  - Do I need to serialize it? Are the keys strings? `{ [K]: V }` ; 
  - Do I need to clear it? Key it by something other than a string? `Map<K, V>` ; 
  - Do I just need to loop over the key value pairs, and that's it? `[K, V][]` ; 
  - Am I trying to be slick with memory/loops? Maybe `[K, V, K, V]` ; 
-  what's most important:
   1. Does it work?
   2. Can my team maintain it?
   3. Can we test it?
- This 1, 2, 3 is very good before creating ANY abstraction
- 87% of the time - arrays. Will enable other indexing/iteration abilities. Examples: index by ID, group by role, filtering, mapping etc.
It's always easy to do _.keyBy(users, 'username') to get the object you mentioned, and keep the flexibility.
- Object has some upsides (ensures key is unique, faster getting value by key) and you can easily turn it into array with Object.entries if needed.
- In this case, it's clearly a set of objects. If needed for data access then reduce the array into a map and use either the objects themselves as the key and the desired result as the value.
- Another benefit of object is you can enforce uniqueness of your object keys.

- ## Just a reminder that using `reduce` doesn't always mean iterating less. 
- https://twitter.com/i_like_robots/status/1418874992146755584
  - 追求极致性能时可适度放弃immutable，使用mutable方法
  - The first example using has O(n²) complexity due to the additional iterations required by the spread operator and is ~50x slower than `filter/map` and ~100x slower than using array `push` .

```JS
// slow
items.reduce((acc, item) => item.prop ? [...acc, item.prop] : acc, []);

// equivalent to slow
items.reduce((acc, item) => {
  if (item.name) {
    return [].concat(
      typeof acc[Symbol.iterator] === 'function' ? acc.map(i => i) : [], item.name
    )

    return acc;
  }
}, []);

// fast
items.filter((item) => item.prop).map((item) => item.prop);

// faster
items.reduce((acc, item) => {
  item.prop && acc.push(item.prop);
  return acc;
}, []);
```

- if you're thinking "that's cool in theory but I'm sure engines have optimisations for this" then nope, you're wrong. And 100x slower is generous, some browsers are 1000x slower! If you're doing this lots of times in your apps then you could make them noticeably faster.
- And of course **`reduce` with object spread creating a newly cloned object for each iteration is no better - it's also super slow**.

- Ditch the `reduce` in the final example for a `for-of` loop to make it more readable. If you're using reduce simple for looping, just use a loop. Way less for the reader to think about, and it reads sequentially.

- Nice! It's also doesn't counted as a harmful mutation because it's internal scoped one with no effect on externals. @getify talked nicely about this in his book "Functional-light JavaScript"
  - tbh I don’t bother sticking to theory and mutate when it is ok

- ## If you were to quickly explain the fetch API to someone and you don't have an URL handy, data: URLs for the rescue!
- https://twitter.com/GNUmanth/status/1415560838472105984
  - const resp = await fetch('data:, {"name":"yoda"}')
  - const data = await resp.json()
- This is actually a great idea for tutorials. Usually I create some sort of mock. But this is definitely interesting
- This would work same way for all HTTP verbs ?
  - No, as it's not HTTP we can't use the verbs.
  - I would use http://httpbin.org (flask) in such cases
- http://httpstat.us/ is another useful site to test HTTP errors.
- What’s the function of the \uFEFF (zero-width no-break space?) here?
  - ou may skip it the ZWSP! According to RFC 2397: If `<mediatype>` is omitted, it defaults to "text/plain; charset=US-ASCII"

- ## Never realized destructing could be used to trim unwanted properties
- https://twitter.com/angustweets/status/1415734961886408704
  - const { yawn, sigh, ...usefulProperties } = obj; 
- I do a lot of that with React where the caller could pass lots of things but I only need to deal with a few.
- Removing a property from an object immutably by destructuring it

- ## TypeScript: How do you format members of enums?
- https://twitter.com/justinfagnani/status/1413886888528605184
- Solution: don't use enums. Stick to the type-system portion of TypeScript.
- Are there any other TS features that are not simply type-strippable?
  - enums, namespaces, constructor parameter properties, JSX, and debatably import assignment. 
  - TypeScript stopped adding non-type features and joined TC39 though, so that's all there ever will be now.
  - Oh and decorators, kind of, but that's a whole other story
- we can write an object that gives nice names to "enum" values, derive the type of the allowed values, and do exhaustiveness.
  - The thing I like about this pattern is the code is what you'd write in JS. The TS is just added types.
  - What you don't get as easily is the reverse mapping from value to name, but I find that I rarely use that, and you can write the utility pretty easily.
- Good points. Objects-as-enums really are easier to understand (compared to the subtle quirks of TS enums).
  - Depending on what is needed, a Java-style enum pattern can be useful, too

- ##  `export default thing` is different to `export { thing as default }`

- https://jakearchibald.com/2021/export-default-thing-vs-thing-as-default/
- Imports are references, not values
- But 'export default' works differently. 导出的是快照值

- ## don't let friends write JS functions with multiple optional parameters, each of which can have multiple overloaded values and behaviors
- https://twitter.com/acemarke/status/1409971795894181904
  - this tweet brought to you by me looking at the `connect` implementation for the first time in a while and my mind boggling at how the `mapState/mapDispatch` overload detection behavior is implemented
- All JavaScript functions should only be allowed to take one argument
  - you already do this in @Reactjs as "props" 
- When I got started with JS, I treated jquery's design as the ideal and made functions with lots of different overloads and argument shortcuts.
  - First awkwardness was when I had to make some wrapper functions around these and it was pain making the wrappers support parsing the args the same way. 
  - It's a solvable problem, but it was effort for a design that had other downsides too. Sometimes you have to judge whether it's worth it to solve a problem versus just removing the problem.
- I’m increasingly close to adding a lint rule that forces all function definitions to have 0 or 1 param. Object definitions are cheap enough that I don’t see much a reason to have multiple function params
  - 0 or 1 required, 1 optional (often boolean), is my empirical limit

- ## What's the best way to dynamically import an npm package on the client-side? Like in documentation code playgrounds.
- https://twitter.com/diegohaz/status/1409278109573160960
- By appending a script at runtime. Use something like react helmet
- Perhaps dynamically replace the imports with links to a CDN like https://skypack.dev ?

- ## named exports exports a dynamic reference to the variable being exported, 
- https://twitter.com/yagopereiraaz/status/1406974989203611654
  - default exports only export the current value of the variable at the time of import.
- This is intentional in the spec.
  - `export default <expr>` snapshots the value of `<expr>` as if it were a new constant binding
  - `let x = 1;  export { x as default }` results in x becoming a live binding for the default export
- I very rarely use default exports as they don't play so well with refactoring tooling. This feels like another reason to double down on that choice!
  - I wrote a short (internal) article to prefer named exports. 
  - In particular, as an alternative to the common pattern of having a default exported object that contains all the functions you want to expose.
  - So far it seems uncontroversial.
- Please tell me you titled it "default exports considered harmful"
  - Unfortunately it's just a preference so doesn't deserve such a famous label.
- is this why you can't default export a declaration? example: export default const hello = 'world'; 
- Default exports de-sugar roughly to the below, which is why incrementing num has no effect. It's assignment by value, not reference.(Invalid syntax since you can't name an export "default", but you get the point).
  - `export const default = num'` 类似
- Same if you actually define a function at the module to update the variable thats being exported. Defaults exports are immutable, it seems
