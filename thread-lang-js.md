---
title: thread-lang-js
tags: [lang-js, thread]
created: 2023-11-10T08:06:12.113Z
modified: 2023-11-10T08:06:18.791Z
---

# thread-lang-js

# guide

```JS
Symbol('a') === Symbol('a'); //false
```

# discuss
- ## 

- ## 

- ## 

- ## TIL: `structuredClone()` will clone only once a reference to the same object
- https://twitter.com/oriSomething/status/1725144694059851866
  - structureClone works with cycles

```JS
const obj1 = { p: 11 };
const obj2 = { a: obj1, b: obj1 }
const c = structuredClone(obj2)
c.a === c.b // true
```

- ## Problem: If a function accepts multiple parameters of the same type, we may accidentally pass arguments in the wrong order. Types can’t protect us. 
- https://twitter.com/housecor/status/1715052861417980207
  - Solution: Accept an object instead.
- I do this when I have more than 3+ params.
- I agree with you, but only on non-performance centric stuff (so, frontend) When you pass an object you need to allocate that space in memory just to destructure that on the other side.

- ## TIL that this is correct syntax and that `finally` runs after the `return` of the function
- https://twitter.com/alexdotjs/status/1704472735219339585
  - https://twitter.com/ryanjhunter/status/1704767415228448948
- You can even `return false` in the finally block and change the return value after the fact.

- ## JS trivial! which `value` breaks if you: `${value}` but work if you do? `String(value)`

- https://twitter.com/manucorporat/status/1656669731892645891
  - i was not aware of this behaviour before, specially since `Symbol().toString()` works!

- ## [Why do you actually need higher order functions? : learnjavascript](https://www.reddit.com/r/learnjavascript/comments/rgddk9/why_do_you_actually_need_higher_order_functions/)
- Your code sample is an example of currying, where a function that accepts multiple arguments can be rewritten as a series of functions that each accept one argument. This is just one of the many uses of higher order functions.
- One much more common use for higher order functions is to abstract some patterns like looping over an array and performing some action for each value in the array
  - This is so common it is built in to the language as a standard method on arrays. 

- ## 函数式编程很讨厌的一点是，压缩后的代码完全不可读，函数名会被完全混淆。如果是之前的对象编程，可以通过查找对象上的方法名进行生产环境的 debugger，对象的名称会被混淆，但是其上的方法和属性不会😅
- https://twitter.com/_Xheldon/status/1548967766211698688
- 转念一想，函数式压缩混淆更有效

- ##  `Object.setPrototypeOf` and `util.inherits` are terrible for performance
- https://twitter.com/jarredsumner/status/1619342661701496833
- for me it’s Object.create
- is class inheritance more performant?
  - Class inheritance is just setting the prototype, i assume the perf issue here is changing the prototype halfway through an object's lifecycle (like setting __proto__!), because it means the JIT has to throw away its work and reoptimise for a completely new set of methods

- ## [A Better Way to Work With Number and Date Inputs in JavaScript](https://www.builder.io/blog/numbers-and-dates)

```JS
const myInput = document.querySelector('input.my-input')
const number = myInput.valueAsNumber

const date = myDateInput.valueAsDate
```

- ## Here are 8 ways to simplify a fetch function.
- https://twitter.com/housecor/status/1596944108794548224
- Why I prefer function declarations for top-level functions
  1. They're more scannable - It's easier to see at a glance that they're functions, not mere variables.
  2. Order doesn't matter. Function declarations are hoisted.
  3. Can export default on the same line if desired.

- ## function call: `return` does override the normal instantiation behavior but only if an object is returned
- https://twitter.com/rauschma/status/1533061880830431232

```JS
function f1() {
  return 123;
}
console.log('f1', new f1() instanceof f1); // true

function f2() {
  return {};
}
console.log('f2', new f2() instanceof f2); // false
```

- if explicitly we are returning an object from a function , even calling with new will get explicit object instead of newly fret we object ? 🙏 whole my life I did not know this 😑
  - not just function, classes too, even if classes require `new` to be invoked, while functions don't (and arrows can't use new)

- ## debugging tip—detecting invisible characters in strings:
- https://twitter.com/rauschma/status/1525840065330659334
  - console.log(JSON.stringify(Array.from('a​b')))
  - // ["a", "​", "b"]
- Why do you need JSON.stringify? u may console.log([...'a​b'])
  - I like to see \n, \t, etc.

