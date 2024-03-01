---
title: thread-lang-js-stars
tags: [js, lang, thread, typescript]
created: 2021-06-22T11:54:15.957Z
modified: 2023-11-10T08:05:31.982Z
---

# thread-lang-js-stars

# guide

# 个人风格

```typescript

// map.get的返回值可适当使用非空断言

let val:string;
val = map.get(key)!; // 简化val中处理undefined的定义
if(val) // doSth

```

# discuss
- ## 

- ## 

- ## Ever wondered what the difference between a class method and arrow function is?
- https://twitter.com/mattpocockuk/status/1763251034565013841
  - arrow functions retain the context they were defined in.

- Important to note you can’t bind arrow functions
  - Binding the arrow function doesn't affect "this" keyword like it does with normal functions

- don’t write code like this

- ## Did you know that `array.sort()` doesn't work with negative numbers?
- https://twitter.com/ccorcos/status/1759665586983084255
  - Just sorts as strings

- It doesn’t work with numbers at all. It performs alphanumeric comparison.
  - Yeah, good point! I didn’t know that. Ironically, it works for dates, because their string representation is in ISO format.

- default comparator is for strings, not numbers; this is more of a criticism of JavaScript being dynamically typed

- ## unwrap: 即使我能理解这段代码的语法，我还是理解不了这代码的作用
- https://twitter.com/ThaddeusJiang/status/1678316196318552064
- 主要是获得强类型，类似于int vs Integer。至于价值和成本，要看具体的应用场景。我大概率不会这么做，就算是要获得强类型，用一个enum就够了。这个设计类型本身已经有了信息，还要再暴露isSuccess, isFailure有冗余。但是这个还要结合具体场景才好判断，比如调用的地方强制实现这个接口。
- rust和rescript都有类似的Result类型，也有点类似于 Golang 的函数返回值类型（如果第二个返回值不是 err 就是有异常）
  - 同感，第一眼看到就觉得是模仿 rust 的风格。但 rust 有问号的语法糖，这里没有，所以我觉得即使模仿了这个形式，也没有带来太大收益。
- 要是忙到最后还是throw了，前面那些反复横跳就算全白费劲了。在我印象里这种模拟option/either的写法一般是为了实现“never fail”吧。
  - unwrap 就是强制解包，实际必须使用它的场景很少，但还是需要有这么个 escape hatch
- 就是为了让你强制检查错误。

