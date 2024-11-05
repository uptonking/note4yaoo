---
title: thread-lang-js-proposal
tags: [js, proposal, thread]
created: 2021-09-14T06:29:14.993Z
modified: 2023-11-10T08:05:25.474Z
---

# thread-lang-js-proposal

# guide

# discuss
- ## 

- ## 

- ## 

- ## promise.unthen(cb) would be pretty useful
- https://twitter.com/justinfagnani/status/1422783049159221250
- Nowadays so many things are  Promises / async/await that EventEmitters and such have almost been forgotten.
  - It’s an interesting thing to remind oneself of: That Promises may not always be the better choice, sometimes events are preferable, like in this case 
- `Abort` works with fetch fine. But generic promises is a no go currently. Lots of holdup on exactly how to handle and expose aborting inside a custom executor.

- ## JSR - the JavaScript Registry - is now available in public beta.
- https://twitter.com/deno_land/status/1763556854716661961
  - Works across runtimes (Node, Deno, Bun, workerd and more) and alongside npm/yarn/pnpm
  - TypeScript first, ESM only
- Interesting choice of esm only, probably the right thing but what happens when cjs is detected?
  - In Node and Deno runtimes, there's a compatibility layer that lets you import CJS modules as ESM. JSR packages use this behavior.

- ## A concise example of why I really don't like decorators that much.
- https://twitter.com/BenLesh/status/1750560391682294159
  - IMO, decorators should have been metadata only. We already have enough ways to duck-punch JavaScript into oblivion(遗忘)
  - Let me tell you about the other thing I don't like, `@defaultExports`

- Where is the problem exactly?
  - Basic: Any given developer reading the code needs to know what a decorator might change.
  - Advanced: You can no longer use static analysis to have any idea what a class, property, method, or argument does when it has a decorator applied unless the tool knows exactly what the decorator does.

- The bad thing about decorators is that they add an unnecessary syntax for function calls. Other than that, they are just functions, so the issues you have are with:
  - Overriding
  - Metaprogramming
  - And fairly enough, because they are dangerous tools.

- Why do people get so angry when a perfectly readable function does exactly what it looks like it does

- ## Almost 1 year ago I tried using WeakRef but had to abandon it because it caused bizarre bugs. 
- https://twitter.com/gaforres/status/1723818760346259631
  - Wrote a bunch of regression tests while diagnosing but ultimately rolled it back.
  - Today I enabled them again and my tests all pass. So I guess I'm trying this again (behind a flag).

- ## you can't async iterate over ReadableStream. It's only supported in Node, Deno, and Firefox
- https://twitter.com/pilcrowonpaper/status/1723406435579834728
- Sad, Generator function reading the stream, loop reading the generator function, function running the loop, program running the function, os running the program, kernel processing the os commands, and i'm out of space to type more...
- The blocking issue was closed 17 days ago, so I wonder if this will be fixed soon.

- ## JS should have a builtin FIFO type, imo
- https://twitter.com/jarredsumner/status/1532503267455795200
  - array.shift() and array.unshift() implementations are poorly optimized for this. fifo’s are very common
- Most user-facing queues where the order matters actually want a fifo instead of a stack — you want to send stuff back in the same order the user provided it instead of the reverse order
  - I mention .unshift() because often you want a prioritized queue — to be able to move some element to the front efficiently as well
- What’s wrong with unshift and pop? Or push and shift?
  - Don’t know if it’s true, but some articles claim that array.shift ist O(n) which would make a Queue iteration pretty inefficient.
  - internally, it clones the entire array each shift() if the list is longer than a handful of elements
  - JSC hasn't implemented the optimization for skipping that on small arrays so it's a little worse in JSC too