```JS
JSON.stringify(Array.from(`a
b​`))
```

- Nice touch: When you enter text in Chrome’s console each zero-width space is displayed as “•”.
  - https://twitter.com/rauschma/status/1525841738140684289

- ## Just added an issue noting that we intend to deprecate the "object" syntax for `createReducer` and `createSlice.extraReducers` , 
- https://twitter.com/acemarke/status/1521439296972115969
  - and intend to add a runtime warning in RTK 1.9 saying to migrate to the "builder" syntax instead.
- In other words, you should change from:

```JS
extraReducers: {
  [todoAdded]: (state, action) => {}
}

// to:

extraReducers: builder => {
  builder.addCase(todoAdded, (state, action) => {})
}
```

- This has better TS inference and circular import handling.

- Any thought of adding builder syntax to the plain “reducer” property of createSlice? Would add consistency and help with file splitting (just pass the builder). 

- ## TIL that assigning default values in object destructure only protects you from `undefined` , not `null`

- https://twitter.com/he_zhenghao/status/1516542439334371335

- ## I was 30 seconds ago years old when I learned this "works":
- https://twitter.com/acemarke/status/1511429178461241354

```JS
let obj = { 42: "life" }
let arr = ["42"]
arr.toString()
// '42'
obj[arr]
// 'life'
```

- ## JS's lack of a `defaultdict` equivalent continues to be an annoyance.  Gotta keep doing checks like:
- https://twitter.com/acemarke/status/1509619347676975114
  - if (!obj[key]) { obj[key] = [] }
  - obj[key].push(item)
- Maybe the logical nullish assignment operator could improve this a little?
  - obj.key ??= []
  - obj.key.push(…)
- This is a pattern you'd typically see in a `.reduce()` loop - typically some kind of a "group by" behavior. It's safe to mutate `obj` because it was freshly created for the loop, but there may not be an array for this key yet b/c we haven't seen it before.

- ## TIL: In javascript, assignment operation returns the value assigned. 
- https://twitter.com/bpsagar/status/1470015051671040000
  - So, the assignment operation can be used in an if condition and create a nice scoped (not syntactically) variable. Found it in Prosemirror's code. 

- ## I rarely see the “in” operator used in JS. Why not?
- https://twitter.com/jarredsumner/status/1471867724678664192
  - 若属性名存在且属性值为undefined，in会返回true，但typeof却是undefined

- ## If you want to run a piece of code multiple times (e.g. while evolving it), you can also wrap it in a code block
- https://twitter.com/rauschma/status/1443339928503529478

```JS
// js代码块，默认是块级作用域，不会污染全局变量，适合用于测试
{
  const str1 = 'abc';
  const str2 = str1 + 'def';
  console.log(str2);
}
```

- ## “foo” === “foo” in JavaScript returned false. Can you guess why? 
- https://twitter.com/jarredsumner/status/1443117924894470147
  - Hint: one “foo” came from a fetch() response body

- ## Moved some of my smaller libs to JSDoc TS; thoroughly recommend it. 
- https://twitter.com/Rich_Harris/status/1440639878065111048
  - Among other things, the resulting code is generally smaller than transpiled code. 
  - Building, testing etc all become much less finicky.
  - An underdiscussed benefit of JS over TS - I'll frequently test individual functions by pasting them into the browser console. There's no faster feedback loop. You can't do that with TS.

- ## null >= 0  // true
- https://twitter.com/andrestaltz/status/1435244740975468547
  - null > 0   // false
  - null == 0  // false
  - null === 0 // false

- ## Anyone have a maintained alternative to node-fetch? Apparently they've gone ESM-only and so I can't use them in my many CommonJS Node servers.
- https://twitter.com/domenic/status/1433190271764860930
- CommonJS cannot use top-level await, and I cannot delay getting the ability to fetch things.
  - You could create a utils/fetch.js in your repo
- I'm kind of ok staying on it - "We recommend you stay on v2 which is built with CommonJS unless you use ESM yourself. 

- ## Are dynamic imports inside npm packages a bad idea? 
- https://twitter.com/devongovett/status/1432864590828769290
  - Usecase: I'm thinking of is loading translations on demand to avoid large bundles, especially when a component supports many languages that not all apps will need. 
  - Generally code splitting decisions should be left to apps IMO
