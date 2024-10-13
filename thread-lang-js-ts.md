---
title: thread-lang-js-ts
tags: [js, lang, typescript]
created: 2021-01-28T14:33:59.037Z
modified: 2021-01-28T14:34:20.579Z
---

# thread-lang-js-ts

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚️ Trying to write an exhaustive pro's/cons list for three different approaches to TS monorepos.
- https://x.com/mattpocockuk/status/1799055070274986098
  - But slowly realising that they're all kind of bad in different ways.

- [Live types in a TypeScript monorepo](https://colinhacks.com/essays/live-types-typescript-monorepo)
  - wasn't satisfied by the 'paths' thing, it has its own downsides.
  - "Need to make sure that packages are correctly ordered inside references in the root tsconfig.json" 
    - Or, each project lists it's dependencies and then TSC automatically figures the order for you (we do this in the Babel monorepo)

- I tried #3 but migrated to #1 at Remotion. 
  - We have 40 packages in one repo and pretty happy with Project References! 
  - Listing all references is a confirmed drawback, but once that is done, it's much faster than invoking tsc many times.

- How common is it that people actually use tsc for building? I'd be very surprised if it was a majority of monorepos/packages. My guess is rollup and esbuild are much more popular

- Not to mention many of them break once you add Metro and React Native.

- I feel most people use monopod because they wanna share types between frontend and backend and in such a case not using a monorepo (having just one package.json) is the way.

- 
- 
- 
- 

# discuss-examples
- ## 

- ## 

- ## 

- ## 🌰 Here's how to get a fully type-safe fetch function in just a few lines
- https://twitter.com/mattpocockuk/status/1746857014255403499
- shouldn't you, like, pass in a zod schema instead, and get the output type from that? otherwise it's just kinda hopes & dreams bc there's no verification that the response actually matches what the type says
  - See my library `zod-fetch`

- Or you share these types in your backend and... oops we've invented `trpc`

- I use this typed API client (with zod validations) almost everywhere. 
  - [Fully typed API client with zod and fetch](https://gist.github.com/jordienr/3127f4186d520e57d3e77fa784058366)
# discuss-news
- ## 

- ## You'll never need to write a `.js` import again, thanks to this new flag in TS 5.7.
- https://x.com/mattpocockuk/status/1840747531740844509
  - If it's got an extension, it'll be transformed (YES). 
  - But if it targets a .d.ts file, or it's a non-relative import, it won't be transformed (NO).

- ## TypeScript 5.7 will load 2.5x faster than TypeScript 5.6 when run in Node 22+, _202409
- https://x.com/andhaveaniceday/status/1839423538203423156
  - thanks to @JoyeeCheung 's work to provide an offical API for V8 compile caching.
  - That's 60% less time waiting for tsc/tsserver to actually start doing work.

- Nice, do you use the concurrent API or the synchronous one?
  - Both CommonJS and ESM are compiled synchronously in Node.js - I think the streaming APIs can’t really be used because most of the source fetching is implemented in internal JS, or has to be customizable by user land loaders written in JS
- Ah got you, makes sense -- if the loaders are hookable then concurrency is tough. Maybe resolved imported module loads could still be concurrent, allowing each import to streaming compile or deserialise while the others are looked up?
  - For ESM that might be possible. Though there's the overhead coming from the C++ <-> JS boundary crossing + async/await/Promise used as a primitive to coordinate these from the JS loader, this is likely why async fs APIs in Node.js tends to be slower than their sync counterpart
  - so it's hard to say whether that would make module loading faster overall e.g. the loading of `import esm` in Node.js uses async fs APIs to fetch the source concurrently (on the libuv thread pool), yet it's still slower than `require(esm)` that just uses blocking & sync fs APIs
- True, without actually parallelising multiple compiles I can totally imagine that the overheads would be visible. The parallelism definitely helps us in the browser, but it's sufficiently different to not map directly.

- ## In TS 5.5, type predicates will be inferred automatically from functions that return a narrowing statement.
- https://twitter.com/mattpocockuk/status/1768809254733951424
  - No more 'val is string' to force TypeScript's hand.
- If you manually write the return type, will TS error if the inference doesn’t match what you wrote?
  - No, it won't - a possible addition for the future.

# discuss
- ## 

- ## 

- ## Sick of Node truncating your objects when you log them? Check out `console.dir(obj, { depth: Infinity })` .
- https://x.com/mattpocockuk/status/1843234819326484629
- inspect() is a more general purpose tool for these things 
  - I learned the hard way Node.js might truncate error chains too This happens when using Error Cause, AggregateError etc 
  - Solution: `console.error(inspect(err, {depth: Infinity}));`

- depth: null > depth: Infinity

- JSON.stringify will use obj.toString() or obj.toJSON() if found.
  - some objects just get skipped altogether by JSON.stringify

- ## The year is 2024 and TypeScript still doesn’t have a built-in JSON type
- https://twitter.com/EricVicenti/status/1778823633248702972
- Super easy to write though

- ## One really neat pattern is to 'brand' the data that can be fetched from a URL _directly_ onto the URL itself.
- https://twitter.com/mattpocockuk/status/1767849338305163333
  - This means you just to use the url directly, and get your data strongly typed.

- i'd rather make a function 'getUser' than doing this.

- ## It annoys me to no end that the return type of `Object.keys(T)` is `string[]` and not `(keyof T)[]` .
- https://twitter.com/rossipedia/status/1766699756745638318
- ts-reset library (which attempts to fix similar shortcomings of ts) comments on the reason why this might not be the ideal solution

- ## 🆚️ Type predicates (like 'pet is Fish' below) are no safer than 'as'.
- https://twitter.com/mattpocockuk/status/1758523382155415953
  - I've started using them less in my code.

- A properly implemented user-defined type provides more safety than `as` because it actually checks for the existence of the expected object shape. `as` can't be safe. Type predicates *can* be.

- ## a #zod schema definition becomes a "single source of truth" for BOTH compile-time (#typescript) and runtime (#javascript).
- https://twitter.com/tomasz_ducin/status/1752300627672416334
  - You can also generate API contracts (e.g. swagger)

- The typescript space evolved a lot since io-ts and then zod paved the way. All major validation libraries have catched on the typescript support (except joi, ajv and deepkit).

- ## TypeScript tip: use undefined explicitly instead of making a property optional
- https://twitter.com/DavidKPiano/status/1741829750333587629
  - Why? It's too easy to forget to specify a property, especially in large codebases or refactors. 
  - You can make it optional later.
- [optional vs. undefined | TkDodo's blog](https://tkdodo.eu/blog/optional-vs-undefined)
  - Required, but potentially undefined does not have the same intent as optional. 
  - Try to be explicit with your type declarations and get some help from TypeScript by opting into new features like exactOptionalPropertyTypes.

- I use a similar technique: Make it required first, then lean on the compiler to assure I’ve updated all the relevant call sites. Then I can make it optional.
- `string | null` might be a more explicit than `undefined` in that case.

- ## Here's a quick thread on a super useful type helper you've probably never heard of (nope, not even advanced folks).
- https://twitter.com/mattpocockuk/status/1622730173446557697

```typescript

type DisplayUnionnedProps<T> = {
  [K in keyof T]: T[K]
}&{};

```

- ## #TypeScript's `infer` keyword is just JavaScript's destructuring assignment
- https://twitter.com/GabrielVergnaud/status/1610637512870871040

```typescript
type GetName<User> = User extends {name:infer Name}? Name:never;

type T = GetName<{name:'Mike'}>; // Mike
```

- ## TypeScript: What’s the cleanest way to enable globalThis.someProperty? A type assertion ( `as` ) works but feels hacky.
- https://twitter.com/rauschma/status/1429887307998535681

```JS
export module globalThis {
  export const POOP = 'test';
}
const test = globalThis.POOP;

declare namespace globalThis {
  let someProperty: any;
}

declare global {
  var someProperty: string;
}
```

- ##  `type C = A | B;` TS won't let me access props that aren't on both.
- https://twitter.com/kentcdodds/status/1420125238436655104
  - You're supposed to use `in` to check structures (to make TS happy)

- ## A very common #typescript pattern with some kinda tricky types behind the scenes. 
- https://twitter.com/steveruizok/status/1415641397265379328
  - The second arg's type is based on the first arg
  - https://codesandbox.io/s/type-mapping-and-filtering-k6k2e

- ## In TypeScript, classes that extend other classes still need to provide parameter types for methods. 
- https://twitter.com/steveruizok/status/1397122781054181377
  - TS knows what these types need to be and will error if the wrong type is provided... so why aren't these types just inferred?
  - Here's the pattern that I've been using instead: a function that enforces the base types on its parameter while still allowing it to be extended. This loses a bunch of good features from classes tho
- I guess it doesn't make sense that it's required, but it makes sense that some types are disallowed due to co- and contravariance

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

- ## Is there a serialisation library with strong TS support? 
- https://twitter.com/glenmaddern/status/1379408751564894208
  - As in, I can share a type def between two projects 
  - but I want to serialize/deserialize with runtime type checking driven from the same type def?
- have you seen https://github.com/gcanti/io-ts ?
- The closest I've come is JSON schema auto-generation from TS types (ts-json-schema-generator) and validation of same (ajv)

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

- ## TypeScript Pro Tip: When creating large conditional types, ensure your conditionals are working as expected by returning string literals mapping to your intent.
- https://twitter.com/mattcompiles/status/1385047092003962880

- ## sometimes I don't have the mental capacity to figure out what some type should be. So use the IntelliSense quick info feature to hover around, figure it out, and copy/paste the type!
- https://twitter.com/DavidKPiano/status/1403500184290664461
- I usually only do it if they're unclear from the implementation.
- You can also combine this with automatic imports, so that you can copy-paste a return type from an external function and then import the missing types automatically.
- the big downside to inferred return types is that they're not explicit. It can accidentally be the wrong return type, and you wouldn't know until further downstream.

- ## you find this when reviewing a PR: `type CategoriesByName = Record<string, Category>;` . Too explicit? Just right? The Best Way™?
- https://twitter.com/erikras/status/1384891209219518466
- I usually prefer doing: `Record<Category['name'], Category>` , just because it's easier to understand what is the key of that map
- If used only once: inline
  - If used in multiple places: yes
- `const nameToCategory = new Map<string, Category>(); `

- ## Having been neck-deep in advanced TypeScript typings for more than a year now (and generally disliking most of that time), I'm in total agreement with: Prefer interfaces over types.
- https://twitter.com/BenLesh/status/1382076661575905283
- Do you think this applies more to widely used libraries vs most apps?
- Only using types for Unions i can agree with all above.
- [TypeScript: Prefer Interfaces_202010](https://ncjamieson.com/prefer-interfaces/)
  - Some time after this blog post was written, Anders Hejlsberg opened a PR that preserves type aliases for union and intersection types. 
  - That PR’s changes should included in TypeScript 4.2, 
  - so when that version is released, the reasons for preferring interfaces might be less compelling.

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

- ## Use TypeScript template literal types to quickly generate a type with all permutations / options based on other types
- https://twitter.com/wesbos/status/1375145379197509634
- This can also be handy when using a Record to define an objects possible properties. 
  - You can even pipe them through string manipulation types like Lowercase<> and Capitalize<>
- [Creating a Scientific Pitch Notation Type using template literal types](https://madewithlove.com/blog/software-engineering/creating-a-scientific-pitch-notation-type-using-template-literal-types/)

- ## TypeScript experts: is there a way to find out which tsconfig files are being used in a given compilation? I'm getting `lib.dom.d.ts` in one of my compilations, but I don't know who is including it. { lib: [] } in my tsconfig isn't helping.
- https://twitter.com/mjackson/status/1370525900819689476
- --explainFiles in 4.2

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

- ## Totally shocked that there's no refactoring to reorder arguments in VS Code for TypeScript.
- https://twitter.com/BenLesh/status/1366543595172470786
  - I get that with type overloads and rest args it's tricky
- Not a problem if you avoid positional arguments altogether and use a single object instead.
  - That's fine for apps, but unfortunately if you're developing a library that needs to be memory sensitive and lower level, you probably don't want to do that.
  - I agree that for hot code GC pressure can be a consideration to opt for positional arguments over POJOs at each call site.
- I would love so much that TypeScript have a transpiled named parameters feature

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

- ## when using TypeScript (or generally being halfway disciplined about your types), using '===' instead of '==' does not actually get you anything.
- https://twitter.com/MarijnJH/status/1442414215940034567
- Except a performance benefit would be a reasonable expectation?
  - Any performance benefit would have to come from a compiler optimization.
- When using input from external sources (API, json files, user input) using == might get you into trouble.  TS types are gone during execution in JS execution contexts so it's always best to use ===
- Unless you have a mixed types accuracy and you never know if something is checked

- ## If you want to learn advanced @typescript techniques quickly, try retro-typing a library written completely in JavaScript. 
- https://twitter.com/DavidKPiano/status/1413149144252702729
  - It's not just a skill, it's an art form and an arduous(艰难的) adventure.
- we have the existing DT types to work from.
