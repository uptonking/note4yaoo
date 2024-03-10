---
title: thread-lang-js-ts-types
tags: [lang, thread, typescript]
created: 2021-08-05T04:30:46.106Z
modified: 2021-08-05T04:31:02.298Z
---

# thread-lang-js-ts-types

# guide

- ts-perf
  - [Performance · microsoft/TypeScript Wiki](https://github.com/microsoft/TypeScript/wiki/Performance)
# discuss-stars
- ## 

- ## 

- ## 

- ## 🤼🏻 My biggest gripe(牢骚；怨言；不满) with @TypeScript is that while it should follow API design, it often drives it. 
- https://twitter.com/LeaVerou/status/1762884918281994281
  - The beauty of JS is that it enables highly dynamic, flexible APIs that can provide great ergonomics, but TS tends to do very poorly with them so they’re often ruled out.
  - The priority of constituencies¹ is end-users > authors² > implementors > theoretical purity.
  - API design decisions should be driven by user needs, not tooling limitations.

- A valid opinion, but I feel the opposite, strong typing drives  API design and that’s a Good Thing. JS is a necessary component to the web, but dynamic typing is not the best choice for everyone. And for library design TS is wildly flexible in comparison to most typed langs

- My biggest gripe with JS are the “clever” APIs that give you 10 different ways to do the same thing.

- https://twitter.com/mattpocockuk/status/1762962933972078594
  - I actually agree with Lea here. When you're designing an API, TypeScript narrows your choices in unexpected ways. It can't describe all of the strange, dynamic, or bizarre things you can do in JavaScript.
  - It leaves you with a relatively narrow subset of tools to power smart inference in your API designs.

- ## 🆚️💡 two choices for how you write the type.
- https://twitter.com/mattpocockuk/status/1759540590025351234
  - Either DECLARE the type, then use it to type the value.
  - Or DERIVE the type from the value.

- I talked about this with @colinhacks (Zod creator) a couple or so weeks ago
  - I build TypeScript code for teams that want to ship SDKs for their APIs but don't necessarily use TypeScript. 
  - For those two groups statically-defined types are gold. Being able to jump to definition in your editor and being able to see the types while browsing repos on GitHub goes a long way.

- Declare. Code is for humans. Deriving is not easier on humans when wanting/needing to track down specific types. I want easily walkable types.

- I prefer declaring in most cases, except those when it is better to define something ‘as const’, in which case it isn’t deriving too. 
  - Deriving is definitely more compute heavy than declaring, which on huge codebases shows up.
- In a larger codebase, or when working with a larger team, I would declare rather than derive. A declared type gives the next person coming in to make a change a better understanding of the original intentions.

- Definitely define the type first. It allows me to define the business rules or domain model before starting any implementation and decoupled from anything. Which Imho should be how ppl code.

- Prefer the first, as I find they easier to read and also prevents me from accidentally changing the type. The secret and best third option is naturally to declare it using Zod

- I prefer the DECLARE approach but I would use `satisfies` when creating the record, has better DX in IDEs that I've used

- Declare. Let your types enforce the shape of data. 
  - Otherwise too easy to change data in a way you didn't intend and now you've also erroneously affected the type which may be used elsewhere.

- I think I prefer deriving the type. Something just feels better about the type coming from the underlying runtime code than the other way around

- Depends, but the second one feels more flexible. I’d rather write JavaScript first and use TS to enhance my coding experience, not the other way around.

- I prefer a single source of truth, so #2

- Library: declare; Application: infer

- ## Since working on Svelte, I always get asked if I really prefer jsdoc over TypeScript. No, I don’t.
- https://twitter.com/trueadm/status/1753562312651211207
  - Furthermore, if we had type definitions in the language (there’s a proposal for it) then Svelte could go back to using types instead of jsdoc. 
  - We just don’t want or need a build process for Svelte (the library). 
  - It does suck though and I’m often conflicted on the topic.

- You still need a build process to generate .d.ts files from jsdoc before publishing though don't you?
  - That’s a one time thing that’s fine via CI

- ## Library authors (and especially .d.ts authors), how do you mark a type as for internal use only? `@internal` via a JSDoc comment?
- https://twitter.com/mattpocockuk/status/1753328532413899231
- Yes, and you can set the `stripInternal` compiler option to strip them, but there be dragons.
- Yes, this practice maintains a clean and clear public API.
- internal + passing it through `api-extractor` to get rid of it in the published package
- My team uses `@private` , but internal may be more conventional.
- You can keep them in a separate .d.ts file and configure tsc to exclude them from the output
- And you can also try `@ignore`

- ## Avoid type and code duplication. Make types and code in sync without having to maintain both whenever you can.
- https://twitter.com/ecyrbedev/status/1723411440000799006
  - https://tsplay.dev/m0VjDw
  - 常用的从object中提取类型定义的技巧

- ## React TypeScript Cheatsheet
- https://github.com/typescript-cheatsheets/react
  - https://react-typescript-cheatsheet.netlify.app/docs/basic/setup

- ## Here's everything I've learned from leading TS dev teams and working on XState's core team.
- https://twitter.com/mpocock1/status/1509964736275927042
- more-cheatsheet
  - https://nerdcave.com/tailwind-cheat-sheet

- ## SvelteKit is written in JS and distributed as source code — no build step — and it's been miraculous for productivity. 
- https://twitter.com/sitnikcode/status/1639686112590323715
  - build steps make sense for apps, they make much less sense for libraries
- Agree. In open source build step (for TS or meaningless bundler) only reduces library maintainability.
  - All my open source ( @PostCSS , @logux_io ) is written in JS and have TS types in separated files (tests also is using TS to check that types and JS code are synced).

- ## If you're working in a TS codebase make sure you have these lint rules enabled, these just caught several serious bugs in a 5+ year old codebase
- https://twitter.com/tommoor/status/1675150188908822530

```JS
{
  '@typescript-eslint/no-floating-promises': 2,
  '@typescript-eslint/no-misused-promises': 2,
  '@typescript-eslint/await-thenable': 2,
}
```

- Pretty sure these are included if you just put these in your eslintrc ‘extends’ rule
  - plugin:@typescript-eslint/recommended
  - plugin:@typescript-eslint/recommended-requiring-type-checking', 
# discuss-ts-perf
- ## 

- ## 

- ## I've heard anecdotally that moving from intersections to 'interface extends' speeds up TypeScript performance significantly in big codebases.
- https://twitter.com/mattpocockuk/status/1764968902105137388
- This is documented in TypeScript wiki itself
- we experienced this with `@panda__css` style props, migrating to interface everywhere when possible solved it and now it's instant

# discuss
- ## 

- ## 

- ## For those of us who wish we had a Rust-like `Option<T>` type in TypeScript.
- https://twitter.com/GabrielVergnaud/status/1766554404650418187
  - I'm sure some of you are thinking "why the heck wouldn't we just do `T | null` " 
  - The reason is that `T` might contain `null` already
- To me `null` inside an `Option` is an oxymoron(自相矛盾的说法/概念). This now adds the unnecessary overhead with `null` having different meanings without an explicit reason. `Option` solves boolean blindness; this approach amplifies(使变得明显, 增强) it.
- JS/TS is just not a nice language to use this pattern. Now you have to unwrap value everywhere, and then you want a Result and have to deal with function colors...

- ## 🌰💡 Here's a quick guide on how to type your globals and env variables in Vite, Node and the DOM.
- https://twitter.com/mattpocockuk/status/1758454430666506589
  - `window.MY_ENV = 'whatever'; `

- `declare global` is not needed if you include file in `tsconfig.json#files`.
  - It's not needed if there are no import/exports in the file OR if you're using a `.d.ts` file.

- Is it a good practice to store these declarations in *.d.ts files?
  - Yes! Then you don't need the declare global.

- Our approach is to zod-parse the whole process.env (or import.meta.env) into a Config module, making them type-safe.

- ## Forcing users to always pass a type argument to your function isn't yet supported in TypeScript.
- https://twitter.com/mattpocockuk/status/1757733431981625565
  - But until it is, you set the default to be an error message

- ## Using a mapped type and key remapping, we can turn a discriminated union into an object 
- https://twitter.com/mattpocockuk/status/1755917714789466423
  - Sometimes you need to receive some data in one shape and return it in another. This gives you the ability to express that on the type level.

- ## If you want to declare a value as constant with type checking in editor but the code is not typescript yet. 
- https://twitter.com/huozhi/status/1754115622667960381
  - Using TSDoc constant type comment is such a relief

- ## TIL - I never knew you could make a method optional using the ?() syntax.
- https://twitter.com/mattpocockuk/status/1753672834688192989
- aMethod?: () => void, isn’t it the same thing for it being optional? I use it all the time this way.
- same energy as `?.()` for optional function invocations

- ## Four ways to define an object type in TypeScript
- https://twitter.com/wesbos/status/1524040757518258176

```typescript
// 1️⃣ 枚举key: 类型

type SizeList = 'small'|'medium'|'large';

// 2️⃣ type Sizes = { [key in SizeList]: number ｝
// sizes2 needs to be a type not an interface, as interfaces don't allow mapped types to declare properties or methods

// 3️⃣ Record<SizeList, number>

// 4️⃣ CustomRecord<SizeList, number>
```

- My rule is just type it straight up until you can't.
  - Usually when the keys of an object are also being generated, or passed in when you need to do this. Is most cases `Record<>` is what you want.

- ## TIL: in TS `satisfies` doesn't set the type of an object, which means you can't assign properties to it later. 
- https://twitter.com/matthewcp/status/1719391086345363664
  - So if you want to both have type safe object literals and mutate them later, you need to use both satisfies and a type annotation.  
- There's never any reason to write `const p: T = e satisfies T;` . It's the same thing as `const p: T = e;` in every case
- To me, the use-case of "satisfies" is kind of like an "instanceof" check. It doesn't cast to the type, but instead tells the compiler its "type-like" but can still be narrowed to a more specific type. So its almost acting like a discriminating union. `{ one: string } | Props`

- ## TIL that `typeof v === 'function'` and `isFunction(v)` behave differently in TS
- https://twitter.com/AndaristRake/status/1676574933407735808
- this might be because **JS classes have typeof 'function' too**, and they can't be invoked like functions

- ## TypeScript pro tip: Instead of using `filter(Boolean)` to remove null and undefined values from arrays, create a type guard function. 
- https://twitter.com/diegohaz/status/1667197904006569991
- I've also been using flatMap for that
  - const nonNullArray = [1, 2, null, undefined, 3].flatMap(v=>v?[v]:[])

- ## 泛型傻瓜式*指南了，从三个角度描述了泛型的作用
- https://twitter.com/mattpocockuk/status/1625838626742435842

- ## Set #TypeScript option `"importsNotUsedAsValues": "error"` to force you to use the `import type` when only a type is imported.
- https://twitter.com/kossnocorp/status/1630120975927836672
  - [Proposal: deprecate `importsNotUsedAsValues` and `preserveValueImports` in favor of single flag · microsoft/TypeScript](https://github.com/microsoft/TypeScript/issues/51479)

- ## Picking #TypeScript Generic Slot order is tricky...
- https://twitter.com/SCooperDev/status/1615000886513750017
- a) go for consistent order across a project
- Pros: 
  - Provides an easy mental model
  - Consistent dev experience
- Cons:
  - Need to know all possible generics upfront 
  - Add placeholder for generic before it is actually used to avoid future breaking change
b) go for most likely to be used per interface?
- Pros:
  - Avoid devs having to provide generic placeholders to be able to set a later generic
  - Update interfaces independently as generics supported
