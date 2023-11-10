---
title: lang-js-proposal-observable
tags: [js, lang, observer, pattern, proposal]
created: 2020-12-14T11:27:40.522Z
modified: 2020-12-14T11:29:00.678Z
---

# lang-js-proposal-observable

# guide

# blogs

## [Signals vs. Observables, what's all the fuss about?](https://www.builder.io/blog/signals-vs-observables)

- ### Want to know what all the fuss is about Signals vs. Observables?
- https://twitter.com/mhevery/status/1637911322745802752
- Signals are values in the bucket that can be accessed synchronously.
  - Observables are values delivered over time asynchronously through a callback.
- The concept of "time' is critical to observables. Observables are values delivered over time (or events over time.)
  - This implies that observables can't be read synchronously and have no "current" value. This makes observable a "push" model.
  - (Think browser events.)
- Signals have no concept of "time." It is just a current value in a bucket.
  - The signal's value can be accessed synchronously through a getter. This makes them pull-based. (no callback required.)
- Observables require explicit subscriptions.
  - Signal subscriptions are created automatically when your code reads the signal's value. (no unsubscribe required.)
  - It also means that as the code runs, the reactivity graph of signals can change and so it is highly dynamic.

- It is a spectrum:
  - Values have no reactivity.
  - Observable can express things that can't be expressed in Signals at the expense of more complex API.
  - Signals are a happy medium where API is simple and good enough for most things UI.
