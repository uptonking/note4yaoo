---
title: lib-pattern-rxjs-faq
tags: [faq, lib, pattern, rxjs]
created: '2020-12-14T14:41:15.362Z'
modified: '2020-12-14T14:42:11.433Z'
---

# lib-pattern-rxjs-faq

## faq-not-yet

### rxjs架构调试困难，如何调试

- [HOW TO DEBUG RXJS CODE_201512](https://staltz.com/how-to-debug-rxjs-code.html)
  - The short answer is: you have to depend mostly on drawing diagrams on paper and adding `.do(x => console.log(x))` after operators, 
  - there are 3 techniques you can use today to debug RxJS:
    - Adding `.do(x => console.log(x))` to trace to the console
    - Drawing a dependency graph and following the flow
    - Drawing a marble diagram
  - The goal of debugging is simply to help you get an accurate mental model of the execution of your code. 
  - This is the most rudimentary(基本的；根本的) technique: to just “console.log” events happening on the streams.
  - We can add `.do(x => console.log(x))` between operators

- [How to debug rxjs5?](https://stackoverflow.com/questions/38590346/how-to-debug-rxjs5)
  - Ultimately, any kind of async programming is going to be harder to debug. 
  - a quick search will reveal plenty of debugging concerns for redux-saga too.
  - It turns out that redux-thunk is the best solution for a vast majority of applications built because a majority of them do not have complex side effect concerns that justify(使齐行) something like redux-observable or redux-saga. 

## faq-repeat

### 如何优化性能，对于rxjs架构的程序

- [RxJS: Don't Unsubscribe](https://medium.com/@benlesh/rxjs-dont-unsubscribe-6753ed4fda87)
  - [[译] RxJS: 别取消订阅](https://zhuanlan.zhihu.com/p/27903919)
  - 不要过多地使用取消订阅操作
    - 如果在程序中出现过多的订阅对象，那就意味着你命令式地管理了你的 subscriptions ，并且没有利用Rx的强大之处
  - 你应该尽可能的使用像 `takeUntil` 这样的操作符来管理你的 RxJS subscriptions 。
  - 作为经验法则，如果你在一个组件中管理发现2个或2个以上的subscriptions，你应该问自己是否能将它们组合的更好。

- [Observables and performance](https://www.reddit.com/r/Angular2/comments/avpag5/observables_and_performance/)
  - General purpose libraries are not meant to be efficient at run-time. 
    - From my own experience when you need high frame rate, you just dump(扔掉；抛弃) all these nice tools and make your own, profiling every line of code. 
    - A few tips
      - don't create objects, don't create other things in run-time (lambdas), make everything as static as possible, use only primitives whenever possible. 
      - And don't use Angular, lol.
  - Use rx-spy to see if you have a subscription leak somewhere. 
    - For example, if your component has a getter that returns an observable, and you bind to that getter in your html with the async pipe, you're gonna have a bad time.
    - Try to use an OnPush change detection strategy everywhere possible
    - if you are smart about how your app handles change detection, you'll be able to do a lot more with very minimal performance issues. Updating the DOM is expensive.
    - Consider looking into web workers if your app is doing anything computationally expensive.
  - I'm not an expert by any means on animation but with games there's generally what's called a game loop. A constantly running update -> draw cycle. 
    - For web that's typically done with the requestAnimationFrame function. 
    - You schedule work for each frame at a more optimal time for the browser. 
    - Without rxjs, normally you invoke rAF manually to start the loop and at the end of your draw logic, you call rAF again and start the loop.
    - With rxjs there's a concept of schedulers, one of which is for animation frames. 
    - I'd imagine you could use this to create a stream of frames, on each from frame, get the latest value from your store and update if necessary.
    - This is all guesswork on my part but hopefully it leads you down a path to the right answer.

- ref
  - [RxJS best practices in Angular](https://blog.strongbrew.io/rxjs-best-practices-in-angular/)
    - The first best practice is the use of pipeable operators.
    - Avoiding nested subscribes
    - A Subject is both a hot observable and an observer at the same time. 
      - Only use them when really needed, for instance:
        - When mocking streams in tests
        - When we want to create streams from outputs in Angular
        - When handling circular references
      - For most other cases an operator or Observable.create might be enough.
      - A BehaviorSubject is commonly used because it has a getValue() function.

### rxjs的引入，对程序的性能影响如何

- I won't choose RxJs for performance reason because any library will add overheads. 
  - However it can boost your productivity if you use it correctly. 

### Cold vs Hot Observables

- Cold observables start running upon subscription, 
  - i.e., the observable sequence only starts pushing values to the observers when Subscribe is called
  - Values are also not shared among subscribers. T
- hot observables such as mouse move events or stock tickers 
  - which are already producing values even before a subscription is active. 
  - When an observer subscribes to a hot observable sequence, it will get all values in the stream that are emitted after it subscribes. 
  - The hot observable sequence is shared among all subscribers, and each subscriber is pushed the next value in the sequence
- Analogies
  - Cold Observables: movies.
  - Hot Observables: live performances.
  - Hot Observables replayed: live performances recorded on video.

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

 

### `ajax()` vs `fromFetch()`

- fromFetch is only a thin wrapper around fetch() and accepts the same options, instead of the ajax wrapper around xhr.
- This would allow us to polyfill fetch() in tests and reuse requestGraphQL functions instead of having to use a full JSDOM environment, with emulated CORS restrictions etc

### [Why to use observables instead of Ajax?](https://stackoverflow.com/questions/47571880/why-to-use-observables-instead-of-ajax)

``` JS
// use observable
this.http.get("MyURL")
  .subscribe(
    (_url: any) => {
      //TODO My job
    },
    (error: any) => {
      //TODO My job
    },
    () => {
      //TODO My job
    });

// use ajax
$.ajax({
  url: "MyURL",
  success: function(result) {
    //TODO My job
  },
  error: function() {
    //TODO My job
  }
});
```

- TLDR
  - You can write cleaner asynchronous code and do more things with less code.
- I have had the same question when I started with angular, 
  - but after working with angular for over a year and having worked a lot with observables and rxjs over that period of time
  - I have learned the following
    - You cannot cancel promises
    - Native promises have 2 methods, rxjs has many more operators

- different usage
  - Observables (which generally refer to the "RxJS" library, though not always) generally have a `subscribe()` method which lets them listen for changes, 
    - and have hooks for onNext() , onError(), and onComplete()
  - jQuery's AJAX syntax is a more "classic" callback structure, 
    - where you call the function and provide it with callbacks directly. 
    - It also has another syntax which allows you to add them as subsequent functions (.done() and the like).
  - nowadays I would argue that the Promise syntax is the most popular
    - `fetch()` is a native implementation of doing AJAX requests with Promise syntax.
  - Out of the three, only the Promise one has any real advantage, which is that it is natively supported by modern browsers (whereas the other two require a third-party library). 
    - But if you're already using a third-party library for something else, that's not a huge benefit.

- Observables vs Promises
  - Observables can define both the setup and teardown aspects of asynchronous behavior.
  - Observables are cancellable.
  - Observables can be retried using one of the retry operators provided by the API, such as `retry` and `retryWhen`.
    - Promises require the caller to have access to the original function that returned the promise in order to have a retry capability.

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
