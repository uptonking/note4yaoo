---
title: lib-pattern-rxjs-faq
tags: [faq, lib, pattern, rxjs]
created: '2020-12-14T14:41:15.362Z'
modified: '2020-12-14T14:42:11.433Z'
---

# lib-pattern-rxjs-faq

## faq-not-yet

### rxjs架构调试困难，如何调试

## faq-repeat

### 如何优化性能，对于rxjs架构的程序

### rxjs的引入，对程序的性能影响如何

### [What are real world examples of RxJS?](https://stackoverflow.com/questions/56311808/what-are-real-world-examples-of-rxjs)

- You use Rx when you need to track a value of a variable over time. 
  - If you just `var x = getVariableValue()` somewhere, and that function return changes after a minute, the `x` will still be the old value. 
  - If you need `x` to change when the return of the method changes, you use Rx to subscribe to all changes. 
  - Otherwise you would have to `setInterval(() => { var x = getVariableValue(); }, 1000)` or something, which is hacky and not very maintainable.
  - Rx doesn't replace VanillaJS, it replaces vanilla variables. 
  - Variables, instead of one value at the time, become infinite values over time
  - a chat is a perfect example. But there are simpler ones

- If you want to poll an API for example you can use RxJS.
- Autocomplete feature can be made using rxjs. 
- Pub Sub pattern in general can be applied very well in front end as there are many events (publisher) which various subscribers can subscribe to. 
  - For example multiple clicks can be listened by different subscribes and take some action accordingly. 
- Managing API calls. 
  - You can do very well with RxJS. 
  - From the result you may want to filter some data, may want to map that data etc.

- RxJS observables are often used for HTTP Requests and another common application is in combination with WebSockets where you get an asynchronous steam of data.

- RXJS is very often used in combination with state management.