# es-observable
- Given the extensive prior art in this area, there exists a public "Observable Contract".
  - [ReactiveX - The Observable Contract](https://reactivex.io/documentation/contract.html)
- many JavaScript APIs been trying to adhere to the contract defined by the TC39 proposal from 2015
  - there is a library, symbol-observable, that ponyfills (polyfills) Symbol.observable to help with interoperability between observable types that adheres to exactly the interface defined here
  - This is similar to how Promises/A+ specification that was developed before Promises were adopted into ES2015 as a first-class language primitive.

- https://github.com/tc39/proposal-observable

- This proposal introduces an `Observable` type to the ECMAScript standard library. 
- The `Observable` type can be used to model push-based data sources such as DOM events, timer intervals, and sockets.
- observables are:
  - Compositional: Observables can be composed with higher-order combinators.
  - Lazy: Observables do not start emitting data until an observer has subscribed.
- The Observable type represents one of the fundamental protocols for processing asynchronous streams of data.
  - It is particularly effective at modeling streams of data which originate from the environment and are pushed into the application, such as user interface events.
  - By offering Observable as a component of the ECMAScript standard library, we allow platforms and applications to share a common push-based stream protocol.

- An Observable represents a sequence of values which may be observed.
- An Observer is used to receive data from an Observable, and is supplied as an argument to subscribe.

- `Observable.of` creates an Observable of the values provided as arguments. 
  - The values are delivered synchronously when subscribe is called.
- `Observable.from` converts its argument to an Observable.
  - If the argument has a `Symbol.observable` method, then it returns the result of invoking that method. 
  - Otherwise, the argument is assumed to be an iterable and the iteration values are delivered synchronously when subscribe is called.
- `SubscriptionObserver` is a normalized Observer which wraps the observer object supplied to subscribe.

- Implementations
  - rxjs
  - core-js

- Example: Observing Keyboard Events

```JS
// create a function which returns an observable stream of events
function listen(element, eventName) {
  return new Observable(observer => {
    // Create an event handler which sends data to the sink
    let handler = event => observer.next(event);

    // Attach the event handler
    element.addEventListener(eventName, handler, true);

    // Return a cleanup function which will cancel the event stream
    return () => {
      // Detach the event handler from the element
      element.removeEventListener(eventName, handler, true);
    };
  });
}

function commandKeys(element) {
  let keyCommands = { "38": "up", "40": "down" };

  return listen(element, "keydown")
    .filter(event => event.keyCode in keyCommands)
    .map(event => keyCommands[event.keyCode])
}

// to consume the event stream, we subscribe with an observer.
let subscription = commandKeys(inputElement).subscribe({
  next(val) { console.log("Received key command: " + val) },
  error(err) { console.log("Received an error: " + err) },
  complete() { console.log("Stream complete") },
});
```

## dom-observable

- https://github.com/domfarolino/observable

- Observables were first proposed to the platform in TC39 in May of 2015. 
  - The proposal failed to gain traction, in part due to some opposition that the API was suitable to be a language-level primitive. 
  - Despite ample developer demand, lots of discussion, and no strong objectors, the DOM Observables proposal sat mostly still for several years (with some flux in the API design) due to a lack of implementer prioritization.

- This is the explainer for the Observable API proposal for more ergonomic and composable event handling.

- This proposal adds an `.on()` method to `EventTarget` that becomes a better `addEventListener()`
- Observables turn event handling, filtering, and termination, into an explicit, declarative flow that's easier to understand and compose than today's imperative version, which often requires nested calls to addEventListener() and hard-to-follow callback chains.

- Observables are first-class objects representing composable, repeated events. 
  - They're like Promises but for multiple events, and specifically with EventTarget integration, 
  - they are to events what Promises are to callbacks. 
- We propose the following operators in addition to the Observable interface

- 
- 
- 
- 

# observable-impl
- https://github.com/vobyjs/oby
  - A tiny Observable implementation
# discuss
- ## 

- ## Every lib has to write its own implementation of observables because it’s such an important and ubiquitous concept. 
- https://twitter.com/lexswed/status/1685027901031256064
  - So why not build it into the language so all these libraries can simply use the built in one instead of rolling their own

- Please, no! To handle observables nicely, you need a lot of operators. All this world of specific semantics doesn't worth it. I wrote a lot of comparisons, and most of the code could be written imperatively and be pretty readable.

- I appreciate you really believe in them. I’m concerned about anti-patterns I’ve seen:
  - Merging two observables requires time assumption hacks
  - Cold vs hot observables are invisible until runtime
  - One observable subscriber writing to another subject creates stateful spaghetti

- Please don't make subscription cause repeated side effects. The mess in rxjs where subscribing initiates the action and then having all the operators to stop that (like replay) is pretty horrible. Promises got this right.

- ## [Java Spring WebFlux vs RxJava - Stack Overflow](https://stackoverflow.com/questions/56461260/java-spring-webflux-vs-rxjava)
- Just like object-oriented programming, functional programming, or procedural programming, reactive programming is another programming paradigm.

- RxJava 2.0 and Reactor are based on ReactiveX project. 
  - 👉🏻 And **Spring WebFlux uses Reactor internally**.
- Since Project Reactor you can consider it fix the drawbacks in RxJava and more suitable for Backend development. 

- Both Spring WebFlux (project-reactor) and RxJava2+ are implementation of reactive-streams.

- ReactiveX is a combination of the best ideas from the Observer pattern, the Iterator pattern, and functional programming. It extends the observer pattern to support sequences of data and/or events and adds operators that allow you to compose sequences together declaratively while abstracting away concerns about things like low-level threading, synchronization, thread-safety, concurrent data structures, and non-blocking I/O.

- ## I'm working to bring Observables to the web platform by reviving a @thedomstandard  proposal that got some attention a while ago.
- https://twitter.com/RyanCarniato/status/1686069829172912129

- I think this is interesting. By boiling down observables to basically standalone primitives (like Array, Map, Set) makes them way more approachable than with operators. But with enough functionality to be useful on their own without RxJS (not that you couldn't use this with it)

- Understanding Signals and Observables are completely different, almost all Signal libraries have interop for them. This is the level of base functionality I'd want. It removes the feeling of introducing a second reactive system. It pushes RxJS back to where it is most natural.
  - What's the ideal use case for RxJS? I may have never stumbled on a scenario where using RxJS-style Observables was a good idea, I think 🤔 Which doesn't mean these scenarios don't exist of course.
- It is a good solution for Observables. But like has nothing to do with Signals which have a ton of other unrelated functionality. We don't really get any benefit here. 👉🏻 I used Observables at the start of Solid and realized they weren't the right fit.

- I think Observables are better off as a library than get included in DOM (what I mean is I hate maintaining Observable infested code, which will multiply if it becomes part of DOM)

- ## A non-RxJS observable in the wild! @solid_js edition!!
- https://twitter.com/BenLesh/status/1666517010354675712
  - https://github.com/solidjs/solid/blob/main/packages/solid/src/reactive/observable.ts
  - [signals are the most primitive of the Observables in Solid, and resemble BehaviorSubjects in RxJS](https://github.com/solidjs/solid/blob/b99587cd8be8b26a92d0ae89d3c46e62effebe48/documentation/observables.md#signals)
- Curious on what angular’s version looks like
  - It's similar

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
