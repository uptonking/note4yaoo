---
title: lib-state-event-pubsub
tags: [pattern, pubsub, state]
created: 2020-11-10T11:59:33.470Z
modified: 2021-05-13T03:13:45.375Z
---

# lib-state-event-pubsub

# faq

- 监听事件的执行顺序如何控制
  - node默认使用队列形式的链表
# guide
- who is using #pubsub
  - redux
  - Vue2.x依赖收集与通知
  - nodejs eventemitter
# EventEmitter
- 优点
  - 可用来替换包含多个callback的场景
  - 可扩展性更强
  - 代码可读性更高

- 缺点
  - 不支持一次触发多个事件名
  - 不支持异步执行监听器函数
  - 不支持事件名通过正则匹配或通配符匹配
  - The loose coupling in event-driven architectures can also lead to increased complexity if we’re not careful. 
    - It can be difficult to keep track of dependencies in our system. 

- tips
  - 可以在constructor构造函数中调用emitter.on注册事件处理函数，然后在其他方法如生命周期方法中调用emitter.emit触发事件，能避免忘记手动注册事件函数
  - 默认同步执行所有监听函数
    - Because the Event loop fetches events from Event Queue and sends them to call stack one by one.
    - And Event Queue is FIFO (First-In-First-Out)

- https://github.com/developit/mitt /9.7kStar/MIT/202307/ts
  - Tiny 200 byte functional event emitter/pubsub.
  - Mitt was made for the browser, but works in any JavaScript runtime
  - Functional: methods don't rely on this
  - a wildcard "*" event type listens to all events

- https://github.com/Olical/EventEmitter
  - /3kStar/Unlicense/202010/js
  - brings the power of events from platforms such as node.js to your browser.
  - You can pass a regular expression to pretty much every function in EventEmitter in place of an event name string
  - `Player.prototype = Object.clone(EventEmitter.prototype);`

- https://github.com/EventEmitter2/EventEmitter2
  - /2kStar/MIT/202010/js
  - A nodejs EventEmitter implementation with namespaces, wildcards, TTL, works in the browser
  - Times To Listen (TTL), extends the once concept with many
  - Async listeners (using setImmediate|setTimeout|nextTick) with promise|async function support
  - The emitAsync method to return the results of the listeners via Promise.all

- https://github.com/primus/eventemitter3
  - /2.1kStar/MIT/202010/js
  - It has been micro-optimized for various of code paths making this, one of, if not the fastest EventEmitter available for Node.js and browsers. 
  - The module is API compatible with the EventEmitter that ships by default with Node.js 
  - The newListener and removeListener events have been removed as they are useful only in some uncommon use-cases.
  - The setMaxListeners, getMaxListeners, prependListener and prependOnceListener methods are not available.
  - The removeListener method removes all matching listeners, not only the first.
  - EventEmitter is written in EcmaScript 3
  - Domain support has been removed.

- https://github.com/yandeu/events /MIT/202211/ts/inactive
  - Simplified and TypeScripted version of EventEmitter3@4.0.7

- more-event-emitter-impl
  - https://github.com/facebookarchive/emitter /js
# discuss
- ## 

- ## 

- ## 🤼🏻 eventemitter is a performance bottleneck and the internals are exposed enough to make it difficult to optimize
- https://x.com/jarredsumner/status/1850311072001192118
  - this is part of why exactly 0 of bun’s APIs use event emitter
- What are you doing instead?
  - functions specified once at creation time, with a .reload method if necessary to update the callbacks later. this makes hot reloading sockets, websockets and http servers work

- Does EventTarget provide any improvement? 
  - It’s worse because there’s capturing and bubbling phases, and the Event objects are not free to create

- I'm a fan of the API that vscode adopted:
  - https://github.com/microsoft/vscode/blob/main/src%2Fvs%2Fbase%2Fcommon%2Fevent.ts

- What is a better API for this use-case?
  - “Pull streams” for streams. 
  - Event emitters should have never be the base for streams.

- ## 🆚️🌰 Non-RxJS Observables in the wild... tanstack edition _202305
- https://twitter.com/BenLesh/status/1656746366553452573
- Yes, yes, it's more of a "Subject"... which is an observable.