- Really wish there was a standardized way of distributing translations that was supported by bundlers/build tools, and maybe even the browser. i.e. imagine being able to specify at build time what languages you support, and generating a JS bundle for each language.
  - A thing I'm worried about with the dynamic import approach is that if each component does this, you'll end up with a ton of HTTP requests as each one loads its own translations separately. Would be more optimal to bundle the translations for the same language across components.
- I had a similar issue with open-sourcing our product tour library. I don’t want to load the code for the tour if it’s not showing up. 
  - The approach I took was accepting a component as a prop to the parent
  - This works for most build systems, including Next
- Radpack: Infusing the greatest benefits of modern bundlers (Webpack, Rollup) and loaders (SystemJS, RequireJS) into an all-inclusive build and run-time solution optimized for the end-user experience.
  - Bundlers like Webpack do a great job at providing a toolset needed to deliver an optimal out-of-the-box delivery solution for your end-users. 
  - Most loaders on the other hand, are focused on delivering only the requested assets, as they are needed. 
  - Radpack fuses the best of both worlds by taking advantage of build-time bundling, with graph-based run-time loading.

- ## My favorite way to create a new JavaScript object with a property omitted is Rest/spread.
- https://twitter.com/housecor/status/1430232426106826754
  - const { address, ...userWithoutAddress } = user; 
- I'd rather use the spread operator and the good old 'delete newObj.prop'.makes it much more readable for non js devs.
- but unnecessary it will create `address` variable
  - I like to pick object properties using `lodash.pick`

```JS
// And if you're using a dynamic field

const propertyToRemove = 'email';

const {
  [propertyToRemove]: removed,
  ...userWithoutEmail
} = user;
```

- ## You can keep your types DRY by using the ReturnType and Parameters built-in types when you wrap an existing function
- https://twitter.com/NetanelBasal/status/1429819098133934080

- ## JavaScript supports dynamic keys on object literals.
- https://twitter.com/markdalgleish/status/1428876341735165954
  - We lean on this feature heavily in vanilla-extract so you can use hashed values as keys.
- Using object keys in WeakMaps for memoization is pretty awesome. Saves writing cleanup code.
  - We have a webpack based static renderer tool that needs access to webpack stats which is quite expensive to generate. We use WeakMaps to cache the stats object per compilation.
- Also your key can be a Symbol, which is a nice way of ensuring it doesn’t clash with an existing key.

- ## New Node module: "base128-encoding", 
- https://twitter.com/fabiospampinato/status/1427298867113037829
  - it's not as memory efficient as base256-encoding _when in memory_, it still doesn't produce friendly strings like base64, 
  - but it's the most memory efficient encoding for writing strings to disk that need to be imported.
- Somewhat interestingly writing a module as latin1/base256 makes it throw when imported at times, I think JS or at least Node is expecting the file to be utf-8 encoded. 
  - base128 is basically the memory-efficient subset of utf-8 that always requires 1 byte per character.
- Some numbers when using different encodings with a file of mine:
  - base64: 1.65MB on memory & disk (utf8 & latin1).
  - base128: 1.45MB on memory & disk (utf8 & latin1).
  - base256 1.25MB on memory & disk latin1-encoded, 1.87MB utf8-encoded.
- Basically when optimizing for memory usage, base256 is the winner in memory and for latin1-encoded files, and base128 is the winner for utf-8 encoded files. 
  - Unless engines change it's impossible to do better than this. 
  - When optimizing for other things, base64 may be the go-to.
- Interestingly gzipped base64-encoded files may be smaller than gzipped base128-encoded files
  - No idea why, maybe using fewer characters overall helps the compression algorithm somewhat, I'm pretty surprised by this.

- ## New Node module: "base256-encoding", 
- https://twitter.com/fabiospampinato/status/1426299747522994181
  - if you need to store something like a big base64-encoded string in memory, switching to base256 will save you up to 75% of memory per string.
  - Base256 is like base64, but it uses all the 256 1-byte codepoints instead of just 64 of them, saving you some memory.

- ## New Node module, a weird one: "base256-archive", 
- https://twitter.com/fabiospampinato/status/1426645445917478915
  - it's basically a tiny serialization/deserialization library designed to leverage base256 encoding in order to save you ~50% of memory  (could be ~88% in pathological cases).
  - You should go with JSON most of the times, but if you need to store a string or mini database in memory (like a spell-checker dictionary or grammars for syntax highlighting or something) this can save you a decent amount of memory.
  - The fundamental problem is that a string of a million "a"s requires 1MB of memory, but add an emoji at the end of that and the whole string suddenly requires 2MB of memory. That's so weird. I wish we could get sane (and fast!) strings like they recently added sane integers.

