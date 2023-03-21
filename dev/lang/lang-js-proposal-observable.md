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

- ### Signals vs. Observables?
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
  - https://github.com/vobyjs/oby
    - A tiny Observable implementation

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