- Cons:
  - Inconsistent order cross entire project potentially confusing for devs

- 👉🏻 Right got you! I have seen this before referred to as a Generic Bag. It's a great solution to the problem and is closest to a name params implementation. Only downside is that you have to educate users how to use it as it's not a standard practice.
  - tannerlinsley: This education is what ultimately made me not ship with it. I was 🤏 this close!!! Generic Bag, Generic Maps, Generic Groups, Object Generics. There’s a lot of terms to describe what I hope someday will be unnecessary.
  - Yeah it's that hard balance between shipping something that works great (if you know what is going on) versus the number of questions and support cost it would lead to explaining how to use it.

```typescript
type NamedGenericParams<TData, TValue, TContext> = {
    data: TData, 
    value: TValue, 
    context: TContext
}

// The main trick lies in the "recursion" here.
// TData is generic parameter, whose default value is type of "data" property on the passed T type.
interface GenericInterface<T extends NamedGenericParams<TData, TValue, TContext>, TData=T["data"], TValue=T["value"], TContext=T["context"]> {
    data: TData;
    context: TContext;
    value: TValue
}

// define type of each field
type UserParams = {data: "userData", context: "userContext", value: "userValue"}

// pass this definition to GenericInterface
interface UserInterface extends GenericInterface<UserParams> {
}

// only way how to assign the values now
const a: UserInterface = {
    context: "userContext",
    data: "userData",
    value: "userValue",
}

```