- Incidentally, @tannerlinsley , I don't know all of the usage here, but as a pro-tip, *if* you can move away from an array of listeners to a `Set` it will help perf a lot. (But comes with idempotent listener adds, obviously)
  - (I've been wanting to do that to RxJS Subjects, but it would be too broad of a breaking change for us)
  - Prior art is `EventTarget` , though: `addEventListener` is idempotent.
- 🌰⚡️ heh, I actually did the `array->Map` switch for the Redux core in v5 alpha
  - [Replace listeners array with a Map for better performance · reduxjs/redux _202301](https://github.com/reduxjs/redux/pull/4476)
  - Redux has always used an array of listener callbacks internally. However, as we found out with React-Redux, using `listeners.findIndex(callback)` is bad for performance
  - I initially tried `Set<ListenerCallback>`, but found that one test failed. A `Set` compares by reference, so the callback got removed in the first `unsubscribe()` call and was no longer around for the second.
  - We don't have a formal statement that we support passing in the same callback more than once, but that's the implicit semantics thus far.
  - Given that, a `Map<number, ListenerCallback>` works equivalently, and we'll just have an incrementing counter for the key.

- Ooh do XState next (we love our bespoke artisanal handcrafted observables)
  - All ActorRefs (what is returned from interpret(...)) are observable

- ## I wrote up a bit about the different types of cancellation/unregistration that exist, and why AbortSignal is a solid choice for DOM Observables in JavaScript.
- https://twitter.com/BenLesh/status/1729970596715376698
  - I think it's worth sharing, because it's a general API design choice some folks need to make. "What's the best way to add and remove some resource like a callback from some other thing?"
- [How to removeEventListener? · WICG/observable](https://github.com/WICG/observable/issues/75#issuecomment-1832698540)
  - Return a means of removing the resource, (RxJS does this with `subscribe(): Subscription` , other APIs might return a removal function like `subscribe(cb: Callback): UnsubscribeFunction` , etc.
  - Provide a separate unregistration function. This is what `addEventListener` and `removeEventListener` are. Or think of like the Observer pattern's Subject: `addObserver/removeObserver` , etc.
  - Allow the consumer to pass in a token-based cancellation mechanism. This is `AbortSignal` , or in something like . NET, `CancellationToken` , etc.
- Every single one of the above is just a different way to do the same thing. They all have advantages and disadvantages.
- `AbortSignal` has the most advantages for `Observable` because it allows the cancellation mechanism to be created before the subscription starts, when the subscription could emit values synchronously (as is required of anything that is going to model `EventTarget` ). It's also nice because there's no need to keep the `EventTarget` instance itself on-hand to unregister the listener, like you would if you had to use `removeEventListener` .
  - Sort of: You not only have to have a handle to your function, but you must also have a handle to the actual target as well, AND you have to know the "magic string" it was registered under. So you need 3 components: `target.removeEventListener('type', func)` . With an `AbortSignal` , you only need to have a reference to the `AbortController` to unregister the listener.

- removeEventListener has to be the most annoying thing in JS. Thankfully in modern JS there's usually a nice framework wrapping it.
  - Terribly, in some cases (DOM events), you need 4 pieces of information to remove a listener! In addition to the three you mentioned, you also need to know whether the listener was added for the capture or bubble phase of the event.

- ## 🆚️ Choosing Between Pub-Sub Brokers and REST APIs in System Design
- https://twitter.com/rixlabs/status/1768901435192664538

- Pub-Sub Broker Pros:
  - Real-Time Operations: Ideal for systems needing instant data sharing like live feeds or notifications.
  - Decoupling: Producers and consumers work independently, improving system resilience and scalability.
  - Event-Driven: Supports reactive architectures, responding to events as they occur.
  - High Volume: Handles large amounts of messages efficiently, distributing them to numerous subscribers.

- Pub-Sub Broker Cons:
  - Complexity: Can be harder to set up and manage compared to direct API calls.
  - Overhead: Might introduce additional overhead for low-volume or infrequent data exchanges.
  - Message Tracking: Tracing and debugging can be more challenging due to asynchronous nature.

- REST API Pros:
  - Simplicity: Straightforward for retrieving or updating data through standard HTTP methods.
  - Statelessness: Each call is independent, making scaling and caching more effective.
  - Interoperability: Easily integrates with different types of clients, from web to mobile.
  - CRUD Operations: Intuitive for standard database operations: create, read, update, delete.

- REST API Cons:
  - Polling: Not suitable for real-time updates without frequent server requests.
  - Coupling: Tighter coupling between client and server; changes in API can affect clients.
  - Scalability: While scalable, high traffic requires careful management to avoid server overload.

- Choose a pub-sub broker when building real-time, event-driven systems where components must react quickly to changes without being tightly coupled. 
  - It’s suitable for systems where the workload is unpredictable or where you expect to scale significantly.

- Opt for REST APIs in scenarios where systems perform direct, specific actions on data like reading or updating records. 
  - REST is more applicable for interfaces that external users or services will interact with, especially when actions are straightforward and stateless.

- Your choice should align with the system’s operational requirements and scalability needs. 
  - Pub-sub is for real-time, high-volume messaging, while REST APIs are for predictable, stateless interactions. 

- This is not Pub/Sub but Point-to-Point.
  - True. I did the schema in 3 min on my iPad. I could have draw better symbols.

- ## TIL the browser event system is basically a built-in pubsub system.
- https://twitter.com/ralex1993/status/1745790936808837331
  - [Patterns for Reactivity with Modern Vanilla JavaScript – Frontend Masters Boost](https://frontendmasters.com/blog/vanilla-javascript-reactivity/#pubsub-pattern-publish-subscriber)
- `EventTarget` in Node.js has some omissions(省略、删除、遗漏) (e.g. no bubbling and sinking, which is sad if you’re trying to build your own DOM library on top of it), but is nonetheless API-compatible and performant

- ## [When should I use EventEmitter?](https://stackoverflow.com/questions/38881170/when-should-i-use-eventemitter)
- Whenever it makes sense for code to SUBSCRIBE to something rather than get a callback from something. 
- The **typical use case** would be that there's multiple blocks of code in your application that may need to do something when an event happens.
- For example, let's say you are creating a ticketing system. 
- The common way to handle things might be like this:

```JS
function addTicket(ticket, callback) {
  insertTicketIntoDatabase(ticket, function(err) {
    if (err)
      return handleError(err);

    callback();
  });
}
```

- But now, someone has decided that when a ticket is inserted into the database, you should email the user to let them know. 
- That's fine, you can add it to the callback:

```JS
function addTicket(ticket, callback) {
  insertTicketIntoDatabase(ticket, function(err) {
    if (err)
      return handleError(err);

    emailUser(ticket, callback);
  });
}
```

- But now, someone wants to also notify another system that the ticket has been inserted. 
- Over time, there could be any number of things that should happen when a ticket is inserted. 
- So let's change it around a bit:

```JS
function addTicket(ticket, callback) {
  insertTicketIntoDatabase(ticket, function(err) {
    if (err)
      return handleError(err);

    TicketEvent.emit('inserted', ticket);
    callback();
  });
}
```

- We no longer need to wait on all these functions to complete before we notify the user interface. 
- And elsewhere in your code, you can add these functions easily:

```JS
TicketEvent.on('inserted', function(ticket) {
  emailUser(ticket);
});

TicketEvent.on('inserted', function(ticket) {
  notifySlack(ticket);
});
```

- ## code-snippet: EventEmitter vs callback

```JS
let events = require("events");
let util = require("util");
let eventEmitter = new events.EventEmitter();

// Example 1 with the EventEmitter:
let Student = function(name) {
  this.name = name;
}
util.inherits(Student, events.EventEmitter);

let student_max = new Student('max');
student_max.on('scored', function(points) {
  if (points > 90) {
    points = points + ' wow you scored more than 90'
  }
  console.log(`${this.name} ${points} points`);
})

student_max.emit('scored', 95);

// Example 2 without EventEmitter
let Student2 = function(name) {
  this.name = name;
  this.score = function(str, points) {
    if (str !== 'scored') {
      return;
    }
    if (points > 90) {
      points = points + ' wow you scored more than 90'
    }
    console.log(`${this.name} ${points} points`);
  }
}

let student_lenny = new Student2('Lenny');

student_lenny.score('scored', 95);
```

- The first example subclasses an event emitter and then uses that event emitter to implement some functionality. 
  - That means that anyone else can take one of your student_max objects and register an event listener for the scored message or they could even emit a scored message themselves. 
  - You could then very easily use the eventEmitter functionality to extend to other events that occurred in your object and then any third party could observe or trigger those events too. 
  - eventEmitter is a standardized way of exposing event based functionality. 
  - You can accomplish things with an eventEmitter by designing your own notification schemes, but it is often better to build on a standard scheme that lots of developers already know and that has a fair amount of functionality already built in.
- Your second example as currently coded accomplishes the same thing, but is not as extensible. 
  - For example, if you wanted to know anything a score happens, you would have to subclass the object and override the score method rather than just adding a listener to an event using the well-established eventEmitter interface. 
  - If you didn't create the object yourself (which makes it hard to subclass), then you'd have to monkey-patch the score method in order to observe it.
- what is the difference of the example1 to example2
  - It's an architectural difference that affects both how outside agents interact with these objects and how extensible they are in the future.
  - The use of the eventEmitter in example1 is very extensible and makes it easy to add future events to the object using the eventEmitter features or for outside agents to monitor or trigger events using a standardized interface. 
  - So, the difference is not in exactly what the code you show achieves, but in how it is architected and thus how extensible it would be in the future or how outside code could interact with your object
- When is it practical to use it(EventEmitter)?
  - You would think about using an eventEmitter object pretty much anytime you want outside parties to be able to observe events or trigger events on your object in a lightweight and easy way. 
  - It's a pre-built system for that and is often better than inventing your own callback notification scheme. 
  - And sometimes, it is useful even for your own implementation when you aren't trying to enable outside interactions.

- ## [How to make an EventEmitter listen to another EventEmitter in Node.js?](https://stackoverflow.com/questions/26465358/how-to-make-an-eventemitter-listen-to-another-eventemitter-in-node-js)
- EventEmitters are kind of sole-source in javascript. 
  - They are not system-wide events that everyone can listen to. 
  - They are objects that can emit events to support the asynchronous patterns. 
  - To accomplish what you want, you need multiple things listening to the same emitter.
  - 可以封装一个方法，方法中执行emitter.on，来模拟在一个事件处理函数中触发另一个事件处理函数
- 还可以在emitterA的事件处理函数中直接调emitterB.emit('evtName')

```JS
var events = require('events');

//create a container that can listen
function EventListener(name) {
  console.log('new event listener, name=' + name);
  this.name = name;
  this.ack = function() {
    console.log(this.name + ' just heard testA');
  };
  this.listenTo = function(event, emitter) {
    var self = this;
    emitter.on(event, function() {
      self.ack();
    });
  };
}

//Create a new sole-source event emitter
var emitterA = new events.EventEmitter();

var listenerA = new EventListener('A', emitterA);
listenerA.listenTo('testA', emitterA);

var listenerB = new EventListener('B', emitterA);
listenerB.listenTo('testA', emitterA);

setInterval(function() {
  emitterA.emit('testA');
}, 1000);
```

- This is good but it has to create a new object each time. I'd like each request object (which is spontaneously created and destroyed) to just listen in, and those listeners to die with the request objects.
- This object was just an example. 
  - The point is that the event emitter must be shared. 
  - You could initialize it at server-start, and perhaps use some middleware on each request to subscribe to (or "attach") that global emitter. 
  - Just remember that an EventEmitter is a sole-source thing though, not Publish-Subscribe. 
  - For that you would need some extra stuff or find a library, or even use redis. 
# ref
- [Why use Node.js EventEmitter instead of just a plain function?](https://stackoverflow.com/questions/39305354/why-use-node-js-eventemitter-instead-of-just-a-plain-function)
  - another code snippet for EventEmitter vs callback
- [Let’s Create a Lightweight Native Event Bus in JavaScript](https://css-tricks.com/lets-create-a-lightweight-native-event-bus-in-javascript/)
- [Event Emitter instead of lifting state up in React](https://medium.com/@krzakmarek88/eventemitter-instead-of-lifting-state-up-f5f105054a5)
