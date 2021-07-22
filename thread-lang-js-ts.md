---
title: thread-lang-js-ts
tags: [js, lang, typescript]
created: '2021-01-28T14:33:59.037Z'
modified: '2021-01-28T14:34:20.579Z'
---

# thread-lang-js-ts

# repeat

- ## React TypeScript Cheatsheet
- https://github.com/typescript-cheatsheets/react
  - https://react-typescript-cheatsheet.netlify.app/docs/basic/setup

- more-cheatsheet
  - https://nerdcave.com/tailwind-cheat-sheet
# pieces
- ## 

- ## 

- ## 

- ## Let's re-implement 10 lodash functions to learn more about how `.reduce` works
- https://twitter.com/benmvp/status/1418003584386359296
  - [Learn the Array reduce method by re-implementing lodash functions](https://www.benmvp.com/blog/learn-array-reduce-method-reimplementing-lodash-functions/)



- ## Async functions & microtasks
- https://whistlr.info/2021/async-and-tasks/
- When you invoke an `async` function, the function will run its synchronous prefix immediately, but whenever you `await` something, the rest of its code will be put into a microtask.

```JS
console.info('a');
const p = foo(); // call async and hold Promise in p
console.info('b');
p.then(() => {
  console.info('c');
});

async function foo() {
  console.info('1');
  await Promise.resolve(); // actually do something async
  console.info('2');
}
// a 1 b 2 c
```

- Any time we `.then()` a Promise, that callback is executed as a microtask—broadly, that code is queued to run "immediately", but after the current execution and other microtasks. (And, the same happens when we use `await` on them.) 

- ## With the rise of async-await, I've noticed more and more JS developers have less understanding of concurrency and how to work with async code flow
- https://twitter.com/dev__adi/status/1417554978130915328
- [How to escape from the async/await hell](https://devadi.netlify.app/blog/async-await-hell)
  - While working with Asynchronous JavaScript, people often write multiple statements one after the other and slap an await before a function call. 
  - **This causes performance issues, as many times one statement doesn’t depend on the previous one** — but you still have to wait for the previous one to complete.
  - One interesting property of promises is that you can get a promise in one line and wait for it to resolve in another. This is the key to escaping async/await hell.
- How to get out of async/await hell ?
  - Find statements which depend on the execution of other statements
  - Group-dependent statements in async functions
  - Execute these async functions concurrently: Two common patterns of doing this is returning promises early and the `Promise.all` method.

- ## TypeScript: .map() only works for Arrays, not for tuples.
- https://twitter.com/rauschma/status/1415750873788071939
- You can still *implement* with .map(), you just need a cast
- In fp-ts this is called `Tuple.bimap`

- ## A very common #typescript pattern with some kinda tricky types behind the scenes. 
- https://twitter.com/steveruizok/status/1415641397265379328
  - The second arg's type is based on the first arg
  - https://codesandbox.io/s/type-mapping-and-filtering-k6k2e

- ## TIL Node.js v15 or higher can generate UUID v4 using `crypto.randomUUID()` ; 
- https://twitter.com/Kikobeats/status/1414661088247963652
  - `crypto.randomUUID([options])` ：Added in: v15.6.0
  - ts-node is a TypeScript execution engine and REPL for Node.js. 
  - ts-node非常适合测试api，内置模块也需要import('fs')或者require('fs')，两者都支持；
  - node版本更新太快，注意兼容性，甚至被删除或不存在

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

- ## If you want to learn advanced @typescript techniques quickly, try retro-typing a library written completely in JavaScript. 
- https://twitter.com/DavidKPiano/status/1413149144252702729
  - It's not just a skill, it's an art form and an arduous(艰难的) adventure.
- we have the existing DT types to work from.

- ## TIL that in JavaScript the `arguments` object holds references to the function parameters and you can even modify them outside. 
- https://twitter.com/aemkei/status/1412880220223381508
  - This is a unique behavior and only works in non-strict mode.

- ## I often use JavaScript Maps and Sets and often have to enumerate over them. 
- https://twitter.com/trueadm/status/1411457860698005504
  - I benchmarked this about a year ago, and found extracting an array via `Array.from` and then looping over was fastest. 
  - Now it turns out `for…of` on the Map/Set is fastest. How things change.
- This was consistent between all browsers JS engines too. 
  - Interestingly, JSC (Safari) performs really well for cloning Sets and Maps via using the `constructor` .
  - `const clone = new Map(oldMap)` // clone
  - Every other JS engine performs better if you manually loop over and copy into the clone.
  - I mean using the `constructor` is by far the nicest way of doing it. I'd love it if the folks working on V8 and SpiderMonkey could optimize this code-path like the folks working on JSC have.
  - Probably not worth micro optimising then?
  - I think it is. I've found compilers and parsers to be good use-cases where these operations are frequent enough to translate into seconds of build time performance.
- The problem of course is the polyfill. Using the Babel polyfill for `for…of` statements means performance drops dramatically. Almost to the point where you consider not using them still.
- This week I found a >2x perf win on latest V8 by switching some heavy nested object iteration from `for (var [k, v] of Object.entries(o))` to `for (var k in o)` .
  - The use-case was to accumulate an array of all keys two levels deep.
  - Yup, `for/in` is much faster especially if your objects have stable shapes; especially in unoptimized code. Be careful with microbenchmarks. (But only if it matters...)
  - When using `for…in` it's also recommended to use `hasOwnProperty` , which adds additional overhead.

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
  - object?.deepProp?.['evenDeeperProp']

- ## Classes were a good addition to JS. Private fields I'm more skeptical about—mostly because classes are not a good level for managing visibility, modules are.
- https://twitter.com/MarijnJH/status/1408004016752283648

- ## I wish there were a way in JavaScript for generators to tell that they have been closed, like when breaking out of a for loop.
- https://twitter.com/justinfagnani/status/1407879232311619587
  - Closing iterators seems to be a concept that's just not part of the iteration protocol?
- A generator is like an array of functions, how does a function know if it's never called? But I'd be curious if you do a try/finally, is the finally called when the .return() is called?
  - Yes, if you call `return()` on a generator, the `finally` block will be called. 
  - If you iterate a generator with `for-of` , it will also be called. 
  - If you call `throw()` on a generator, the `catch` block will be called, then the `finally` . 
  - Also works with async generators. 
  - RxJS leverages this.

```JS
let canceled = true;
try {
  yield 'foo';
  canceled = false;
} finally {
  if (canceled) // ...
}
```

- I think since V8 fixed how try/catch is optimized, I like wrapping the whole function in try/finally so that any reason that the generator exits will run the cleanup code.
  - Sure, depends on the cleanup code you're running. I really hate the whole pattern. It's super unintuitive, only works with for-of I think, and causes certain edge cases which no programmer would reasonably expect without being told of this behavior.
- `done` property is only for the consumer of the generator, and if the producer has returned. The generator function itself can't see that the iterator was closed by the VM when breaking from a loop.

- ## we can use Opaque or Branded types in our advantage to detect if user passed a value or the value has been initialized to default set value. 
- https://twitter.com/anuraghazru/status/1405925522102657029
  - Use branded types or opaque types to make them act as nominal types.
  - 处理多级很深的路径属性及默认值的一种方法

- ## Problem with `Promise.all()` : Once it encounters a rejection, it doesn’t wait until all Promises are settled (short-circuiting (*)). Consequence: Unexpected things can happen after error handling.
- https://twitter.com/rauschma/status/1405568325724291080
- Tentative idea: Promise.forkJoin(objOrArr). Once all Promises are settled:
  - All fulfilled: fulfill result with obj/arr of values
  - 1+ rejected: reject with AggregateError
  - This is what an implementation of forkJoin() could look like:
  - https://gist.github.com/rauschma/bdc56a046b18528959ad1db3eed05386
- What about `Promise.allSettled` ? I’ve taken to chaining the outcome to array filter and map (depending on intent, of course).
- There’s `Promise.allSettled` , combine it with `Promise.all`

- ## You can substitute an if-statement checking for a truthy value with an expression using short-circuit evaluation and the logical && and
- https://twitter.com/ThaddeusJiang/status/1403848377943543809
- 说实话，我现在负责的项目中已经存在了大量这样的代码，我非常不喜欢。已经和同事解释过了，今后不允许这样的代码，已经存在的也在慢慢改回 if
  - 从可读性考量，减少不必要的脑力负担。
- React 中用来判断一个 Component 是否该出现，我感觉挺有用的哈哈。
  - 不一样。Component 的 return 一定是 jsx，但是普通函数返回值可以是任意，甚至可以不返回。
- 比较赞同，代码的可读性更重要
  - 代码逻辑直观比较好，
  - 利用语言特性去体现逻辑太隐晦了

- ## sometimes I don't have the mental capacity to figure out what some type should be. So use the IntelliSense quick info feature to hover around, figure it out, and copy/paste the type!
- https://twitter.com/DavidKPiano/status/1403500184290664461
- I usually only do it if they're unclear from the implementation.
- You can also combine this with automatic imports, so that you can copy-paste a return type from an external function and then import the missing types automatically.
- the big downside to inferred return types is that they're not explicit. It can accidentally be the wrong return type, and you wouldn't know until further downstream.

- ## Most (all?) non-collection iterables created by JS are iterators
- https://twitter.com/rauschma/status/1402202573646540802

```JS
const IterProto = Object.getPrototypeOf(Object.getPrototypeOf([][Symbol.iterator]()));
IterProto.isPrototypeOf([].keys()) // true
IterProto.isPrototypeOf(new Map().keys()) // true

Uint8Array.prototype[Symbol.iterator] === Float64Array.prototype[Symbol.iterator] // true
```

- ## In TypeScript, classes that extend other classes still need to provide parameter types for methods. 
- https://twitter.com/steveruizok/status/1397122781054181377
  - TS knows what these types need to be and will error if the wrong type is provided... so why aren't these types just inferred?
  - Here's the pattern that I've been using instead: a function that enforces the base types on its parameter while still allowing it to be extended. This loses a bunch of good features from classes tho
- I guess it doesn't make sense that it's required, but it makes sense that some types are disallowed due to co- and contravariance

- ## here are my thoughts on reduce vs chaining array methods vs for loop
- https://twitter.com/kentcdodds/status/1396820360792731648
  - [Array reduce vs chaining vs for loop](https://kentcdodds.com/blog/array-reduce-vs-chaining-vs-for-loop)
  - Actually, I wrote this over a year ago and now I use for loops a lot more. 
  - I think I should probably update the post to give the loop a more positive light. 
  - I think for of **loops are definitely easier to understand** than reduce.
- Ya, it’s obviously all subjective. but the for-loop (to me) is far more explicit and easy to parse
- Finally someone with a sensible and pragmatic take on this issue. I too just map and filter specially cause most UI is short lists (short for processing by even slow phones). I only use reduce for transformation between data types (array to object).

- ## reduce() is a very helpful function because it accomplishes two important tasks at once: writing unreadable code and showing off how smart you are
- https://twitter.com/eevee/status/1396445889883906053
- 2 years ago me was totally with you, but now i use it frequently. just give it a go
- “our core user metrics improved after replacing reduce with map and filter in our JavaScript code base” said no one ever

- ## When should you consolidate generic type params: what's better?
- https://twitter.com/DavidKPiano/status/1396161493075431426

```typescript
function somethingA<T, U>(
  thing: Thing<T, U>,
  other: U
) { 
  // ... 
  }

// Or this?

type GetUFromThing<T extends Thing<any,any>> =
  T extends Thing<any, infer U> ? U : never;

function somethingB<T extends Thing<any, any>>(
  thing: T,
  other: GetUFromThing<T>
) { 
  // ... 
  }
```

- Notice they mean different things. So, it depends.
- I've found the second one gets tricky in public APIs because you have to make Thing public too 
- To me it would depend on if it’s public API or internals? 
  - If it’s public, do the magic to keep the API simple. 
  - If it’s internal, write the easiest code.

- ## It looks like @typescript 's declaration merging is "addivitve", 
- https://twitter.com/tannerlinsley/status/1395379651346767877
  - meaning that clashing members become a union (as long as they are compatible) or just another overload. 
  - Is there no way to actually "overwrite" types across modules?
- I use a pattern of extending a type using omit on another type but I may not fully understand your question
  - The built in utilities like ` Omit<>` can get you pretty far if you want to modify types (eg. completely replacing a prop)
  - I don't think that would work with declaration merging. You're not creating a new type with declaration merging, you're merging additional types to an existing one. 
  - to be clear, I'm suggesting an alternative to using declaration merging
- Declaration merging is nice, but it doesn't work for this specific use case of completely overriding the type
  - If the types are actually wrong, then overriding is also possible using something like patch-package
  - But long term harder to maintain
- No - i dont believe you can override stuff, which makes sense: some module could depend on what u’d like to rewrite

- ## Why does @typescript not have some native operator to *merge* types? 
- https://twitter.com/tannerlinsley/status/1393704549240606720
  - I don't want an intersection or union, 
  - I want the equiv. of TS-Toolbelt's Union/Object. Merge<> but with support for recursive types
- [Add a Merge utility type](https://github.com/microsoft/TypeScript/issues/35627)
  - Why not use `Omit` ?

- ## PSA: Using Node.js 16+ and want to compare the runtime performance of two functions ... Use `timerify` and `createHistogram` !
- https://twitter.com/jasnell/status/1392589770140774402

- ## I've figured out my primary reason for choosing types before interfaces with TypeScript. 
- https://twitter.com/kentcdodds/status/1392678508954980353
  - It's because interface augmentation feels like mutability whereas you can't do that with types and must do unions instead which feels like immutability.
  - Type unions are sorta like: NewType = {...a, ...b}
  - Interface augmentation is sorta like: Object.assign(a, b)
  - They both have their use cases, but I prefer the union over augmentation, so I start with types and only use interfaces when I need them.

- ## I wanted a way to extend/override an object's properties and type without changing its referential identity
- https://twitter.com/tannerlinsley/status/1391786858619699203
  - I want to be able to enforce identity consistency, but allow for type changes
- That pattern works very well with `Object.assign` .
  - Or you go for the "internal signature, external signature" shizophrenia by using an overload signature.
- If that's really all you want, might as well just use `Object.assign` directly.
- Maybe just adding a dynamic key to the thing object which can then be assigned any value you want? 
  - `[key]: [value]` .
- use `as` to force conversion

- ## I can't say this for *every* situation, but I get this feeling that setting default generics in @typescript has bitten me in behind more often than it has helped. 
- https://twitter.com/tannerlinsley/status/1390780257897115649
  - It might have *felt* good at first, but I swear it causes so many issues later on.
- I’m so many cases generics can be precisely inferred, default only when you start to get these non inferred cases... sometimes you can tell ahead of time by the nature of the signature
- Because you do not span your focus where you consume the data but where it is produced. Which makes it much harder trucking the type of that data. Imho

- ## Repeat after me: Adding enforced type checks to JS slows down JS performance at runtime.
- https://twitter.com/bradleymeck/status/1390373380319219719
- for runtime checks, no? you should be able to statically check the types and erase them a la typescript and dump it all into the load step right?
  - for runtime checks, no? you should be able to statically check the types and erase them a la typescript and dump it all into the load step right?
- I think what Bradley is suggesting is compiling so the runtime knows the types ahead of time. But you can't be sure that `"foo" + object.toString()` is concatenating strings since toString could be patched.

- ## When you get deep enough into @typescript generics, they basically become functions that you invoke with `<>` instead of `()` ... 
- https://twitter.com/tannerlinsley/status/1387806690364465152
  - but without optional *named* param support... and a lot of other things that I would expect from a "function"
- And when you come to this realization it's even more bizarre that people use single-letter "parameter names"
  - Agreed. I very rarely have a single "T", unless it's something obvious like: `type Identity<T> => T` ; 
  - The rules say that generics are single letter always. Look at any programming language in history that supports them. Always 1 letter
- Great point. At some point we started expecting Typescript to behave more like an expressive language in itself, instead of just a typed superset. It feels like we're a couple of major versions away.
- This is exactly how I've been thinking about them. And using a generic to create a new type is like "currying" or "function parameter binding" to create a new function.
  - I wonder if they could do something like how zig does generics.  There is no special syntax at all, only that comptime functions treat types as first-class values.
- I've started naming my aliases with camelCase for this exact reason. I import and use them like functions and it feels weird to use CapitalCamelCase for them
- I don't really know your usecase but have you seen Module Augmentation?
  - When you reference the same interfaces, it will even work across multiple modules.
- They should add meta programming to generate genetics

- ## New JavaScript features in Node.js v16 (compared to the latest v14)
- https://twitter.com/mathias/status/1387023971741315075

➡️ String.prototype.replaceAll
➡️ Promise.any + AggregateError
➡️ logical assignment
➡️ RegExp match indices
➡️ Atomics.waitAsync

- If we compare against Node.js v14.0.0, then these features are new, too!
  - top-level await
  - private methods and accessors
  - WeakRefs

- ## Is there a serialisation library with strong TS support? 
- https://twitter.com/glenmaddern/status/1379408751564894208
  - As in, I can share a type def between two projects 
  - but I want to serialize/deserialize with runtime type checking driven from the same type def?
- have you seen https://github.com/gcanti/io-ts ?
- The closest I've come is JSON schema auto-generation from TS types (ts-json-schema-generator) and validation of same (ajv)

- ## Did you know that in Node.js 16 you can use emojis as imports and exports names?
- https://twitter.com/NicoloRibaudo/status/1385346663842127873
- And is this useful?
  - Yes! When importing from other languages (e.g. wasm) you might have to import something that is not a valid JS identifier. 
  - My tweet was about emojis, but the actual feature is that you can use arbitrary strings in imports. 
  - I think exports support it just for symmetry.
- when did strings become identifiers?!
  - It's not part of the spec yet, but in practice it's a stage 4 feature (it has consensus from the committee, tests, and it's implemented in 3 major engines)
  - Is it just for WebAssembly?
  - Yeah the main motivation is integrating with other languages.

- ## is it fairly common to have a types.ts file in your projects where you keep all of your interfaces?
- https://twitter.com/mjackson/status/1385414736511070211
  - I've seen it done this way in a few projects, 
  - but I've also seen the types defined alongside the implementations as well.
- I keep in types.ts all the shared types, which are typically the interesting ones exported by the library. 
  - I keep a type in the file that uses it if it is used just there. 
  - So a type may be in the file using it and then moved to types.ts when it is shared by other modules.
- I prefer to collocate types with the code that needs them
- I personally prefer alongside the methods or the functions.  it's creating that type.
  - I also have a types folder for like files where all my autogenerated types.
- why do you not import FC explicitly instead of typing React. FC? While also importing useState and not using React.useState
  - I personally really like the concept of Namespaces where you can have short method names for specific functions while keeping the logic encapsulated. 
  - explicitly importing means you can not fave the same method name for another thing unless use import as
- For public interfaces it’s most ideal, and then private interfaces you can just declare locally to the file
- I do it both ways. Types.ts for regularly used types, but mostly they start inline with other code.
- Even if it is common, don’t do it. What changes together should stay together. Co-locate types and the operations on them within the same module.
- I've seen a API.ts more often, a codegen file that has all your graphql queries and mutations from a schema

- ## in Node.js 16 you can prefix CJS require() and ESM import() specifiers for Node.js core modules with `node:` .
- https://twitter.com/jasnell/status/1385238402149150721
  - for instance `require('node:fs')` instead of `require('fs')` . 
  - This makes it clearer that it's a core module.
- Yeah I like this pattern, it’s worth using for weird cases when you want to ignore any mocking

- ## TypeScript Pro Tip: When creating large conditional types, ensure your conditionals are working as expected by returning string literals mapping to your intent.
- https://twitter.com/mattcompiles/status/1385047092003962880

- ## you find this when reviewing a PR: `type CategoriesByName = Record<string, Category>;` . Too explicit? Just right? The Best Way™?
- https://twitter.com/erikras/status/1384891209219518466
- I usually prefer doing: `Record<Category['name'], Category>` , just because it's easier to understand what is the key of that map
- If used only once: inline
  - If used in multiple places: yes
- `const nameToCategory = new Map<string, Category>(); `

- ## The point of Symbols is that they are unique and primitive at the same time. 
- https://twitter.com/asleMammadam/status/1382641865883852802
  - We can use them as a sign of our values. 
  - As we may know, objects are unique too, but not primitives, which means they're not something like numbers or strings, but Symbols are.
  - You can also use Symbols for object's keys, so no one can access them unless they have that symbol.

- ## I'm starting to avoid putting any data in an object keys.seems easier to iterate, filter, expand, 
- https://twitter.com/daKmoR/status/1382313714276270090
  - from `{k: 'v'}` to `{name: ` k `, value: 'v'}` .
  - Filtering and iterating especially seems nicer with an array of objects.
  - But by FAR the biggest benefit is extendability without a "breaking" change.
- `Object.keys, Object.values, Object.entries` are very helpful for structure #1. 
  - I tend to prefer the readability of #1 personally.
- I'm curious: in which cases? What are the pros/cons? The second object structure reminds me of XML.
- I tend to prefer Map. Best of both worlds imo. 
  - You can initialize it using an array, it's easy lookup (no need for find + predicate), easy filtering and iterating because it is Iterable by default.

- ## Having been neck-deep in advanced TypeScript typings for more than a year now (and generally disliking most of that time), I'm in total agreement with: Prefer interfaces over types.
- https://twitter.com/BenLesh/status/1382076661575905283
- Do you think this applies more to widely used libraries vs most apps?
- Only using types for Unions i can agree with all above.
- [TypeScript: Prefer Interfaces_202010](https://ncjamieson.com/prefer-interfaces/)
  - Some time after this blog post was written, Anders Hejlsberg opened a PR that preserves type aliases for union and intersection types. 
  - That PR’s changes should included in TypeScript 4.2, 
  - so when that version is released, the reasons for preferring interfaces might be less compelling.

- ## @nodejs is fast and easy to use. 
- https://twitter.com/matteocollina/status/1381639256842584069
  - The fact that your JavaScript libraries are either (1) buggy (2) slow is not a problem of JavaScript. 
  - Simply put, those libraries are not well written. 
  - Rewriting everything in another language is unlikely to solve either problems.
- Node is also SOOO easy to use in ways that seem fine at first but break in a myriad of strange and surprising ways at scale.
  - Yes, I'm looking at you Streams and your hostile frenemy EventEmitter.
- I'm not sure how fast it actually is, I recently made a couple of libraries for reading files and fetching their stats objects about ~2x faster than what Node itself can do, and those libraries are build on top of Node itself too, this kind of stuff shouldn't really be possible.

- ## TypeScript question: When have you used "never" in a production codebase?
- https://twitter.com/kentcdodds/status/1381453907730128900
- `never` and `unknown` are good replacements for `any` . 
  - A generic function for example can look something like this:
  - type GenericFunction = (...arg: readonly never[]) => unknown; 
  - An empty array type can look like this:
  - type EmptyArray = readonly never[]; 
- Restricting prop combinations, e.g. `<List type="icon" icon={<IconPositive />}>` — the type of the `icon` prop is `never` when the `type` prop isn't icon
  - icon?: undefined would work too, right?
  - That’s not the same, though. `("icon" in { icon: undefined }) === true` .
  - never entirely disallows the property
  - But who relies on that in React components to check if a prop was passed? 
  - Imo it's better to assume undefined to be not passing a prop, behavior like default props rely on that. I have also passed undefined to signal no prop many times, not reason to prevent that.
- We almost never use never directly, but it's a useful concept for type narrowing. Specifically, the case of 'switch'ing over a union type.

- ## No, js classes have never been just sugar, various things are better/different.
- https://twitter.com/WebReflection/status/1380809258095247360
- [JS classes are not “just syntactic sugar”](https://webreflection.medium.com/js-classes-are-not-just-syntactic-sugar-28690fedf078)
  - Strictly guarded by default
  - Builtin Extends
  - Species
  - The super
  - Methods
  - Enumerability
  - Arrows
  - Privates
- Summary
  - there are many things that could be simulated via ES5 and old prototypal inheritance, but none of these come out of the box, are as fast, or as safe, as using appropriate syntax for classes and, 
  - on top of that, there are things that are just not possible with prototypal inheritance.
- Do you have resources explaining how JS classes are not syntactic sugar?
  - The spec has some differences:
  1. A class constructor can't be called without new.
  2. Class methods are have their enumerable flag set to false.
  3. The internal flag [[FunctionKind]] has the value "classConstructor".
  4. "use strict" by default.

- ## You'll never convince me that: `fn({ // One thousand random things here })` Is better than a class.
- https://twitter.com/matthewcp/status/1380610388467793920
- This is so prevalence with web component libraries, and I just don't get it.
  - How is writing special object properties named "props" and "methods" any better than using plain class fields and methods? Just to avoid the class keyword? It's so weird.
- There’s no problem with classes per se, the problem is subclassing. 
  - A struct with a million random things is fine compared to a function with a million random things. 
  - The issue is wrangling covariance/contravariance, jumping between definitions of overridden methods, etc.
- You'll never convince me that 1, 000 random things in a class is better than 1, 000 random things in a function.
  - 1, 000 random things anywhere is bad.
- I like classes, as long as I don't do any inheritance with them.
  - What I don't like is the sea of `.this` that easily ends up being almost 50% of the code. I'd rather take a `<div>` soup or a HOC hell anytime.

- ## Node.js is terrible at two things:
- https://twitter.com/jevakallio/status/1380073988802670595
  - Traversing big trees
  - De/serializing large strings
  - Also known as: - GraphQL Servers; - React SSR; 
- Serialization in all languages is costly and CPU intensive tasks the same, 
  - but this is a very good opportunity to write some native code in rust to cover those requirements.
- the purpose of event loop do not regards to it's limitation in certain kind of algorithms solving, 
  - because we pretty know that we have C to do this, the nodejs is a multipurpose tool that we use to do abstract things.

- ## I don't like much Promise.all
- https://twitter.com/sebastienlorber/status/1379731789707632640
  - Too sensitive to array destructuring typo
  - Code becomes verbose when input to transform is an object
  - Finally published this little utility: combine-promises
- Reminds me of `Promise.props` in Bluebird. 
  - I wonder why something like this wasn’t part of the Promise spec.
- Another big pain point with Promise.all and variations, is error handling IMO (ex: calling 3 APIs from diff providers). It would be awesome if you could solve this in the lib too. I'd love to help, got some ideas on how to go about doing it.

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

- ## For those of you looking to write cross-environment, isomorphic javascript that works in browsers and Node.js --- other than fetch and WHAT-WG streams, what globals from the browser are missing in Node.js that you want to have?
- https://twitter.com/jasnell/status/1376618110099226626
- It would be neat if there were an official require(”vm”) factory to produce a browser-compatible context. Something along those lines might be a nice way to sandbox the sometimes incompatible underpinnings.
- Important: WebSocket + SSE, IndexedDB, FormData, FileSystem, Text{Encoder/Decoder}Stream, Sanitizer
  - Important-ish: WebRTC/Media*/Video*
  - Fun, but not important: Bluetooth, USB, Audio

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

- ## Use TypeScript template literal types to quickly generate a type with all permutations / options based on other types
- https://twitter.com/wesbos/status/1375145379197509634
- This can also be handy when using a Record to define an objects possible properties. 
  - You can even pipe them through string manipulation types like Lowercase<> and Capitalize<>
- [Creating a Scientific Pitch Notation Type using template literal types](https://madewithlove.com/blog/software-engineering/creating-a-scientific-pitch-notation-type-using-template-literal-types/)

- ##  what do you mean when you say:"objects naturally represent orthogonality"?
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

- ## Are you using async/await safely in Node.js? @simonplend explains why Express is not a safe choice and why you should consider an alternative like Fastify instead.
- https://twitter.com/sebastienlorber/status/1374029709210701831
- [Are you using promises and async/await safely in Node.js?](https://simonplend.com/are-you-using-promises-and-async-await-safely-in-node-js/)

- ## I was chasing the race conditions today in the code that is using observers and async/await syntax. Oh, boy, a day full of fun.
- https://twitter.com/maciejadamczak/status/1374286061543718916
- I still need to fix the root problem

- ## Deleted a thread about async/await flows since I hadn’t realized that it made error-handling more complicated.
- https://twitter.com/JoshWComeau/status/1374056481524482054
- I still think it's a valuable tip. I use it all the time - it really helps to speed things up when you've got independent parallel requests.
- You can use try catch.
  - I think it doesn't work when you don't `await` the async function! And that's what Josh means.
- Now I'm interested in a thread about proper error-handling when working with async functions
  - imo async makes it _easier_ (you just use try/catch). I think the difficulty is when you're mixing async/await with raw promises.

- ## When you have a complex series of async functions to call, how do you manage them? 
- https://twitter.com/JoshWComeau/status/1374027384119263233
  - we'll look at 3 different ways, including an *awesome* way that isn't super well-known.
- First, though, let's look at the most straightforward way: serially, one at a time.
  - The beauty of `async/await` is that it lets us read the code in the order it executes. I love how easy it is to understand.
  - The trouble is that it can be quite slow, since none of these tasks can start until the previous one finishes.
- What about `Promise.all` ? Well, we can't dump all 5 into a single call, since there are dependencies.
- From a performance standpoint, this is quite a lot better, since we can let 3 operations run in parallel.
  - But we can make this even faster 
- This final way makes selective use of the `await` keyword. 
  - We can weave the promises together to create a tapestry without gaps. 
  - Each function starts as soon as possible! 
  - The key insight is that promises can be await-ed at any time, not just on creation!
- Which way is best? Well, it depends on the circumstances.
  - The third way is the fastest, but it's also (IMO) the hardest to follow. 
  - We're trading away some simplicity in order to gain some performance.

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

- ## Generators are _so_ handy for stuff like AST walkers or similar traversing algorithms.
- https://twitter.com/DasSurma/status/1373226617938571264
- generators are everywhere in Python. I’m surprised they don’t get more attention in JS. I love them for tree traversal.
- Wow, this is so cool. Not only for AST, but for any type of nested datastructure

- ## Has anyone ever use a pattern of hybrid sync/async iterables in JS?
- https://twitter.com/justinfagnani/status/1372579326953103364
  - I have a case where I want the highest throughput and all-async is just slower than sync. But a couple of features require async. 
  - I'm thinking about a sync iterable that can emit Promises as a middle ground.
- It’d be great if JavaScript supported code that can be run either synchronously or asynchronously. I did some experiments a while ago, but was never happy with the results

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

- ## In Node.js, we have awaitable timers built in, with cancellation support.
- https://twitter.com/jasnell/status/1371955481342742529

```JS
import { setTimeout } from 'timers/promises'
const ac = new AbortController()
await setTimeout(1000, undefined, { signal: ac.signal })
```

- ## Converting an array of objects into an object lookup is something I've always needed in my data utility functions
- https://twitter.com/benmvp/status/1371966367100891140
  - I think I've gotten it down to its minimalist version! 🤓
  - all the way from creating an empty object and assigning to it within a for-loop
- I would really like to use Map (and Set) more but I find that using regular objects ends up being easiest

- ## We really need an API for inspecting the ES module graph. Wasn't someone working on this?
- https://twitter.com/_developit/status/1371528639926403079
- It's sort of possible in Node by hooking into the module loader, with a small amount of guesswork but no reparsing. But it's straight up not a thing in-browser. This would make HMR so, so much more effective.

- ## TypeScript experts: is there a way to find out which tsconfig files are being used in a given compilation? I'm getting `lib.dom.d.ts` in one of my compilations, but I don't know who is including it. { lib: [] } in my tsconfig isn't helping.
- https://twitter.com/mjackson/status/1370525900819689476
- --explainFiles in 4.2

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

- ## How to write a Constrained Identity Function (CIF) in TypeScript
- https://twitter.com/kentcdodds/status/1370380876568170499
  - A handy advanced TypeScript pattern to increase your productivity.
- we have 2 goals:
  - Enforce that the type of each property is the same
  - Ensure that `keyof typeof` for our object results in a finite union of the keys
- With TypeScript, it's a challenge to have both of these. 
  - By default, we get the second goal. The problem is that when you try to accomplish the first goal with a type annotation like const operations: Record `<string, OperationFn> = ...` , you end up widening the key so keyof typeof results in string. Ugh, how annoying.
  - So here's where the constrained identity function comes in. By the way, "constrained" describes a situation where you have a function that accepts a narrower version of an input than it's passed

```typescript

type OperationFn = (left: number, right: number) => number
const createOperations = <OperationsType extends Record<string, OperationFn>>(
  opts: OperationsType,
) => opts
const operations = createOperations({
  '+': (left, right) => left + right,
  '-': (left, right) => left - right,
  '*': (left, right) => left * right,
  '/': (left, right) => left / right,
})
type CalculatorProps = {
  left: number
  operator: keyof typeof operations
  right: number
}
```

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

- ## Totally shocked that there's no refactoring to reorder arguments in VS Code for TypeScript.
- https://twitter.com/BenLesh/status/1366543595172470786
  - I get that with type overloads and rest args it's tricky
- Not a problem if you avoid positional arguments altogether and use a single object instead.
  - That's fine for apps, but unfortunately if you're developing a library that needs to be memory sensitive and lower level, you probably don't want to do that.
  - I agree that for hot code GC pressure can be a consideration to opt for positional arguments over POJOs at each call site.
- I would love so much that TypeScript have a transpiled named parameters feature

- ## Performance tip: if you're working with *large* objects (10KB and larger), it'll be way faster to parse them as JSON strings rather than consuming them directly in your JavaScript as objects
- https://twitter.com/mgechev/status/1366259446154989569
  - because json grammar is uch simpler than js grammar
  - json can be parsed more efficiently than js.
- not for GTA apparently

- ## is there a way to wait for N promises on tests?
- https://twitter.com/sseraphini/status/1365297469911937025
  - I have a test that will receive N messages and process each of them using an async code
  - so I need to wait N process to be processed to do some assertion
- Promise.all() or Promise.allSettled() might be work.
- `await new Promise(setImmediate)` .
  - will this awaits a single promise or all the pending promises?
  - This awaits all promises that are to be resolved in the same event loop

- ## I just realized ternary operator is called that way because it handles THREE things at once
- https://twitter.com/vishwajeetv/status/1365121673922543622
- Personally I am not fan of the reduced readability introduced by ternary operator. I avoided them for years, and even today I use it sparingly. 
  - If else is much more readable and maintainable.
  - Short expressions *should* use the ternary operator.
  - The problem is that if/else is not an expression, but a statement

- ## I think most JS libraries that vend some kind of observable value could just use async iterables instead of an actual observable library.
- https://twitter.com/justinfagnani/status/1360793286781247491
  - Clients mostly need to be able to subscribe and unsubscribe to new values. 
  - The rest isn't strictly needed and a client can pipe the async iterable into their library of choice if they really want.
  - No need for clients to read about rxjs/wonka/zen-observable or whatever is used.
- I think the platform should have added a simple type like observables, instead of a heavy complicated type like AsyncIterables.
  - A promise allocation for each event?
  - No cancellation other than not iterating, ignoring the next event, or rejecting the next event and handling it?
- It always surprised that Angular 2+ went all in on RxJS, while other frameworks could perfectly live with only promises.
  - IMO the choice for RXJS causes a way too high learning curve. 
  - And also are error prone because unsubscribe is sometimes automatically but not always.
- I disagree with things like react being able to live with only promises. 
  - You end up building your own ad-hoc chains in likely buggy async/await code and probably doing it in some complex hook with race conditions or difficult to debug code. 
  - I don't use rxjs but I see the appeal.

- ## Babel gave us an incredibly flexible ecosystem of plugins and presets. TypeScript (as a language) limits you to using whatever language features they choose to implement.
- https://twitter.com/mjackson/status/1361525113175171072
  - It’s always trade-offs when it comes to engineering, but what a price for type safety!
- TS is usually pretty good about implementing features at Stage 3

- ## Writing app TypeScript is *way* easier than writing library TypeScript
- https://twitter.com/tannerlinsley/status/1361159377051262977
- I have written a couple bits of app-level TS that were fairly complex and resembled "lib"-style TS, but it was an internal abstraction that bordered on lib-like.
  - [Thoughts as a Library Maintainer](https://blog.isquaredsoftware.com/2019/11/blogged-answers-learning-and-using-typescript/)
- TS keeps your app consistent. Found a better way to structure some object? Change it and TS tells you all the places you need to fix its usage.
- Generics come in handy quite a lot, but I never reach for them right away. 
  - I just write the code I need and always try to think about how to avoid `any` , and if I end up factoring out reusable stuff at all, generics tend to emerge as the right solution.
- Needing generics in app code tends to be rare. 
  - Typescript is fantastic for defining API boundaries such as component props.
- In our team, we start types without genetics, but add them if we need more reusable parts, and more type safety around those parts. 
  - We try to communicate intent rather than expectation.

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

- ## Trick—JavaScript superclass that can’t be instantiated 
- https://twitter.com/rauschma/status/1356134928707153920
- why is this pattern useful, when we have structural typing and interfaces? 
  - This is when you do OOP-style abstract superclasses: You want the subclasses to be instantiated, but not the superclass.

- ## Yet again I'm reminded that JavaScript class fields are a bad design
- https://twitter.com/justinfagnani/status/1355665301979897860
  - Define semantics means you can't meta-program over them like other class members, and you can't override them with accessors.
  - Class fields should have been sugar for accessors.
  - ES Classes in general feel like an opportunity to carve out some static niche and forgo metaprogramming altogether.
  - Which really limits them. The list opportunity here is that they don't need to have false equivalences to object literals because they aren't.
- A similar issue is happening for decorators as a decorator won’t be able to convert a field to an accessor unless you prefix with prop, as in: `@example prop field` . 
  - I wonder if this could lead to some `prop field` as sugar to set accessors without the decorator.
  - It’s a workaround and honest I’d just prefer the decorator without prop but that’s the much we can do in the consensus model.

- ## In JavaScript, there are no classes.
- https://twitter.com/SimonHoiberg/status/1355453046617108484
  - t’s syntactical sugar added to please developers from other languages such as Java or C#.
  - Most of the time, they don’t serve a good purpose, and are not really useful.
  - Instead, use modules.
- don’t you think classes help maintain order and principles of programming that have been established over a longer period of time?
- The singleton pattern would like to have a word with you.

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

- ## Using TypeScript without classes feels suboptimal, like I'm using it for something it wasn't designed for. TypeScript really shines with classes and static methods.
- https://twitter.com/BenLesh/status/1354541556234137600
- [To clarify: I'm not advocating programming with classes. ](https://twitter.com/mjackson/status/1354524449706414080)
  - I typically avoid them. There is 1 class in the codebase I'm currently working on, and it's a React class because there is no hook for React error boundaries 
  - I'm just saying, TypeScript seems designed for them.
- That's interesting.
  - I view TS as just a type system on top of JavaScript
  - Classes in TS are just interfaces.
  - TS is all just interfaces, types, and function signatures. 
  - In my head, the actual "class" is a runtime thing.
  - So functions and classes feel pretty much the same to me.
  - Totally agree with everything you said here. I think about it the same way.
  - But there are a few spots where I wish TS had better support for working with functions, like typing a whole module of functions, for example. I could easily do it w/ a class, but not w/ a module.
  - What is a "module of functions"?
  - Just talking about JavaScript modules. There is no way to type all the exports of a module in TypeScript.
  - namespaces are nice for that but unfortunately discouraged because of tree shaking issues (i think...)
  - referring to ECMAScript Modules.
  - Modules =/= Classes.  You can have a javascript file that exports only functions.
- I find it exactly the opposite. 
  - I use plain functions and values 90% of the time with TS and classes only when I really need to (mostly for perf). 
  - Generics are easier to manage with functions too.
  - I do the same thing. There are 0 classes in the codebase I'm currently working on, but sometimes it feels like things would be easier if there were. For example, typing a whole module would be easier using static methods on a class.
  - I don't see how this is different than just plain typed functions?
  - You can't get a type for the whole module, just each individual function.
  - 但是可以通过单独的文件专门导出一个文件中所有的export，虽然可行，但增加了文件数量
  - Clever, but there’s no way to open up a new module and say “this module is one of these” (ie implements an interface)
