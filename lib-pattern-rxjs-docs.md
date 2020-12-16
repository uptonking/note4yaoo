---
title: lib-pattern-rxjs-docs
tags: [docs, lib, pattern, rxjs]
created: '2020-12-14T11:22:08.779Z'
modified: '2020-12-14T11:22:48.700Z'
---

# lib-pattern-rxjs-docs

- A reactive programming library for JavaScript

## guide

- Goals
  - Provide better performance than preceding versions of RxJS
  - To model/follow the [Observable Spec Proposal](https://github.com/zenparsing/es-observable)
    - This proposal introduces an `Observable` type to the ECMAScript standard library.
  - Provide more debuggable call stacks than preceding versions of RxJS

## Overview

- RxJS is a library for composing asynchronous and event-based programs by using observable sequences.
- It provides one core type, the Observable, satellite types (Observer, Schedulers, Subjects) 
  - and operators inspired by Array#extras (map, filter, reduce, every, etc) to allow handling asynchronous events as collections.
- Think of RxJS as Lodash for events.
- ReactiveX combines the Observer pattern with the Iterator pattern and functional programming with collections to fill the need for an ideal way of managing sequences of events.

- The essential concepts in RxJS which solve async event management are:
- Observable
  - represents the idea of an **invokable collection of future values or events**.
  - represents a sequence of values which may be observed.
- Observer
  - It is a **collection of callbacks** that knows how to listen to values delivered by the Observable.
  - An Observer is a consumer of values delivered by an Observable. 
- Subscription
  - represents the **execution of an Observable**, is primarily useful for cancelling the execution.
  - Subscribing to an Observable is analogous to calling a Function.
  - Subscribing to an Observable is like calling a function, providing callbacks where the data will be delivered to.
  - When you subscribe, you get back a Subscription, which represents the ongoing execution. 
- Subject
  - is the **equivalent to an EventEmitter**, and the only way of multicasting a value or event to multiple Observers.
- Operators
  - are **pure functions** that enable a functional programming style of dealing with collections with operations like map, filter, concat, reduce, etc.
- Schedulers
  - are **centralized dispatchers to control concurrency**, allowing us to coordinate when computation happens on e.g. `setTimeout` or `requestAnimationFrame` or others.

- What makes RxJS powerful is its ability to produce values using pure functions. 
  - That means your code is less prone to errors.
- RxJS has a whole range of operators that helps you control how the events flow through your observables.
- You can transform the values passed through your observables.

## Observables

- Observables are lazy Push collections of multiple values.

| title  | single   | multiple |
|--------|-----------|-----------|
| pull   | Function(fetch)   | Iterator |
| push   | Promise           | Observable |

- **pull vs push**
- Pull and Push are two different protocols that describe how a data Producer can communicate with a data Consumer.
- In Pull systems, the Consumer determines when it receives data from the data Producer. 
  - The Producer itself is unaware of when the data will be delivered to the Consumer.
  - Every JavaScript Function is a Pull system. 
  - The function is a Producer of data, and the code that calls the function is consuming it by "pulling" out a single return value from its call.
  - ES2015 introduced generator functions and iterators (`function*`), another type of Pull system.
    - Code that calls iterator.next() is the Consumer, "pulling" out multiple values from the iterator (the Producer).

- In Push systems, the Producer determines when to send data to the Consumer. 
  - The Consumer is unaware of when it will receive that data.
  - Promises are the most common type of Push system in JavaScript today. 
    - A Promise (the Producer) delivers a resolved value to registered callbacks (the Consumers), 
    - but unlike functions, it is the Promise which is in charge of determining precisely when that value is "pushed" to the callbacks.
  - RxJS introduces Observables, a new Push system for JavaScript. 
    - An Observable is a Producer of multiple values, "pushing" them to Observers (Consumers).

- A Function is a lazily evaluated computation that synchronously returns a single value on invocation.
- A generator is a lazily evaluated computation that synchronously returns zero to (potentially) infinite values on iteration.
- A Promise is a computation that may (or may not) eventually return a single value.
- An Observable is a lazily evaluated computation that can synchronously or asynchronously return zero to (potentially) infinite values from the time it's invoked onwards.

- Observables are not like EventEmitters nor are they like Promises for multiple values. 
  - Observables may act like EventEmitters in some cases, namely when they are multicasted using RxJS Subjects, but usually they don't act like EventEmitters.
  - Observables are like functions with zero arguments, but generalize those to allow multiple values.

``` JS
function foo() {
  console.log('Hello');
  return 42;
}
const x = foo.call(); // same as foo()
console.log(x);
const y = foo.call(); // same as foo()
console.log(y);

// 上下两段代码都会打印出
// "Hello"
// 42
// "Hello"
// 42

const foo = new Observable(subscriber => {
  console.log('Hello');
  subscriber.next(42);
});

foo.subscribe(x => {
  console.log(x);
});
foo.subscribe(y => {
  console.log(y);
});
```

- both functions and Observables are lazy computations
  - If you don't call the function, the `console.log('Hello')` won't happen. 
  - Also with Observables, if you don't "call" it (with `subscribe`), the `console.log('Hello')` won't happen. 
- Plus, "calling" or "subscribing" is an isolated operation
  - two function calls trigger two separate side effects, 
  - and two Observable subscribes trigger two separate side effects.
- As opposed to EventEmitters which share the side effects and have eager execution regardless of the existence of subscribers, Observables have no shared execution and are lazy.

- Some people claim that Observables are asynchronous.
  - That is not true. 
  - Which proves the subscription of `foo` was entirely synchronous, just like a function.
  - **Observables are able to deliver values either synchronously or asynchronously.**

- What is the difference between an Observable and a function? 
  - `func.call()` means "give me one value synchronously"
  - `observable.subscribe()` means "give me any amount of values, either synchronously or asynchronously"
  - Observables can "return" multiple values over time, something which functions cannot. 
  - you can also "return" values asynchronously

- Observables are created using `new Observable` or a creation operator, 
  - are `subscribe`d to with an Observer, 
  - execute to deliver `next/error/complete` notifications to the Observer, 
  - and their execution may be disposed. 
  - These four aspects are all encoded in an Observable instance, 
  - but some of these aspects are related to other types, like Observer and Subscription.

- **Creating Observables**

``` JS
import { Observable } from 'rxjs';

const observable = new Observable(function subscribe(subscriber) {
  const id = setInterval(() => {
    subscriber.next('hi')
  }, 1000);
});
```

- The `Observable` constructor takes one argument: the `subscribe` function.
- Observables can be created with `new Observable`. 
- Most commonly, observables are created using creation functions, like `of/from/interval`, etc.

- **Subscribing to Observables**

``` JS
observable.subscribe(x => console.log(x));
```

- It is not a coincidence that `observable.subscribe` and `subscribe` in `new Observable(function subscribe(subscriber) {...})` have the same name. 
  - In the library, they are different, 
  - but for practical purposes you can consider them conceptually equal.
- This shows how `subscribe` calls are not shared among multiple Observers of the same Observable.
  - When calling `observable.subscribe` with an Observer, the function `subscribe` in `new Observable(function subscribe(subscriber) {...})` is run for that given subscriber. 
  - Each call to `observable.subscribe` triggers its own independent setup for that given subscriber.
- Subscribing to an Observable is like calling a function, providing callbacks where the data will be delivered to.
  - This is drastically different to event handler APIs like `addEventListener`/`removeEventListener`. 
  - With `observable.subscribe`, the given Observer is not registered as a listener in the Observable. 
  - **The Observable does not even maintain a list of attached Observers**.
- A `subscribe` call is simply a way to start an "Observable execution" and deliver values or events to an Observer of that execution.

- **Executing Observables**

- The code inside `new Observable(function subscribe(subscriber) {...})` represents an "Observable execution", a lazy computation that only happens for each Observer that subscribes. 
- The execution produces multiple values over time, either synchronously or asynchronously.
- There are three types of values an Observable Execution can deliver:
  - "Next" notification: sends a value such as a Number, a String, an Object, etc.
  - "Error" notification: sends a JavaScript Error or exception.
  - "Complete" notification: does not send a value.
- "Next" notifications are the most important and most common type
  - they represent actual data being delivered to an subscriber.
  - "Error" and "Complete" notifications may happen only once during the Observable Execution, and there can only be either one of them.
- These constraints are expressed best in the so-called Observable Grammar or Contract 
  - `next*(error|complete)?`
  - In an Observable Execution, zero to infinite Next notifications may be delivered. 
  - If either an Error or Complete notification is delivered, then nothing else can be delivered afterwards.
- It is a good idea to wrap any code in subscribe with `try/catch` block that will deliver an Error notification if it catches an exception

- **Disposing Observable Executions**

``` JS
import { from } from 'rxjs';

const observable = from([10, 20, 30]);
const subscription = observable.subscribe(x => console.log(x));
// Later:
subscription.unsubscribe();
```

- Because Observable Executions may be infinite, and it's common for an Observer to want to abort execution in finite time
- Since each execution is exclusive(专有的；独有的) to one Observer only, 
  - once the Observer is done receiving values, it has to have a way to stop the execution, in order to avoid wasting computation power or memory resources.
- When `observable.subscribe` is called, the Observer gets attached to the newly created Observable execution. 
  - This call also returns an object, the Subscription
  - The Subscription represents the ongoing execution, and has a minimal API which allows you to cancel that execution.
  - With `subscription.unsubscribe()` you can cancel the ongoing execution
- When you subscribe, you get back a Subscription, which represents the ongoing execution. 
  - Just call unsubscribe() to cancel the execution.

- Each Observable must define how to dispose resources of that execution when we create the Observable using `create()`. 
  - You can do that by returning a custom unsubscribe function from within `function subscribe()`.

- we remove the ReactiveX types surrounding these concepts

``` JS
function subscribe(subscriber) {
  const intervalId = setInterval(() => {
    subscriber.next('hi');
  }, 1000);

  return function unsubscribe() {
    clearInterval(intervalId);
  };
}

const unsubscribe = subscribe({ next: (x) => console.log(x) });

// Later:
unsubscribe(); // dispose the resources
```

- The reason why we use Rx types like Observable, Observer, and Subscription is to get safety (such as the Observable Contract) and composability with Operators.

## Observer

- An Observer is a consumer of values delivered by an Observable.
- Observers are simply a set of callbacks, one for each type of notification delivered by the Observable: `next/error/complete`.

``` JS
const observer = {
  next: x => console.log('Observer got a next value: ' + x),
  error: err => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};

observable.subscribe(observer);

// 也可以由rxjs框架自动创建observer对象，注意顺序
observable.subscribe(
  x => console.log('Observer got a next value: ' + x),
  err => console.error('Observer got an error: ' + err),
  () => console.log('Observer got a complete notification')
);
```

- Observers are just objects with three callbacks, one for each type of notification that an Observable may deliver.
- Observers in RxJS may also be partial. 
  - If you don't provide one of the callbacks, the execution of the Observable will still happen normally, 
  - except some types of notifications will be ignored, because they don't have a corresponding callback in the Observer.
- When subscribing to an Observable, you may also just provide the callbacks as arguments, without being attached to an Observer object
  - Internally in `observable.subscribe`, it will create an Observer object using the first callback argument as the `next` handler. 
  - All three types of callbacks may be provided as arguments

## Subscription

- A Subscription is an object that represents a disposable resource, usually the execution of an Observable. 
- A Subscription has one important method `unsubscribe`, that takes no argument and just disposes the resource held by the subscription.
- A Subscription essentially just has an `unsubscribe()` function to release resources or cancel Observable executions.
- Subscriptions can also be put together, so that a call to an unsubscribe() of one Subscription may unsubscribe multiple Subscriptions. 

## Subjects

- An RxJS Subject is a special type of Observable that allows values to be multicasted to many Observers. 
- While plain Observables are unicast (each subscribed Observer owns an independent execution of the Observable), Subjects are multicast.
- A Subject is like an Observable, but can multicast to many Observers.   
  - Subjects are like EventEmitters: they maintain a registry of many listeners.
- Every Subject is an Observable.
  - Given a Subject, you can `subscribe` to it, providing an Observer, which will start receiving values normally. 
  - From the perspective of the Observer, it cannot tell whether the Observable execution is coming from a plain unicast Observable or a Subject.
  - Internally to the Subject, subscribe does not invoke a new execution that delivers values.
    - It simply registers the given Observer in a list of Observers, similarly to how `addListener` usually works in other libraries and languages.
- Every Subject is an Observer.
  - It is an object with the methods `next(v)/error(e)/complete()`. 
  - To feed a new value to the Subject, just call `next(theValue)`, 
  - and it will be multicasted to the Observers registered to listen to the Subject.
  - Since a Subject is an Observer, this also means you may provide a Subject as the argument to the subscribe of any Observable

``` JS
import { Subject } from 'rxjs';

// we have two Observers attached to a Subject
const subject = new Subject();

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

subject.next(1);
subject.next(2);

// Logs:
// observerA: 1
// observerB: 1
// observerA: 2
// observerB: 2
```

``` JS
import { Subject, from } from 'rxjs';

const subject = new Subject < number > ();

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

// convert a unicast Observable execution to multicast
const observable = from([1, 2, 3]);

// This demonstrates how Subjects are the only way of making any Observable execution be shared to multiple Observers.
observable.subscribe(subject); // You can subscribe providing a Subject

// Logs:
// observerA: 1
// observerB: 1
// observerA: 2
// observerB: 2
// observerA: 3
// observerB: 3
```

- A "multicasted Observable" passes notifications through a Subject which may have many subscribers, whereas a plain "unicast Observable" only sends notifications to a single Observer.
- Under the hood, this is how the `multicast` operator works:
  - Observers subscribe to an underlying Subject, 
  - and the Subject subscribes to the source Observable. 
- The following example is similar to the previous example which used `observable.subscribe(subject)`

``` JS
import { from, Subject } from 'rxjs';
import { multicast } from 'rxjs/operators';

const source = from([1, 2, 3]);
const subject = new Subject();
const multicasted = source.pipe(multicast(subject));

// These are, under the hood, `subject.subscribe({...})`:
multicasted.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
multicasted.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});

// This is, under the hood, `source.subscribe(subject)`:
multicasted.connect();
```

- `multicast` returns an Observable that looks like a normal Observable, but works like a Subject when it comes to subscribing. 
  - `multicast` returns a `ConnectableObservable`, which is simply an Observable with the `connect()` method.
  - The `connect()` method is important to determine exactly when the shared Observable execution will start. 
  - Because `connect()` does `source.subscribe(subject)` under the hood, 
  - `connect()` returns a Subscription, which you can unsubscribe from in order to cancel the shared Observable execution.
- Calling `connect()` manually and handling the Subscription is often cumbersome. 
  - Usually, we want to automatically connect when the first Observer arrives, and automatically cancel the shared execution when the last Observer unsubscribes.
  - If we wish to avoid explicit calls to `connect()`, we can use ConnectableObservable's `refCount()` method (reference counting), which returns an Observable that keeps track of how many subscribers it has.

- One of the variants of Subjects is the `BehaviorSubject`, which has a notion of "the current value". 
  - It stores the latest value emitted to its consumers, 
  - and whenever a new Observer subscribes, it will immediately receive the "current value" from the BehaviorSubject.
- `BehaviorSubjects` are useful for representing "values over time". 
  - For instance, an event stream of birthdays is a Subject, but the stream of a person's age would be a BehaviorSubject.
- `ReplaySubject` is similar to `BehaviorSubject` in that it can send old values to new subscribers, 
  - but it can also record a part of the Observable execution.
- A `ReplaySubject` records multiple values from the Observable execution and replays them to new subscribers.
- You can also specify a window time in milliseconds, besides of the buffer size, to determine how old the recorded values can be.
- `AsyncSubject` is a variant where only the last value of the Observable execution is sent to its observers, and only when the execution completes.
  - `AsyncSubject` is similar to the `last()` operator, in that it waits for the complete notification in order to deliver a single value.

## Operators

- Operators are the essential pieces that allow complex asynchronous code to be easily composed in a declarative manner.
- Operators are functions.
- A Pipeable Operator is essentially a pure function which takes one Observable as input, generates and returns another Observable as output.
  - It is a pure operation: the previous Observable stays unmodified.
  - Pipeable Operators are the kind that can be piped to Observables using the syntax `observableInstance.pipe(operator())`. 
  - like `filter(...)`, and `mergeMap(...)`. 
  - When called, they do not change the existing Observable instance. 
  - Instead, they return a new Observable, whose subscription logic is based on the first Observable.
  - Subscribing to the output Observable will also subscribe to the input Observable.
- Creation Operators are the other kind of operator, which can be called as standalone functions to create a new Observable. 
  - For example: `of(1, 2, 3)` creates an observable that will emit 1, 2, and 3, one right after another. 
  - Creation operators will be discussed in more detail in a later section.

- Pipeable operators are functions, so they could be used like ordinary functions: `op()(obs)`
  - but in practice, there tend to be many of them convolved together, and quickly become unreadable: op4()(op3()(op2()(op1()(obs)))). 
  - For that reason, Observables have a method called `.pipe()` that accomplishes the same thing while being much easier to read

- Creation operators are functions that can be used to create an Observable with some common predefined behavior or by joining other Observables.

- Observables most commonly emit ordinary values like strings and numbers, 
  - but surprisingly often, it is necessary to handle Observables of Observables, so-called higher-order Observables. 

- The `concatAll()` operator subscribes to each "inner" Observable that comes out of the "outer" Observable, 
  - and copies all the emitted values until that Observable completes, 
  - and goes on to the next one. 
  - All of the values are in that way concatenate

- Many operators are related to time, they may for instance delay, sample, throttle, or debounce value emissions in different ways

- There are operators for different purposes, and they may be categorized as: creation, transformation, filtering, joining, multicasting, error handling, utility, etc
- If there is a commonly used sequence of operators in your code, use the `pipe()` function to extract the sequence into a new operator. 
  - Even if a sequence is not that common, breaking it out into a single operator can improve readability.
- You can write an custom new operator from scratch using the Observable constructor

## Schedulers

- A scheduler controls when a subscription starts and when notifications are delivered. 
- A Scheduler lets you define in what execution context will an Observable deliver notifications to its Observer.
- A Scheduler consists of three components.
- A Scheduler is a data structure. 
  - It knows how to store and queue tasks based on priority or other criteria.
- A Scheduler is an execution context.
  - It denotes where and when the task is executed 
  - (e.g. immediately, or in another callback mechanism such as setTimeout or process.nextTick, or the animation frame).
- A Scheduler has a (virtual) clock. 
  - It provides a notion of "time" by a getter method now() on the scheduler. 
  - Tasks being scheduled on a particular scheduler will adhere only to the time denoted by that clock.

- The `asyncScheduler` operates with a `setTimeout` or `setInterval`, even if the given delay was zero. 
  - As usual, in JavaScript `setTimeout(fn, 0)` is known to run the function fn earliest on the next event loop iteration. 
- The `schedule()` method of a Scheduler takes a `delay` argument, which refers to a quantity of time relative to the Scheduler's own internal clock. 
  - A Scheduler's clock need not have any relation to the actual wall-clock time. 
  - This is specially useful in testing, where a virtual time Scheduler may be used to fake wall-clock time while in reality executing scheduled tasks synchronously.

- Scheduler Types
  - null
    - Use this for constant-time operations or tail recursive operations.
    - By not passing any scheduler, notifications are delivered synchronously and recursively. 
  - queueScheduler
    - Use this for iteration operations.
    - Schedules on a queue in the current event frame (trampoline scheduler). 
  - asapScheduler
    - Use this for asynchronous conversions.
    - Schedules on the micro task queue, which is the same queue used for promises. 
    - Basically after the current job, but before the next job. 
  - asyncScheduler
    - Use this for time-based operations.
    - Schedules work with setInterval. 
  - animationFrameScheduler
    - Can be used to create smooth browser animations.
    - Schedules task that will happen just before next browser content repaint. 

- All Observable operators that deal with concurrency have optional schedulers. 
  - If you do not provide the scheduler, RxJS will pick a default scheduler by using the principle of least concurrency. 
  - This means that the scheduler which introduces the least amount of concurrency that satisfies the needs of the operator is chosen.
  - For example, for operators returning an observable with a finite and small number of messages, RxJS uses no Scheduler, i.e. `null` or `undefined`. 
    - For operators returning a potentially large or infinite number of messages, queueScheduler is used. 
    - For operators which use timers, asyncScheduler is used.
- Static creation operators usually take a Scheduler as argument.

- Use `subscribeOn` to schedule in what context will the` subscribe()` call happen. 
  - By default, a `subscribe()` call on an Observable will happen synchronously and immediately. 
  - However, you may delay or schedule the actual subscription to happen on a given Scheduler, using the instance operator `subscribeOn(scheduler)`, where scheduler is an argument you provide.

- Use `observeOn` to schedule in what context will notifications be delivered.
  - instance operator `observeOn(scheduler)` introduces a mediator Observer between the source Observable and the destination Observer, where the mediator schedules calls to the destination Observer using your given scheduler.