- [Why Angular uses Observable for HttpClient?](https://stackoverflow.com/questions/50495701/why-angular-uses-observable-for-httpclient)
- On top of my head:
  - Retry
  - Cancel
  - Enjoy all the Rxjs operators
  - Possibility to combine them as streams
  - Thinking reactively in your whole app
  - Consistency
  - Observables are cold by nature, no need to wrap them like Promises into a factory function if you want to trigger it later

- By making Http requests observables, the Angular team is making async operations in the core consistent with everything elsewhere.
  - Observables are the standard async handlers in the Angular framework.
  - By standard, I mean that observables are supported by the async pipe, routing guards, routing resolvers, component event emitters and many other places.
  - The Angular team has put in a lot of effort to support promises as a fallback for a lot of those features, but under the hood those promises are just converted to observables anyway.
- There are still some advantages of observables over promises, but this is primarily opinionated
  - You can easily mix between Http requests and WebSockets in a service and expose the APIs as observables. 
    - The consumer of the service will not know the difference.
  - You can easily convert a Http request for an array into an observable that emits each item individually. 
    - This makes dispatching data to different consumers a lot easier.
  - Promises can break when they are not chained properly. 
    - These common bugs are often avoided with observables.

- To maintain API consistency. No need to introduce Promises
  - Observables are more flexible than Promises anyway. 
  - Moreover observable can track its subscribers. 
  - In case of HttpClient call is made once subscribear appear.
  -  If you dont subscribe to http call, request will not be made.
  -  That is why if you subscribe multiple times to 1 observable, multiple request will be made.

- ref
  - [Should I always use Observables where a promise can be used?](https://stackoverflow.com/questions/58319625/should-i-always-use-observables-where-a-promise-can-be-used)
    - Using a single async style is more consistent that a mix and match style and it also lets you refactor at a later date when your http request becomes a stream.

## faq

 

### [Mobx 与 rxjs 在用法和本质上有何异同?](https://www.zhihu.com/question/283589041)

- 相同的地方大概就是用到了观察者模式，不同的地方是很多的。
- 首先Mobx主要作用是做状态管理，给框架做model层，
  - RxJS属于Rx的Js实现，用途更为广泛，但凡事件驱动的程序，都可以用Rx的思维进行优雅的开发，两者都很好的解决了异步编程这个难题。
  - 但RxJs不仅局限于异步编程，更加可以结合同步，并行等各种复杂场景的开发。如果结合webworker等，就能实现多线程编程。

- [Mobx vs Reactive Stream Libraries (RxJS, Bacon, etc)](https://github.com/mobxjs/mobx/wiki/Mobx-vs-Reactive-Stream-Libraries-(RxJS, -Bacon, -etc))
- MobX is a battle tested library that makes state management simple and scalable by transparently applying functional reactive programming(TFRP).
- First, it is important to realize that stream libraries, although similar, solve a different problem than Mobx. 
  - These are not competing, but rather complementing concepts. 
  - For example, RxJS helps you react to events while MobX will help you react to values (the state). 
  - As Andre Staltz argued and proved with Cycle.js, events and state are actually interchangeable.
- In MobX you hardly have operators, as stuff is normally combined through normal javascript constructions.
  - In RxJS you need to do this using combineLatest or any other operator.
  - MobX will automatically stop listening to observables that are not actively in use.
  - MobX has first class support for efficiently working with complex data structures like objects, arrays and maps.
- So, in summary, when should you use stream libraries over MobX? 
  - Answer: when time or history plays an important role.
  - if you can derive it from the state you have now, transparent reactive programming is a lot easier and more consistent due to the transparent tracking and support for complex object models. 
    - You don't have to learn operators and dependencies are tracked automatically.
  - But if time plays an important role, like when throttling, accumulating events or having complex join patterns like zip, these are the cases where you want to work with streams.
- MobX suffices and is easier and more efficient in 90% of the cases; 
  - where you want to derive something consistently from the latest state. 
- But for the other 10% of use cases, reactive stream libraries really shine. 
  - This is usually when I/O plays an important role.
- there are cases when these two concepts can combine together really nicely.
  - For example, if you want to throttle the user input before updating the state and the rest of the app. 
  - You could accomplish this with a workflow like this:
  - `DOM events -> RxJS -> Update state -> MobX -> Update UI`

- [Does MobX Observables have anything to do with RxJS ones?](https://stackoverflow.com/questions/53707860/does-mobx-observables-have-anything-to-do-with-rxjs-ones)
- From what I see in the MobX source code, there aren't many overlaps. 
  - Neither of them uses each other or has a common dependency with the other.
- The interpretation of Observable in MobX 
  - seems to be that objects, arrays, maps, etc. are wrapped with a Proxy object to track and be notified on property changes. 
  - This is used for communicating state changes through the application while changing relatively little to the vanilla javascript types ("transparent"). 
  - While these types may be observable (as in the verb), they are not an implementation of Observables defined by ReactiveX.
- RxJS 
  - provides a completely new, some would say huge, API that is used to modify so-called "notifications" generated by abstract Observable types that don't necessarily represent vanilla javascript types. 
  - Instead of directly changing objects imperatively, a "LINQ-ish" language, made up of pipeable operators, is used to express execution flows. 
  - In many ways, RxJS can be seen as an language extension for JavaScript to enable Reactive programming as defined in the Observable contract.

### [Will callback architecture from Andre be adopted to RxJS? What's difference between each RxJS architecture?_202011](https://twitter.com/BenLesh/status/1328449063910596613)

- At this point, I think it's unlikely. 
- One of the goals of using that architecture was to get the library to be smaller. 
- There was also another experimental branch where we used a "mutable subscriber" approach that had even more size benefits
- however, since then, we've been able to refactor the existing architecture to make the operators much, much smaller, and easier to maintain, 
  - to the point where the size benefits to the rxjs callbag architecture aren't as good (in fact, it might be larger)
- The rxjs callbag architecture was further troubled by the fact it made the barrier to entry for writing a custom operator or maintaining the library MUCH higher than it was, as it was harder to follow/read.
- The barrier is now lower in 7.x.
- All of that said, I still think that @andrestaltz has a brilliant idea with callbags, 
  - and I wouldn't rule out(排除；阻止) the architecture or supporting callbags in some way
  - but at the moment we're not headed that direction.
- Interop via fromObservable/toObservable is good enough
