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
# discuss-array/map
- ## 

- ## Performance tip: if you need to set a lot of dynamic keys to an object, a Map can give you better perf
- https://twitter.com/Steve8708/status/1508502291170484224
  - In short, JS VMs try to assume a shape of an object using a hidden class. When the shape changes, this can lead to a deopt
  - It's the same reason why setting a property to null/undefined can be faster than deleting
  - A Map, on the other hand, is optimized for this very use case of frequently adding and removing keys (see the "performance" table row here)

- ## 💡 And as a principal dev, I've had the map/filter/reduce ripped out in hot paths where copying Arrays is a lot more expensive than just a for loop.
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
# discuss
- ## 

- ## 

- ## 

- ## 

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
