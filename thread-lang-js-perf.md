---
title: thread-lang-js-perf
tags: [lang-js, perf]
created: 2023-11-10T07:15:33.022Z
modified: 2023-11-10T08:05:19.107Z
---

# thread-lang-js-perf

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [Fun fact JSON | JSONMASTER : r/webdev](https://www.reddit.com/r/webdev/comments/1qdfq3t/fun_fact_json_jsonmaster/)
  - Up to 40% of backend CPU in large systems is spent just on: JSON.parse() and JSON.stringify(). Data is heavy.
- CPU cycles are cheap. Backend developers sanity is not
  - CPU will rarely if every be a bottleneck for backend, most time is spent on IO/db

- JSON parsing in every js runtime is faster than object literal instantiation...
  - This. Typical request handler is 1) parse json 2) a few conditions 3) a few assignments 4) go to database and/or network 5) stringify json. Obviously JSON handling is the only CPU bound task here. It doesn't (necessarily) make JSON handling CPU-heavy.

- 40% on JSON and not SQL?! What is your backend doing?!

- structuredClone
  - still annoying that jest still cant handle this

- We can debate this all day, or we can actually measure it. I just did in an application I'm maintaining:
  - Database call: 101 ms
  - JSON.parse(JSON.stringify(largeObject)): 0.143 ms
  - Let's say you are asked to improve the performance of the program that performs these two operations. Which of them would you work on?

- ## Needed some I/O latency numbers for a piece I'm working on, and this came in absolutely clutch(紧紧地抱住、握住).
- https://x.com/BenjDicken/status/1841883864144429228

# discuss-ts-perf
- ## 

- ## 

- ## You can do some really amazing things with typescript, but seems like beyond the basic types it gets pretty slow. 
- https://twitter.com/devongovett/status/1741014840494473433
  - Spent hours coming up with a way to auto infer style variants but might have to rip it out because it slows down autocomplete so much. Any TS optimization tips?