- b. But I always leave JS Doc comments so the user can hover over the type and see the order and anything else relevant to its usage.

- I wish TypeScript had named generics sometimes, e.g. `Foo<data: TData, context: TContext, value: TValue>`

- ## IterableType
- //localhost

```typescript

const FRUIT_TYPES = ['apple', 'orange', 'banana'] as const

type IterableType<T> = T extends Iterable<infer U> ? U : never

type FruitType = IterableType<typeof FRUIT_TYPES>
    // ^? 'apple' | 'orange' | 'banana'

const FRUIT_TYPES_SET = new Set(['apple', 'orange', 'banana'] as const)

type FruitTypeSet = IterableType<typeof FRUIT_TYPES_SET>
    // ^? 'apple' | 'orange' | 'banana'
```

- ## I really don't like that TS is introducing inconsistencies, the other day I learned that `Array<A>` and `A[]` are not the same thing

```typescript
type A = [string, ...Array<number>, ...Array<boolean>];
type B = [string, ...number[], ...boolean[]]; // 🚨 error

type Aliased = boolean[];
type C = [string, ...number[], ...Aliased]

```

- ## [typescript package visibility (create library) - Stack Overflow](https://stackoverflow.com/questions/44821327/typescript-package-visibility-create-library)
- typescript skipped all fields annotated with `/** @internal */` even with public modificator