- ## Why does TypeScript make us use "./foo.js" extensions when importing?
- https://twitter.com/mattpocockuk/status/1711697978140852695
  - To me, it makes sense - it speeds up Node startup and means your TS code more closely resembles your compiled .js code.
  - But, it can be pretty confusing on first look.
  - [Relative import paths need explicit file extensions in EcmaScript imports | Total TypeScript](https://www.totaltypescript.com/relative-import-paths-need-explicit-file-extensions-in-ecmascript-imports)

- Node always complicating our lives

- ## Is there an alternative to `JSON.stringify` for getting a stable string representation of a serializable JS object that’s suitable for use in a hot path?
- https://twitter.com/andrewingram/status/1710799442050200048
- What’s your goal? Speed? Obfuscation? Predictability?
  - Using as a lookup key on a hot path

- Relay code is here: https://github.com/facebook/relay/blob/main/packages/relay-runtime/util/stableCopy.js
- IME any optimizations on JSON stringify only work on smaller objects, in which case the optimizations are hardly meaningful. On larger objects the runtime is better optimized to serialize. I would only worry about the stable order fn in terms of time cost.

- https://twitter.com/andrewingram/status/1710981678284312997
  - Related question, looking for prior art of a Map implementation that works in scenarios where the keys are argument arrays. The solution seems to be nested maps, one per array position, only falling back to JSON.stringify for non-primitive arguments.

- hmm isn't this technically just a Trie? (over arbitrary values instead of characters)

- ## ✝️ What if you could store a global state at typelevel in typescript.
- https://twitter.com/ecyrbedev/status/1686852448915189760
  - Thanks to interface and function overriding, you can
- I use this in all my tanstack libraries
  - coming to TanStack Query in v5
- http://viem.sh uses this. its a pretty cool feature

- ## What library do JS developers use to set/remove/update values in deeply nested objects and arrays?
- https://twitter.com/sgrove/status/1157375114490478592
  - lodash: setPath(data, ["user", "id"], userId); 
  - immer: updatePath(data, ["user", "greeting"], greeting => (greeting || "Hello, ") + userName; 

- If immutable, I use immer. Otherwise lodash.set/get
- ramda
- Immer. Or automerge if you need CRDT.

- ## 开发小建议：代码的switch case分支条件超过8个以上，switch case效率下降，不妨替换成map
- https://twitter.com/stephenzhang233/status/1660478131764080641
- map还有个好处，支持 fp 还可以 partial
- 直接多维数组
- 看语言支持不支持。Java我一般使用枚举来实现了。

- ## 如果希望能准确表示js小数和计算，那该怎么做？
- https://twitter.com/lewangdev/status/1657046362452819969
  - 前几天公司有位前端小哥发现一个奇怪的浮点数问题来问我：通过 MQTT 上传了温度 23.4，经过后台处理后存到数据库再读出来后却变成了 23.399999618530273
- 这不是基础中的基础么，搞前端的天天跟 JS 打交道，应该更敏感才对。
  - 最好的处理方法是，增加位数，**全程转换成整数处理**，只在展示的时候，恢复度量。
  - 比如，约定温度全部乘以10000，温度 23.4 视作 234000 ，后续经过数据处理（比如说取一段时间的平均值）得到了 225417 这个数，最终展示为 22.54 即可
- 数据库里只存integer , 读写时用getter 和 setter 指定小数点位置
- 温度的话应该直接四舍五入就可以了，如果是类似金额比较敏感的数据的话，就先乘100再存，读了之后再除100。
- 做工业控制系统的时候，在**传输的时候都是用整型**，只有最后显示才按照位数计算取整。
- 我们现在这类数据禁止使用浮点类型，全部使用整型➕标度
- 两个办法。
  - 第1种是保存在字符串，运算的时候使用 decimal.js 这样的工具类；
  - 第2种是乘以100（视情况而定）保存成整数，运算的时候使用整数运算。显示的时候 ( var1 / 100 ).toFixed(1)

- 前端用字符串，后端用bigdecimal

- IEEE 754，这不是 CS 常识嘛🤔
  - JS 用 string，Java 用 BigDecimal，MySQL 用 decimal，或者存两个 int precision+scale ，对精度没什么要求的话，直接 format 就好

- 我们一般是，前端/客户端不处理展示逻辑，一律后端返回字符串，设备原数据一律透传二进制，后续处理的内容所有字段都携带 meta，比如 前端/客户端 有命令下发逻辑需要使用。
- 直接乘以100
  - 那就需要 bignumber.js 了
- 非金融场景，就用浮点数就可以，然后输出的时候format格式化一下，保留N位有效数字。
  - 不必担心精度损失，在计算登月的时候，Pi只用单精度浮点数就够了。
  - 此外温度测量器的误差一般都在0.1度以上，所以显示这么多位数字是没有意义的，建议直接format成 20.1 就行
- 我们一般是，前端/客户端不处理展示逻辑，一律后端返回字符串，设备原数据一律透传二进制，后续处理的内容所有字段都携带 meta，比如 前端/客户端 有命令下发逻辑需要使用。

- ## 💡 JS private class fields considered harmful
- https://twitter.com/LeaVerou/status/1652053835094065153
  - [JS private class fields considered harmful](https://lea.verou.me/2023/04/private-fields-considered-harmful/)
  - a very sad realization: instances of classes that use private fields cannot be proxied.
- Vue 1 and 2 used accessors for reactivity. The problem is this approach was more fragile, many operations were not detected, one could not add new reactive properties without using special syntax etc.
  - When implementing @mavoweb ’s reactivity system I briefly considered accessors but ruled them out for that reason and went for proxies even though they were brand new at the time and nobody was using them for that yet. They just seemed like the obvious tool for the job.

- I'm not sure reactive frameworks should be really using proxies. They're enticing(诱人的；有吸引力的), but have these problems, as well as known issues of you access objects outside the proxies.
- What should they be using?
  - FAST uses decorators to generate getter/setter pairs on classes. It also has APIs to convert plain objects into reactive objects. The whole system is signals-based and has low-level APIs for creating your own types that integrate into the reactive system.
  - When I was first designing FAST's reactivity system, I considered various options for the implementation, including proxies. In the end, I decided it wasn't the right way to go, based on some of the issues above, and a few other practical challenges I encountered along the way.
  - One thing I would like to investigate is using proxies to create better reactive collections. Today, we patch Array to track splice operations, and use that for observation. But we could use a proxy that looks like an Array to do that.
  - A proxy-based collection would enable tracking changes through the index, which isn't possible today on a standard array. It might also enable other possibilities more easily, such as invalidating the results of map/filter/reduce operations when the original array changes.

- The problem is libraries / frameworks using proxies in a way that changes the `this` object seen by the proxied object. It's impossible to trap identity comparison. So these proxy usages are not transparent and incompatible with code relying on `this` identity.
  - TLDR is that frameworks like Vue use proxies to interfere with a target object's internal implementation, i.e. it's trying to break encapsulation. The target object should instead opt into the reactivity / observability mechanism, or accept to only support external observability.

- `WeakMap` + property object might help a bit as a suitable alt
- `Symbol`s work well too as private field identifiers. They are impossible to duplicate without access to the original, making such fields fairly well protected, but not truly private.

- For a while, there were the Object.observe and Array.observe proposals. Those were abandoned, I think mostly due to the champion's loss of interest.
  - My understanding is that it wasn't lack of interest but pushback from implementors because Object.observe() and friends could not be implemented performantly.

- https://github.com/deebloo/observable-stage3-decorators
  - Demonstrates a technique for monitoring property changes on a class instance using stage 3 decorators. 
  - This should work with both plain classes and with custom elements. 
  - It is important that this does not require subclassing.

- ## [Suggestion: avoid `delete` keyword](https://github.com/ianstormtaylor/slate/issues/4425)
  - we could look at swapping set_node to do node[key] = undefined and improve performance instead of using delete node[key].
- While this was once true (delete being slow), I think there's sufficient evidence that it's no longer a primary issue
- I'm not 100% convinced but you're right performance characteristics can change.

- ## 💡 The number of times I see this makes me want to cry: `element.addEventListener("click", (e) => handleClick(e))` .
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

- ### [如何实现准时的setTimeout](https://mp.weixin.qq.com/s/ENU93_jSUaAONCkfTQTK-Q)
- while: 想得到准确的，我们第一反应就是如果我们能够主动去触发，获取到最开始的时间，以及不断去轮询当前时间，如果差值是预期的时间，那么这个定时器肯定是准确的，那么用 while 可以实现这个功能。
  - Web Worker为Web内容在后台线程中运行脚本提供了一种简单的方法。线程可以执行任务而不干扰用户界面。
  - 在 worker 中写入一个 while 循环，当达到我们的预取时间的时候，再向主线程发送一个完成事件，就不会因为主线程的其他代码的干扰而造成数据不准的情况。
- requestAnimationFrame() 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。
  - 该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行，回调函数执行次数通常是每秒60次，也就是每16.7ms 执行一次，但是并不一定保证为 16.7 ms。
  - 可以尝试一下将它来模拟 setTimeout
  - setTimeout 系统时间补偿
  - 当每一次定时器执行时后，都去获取系统的时间来进行修正，虽然每次运行可能会有误差，但是通过系统时间对每次运行的修复，能够让后面每一次时间都得到一个补偿。

- ## 💡 I'm not a fan of premature optimisation but if you know a structure is going to be created *a lot* you're probably better off with a class over a factory function.
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