- TypeScript is the only piece of coding stack that could benefit from a Rust rewrite but nobody wants to do it
- I don't understand why the TS team won't just focus on perf instead of new features. It's crazy we have to work around the type system for perf reasons.
  - Please read this comparison carefully [Benchmark TypeScript Parsers: Demystify Rust Tooling Performance_202311](https://medium.com/@hchan_nvim/benchmark-typescript-parsers-demystify-rust-tooling-performance-025ebfd391a3)
  - From what I can see, the typescript team does have a strong focus on performance. Outside of complicated recursive types the performance is generally very good. I'm starting to investigate memorization to help with complicated types, but there is no silver bullet.

- Besides use interfaces over types when composing types, you should profile it and see what is causing the slowdowns. You can use the —generateTrace and @typescript/analyze-trace to see what are the slowest ops the typechecker is stuck on.

- TS isn't really designed around performant inferred types, unfortunately. Any time you get into complex derived / mapped / conditional types, it tends to bog down rather quickly. The solutions almost invariably end up at "define your types AOT"
# discuss-array/map
- ## 

- ## 

- ## The "fill then map" is obviously slower because of extra iterations. Me: Laughs in JIT
- https://twitter.com/cmgriffing/status/1753556666396930127
- This is simply a post about how you can't predict the JIT compiler.
  - The code needs to run often enough to be JIT'd. A React render block is a great example.
  - Depending on the use case the readability of using `Array.from` might still be preferred.
- The difference in execution time should mainly be attributed to `new Array()` and `Array.from()` execution. And the iteration appears to have minimal impact on the difference of the execution time.
- this is why JavaScript is fucked.

- ## Performance tip: if you need to set a lot of dynamic keys to an object, a Map can give you better perf
- https://twitter.com/Steve8708/status/1508502291170484224
  - In short, JS VMs try to assume a shape of an object using a hidden class. When the shape changes, this can lead to a deopt
  - It's the same reason why setting a property to null/undefined can be faster than deleting
  - A Map, on the other hand, is optimized for this very use case of frequently adding and removing keys (see the "performance" table row here)

- ## 💡 as a principal dev, I've had the map/filter/reduce ripped out in hot paths where copying Arrays is a lot more expensive than just a for loop.
- https://twitter.com/mattpodwysocki/status/1722687839660376469
- Absolutely. Just this week I found an optimization where I reduced sudden +700MB bursts of allocations (and consequentially, OOMs) due to 3 .map()s with a simple for loop, where heap stays at maximum 100MB.
  - Yeah, most languages/runtimes aren't suited for that style, especially with eager evaluation and intermediate allocations will just blow the memory
- there are also reducers that are so convoluted that it's not only more efficient to use a loop, but more clear as well.
  - Reduce often lacks clarity, number one reason I use it hardly ever
- Map and filter often express intent more clearly as long as you aren’t in a hot path. Reduce not so much.

- What are the smells for when the for loop is just better? Size?
  - Mostly size, but also intent, such as side effects or simply projecting to a new collection, etc. If we can avoid extra allocations, then that's what's important in some hot paths

- 9 times out of 10 optimizing JS to this degree is pointless. There are almost always bigger fish to fry, and if you're at the point where for loops vs map actually matters then you shouldn't be using JS.

- ### Unpopular opinion: I often prefer for-loops over map calls. 
- https://twitter.com/elmd_/status/1722957524062576975
  - I find them easier to read. 
  - Also `map` and then `filter` iterates the array twice as it's not like a stream (as in RxJS for instance) where each value flows through the entire pipeline.
  - Or maybe, if you want, use `reduce` instead to map and filter.
- That's premature optimization. It's not like an order of magnitude improvement, right? Unless you're building a framework, it's good to prefer declarative code. 
  - I find the declarative version far more readable.  The noise from the for loop is annoying.

- ## Apparently Array.from(arr) is like 70x slower than arr.slice() 
- https://twitter.com/fabiospampinato/status/1719825922407186723
  - I guess it goes through iterators even for normal arrays, for no reason I guess?
  - const arr = new Array ( 10_000 ).fill ( 0 ).map ( Math.random ); 
- slice() without args is particularly fast. It's a fast path for cloning.
- I guess they would need to check that the array is not proxied and the Symbol.iterator they get is equal to the built-in one?

- ## JavaScript Map usually performs better than plain objects when you have a large dataset and/or often set new key/value pairs.
- https://twitter.com/diegohaz/status/1534888291732013058
  - Here's how you can use Map with React state
  - As others pointed out, it's better to copy the map before mutating it
  - setSizes((sizes) => new Map(sizes) .set("item-1", 30) .set("item-2", 40) .set("item-3", 20) )
  - I'm currently working with virtualized lists(ariakit-virtual-list) which require the manipulation of large datasets (for measurements, for example)
  - I significantly improved performance by replacing some plain object states with maps.
- Here's another piece of info to consider. The difference between `Object.keys(obj).length` and `map.size` is huge with large datasets.
  - Basically O(n) vs. O(1).

- It's probably safer to copy first before mutating.
- Can I ask why useState(() => new Map()) and not useState(new Map())? What’s the difference between the two? Besides the syntax ofc. Is it a perf thing?
  - Just to avoid creating a new map unnecessarily on every render, but that probably doesn’t make much difference.
- I use a combo of Map with an array of tuples as initializer and Object.entries to generate a collection/dictionnary ? I found this pattern useful when dealing with tree data structure. Are they any caveats to this approach ? Should I be using Map instead ?
  - Also I find Map not so typescript friendly. I don’t understand why the has method is not some kind of typeguard under the hood. When using .has() the item is still undefined for typescript. Using some kind of collection instead I only have to check for the key existence
  - That .has() undefined bullshit pissed me off for a whole day I ended up abandoning Map permanently
- Copy before update to prevent state changes that can be read before re-rendering.
  - Considering objects, in Chrome/V8 the hidden class is preserved when a new prop with an integer key is added to the object. This speeds up the lookup since such props are stored as elements.
# discuss-gc
- ## 

- ## JavaScript garbage collection doesn't work how I expected when it comes to closures
- https://x.com/buildsghost/status/1818346107766030584
- A different design of timeouts could fix this problem, definitely more libraries need to be aware that they need to release scopes like this

# discuss
- ## 

- ## 

- ## 

- ## I wouldn't mind seeing some performance-oriented APIs being added to JS
- https://x.com/fabiospampinato/status/1866210254725239195
  - `Object.copyOwnPropertyDescriptor(s)` , it would delete the need to actually create property descriptors if we just want to copy stuff from an object to another.
  - String.isLatin1, you can check for this in userland by going through the whole string, but for the engine it can be a constant time operation.
  - `Object.isPropertyGetter/Setter` , you could check for this by getting the property descriptor, but if you want to specially handle getters/setters in an environment where usually you wouldn't see any of them, then you'd be paying the cost of these property descriptors for nothing.
  - `Function.prototype.bound` , being able to know what the originally function that was bound is could be a very cheap form of branding, adding symbols to the bound function or anything else I've tried isn't as fast as that could be.

- I think it’d be nice to be able to make certain optimization assertions to the engine, and have it fail hard on deopt. Like “all usage of this function is monomorphic”. Could be high impact for lots of code & could act as automated test to catch broken perf assumptions
  - I think it may be worth collecting a bunch of these and introducing a "use stricter" eventually 
  - it was discussed already and discarded as an idea (it was called "use strong"), but it feels to me like there's still stuff that should be fixed 

- Object.create(Object.getPrototypeOf(source), Object.getOwnPropertyDescrptors(source)); is not too bad but agreed creating those to reparse those is a waste, although engines could optimize that pattern like they do in other occasions, see the for loop i to length.

- ## [Optimizing Javascript for fun and for profit _202403](https://romgrk.com/posts/optimizing-javascript)

- ## 真的绝了，没想到分支预测对性能的影响有这么明显。不论怎么跑，三元表达式一定相对更慢
- https://twitter.com/isukkaw/status/1764654438785200536
  - map['p1'] (更快; p1对应0/1)   vs   false ? 0 : 1

- ## if you store values in a `Map` (as key) and to avoid leaks use `WeakRef` to wrap their counterpart, 
- https://twitter.com/WebReflection/status/1752296107680416191
  - don't test `.has(value)` on map, test `.get(value)?.deref()` instead because the GC might kick after the WeakRef has stopped retaining the ref.

- ## For JS runtimes/engines, a lot of performance optimizations look like
- https://twitter.com/jarredsumner/status/1743982090100908068
  - if you want to loop over all the properties in an object quickly, first you have to check if it’s an object and then if it’s observable that you can loop over the properties (Proxy trap for getOwnPropertyNames) 
  - And if it is not observable, maybe you can do a fast path
  - Is there only indexed properties (numbers)? Looping over an array as a string means converting every property from an integer to a string first. You probably don’t want that. So first you have to check 
  - The number of edgecases to worry about balloon as you add more specialized optimizations 
  - I would say runtime I/O APIs have different challenges, more about wiring up system calls together in a developer-friendly way + cross-platform + error handling

- The fun part (security problems and bugs) come from being incorrect in that assumption it isn't observable. Proxy has done this to a lot of things.

- ## when you pay attention to memory usage in javascript (TL; DR: be careful with overusing spread operators)
- https://twitter.com/vcapretz/status/1737575234247561465

- ## 深拷贝 JSON.parse(JSON.stringify(obj1))
- https://twitter.com/buaaxhm/status/1735484597159530650
- v8对这种写法有特殊优化，只要识别到这种函数调用方式就会自动做深拷贝优化
  - 很多老旧的library里面也是这样写的，新项目可能还在依赖旧版本的npm包，所以js引擎对这种旧写法也要做优化
- 如果需要深拷贝，可以试试 structuredClone
  - structuredClone 性能甚至只有通过 JSON 拷贝的三分之一

- ## benchmarking JS parsers' napi speed.
- https://twitter.com/hd_nvim/status/1726505034287030367
  - I am not confident in the benchmark code. 
- I'm pretty sure serialization/ffi is the bottleneck of most Rust parser. e.g. oxc can outperform tsc by twofold if no serde is done.
- tree-sitter itself is on-par with babel parser, both of which are slower than tsc.
  - one more thing: @babel/core is slower than @babel/parser . I used core here because only core has the async API. Under the hood core still uses sync parser and the extra code around core makes it slower.  That said, core is probably the better choice to emulate real-life usage.

- ## Timers are expensive in general. 
- https://twitter.com/jarredsumner/status/1660421032027750400
  - setTimeout is at least one JS value that has to be held onto and keep the event alive (your function). 
  - Calling the function itself is a little bit expensive. Reading the timer is a syscall (系统调用 on Linux)
  - Each one is a memory allocation to hold those values and the function and a reference to an event loop timer
- isn't it just a while(true) loop and very interaction checking if something needs to happen?
- Does AbortSignal.timeout() follow this same behavior?
  - Depends on the implementation but in bun yes and I imagine in other implementations too

- ## Performance tip: if you're working with *large* objects (10KB and larger), it'll be way faster to parse them as JSON strings rather than consuming them directly in your JavaScript as objects
- https://twitter.com/mgechev/status/1366259446154989569
  - because json grammar is uch simpler than js grammar
  - json can be parsed more efficiently than js.
- not for GTA apparently

- ## what's the best way to do a perf profile trace on a TS file under Node, then view the results as line-by-line hotspot information in VS Code?
- https://twitter.com/acemarke/status/1372385260147724288
- you mean like flamegraph?
  - No, because that's normally per-function. I actually want to get an idea of how many ms were spent per line

- ## It always cracks me up when JavaScript developers are concerned about performance.
- https://twitter.com/mjackson/status/1372285513969725440
  - Like, you're using JavaScript. That ship already sailed.
- Depends on what you’re doing I guess. 
  - Sure, if you’re building a compiler, JS might not be the best language (we’ve seen this play out lately). 
  - But most tasks people use JS for are not CPU bound at all, and JS is plenty fast. Definitely way faster than other scripting languages.
- Is it just sarcasm(讽刺，嘲讽，挖苦)? Doesn’t make any sense to me though. 
  - Whats alternate on client side? Even if you use server side rendering, still you need to use JS on client side (mostly). 
  - For NodeJS, it has its own pros and cons but you can’t argue its performance, Its just fine.
  - I'm sure he means from the Server Side. Sure, NodeJS is *fine*, but there are faster alternatives, such as those coming from Rust, such as actix-web.
  - This is a reason to care about performance even more in JS, since you're already starting out at a disadvantage (compare to compiled languages, JS is faster than Python or Ruby).
- I agree, as long as we do not use JavaScript to do the thing basic HTML and CSS animation can do.
- In most of cases, performance is an architectural problem, not language problem.

- ## [Deep Cloning Objects in JavaScript, the Modern Way](https://www.builder.io/blog/structured-clone)
- there's now a native way in JavaScript to do deep copies of objects
- `structuredClone` function is built into the JavaScript runtime
  - Clone infinitely nested objects and arrays
  - Clone circular references
  - Clone any transferrable objects, such as Date, Set, Map, Error, RegExp, ArrayBuffer, Blob, File, ImageData, and several more
- Why not just Object.assign or object spread?
  - shallow copy
- Why not JSON.parse(JSON.stringify(x)) ?
  - JSON.stringify can only handle basic objects, arrays, and primitives. 
- Why not _.cloneDeep?
  - Import Cost 

- ## Understanding monomorphism(单态，单一形式) can improve your JavaScript performance 60x.
- https://twitter.com/mhevery/status/1622499229813047296
- First things to understand is that CPUs only understand arrays, so your object/classes need to get translated into arrays which CPUs can work with.
  - Similarly a property access needs to get translated into an array access.
- Doing indexOf all of the time would be expensive, (and it is) so VMs employ a special strategy called inline-caching which speed up the access 60x like so:
  - If it is a class we have already seen, then we know the property is at location 1 otherwise we revert to indexOf.
  - Most VMs are willing to inline-cache up to 4 different shapes, before they give up.
- `indexOf` implementation is a bit more complicated. The actual function has something called megamorphic cache which in chrome is 1024 entries.
  - This explains why access gets slightly slower for 1-4, and than stays relatively stable until 1, 000 entries.
  - Past that no cache.
- This is important to keep in mind when you are creating micro-benchmarks. Most micro-benchmarks don't have enough variety of class shapes to overwhelm the inline or megamorphic cache and so the performance in benchmarks looks better than real world performance.
- These perf tricks are only applicable once the JIT kicks in. Which means the first N executions run in slow mode with no caching.
- The thing to think about is for any given property read how many possible ClassShapes do you expect that the objects will have. Your goal should be to have exactly one for best performance.