- ## What are your favourite type helpers? I.e. helpers which return types from other types.
- https://twitter.com/mattpocockuk/status/1597955503480414208
- Zod's Infer

```typescript
type Truthy<T> = T extends false | '' | 0 | null | undefined ? never : T;

function truthy<T>(value: T): value is Truthy<T> {
return Boolean(value);
}

type NonEmptyArray<T> = [T, ...Array<T>]

```

- ## I've changed my mind about interface vs type again
- https://twitter.com/mattpocockuk/status/1597561667520299008
- My old opinion:
  - Prefer interface over type where possible
- My recent opinion:
  - Doesn't matter, as long as you stay consistent
- My new opinion:
  - Prefer type unless you need a specific feature of interfaces
- Why? Because at the end of the day, interfaces give you lots of features that you don't usually anticipate needing. Like declaration merging
  - These make them behave subtly different to types in some circumstances.
  - A type is a type is a type. Can't be extended, can't be declaration merged, can't be messed about.
- If you want to use 'extends', or just love the 'mental model' of interfaces - go right ahead.
  - But I think I'll be defining my object types as types from now on.

- Exactly our take as well! Everything is a `type` until you need to extend it or some interface features!

- I would argue that if you expect your types to be used by others (eg in a library) keep them as interfaces. Your users may want those extra features
  - Imo the only use-case for declaration merging. In an app, declaration merging just hurts maintainability in the long run.
- Yeah in lib code you should default to interface. And absolutely, this is a big ol' bikeshed.