- ## What is `[] + []` in JavaScript?
- https://twitter.com/jaredpalmer/status/1423394089207312387
  - `''`

- ## namespace import items order
- https://twitter.com/haoqunjiang/status/1422951822864515082
  - ECMAScript actually requires the keys to be sorted by %Array.prototype.sort% using undefined as comparefn. 
- So if using a minifier this would be, more or less, undefined behavior? Seems an odd decision to make. 

- ## Let's re-implement 10 lodash functions to learn more about how `.reduce` works
- https://twitter.com/benmvp/status/1418003584386359296
  - [Learn the Array reduce method by re-implementing lodash functions](https://www.benmvp.com/blog/learn-array-reduce-method-reimplementing-lodash-functions/)

- ## Someone is trying to convince me (with several exclamation marks) that `() => []` is not a pure function because it returns a different array every time. That… can’t be right? Or is it? I’m genuinely confused.
- https://twitter.com/dan_abramov/status/1413982626302631938
- From my understanding from purity and functional programming, a function would return the same result with the same input. This doesn’t mean the same reference. Creating a new object will mean creating a new reference
- At least in practical coding, I've never seen an argument that a pure function must return literally the _same reference_ given the same inputs.  Just a _consistent_ set of values for those inputs.
- Maybe technically? But if memory allocation is a side effect then I’m not sure there are many pure functions at all.
- A pure function returns identical results for identical inputs. So it depends on your definition of identical. Once records and tuples are available in JS: `() => []` is not pure; `() => #[]` is pure
  - Said another way, a function can't be pure in JS unless fn(x) === fn(x)
- Pure doesn't mean it returns the same reference in memory, it means it returns an identical value every time. If it *did* mean that, it would be a worthless definition for practical application
- Technically impure; Conceptually pure
- With proxy-based usage tracking in mind any memorised function is not pure, even having the absolutely same result across different runs, as it causes different reads and thus different side effects in trackers… and pure function should not have side effects

- ## TIL that in JavaScript the `arguments` object holds references to the function parameters and you can even modify them outside. 
- https://twitter.com/aemkei/status/1412880220223381508
  - This is a unique behavior and only works in non-strict mode.

- ## alias vs dot in property accessors
- https://twitter.com/tannerlinsley/status/1408919939168100353
- You can always alias in a destructure, but these days I’m destructuring way less than I used and most others. Keeping context for variables/properties is actually extremely helpful
  - Keeping context is a plus, and also TypeScript likes it more. For react-query, the `status` field and the derived booleans can narrow the type of `data` and `error` , but that doesn’t work if you destruct
- Same here. Even stopped destructuring component props. Namespaces help me know where variables come from.
  - Also less worrying about name conflicts

- ##  `obj?.prop1?.func?.(args)` TIL you can use optional chaining on function calls 
- https://twitter.com/Swizec/status/1407762472614854656
- Yes! It's a substitute for short circuit syntax
  - `foo && foo();` vs foo?.(); 
- And property accessors using bracket notation / arrays:
  - `object?.deepProp?.['evenDeeperProp']`

- ## we can use Opaque or Branded types in our advantage to detect if user passed a value or the value has been initialized to default set value. 
- https://twitter.com/anuraghazru/status/1405925522102657029
  - Use branded types or opaque types to make them act as nominal types.
  - 处理多级很深的路径属性及默认值的一种方法

- ## You can substitute an if-statement checking for a truthy value with an expression using short-circuit evaluation and the logical && and
- https://twitter.com/ThaddeusJiang/status/1403848377943543809
- 说实话，我现在负责的项目中已经存在了大量这样的代码，我非常不喜欢。已经和同事解释过了，今后不允许这样的代码，已经存在的也在慢慢改回 if
  - 从可读性考量，减少不必要的脑力负担。
- React 中用来判断一个 Component 是否该出现，我感觉挺有用的哈哈。
  - 不一样。Component 的 return 一定是 jsx，但是普通函数返回值可以是任意，甚至可以不返回。
- 比较赞同，代码的可读性更重要
  - 代码逻辑直观比较好，
  - 利用语言特性去体现逻辑太隐晦了

- ## The point of Symbols is that they are unique and primitive at the same time. 
- https://twitter.com/asleMammadam/status/1382641865883852802
  - We can use them as a sign of our values. 
  - As we may know, objects are unique too, but not primitives, which means they're not something like numbers or strings, but Symbols are.
  - You can also use Symbols for object's keys, so no one can access them unless they have that symbol.

- ## Who's interested in mutation-free JS "algorithms" for common data transformations that are only a single statement?
- https://twitter.com/benmvp/status/1379569782656135169
- Deleting an item from an array by using `.filter` to return everything but the target
- Replacing an item at an array index by taking slices before and after the index, and then spreading into a new array with the new item
  - (probably not the best solution if your array can be large because of the intermediary array slices)
- Creating an empty array of X items (a la _.times) by using `Array.from` and its lesser-known(?) 2nd argument that's a map function
  - ( `Array.from` accepts any object that has a length property and indexed elements 😉)
- Mapping the values/keys of an object (a la _.mapValues & _.mapKeys) by using `Object.entries` (object ➡️ pairs) + `.map` (new pairs) + `Object.fromEntries` (new pairs ➡️ new object)
  - we can even map the keys & values simultaneously 
- Creating an array of unique values (a la _.uniq) or a union of arrays (a la _.union) by converting to a `Set` and spreading it into a new array
- Picking / omitting from an object (a la _.pick & _.omit) by using `Object.entries` (object ➡️ pairs) + `.filter` (select/drop pairs) + `Object.fromEntries` (filtered pairs ➡️ new object)
  - (very similar to mapping values/keys but uses `.filter` instead of `.map` )
- [Generate a Dynamically Sized Array with Unique Values](https://justinnoel.dev/2019/09/27/generate-a-dynamically-sized-array-with-unique-values/)

- ## Which could pick non-enumerable properties from object
- https://twitter.com/buildsghost/status/1378138160664735744
- To be clear, there are correct answers either way, Lodash and TypeScript made different choices (intentionally or not), each might have been the most reasonable choice for them. I'm wondering if a new library should match one or the other
- TypeScript's behavior matches my mental model. Omit to me is "copy literally everything except these specific properties" IMO that includes non-enumerable properties, but tbh I don't think I care about non-enumerable properties very often so I haven't thought too hard about it.

- ## [RFC] Proposal for dropping ie11 support in Vue 3
- https://twitter.com/youyuxi/status/1378006612435214337
  - https://github.com/vuejs/rfcs/discussions/296
- [The cost of supporting IE11 in Vue 3](https://github.com/vuejs/rfcs/blob/ie11/active-rfcs/0000-vue3-ie11-support.md#motivation)

- ## why don't other languages have destructuring assignment like JS added in ES6?
- https://twitter.com/acemarke/status/1375564793361358851
- other people are saying it too, but this is generally a functional programming thing that imperative languages are adding. elixir, haskell, ocaml all have it
- AFAIK you can destruct a Tuple and List returned from a function in Python. Not fully feature fledged like in JS but it fill in some gaps
- Pretty much any language with pattern matching allows you to do this. eg.  Rust, ReScript
  - Swift and scala also. I suppose a requirement is for pattern matching to be allowed as an expression
- I might be wrong but I think Kotlin has this as well.

- ## what do you mean when you say:"objects naturally represent orthogonality"?
- https://twitter.com/hhg2288/status/1374707460397760512
- If you modify one value in an object, the other values are unaffected. 
  - An object can represent multiple things (key-value pairs) at the same time, and those things can change independently.
- also from Wikipedia:
  - "Orthogonality is a system design property which guarantees that **modifying the technical effect produced by a component of a system neither creates nor propagates side effects to other components of the system**."

- ## "let" and "else if" are often bad smells in JavaScript. 
- https://twitter.com/neoziro/status/1374002846681731078
  - You can easily replace them using a ternary or a self-invoking function.
- Immutability helps, sure. 
  - But you've got a function with three returns and two if statements. 
  - The cyclomatic complexity is higher because of multiple paths and the risk of error is higher because the default value is at the end. 
  - Increased complexity <= immutability
  - Additionally, i don't understand why you'd choose an IIFE over a function that could return. 
  - Agree, since the time we acquired `let` and modules, IIFE is a smell. Are there still any use cases for it?
- I would disagree with that statement. Ternary is good but if you have more than one condition it often becomes nightmare. And IIFE produces unnecessary memory allocation.
  - Let-else-if has the same level of visibility as IIFE and comes with less cost.
- Both ways are ugly at some point. We need pattern matching to stop these discussions.

- ## I'm always surprised when I see `window.` in front of global APIs in JS code, but I guess it's just a matter of preference?
- https://twitter.com/RReverser/status/1373817866420695042
  - What do you normally use for global things like `document` , `postMessage` , `addEventListener` , `fetch` etc.?
- funny self.someAPI wasn't there ... as window doesn't exist in Workers ... 
  - anyway, there are cases where you don't have globals (see LinkeDOM) so, in such case, passing a window/self and a document is better than polluting the global NodeJS env with these.
  - No other use cases here
- When the context is specific to window and not that it happens to be the same object as the “global” I include it. Like window.addEventListener() but not fetch()
  - Said another way, addEventListener is defined in the spec on EventTarget. Window extends EventTarget like other things like Node does. It isn’t conceptually on window just because it’s a “global variable” (conceptually, I know WebIDL is complicated)
  - fetch() is not. It’s specifically specced as being on the WindowOrWorkerGlobalScope
  - What about non-functions - document, location, etc.?
  - When it’s effectively only on window because global variables are the rage, I don’t do window. XXX (document, location) but when it very specifically refers to the physical window itself like window.innerWidth I do. There are probably ones that are grey areas or where I break this “rule” because I don’t really give it much thought other than what just feels natural. Just explaining the gist of the feeling. It’s not actually a rule.
  - Doing the same, often out of what feels natural, or when I know that it is specific to window, for clarity. Seems like an opportunity to shine some light on in devrel channels, at least I'd find it interesting 
- window.someAPI is more greppable and guarantees codebase-wise consistency if enforced
  - I saw many times where something that seemed like a global API was a ref to a local var (or `fetch` was from an imported lib)
  - Too, I mostly prefer to explicitly put `window` everywhere to make globals more distinct, b/c I think it's generally helpful too see where things are coming from, but `window.document` seems super odd to me and I have never used it.
- We use window-prefixed in our project to be able to mock all the DOM stuff in tests with something like jsdom. Generally the less global references, the easier to stub/mock/test
  - Eg a library for browsers being unit-tested under Node, where there’s no window or document.
- I find that prefixing with window is a useful visual cue when using SSR that someAPI is only meant for client side and cannot/shouldn’t be polyfilled.
  - Examples: window.localStorage (client only) vs fetch (client or server)

- ## TIL "void" operator evaluates the given expression and then returns undefined.
- https://twitter.com/neoziro/status/1373645418035306496
- Oh I gotta use `void` more instead of adding dumb ugly curly braces

- ## Converting an array of objects into an object lookup is something I've always needed in my data utility functions
- https://twitter.com/benmvp/status/1371966367100891140
  - I think I've gotten it down to its minimalist version
  - all the way from creating an empty object and assigning to it within a for-loop
- I would really like to use Map (and Set) more but I find that using regular objects ends up being easiest

- ## We really need an API for inspecting the ES module graph. Wasn't someone working on this?
- https://twitter.com/_developit/status/1371528639926403079
- It's sort of possible in Node by hooking into the module loader, with a small amount of guesswork but no reparsing. But it's straight up not a thing in-browser. This would make HMR so, so much more effective.

- ##  `export default` is bad. Don't do it. Ever.
- https://twitter.com/BenLesh/status/1370447621970669580
- Counterpoint(对照物): now you have to open the file to know what the module exports. Just a tradeoff. I ack your IDE may do this for you… Eclipse did lots for Java too.
- Unfortunately, React.lazy() only supports default exports.
  - Loadable Components could help us out here, though.
- From 20 Years of JavaScript, export default is only added late in the proposal to accommodate module.exports.
- I’d state it like this:
  - export named when you export for other humans to use
  - export default for frameworks to collect when traversing your directories (Next doesn’t care about the page component name, and no human will auto-import the page)
- I use default exports all the time. They're useful when you want to enforce a 1:1 relationship between a module and the interface it provides.

- ## 19 JAVASCRIPT NUGGETS!
- https://delicious-insights.com/en/posts/js-nuggets/

- ## All JavaScript functions should only be allowed to take one argument. 
- https://twitter.com/swyx/status/1198632709834326021
  - Take an object if you need to pass more than one piece of data.
  - Order independent
  - More Greppable codebase
  - Low cost of adding API
  - predictable pointfree JS
  - you already do this in @Reactjs as "props"
- i've been calling this the "Single All The Way" rule
  - there's a backend version of this too
  - Someone already coin the term for this philosophy, it's called RORO (Retrieve Object, Return Object). 
- In that way you lose currying unless you implement one that works with object
- Note that if the object is not persisted/wrapped in a closure, V8 will optimize that away. It’s pretty amazing. 
  - There are quite few more rules to it, so using multiple args might be better for performance sometimes.
- controversial controversial opinion: object destructuring should not be done in the function's params
  - I like destructuring in the arguments, but one pro to the latter form is that they're consts and the destructured ones are not (and, apparently controversial, but I think everything should be const unless you plan on reassigning it).
- I’m applying this rule when a function has more than 2 arguments, but applying to _every_ function is like too much.
- But React components are called with two arguments.
- This is where I love named params in swift. Wish JS had that.
- I’ve mostly only use positional args for either construction/dependency closure or in cases where partial application is expected.
  - Though an argument can be made that partial application is better served by a function that returns a function in many cases.
- Deno (typescript runtime) has it in their style guide of 3 args max, with the 3rd arg being an object if more than 3 properties are required.
- Yup, the 1 argument is better, especially the bigger the codebase is. Same reasoning applies to C#.
- Except lots of built in callbacks take two.

- ## I’m starting to have an opinion that *every* JS/TS function that takes more than one argument should take an object instead
- https://twitter.com/tlakomy/status/1362828075390631936
  - Better IDE support, code completion and you’ll never screw up the order of arguments
- I still prefer two args when there is a main argument and I put the rest in the second. eg: `format(code, options)` .
  - I hate losing myself in custom types for each function param object
- There is a pattern for that, its name is RORO (receive an object, return an object)
  - [Javascript RORO pattern - A nice way to write more readable functions](https://www.tinyblog.dev/blog/2020-07-13-javascript-roro-pattern/)
  - Receive an Object, Return and Object
  - functions should always accept an object as their parameters and they should always return an object as their result.
  - Receiving an Object as standard for all the functions I write is something I started doing after learning Python and getting experience with kwargs, which I greatly enjoyed since it made it so easy to know what was going into a function
  - I personally get a lot less utility of Return an Object than I do Receive an Object. 
  - Multiple return items are pretty nice, but I find that most functions I write only concern themselves with a single thing.
- One potential downside is that if you do not make the object properties readonly, the incoming object is mutable. 
  - This is not the case with non-object parameters since they are passed by value, not by reference.
- I find the pattern of having a max of two args a good balance: first is required and the second is optional. 
- Been doing this for years. 
  - The only exceptions are extremely rare: functions which implement unary or binary operators, which by definition are future proof. 
  - Another advantage in @typescript : it naturally encourages using named interfaces, making them readable and composable.
- I often follow this pattern as well, much more predictable for end user/third party and you can build in default behavior for undefined configuration options
- only downside is having to repeat every argument twice for TS declarations
- better for extending APIs without breakages as well. it’s the closest thing we have to named function parameters (yet)
  - I am absolutely of the same opinion. Also the extension or modification is much easier.
- Every time I don't make a function that accepts an object, I find myself regretting it so hard in the future 
- In @PixiJS we've been doing more of this. There are some APIs with perplexingly long args for historical reasons.
  - I only favor args when it really the logical order is baked-in, eg. setPosition(x, y) 
- The main advantage of the object arg is that it's super easy to refactor. 
  - Imagine you need to change the order, or add some optional arg
- I would prefer a python way. They have positional and named arguments at the syntax level.

- ## I just realized ternary operator is called that way because it handles THREE things at once
- https://twitter.com/vishwajeetv/status/1365121673922543622
- Personally I am not fan of the reduced readability introduced by ternary operator. I avoided them for years, and even today I use it sparingly. 
  - If else is much more readable and maintainable.
  - Short expressions *should* use the ternary operator.
  - The problem is that if/else is not an expression, but a statement

- ## Babel gave us an incredibly flexible ecosystem of plugins and presets. 
- https://twitter.com/mjackson/status/1361525113175171072
  - TypeScript (as a language) limits you to using whatever language features they choose to implement.
  - It’s always trade-offs when it comes to engineering, but what a price for type safety!
- TS is usually pretty good about implementing features at Stage 3

- ## Don’t use `delete` to remove a property from an object.
- https://twitter.com/SimonHoiberg/status/1357998820106399744
  - Instead, use the rest operator to create a new copy without the given property.
- Because `delete` mutates the original object, and the spread operator creates a ref to the original, it doesn't mutate it.
- How you will cover eslint error? Age variable is defined but not used.
  - `{ age: _age, ...other}` . Adding _ in front of a variable name tells the linter that it's ok if the variable in not being used
- The object will mutate when you add new properties or modify existing properties, so why decry(批评) only `delete` ?
  - If you want to avoid mutating object, use `Object.freeze()` ?

- ## Did you know that there was a time pre-ES5 where undefined could be globally redefined?
- https://twitter.com/oliverjumpertz/status/1357421013303259142
  - This is where the void operator came in handy. 
  - It forces an expression to return the primitive undefined instead of any overridden value.
- Saw void 0 today generated by TS, was a bit surprised
  - Yea, void 0 is the idiomatic way to enforce undefined

- ## does anyone know if using Symbol, instead of direct properties, is either faster or slower, *especially* in NodeJS or, in general, v8?
- https://twitter.com/WebReflection/status/1356911723920445440
- It made no difference
  - In this benchmark, symbols are 3.2 times slower

- ## I wish JavaScript import statements were written in reverse order so that autocomplete worked properly.
- https://twitter.com/markdalgleish/status/1356404787244195840
  - e.g. from 'lodash' import { debounce }
- Seems like a nice improvement at first glance, but I’m wondering how imports with side-effects could look
  - `from "./styles.css" import *` ; 

- ## Don't use functions as callbacks unless they're designed for it
- https://twitter.com/jaffathecake/status/1355188620932608006
- [Don't use functions as callbacks unless they're designed for it](https://jakearchibald.com/2021/function-callback-risks/)
- Here's the problem:

```JS
// Convert some numbers into human-readable strings:
import { toReadableNumber } from 'some-library';

// We think of:
const readableNumbers = someNumbers.map(toReadableNumber);
// …as being like:
const readableNumbers = someNumbers.map((n) => toReadableNumber(n));
// …but it's more like:
const readableNumbers = someNumbers.map((item, index, arr) =>
  toReadableNumber(item, index, arr),
);
```

- Everything works great until `some-library` is updated, then everything breaks.
- `toReadableNumber` wasn't designed to be a callback to `array.map`, so the safe thing to do is create your own function that is designed to work with `array.map`
- **The same issue, but with web platform functions**

```JS
// A promise for the next frame:
const nextFrame = () => new Promise(requestAnimationFrame);

// this is equivalent to:
const nextFrame = () =>
  new Promise((resolve, reject) => requestAnimationFrame(resolve, reject));
```

- **Option objects can have the same gotcha**

```JS
const controller = new AbortController();
const { signal } = controller;

// it's best to create an object that's designed to be addEventListener options:
el.addEventListener('mousemove', callback, { signal });
el.addEventListener('pointermove', callback, { signal });
el.addEventListener('touchmove', callback, { signal });
// el.addEventListener(name, callback, options);

// Later, remove all three listeners:
controller.abort();

// code below works today, but it might break in future.
const controller = new AbortController();
el.addEventListener(name, callback, controller);
```

- Watch out for functions being used as callbacks, and objects being used as options, unless they were designed for those purposes. 
  - Unfortunately it isn't something TypeScript warns about

- I guess that's probably more relevant when passing your own class functions as callbacks. Anyway, great advice!
  - yes that's a gotcha too, but thankfully it tends to obviously fail straight away

- ## Don't destructure deep properties. Put more on the right side. Use dot notation.
- https://twitter.com/tannerlinsley/status/1354948274281566208
  - Reserve it for smaller functions and variable namespaces.
  - It can *feel* like a productivity hack, but time and experience have taught me the opposite.
  - If you do too much of it unnecessarily, you might find yourself *re*structuring a lot, eg. Taking those same variables and reforming them into functions or other structures. 
  - It's much easier to spread an object than it is to type it all out again.
- I'm saying this because I am literally in the middle of a painful refactor caused mostly by this issue. I only have my yester-self to blame, too. Live and learn, right?
  - I'd add that when you destructure too much - especially down into primitives - then you discard your data model and pass props 1 by 1. When the structure changes, there'd be multiple places to change. If you keep your data model and pass it down, refactors will be cheaper.
- I dislike destructuring because ts won't narrow down the type.
- Destructuring also makes project wide search harder.
  - I want to find if user dot id is used. If I search for the whole term, destructured cases will be missed. If I search only for id, the search will have lot of other results like post id, item id.
  - You can destructure and alias