- ## I've taken the time to articulate all of my thoughts in a single space about the current pipeline proposal. (It's opinionated, sorry)
- https://twitter.com/BenLesh/status/1436890184449236994
  - [TC39 Pipeline Operator - Hack vs F#](https://benlesh.com/posts/tc39-pipeline-proposal-hack-vs-f-sharp/)
- What Is A "Pipeline Operator"?
  - Simply put, the pipeline is an operator, |> in this case, that allows a software developer to "pipe" the evaluated expression from the left-hand-side (LHS) to some function or expression on the right-hand-side (RHS).
  - There were many competing proposals, two stood out the most, the Hack pipeline — currently in stage 2, and the F# pipeline — skipped despite being very popular.

- I was an early advocate of pipe, but the longer I've used JS the more I've gravitated(被吸引，吸引而转向) towards explicitness: debuggability over brevity. 
  - I favor the hack version but honestly in my day job I'd probably bias towards neither and use let.
- One of the biggest advantages of the F# pipeline is that it allows for destructuring of arguments- this is something I use _loads_, as I prefer working with single arg object instead of multiple parameters (creates inflexible APIs). You should list it in the cons for Hack.
- Piping is such a crucial FP concept, it's really strange that the proposal doesn't take partial application, the other crucial FP concept, into account. 
- Is it not possible to have both options?
  - Yes you would have both options if F# and partial application both landed. In fact, that would give us all the most options.
- I don’t really get why the community didn’t go for the F# way since it’s definitely the way  (most) FP minded people tend to think imo. If you’re not using pipe/compose at this point, you won’t use the pipe operator anyway.
  - Counterpoint: I'm going to use hack pipes all the time when they come to JS and I'm not very FP minded (IMO having every bit of logic abstracted into a small function tends to cost too much flexibility). Hack pipes would be awesome for everyone and would quickly spread
- Partial application has much wider applicability anyway, and should get in first to reinforce the cowpaths that ACTUALLY need to be paved.
- I agree deeply with your conclusion. The F# + partial application proposal makes much more sense than the Hack proposal. The Hack proposal feels really bad. JS has been making progress by adding features that make sense and compose well together. The second proposal makes sense.
- Sad they skipped the F# pipe.
# discuss-js-proposals
- ## 

- ## 

- ## 

- ## 

- ## 🔀 JavaScript 标准委员会今天通过了新的提案，增加 struct, shared struct, unsafe 块，内存顺序，Mutex 同步原语等概念，解锁 JavaScript 多线程共享内存的能力
- https://x.com/_hisriver/status/1843671089534382244
  - 未来可以让 JavaScript 像 Rust 和 Go 一样拥有高并发能力。我看 JS 的大佬一致叫好，不过这些复杂的东西引入 JavaScript 真的有必要吗？
  - 那个 Memory Ordering 挺复杂的，Rust 里面我花了好久才搞明白。以后 JavaScript 也要写 Unsafe 代码了？
- Stage 1 而已，至少要到 Stage 3 才算通过

- 挺好的，worker终于有靠谱数据传递和锁机制了
- 引入了worker却不能共享对象才叫奇怪，这个是对之前奇怪地方进行修正，当然如果当初不加worker就不会有这些需求。

- 这个提案其实已经有一段时间了，也不是今天才加的。而且这个多线程共享内存的能力原本就有（SharedArrayBuffer），只是是个底层api，不是给人用的（一般是作为编译target，手写太蛋疼）

- 这个早晚的事情，要不然web 平台很难跟 android 和 ios 竞争。而且 web 是开放的，我认为更应该进化。

- 已经完全成为rust了？？不过这么多新标准要一一落实估计得10年了

- ## This presentation to TC39 has me *worried* for the future of JavaScript. _202410
- https://x.com/nullvoxpopuli/status/1842389133810913338
  - JS0 -- the minimum JS the engines want to implement
  - JSSugar -- what you're already writing today that is ultimately compiled down to JS0

# discuss-feat-number
- ## 

- ## 

- ## protobuf-ts 竟然提供了参数将 int64 数据转成 JS string，以保证精度不丢失。 虽然，需要额外安装插件
- https://twitter.com/ThaddeusJiang/status/1724686886781047040
  - npm install @protobuf -ts/plugin
  - 不过 TS 社区里 protobuf codegen 可真多，而且名字起的都很像，我快被搞晕了

- ## 虽然我知道 JavaScript 的 number 在精度上和其他语言不匹配，没有 int32 int64 这种细分，但我也不喜欢 long.js ，很容易出 bug。
- https://twitter.com/ThaddeusJiang/status/1693578008601526470
  - 建议轻易不要使用 long.js， 除非，你也上了 #gRPC #protobuf 的破船
  - 代码能跑，但结果不符合期待

- 我知道js只支持到2**53 但是我之前记得在那看过 新特性解决了这个问题 还支持有无符号 难道是我记忆错位
# discuss-feat-enum 📍
- ## 

- ## 

- ## [Why you shouldn't use Enums _202403](https://www.wordman.dev/blog/typescript-enums)
- basically TypeScript creates an Object that looks like this
  - The nice thing with this approach is that is lets us have access to every possible information of the HttpStatusCode in a bidirectional way
  - it does come with an increase in bundle size
  - `const enum` s in TypeScript don’t create any code at runtime, they just act as a type and their value is automatically resolved when used. The result of this looks great to me, but you can run into problems with this. It is getting more and more common to use other transpilers to generate JavaScript code from TypeScript. Often those transpilers work on a file-by-file basis, transpiling just a single file without fully understanding the full type system. Vite and Babel work this way for instance. Just transpiling a single file does not read imported modules, so there is no way to support const enums. 
- don’t use enums! TypeScript has Literal Types that are a great replacement for enums

- ## [You might not need TypeScript Enum - DEV Community _202309](https://dev.to/maafaishal/you-might-not-need-typescript-enum-1f4n)
- TypeScript provides both numeric and string-based enums.
- While Constants can cover an object with string and number property values including all data types.

- I used https://babeljs.io/repl to know the size after the code has been transpiled.

- Based on several aspects I've discussed earlier, we can replace Enum with Object. Object has the flexibility for defining various data types, has a smaller transpiled size, and can detect both property values or property access.

- I'm avoiding TypeScript enums with all cost. I prefer to use string unions instead

- ## 🤼🏻 [Insights from Adopting TypeScript at Scale | Hacker News _202011](https://news.ycombinator.com/item?id=25043541)
  - Fascinating that Bloomberg started adopting server-side JS in 2005 and client-side JS only in 2012. And that they use their own deno-like JS engine.

- > Back in 2005, the company started migrating those apps from Fortran and C/C++ to server-side JavaScript
  - Since their use of Javascript predates Node (and the rest of that ecosystem, like Webpack or Babel or whatever), they've built up their own Javascript environment that doesn't rely on Node or Node conventions at all. 

- There isn't much of a difference between regular enum and const enum when it comes to the usage of the enum keyword. The big difference is what they compile to - where const enum evaporates by inlining the values into the usage sites.

- 
- 

- ## Bloomberg hates enums, and so should you _202410
- https://x.com/mattpocockuk/status/1841564439281029272
  - 📝 [10 Insights from Adopting TypeScript at Scale | Bloomberg LP _202011](https://www.bloomberg.com/company/stories/10-insights-adopting-typescript-at-scale/)
- this is actually false... Bloomberg RECOMMENDS enum as one of the options to avoid type inlining. I don't get why you hate enums so much. My only problem with them in TS is the lack of features.

- Just treat them as values that get inlined and problems are gone. TS implementation of enums is just ... suboptimal.

- I think enums have their place. For simple things, union types are a better solution when the language supports it like in TS.
  - However, enums can have (e.g. in Kotlin) additional benefits like supporting runtime enumeration of options, methods, reverse mappings, and so on.

- They are quite wasteful when you really want to squeeze things.

- ## Did you know that numeric and string enums compile differently?
- https://twitter.com/mattpocockuk/status/1765700809113645458
  - Numeric enums create a reverse mapping(keys and values all mapped to keys), but string enums don't
- Also weird that you can mix them and the individual values compile differently

- Probably because typescript numeric enums are bit mask, as in bitwise a | b satisfies the type. That number value won’t be in the object map, so it could lead to runtime errors. So it’s better to not support mapping in that direction at all.

- I don't like enums at all. I prefer mapped object or union types 
  - but in case I have to use them... I prefer they are not compiled, just defining the enum as const.

- I'm going to stick with the plain JavaScript object with as const from now on

- I’m rewriting enums to simple union types all the time.

- If you reverse mapped string enums, you could create collisions between keys and values

- ## TypeScript Tips: Always use Integer as Enum values.
- https://twitter.com/ThaddeusJiang/status/1752971923167064159
  - Since some dependencies only support `Integer` Enum values, like protobuf.

- ## I will admit, TS enums are kind of useful. But only for one specific case.
- https://twitter.com/mattpocockuk/status/1694703900778025210

- JS people don’t see object syntax having anything to do with ordering anyway. i would rather use the enum with explicit order values for readability

- Object mapping communicates the intent better than implicit enums. Someone not familiar with the syntax will scratch their head after looking at your example.

- I would avoid enums at all costs, too manny issues with tools.

- string union > enums

- ## [The difference between enum, const enum and declare enum in Typescript : javascript](https://www.reddit.com/r/javascript/comments/pp08u5/the_difference_between_enum_const_enum_and/)
- i recommend using union types instead of enums, like: `type DownloadStatus = 'IDLE' | 'LOADING' | 'DONE';` , 
  - it will cause a lot less problems than enums when dealing with webpack&babel&etc.
- For me the thing that really eliminated the desire to use enums, was deriving union type alias from an array, so the values can also be iterated without being repeated. Like:

```typescript
export const colors = ['red', 'green', 'blue'] as const;
export type Color = typeof colors[number];

export const COLORS = Object.freeze(['red', 'green', 'blue'] as const);
```

- That's very close to what we had to do at my job. We now define our "enums" as a `const` object, which lets us change the const object without having to also change the type

```typescript
export const Example = { First: "first", Second: "second" } as const;
export type Example = (typeof Example)[keyof typeof Example];
```

- The only downside so far is that array's type is narrowed to a tuple of literals
  - 数组的includes方法会异常
  - Because this is an extremely common pattern for us, we've taken to using the `lodash` function includes which is typed differently but performs the exact same check under the hood.

- [enum vs "as const" vs Object.freeze() what is the difference between those 3? : typescript](https://www.reddit.com/r/typescript/comments/ztpl9k/enum_vs_as_const_vs_objectfreeze_what_is_the/)
  - `Object.freeze` is a runtime thing whereas `as const` is purely in compile time

- ## Is there EVER a reason to use enums in TypeScript?
- https://twitter.com/erikras/status/1418279793993338880
  - outside of t-shirt sizes, where you need SMALL to be < MEDIUM, I’ve found almost no use compared to string union types
-I have the same experience. Every time I've decided to use enum it has felt very cumbersome(复杂的，笨重的). 
  - Using arrays or objects literals with "as const" seems to cover all the cases where I'd feel enum would be better.
- most of the time you need to marshal enum values to strings. And that’s why string union types work.
- Isn't enums more readable and maintainable?
Consider the case where I have a Widget enum on FE and BE sends its value. I use the enum for variables, arguments, conditionals and TS enforces to pick from enum. One day BE chose to change value, I just have to change my enum's value.
  - This is arguably the only thing that enums have over constant union types. However, I would argue that you're very unlikely to ever change an enum's values later on. You're much more likely to extend it with new values, which enums give you no additional benefit with.
- [Comparing TypeScript's union types, enums and const enums](https://kajetan.dev/2021/typescript-unions-and-enums/)
- Compile time vs run time
  - Only enums result in JS output after compilation. Others are dropped during the compile time.
- Iterating through values
  - Only enums can be iterated through
  - If there's no value at runtime, we cannot iterate through it.
- Switch-case and matching values
  - Non-exhaustive matching on either of the three results in error when --strictNullChecks compiler option is on.
- Numeric values
  - Enums are numeric by default (if you don't assign any value to its members). You can assign any number to the numeric enum.
- Extending
  - Unions can be extended by declaring a "union of union types". 
  - One way to extend an enum or const enum is to convert them to a type by creating a sum.
- Impact of refactoring
  - With union, you'd have to check all places impacted by the change and update those places to match new value of the union.
  - With enum, you'd apply the change just on the value of enum's member. 
- Template Literal Types
  - TLT can be created only as a union type
- Structural vs nominal types
  - Enum is an example of a nominal type (enums are not equal if they differ by name). 
  - Unions represent structural types (if literal values match, they are equal).

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