- Exactly where I landed and exactly for the same reasons.
  - I'd even go as far as to say that most of the examples of "good uses" of declaration merging are actually wrong, because they distribute the ultimate type definition over multiple places, which hurts maintainability.

- I've been pretty consistently in the type camp specifically because declaration merging feels an anti-feature that shouldn't ever be used.

- Interfaces for OOP in general and types for everything else (like react function components)?

- unfortunately typescript suggests preferring interfaces in the docs
  - Yeah I think this is out-of-date advice based on tweets I've exchanged with the team.

- ## ts-unused-exports deserves a TypeScript tip.
- https://twitter.com/JNYBGR/status/1597178235804012544
  - It is a underrated but invaluable tool for finding code you can safely delete!

- ## Is there a tool for #TypeScript that checks static type assertions similar to the following one?
- https://fosstodon.org/@rauschma/109400498171074927

```JS
// %inferred-type: (string | number | boolean)[]
const arr = [1, 'a', true];
```

- https://github.com/JoshuaKGoldberg/eslint-plugin-expect-type
  - ESLint plugin with $ExpectType and $ExpectError type assertions
  - This plugin also supports twoslash annotations, which is a comment line that starts with two slashes (`//`) and the `^?` identifier to annotate the symbol 

- [typescript - How to test if two types are exactly the same - Stack Overflow](https://stackoverflow.com/questions/53807517/how-to-test-if-two-types-are-exactly-the-same)

- ## I'm still horrified that a certain subset of TypeScript developers think coercing(强制、强迫) types unsafely during decoding (JSON to structured data types) without checking the JSON is in the least bit reasonable. We have io-ts and many more libs that do the right things.
- https://twitter.com/SusanPotter/status/1531309620857294851
- There may also be a literacy problem here... people just don't understand why `unknown` is so much better than `any` or why type coercion ( `as` ) is bad, but type assertion ( `is` ) can be a great tool when used right.
- Utilities like Zod + TRPC are great at avoiding situations like this IMO. That said, I believe that validation on the *client* (public code) isn't always necessary if it receives its data from a source it *should* be able to trust wherein static checks + try/catch should be fine.
  - But just to reiterate for clarity and posterity...
  - 👏 Validate 👏 Your 👏 User 👏 Inputs 👏 On 👏 The 👏 Server 👏 (at least)

- ## TypeScript protip: accept any string, but suggest some specific values on autocomplete.
- https://twitter.com/diegohaz/status/1524257274012876801
  - `type StringWithAutocomplete<T> = T | (string & Record<never, never>)` ; 
  - `type Fruit = StringWithAutocomplete<"apple" | "banana" | "grape">` ; 

- ## which is the best approach to have type safety in the object values, while getting the literal types on the `keyof` expression?
- https://twitter.com/P_FFigueiredo/status/1521417203064651776
  1- Adding a type assertion to each value; 
  2- Adding each property to the Object's key; 

- What about "as const" assertions? It can be used for type safety for keys and for values

- ## One of my favorite little ts utils `export type Maybe<T> = T | undefined | null;` 可空类型
- https://twitter.com/alexdotjs/status/1518915886400290818
- I mean, it's good, but this is my fave
  - `type ValueOf<T> = T[keyof T]; `

- ## Generic maps (and hopefully the future of large-scale generics in TS) change everything. 
- https://twitter.com/tannerlinsley/status/1521221444084002816
  - Now, you only need to add a few lines of inference types to your public API call sites and subsequently use your new generic in your types. It's so liberating.
  - P. S. Generic maps are not a TS "feature". They are a pattern of providing "maps" of key-value style generics as a single generic to a type, instead of passing each of those generics individually.
  - The next missing piece to this pattern is TypeScript's ability to infer these maps.

- I think it's just re-discovering `fn(one, two three)` vs `fn({ one, two, three })`. But for types instead of runtime. If you expect your parameters to grow, or contain values that should have an explicit label => use a bag (here: type map)
  - I heard "option bags" before so "type bags" makes sense to me.
- I wonder if there's a case for all internal types (i.e. those that aren't responsible for actually _inferring_ things from the generic slots) being objects, not separate slots.
  - `myFunc<T1, T2>(): InternalThing<{ t1: T1; t2: T2 }>`; 
  - You just described React Table v8
