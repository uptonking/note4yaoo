---
title: thread-lang-js-ts-types
tags: [lang, thread, typescript]
created: 2021-08-05T04:30:46.106Z
modified: 2021-08-05T04:31:02.298Z
---

# thread-lang-js-ts-types

# guide
- ## React TypeScript Cheatsheet
- https://github.com/typescript-cheatsheets/react
  - https://react-typescript-cheatsheet.netlify.app/docs/basic/setup
- ## Here's everything I've learned from leading TS dev teams and working on XState's core team.
- https://twitter.com/mpocock1/status/1509964736275927042
- more-cheatsheet
  - https://nerdcave.com/tailwind-cheat-sheet
# discuss
- ## 

- ## 

- ## 

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

- ## I’ve been spiking on runtime validation today using zod
- https://twitter.com/steveruizok/status/1600512479305539585
  - We were finding some edgy cases in @tldraw where shapes would have null values in one of their points, or some other obscure issue that wouldn’t be immediately recognized.
  - Sometimes the bad shape would render fine, but it’s indicator would crash when a user would hover or select the shape, or when it was resized or duplicated.
- Defensive coding? Sure, we can do that. But we would always be chasing bugs, one step behind the complexity of the project, unless we had a way to describe how shapes should look at runtime: no zero-width shapes, no Infinity rotations, etc.
  - Hence run time checking! zod provides a really great API for this sort of validation.
- My only concern there is that inferring types from the library’s definitions seems substantially slower than declaring them straight out; and that our opaque type tricks don’t work with the lib, so we may have to change that
  - Have you tried the alternatives? I've used Valita with no issues, but ts-runtime-checks looks pretty interesting.
  - You can use tozod to define a zod schema from an existing interface

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
  - `type Fn<T extends any[]> = (...args: T) => any; `
