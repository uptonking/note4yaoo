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
- `const nameToCategory = new Map<string, Category>();`

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

``` JS
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

``` typescript

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

``` JS
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

``` JS
// A promise for the next frame:
const nextFrame = () => new Promise(requestAnimationFrame);

// this is equivalent to:
const nextFrame = () =>
  new Promise((resolve, reject) => requestAnimationFrame(resolve, reject));
```

- **Option objects can have the same gotcha**

``` JS
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