- Lovely, and it all works as expected? I don't see why it wouldn't
  - It works great! It's really just the inference sites that get a bit... interesting. You have to use call chaining (type builder pattern) to split up "optional" inference using a little `Overwrite<TGenerics, { ...partialGenerics }>` magic. Then you're home free.
  - Yep. Once the language actually supports 1st-class inference for generic objects, I could see a lot of libraries moving to this pattern.

- ## ts类型练习
- https://twitter.com/tannerlinsley/status/1520057027124367360

```JS
// 要实现的效果，将创建对象实例的方法提取出去作为普通工具方法
// 注意，属性和渲染方法都在参数中传进去

function createFoo(options) {
  return () => options.render(options.foo);
}

function Foo() {
  const render = (d) => `${d}`;
  const getFoo = createFoo({
    foo: 1234,
    render,
  });
  const foo = getFoo();
}
```

```typescript

import * as React from 'react'
type Generics = {
  Render: () => React.ReactNode | JSX.Element
}
type Renderer<T extends Generics> = () => ReturnType<T['Render']>
const MyComponent = <T extends Generics>() => {
  // Why does this work?
  const div1: ReturnType<Generics['Render']> = <div />
  // But these don't?
  const div2: ReturnType<T["Render"]> = <div />
  const renderDiv: Renderer<T> = () => <div />
}
// this does not make sense:
const foo = <T extends number | string>() => {
const bar: T = 'bar'
}
```

- ## Scared by TypeScript generics? The best way to get to grips with them is to understand how they're made.
- https://twitter.com/mpocock1/status/1508757718630342657
  - Here's a guide to EVERY way you can instantiate a generic in TypeScript.
- ## yet another use case for higher order generics
- https://twitter.com/tannerlinsley/status/1509208626338050055
  - `type Foo<T> = { foo: T }` 普通泛型
  - `type UseFoo<Foo extends any<T>, T> = Foo<T>` 高阶泛型
- One use case for this in #ReactTable v8 would be the ability for other frameworks to provide their own type for what a "renderable" is (a generic provided to RT), and have React Table internals be able to pipe through other types to that generic (column, row, options, filters...)
- ## Object.entries() and Object.fromEntries() are soo useful but TypeScript’s built-in types for them are soo bad
- https://twitter.com/buildsghost/status/1498895804798357510
- ## You are probably familiar with index access operations. 
- https://twitter.com/TitianCernicova/status/1494683318230605827
  - Where you can get the type of a property in another type using the T[K] syntax. 
  - This works well for when K is literal type or a union of literal types
  - It also works if T is a union, but only for common keys. This isn’t necessarily surprising as only common keys are accessible on a union.
- ## Cross-fading any two DOM elements is impossible right now. Here's why
- https://twitter.com/jaffathecake/status/1462803936679763971
  - [Cross-fading any two DOM elements is currently impossible](https://jakearchibald.com/2021/dom-cross-fade/)
- The spec change has landed, and there's an implementation behind a flag in Chrome Canary!
- This is a good explanation of why there can be subtle opacity dips with Framer Motion's shared layout animations. We use opposing easing curves that keep the overall opacity as close to 1 as possible but something like this CSS rule would really help.
- ## Note to future self: this is the tsconfig you want for a library in a monorepo. Don't use `paths` to get types from other packages, use `references` !
- https://twitter.com/steveruizok/status/1464906551664250884
  - The reason for this is that you'll also want to run some code after build to replace the "~" paths with relative paths, but you don't want to replace imports from other packages in the repo (e.g. @monorepo/vec) with relative paths
- do you build with tsc or esbuild? I found that references only work with tsc and it's extremely slow
  - I do use esbuild! I only use tsc to generate type declarations.
- If the dep is meant to be published and depended upon - ye, it should still be defined as a dep in pkg.json
- ## Always publish `src` files, 
- https://twitter.com/__morse/status/1471169129478508551
  - if you use typescript you can also pass the `declarationMap` option to tsconfig to make cmd+click go to the original src file instead of the `.d.ts` file
- ## Using generics in @TypeScript beyond simple use cases becomes a massive deep dive into the variable/type dependency graph of any system it touches. 
- https://twitter.com/tannerlinsley/status/1476604095817404452
  - TLDR: If your types have circular dependencies, you will eventually have to short circuit your inference and pick a starting point.
- This is the primary reason why migrating JS libraries to TS is never a simple .js => .ts rename with added annotations. 
  - The Typescript compiler forces you to write code that can incrementally reason about the inferrable and knowable parts of the entire system
  - As you consume more generics, complexity grows linearly. If those generics begin to rely on each other or need to come in a specific order, the complexity skyrockets. And this is where the dependency graph of your vars/types comes in.
- In the case of #ReactTable, we need to know the shape of your row data, filterFns, sorters, aggregators, etc, before we can infer anything in your column definitions, which consume all of those types together. Columns also have value-based inference as well, 
  - So technically we need to know about your column accessor, too, before we let you configure anything else. 
- ## how to extract the generic type determined by a type guard function
- https://twitter.com/acemarke/status/1435731824303648771
  - type GuardedType<T> = T extends (x: any) => x is (infer T) ? T : never; 
- [Get the guarded type of a custom type guard](https://github.com/microsoft/TypeScript/issues/30542)
- ## TypeScript—I’ve switched:  From: `string[]` To: `Array<string>`

- https://twitter.com/rauschma/status/1431884615862603781
  – Better for complicated element types: Array<[string, number]>
  – Looks similar to other types.
  – Look similar to new `Array<string>()` which helps with type inference (default values, class field initializers).
- Definitely better readability. When you see `Array<number>` you read it from the start as "array of numbers".
- I used to prefer `Array<string>` for the same reasons but then switched to `string[]` because of readability in nested types. 
  - `Promise<Array<string>>` vs `Promise<string[]>`

- After personally having strong opinions about code style in the past, I've learned that it's better to just align with common practices.
  - By applying common practices you will get a trained eye for it, which helps to read third-party code that most likely uses the same code style
  - Therefor I personally decided to just keep using `[]` for arrays.
  - Unless things really get error prone... like with tuple element type... in which case I will use `Array<..>` for an array.
- In the same way, prefer `Record<string, T>` over `{ [key: string]: T }` for key value objects with consistent key value types.
- Linters say to use [] though, so that's what I follow, simply so that the whole team can standardize on one model
- ## Specifying the type of this for functions
- https://stackoverflow.com/questions/44164032
- Following up on specifying the type of `this` in a class or an interface, functions and methods can now declare the type of `this` they expect.
  - By default the type of `this` inside a function is `any` . 
  - Starting with TypeScript 2.0, you can provide an explicit `this` parameter. 
  - `this` parameters are fake parameters that come first in the parameter list of a function
- Notice that `this` won't get translated into js, so it's not a real argument in the function.
- function f(this: void)  // make sure `this` is unusable in this standalone function

- ## how do people handle functions that can throw in typescript? 
- https://twitter.com/tmcw/status/1423404151149580292
  - half-considering starting to use an Either type of returning result | Error, don’t want to rely on just remembering which functions are throwy
- In majority of the cases it should be fine, but in some weird cases you might encounter some of the system errors `RangeError` or `TypeError` to name a few. Which makes me think exhaustively typing all the possible errors  is impossible.
- I would even recommend creating a simple `Err` class for the error side of it's a logical error and not an actual unrecoverable error. Switching our parser to our own error type was a massive perf boost (somewhere around 100x for us)

- ## how do you type a memoize function that accepts an arbitrary length of arbitrarily-typed arguments?
- https://twitter.com/Rich_Harris/status/1423023727680315392
  - we have a winner! guardian alumni network to the rescue 
  - `type Fn<T extends any[]> = (...args: T) => any;`
