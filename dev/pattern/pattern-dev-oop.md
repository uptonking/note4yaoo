---
title: pattern-dev-oop
tags: [object-oriented-programming, oop]
created: 2020-12-20T15:47:40.025Z
modified: 2020-12-20T15:48:03.553Z
---

# pattern-dev-oop

# guide

- oop-examples
  - jdk
  - wikimedia-oojs
# [Event Listeners: Delegation VS Direct Binding - JASON Format](https://jasonformat.com/event-delegation-vs-direct-binding/)
- The DOM provides a mechanism for registering event handlers that supports two techniques for observing events: 
  - directly-bound per-element listeners, 
  - and “delegated” listeners that receive events originating from within an entire subtree.
- Frameworks and libraries that abstract event listener registration generally choose between the two approaches
- Library developers often rely on past experience to make decisions relating to event delegation vs direct binding

## Direct Binding

- The oldest and simplest way to listen for DOM events is to register an event handler function directly on the node that will emit that event. 
  - Most DOM events propagate up the tree from their originating target Node, so this approach can be combined freely with delegation techniques.
- This is a case where direct binding is also the best approach from a performance standpoint, since no DOM tree traversal is required to register or handle the event. 
  - Strictly looking at our own logic, registering and invoking the listener are both `O(1)` operations.

## Event Delegation

- Event delegation is a technique for listening for events in the aggregate. 
  - It leverages the fact that most events “bubble” up the DOM tree, which means they can be intercepted at the tree’s root and handled there.
- One of the key features that makes event delegation valuable is that it is possible to handle events from any target node without having a prior reference to that node.
- In cases where an event handler needs to listen on a large or changing set of target nodes, this avoids having to manually manage adding and removing handlers from each node.

```html
<a href="/">Home</a>
<a href="/profile">Profile</a>
<a href="/search">Search</a>
<script>
  function handleClick(e) {
    history.pushState(null, null, this.href);
    fancyPageLoad(this.href);
    e.preventDefault();
  }
  for (let link of document.querySelectorAll('a[href]')) {
    link.addEventListener('click', handleClick);
  }
  // ...listen for added/removed links using MutationObserver...
</script>
```

- Implementing this using direct binding requires searching the DOM for anchorlink elements and registering event handlers on each. 
  - We’d also need to use something like MutationObserver to detect newly-added links and register our handler on them. 
  - This would be expensive, since searching the DOM incurs a runtime performance cost and increases memory usage, as does MutationObserver. 
  - Listener invocation has the same performance as the previous simple direct binding example, but registration no longer runs in constant time.

```HTML
<a href="/">Home</a>
<a href="/profile">Profile</a>
<a href="/search">Search</a>
<script>
  addingEventListeners('click', e => {
    let target = e.target;
    do {
      if (target.localName === 'a') {
        history.pushState(null, null, target.href);
        fancyPageLoad(target.href);
        e.preventDefault();
        break;
      }
    } while (target = target.parentNode);
  });
</script>
```

- Now our example uses a single delegated event handler, which removes all event handler management costs. 
  - There is a small performance tradeoff being made here, which is that the handler has to walk up the DOM tree to detect if a click occurred on a link. 
  - In this case our logic for registering the listeners is `O(1)`, and the listener's invocation is `O(log(n))`.
- In many cases where there’s a very large number of event targets or where event targets are not known up-front, event delegation can improve performance by relying on the browser’s hit testing logic to dynamically observe events of a given type.

## Event delegation can be tricky

- event delegation can create a set of problems not found when using directly-bound event handlers. 
- Delegation can make event “pathing” difficult, and the effects of this are sometimes only revealed as a codebase increases in complexity. 
  - One example of this occurs when the DOM tree is mutated during the course of an event’s capturing or bubbling phase: should an event continue bubbling if its target or an ancestor is removed?
- A concrete example of where event pathing grows difficult is handling events from other documents in a fully delegated event handling model. 
  - An event triggered within an iframe does not bubble up to the parent document, which means it cannot be handled via delegation. 
  - This can be addressed by adding additional delegated event handlers in documents, which can either handle or retarget/refire the event in the parent document to emulate bubbling. 
  - While edge cases like these are not always important to account for, if they become necessary it can complicate event delegation and reduce its performance value.

## Missing out on features

- it’s important to take note of some direct binding features that are more difficult or even impossible to leverage in a delegated model. 
- `addEventListener` API has gained support for one-time handlers that are automatically removed after being fired, which can help avoid a class of memory leak caused by DOM references retained solely to allow for listener removal.
- Passive listeners are another addEventListener feature introduced somewhat recently, offering a way to listen for events without blocking user interaction when they occur. 
  - This is an important technique to have at your disposal when implementing things like touch and scroll reactivity. 
  - Browsers are actively moving towards firing passive events by default, however this is happening slowly
  - it’s a good idea to make sure your solution for delegating events provides a way to register passive listeners - or even uses passive listeners by default.
- Another feature that event delegation implementations sometimes struggle with recreating is the level of optimization already present in browser event implementations. 
  - Events are created and initialized at the root of a document and their hit-tested event path is constructed in advance despite its JavaScript representation being lazily-constructed. 
  - The same Event object instance is passed to each handler invoked during the capturing and bubbling phases. 
  - Browsers engines can optimize garbage collection of Event instances, since they do not have to hold a strong reference to an event
- It should be possible to approximate these optimizations in a JavaScript implementation using recently-added language features like WeakRef and Finalizers, however it’s unlikely any popular solutions will leverage this for some time.
- Finally, one of the most compelling arguments in favor of directly binding event listeners rather than using global event delegation is interoperability
  - Event listeners registered directly on nodes are partaking in the DOM’s cooperative event handling model: every element and its listeners have a chance to observe or intercept events, and can participate in a shared decision on how a given event should be handled. 
  - This becomes apparent when combining multiple frameworks on a page
  - if each framework implements its own event propagation model using global delegated listeners, important event handling concerns like default behavior prevention and retargeting can become difficult or even impossible.

## Event delegation is not a better addEventListener

- The tradeoff between direct binding and event delegation is hard to measure
- One generalization that can guide the decision between these approaches is that direct binding is generally a better option if the code in question already has a stable reference to the DOM node on which an event will be fired. 
  - As a rule of thumb, if you don’t have to search for a node in order to attach an event handler to it, it’s likely a good case for binding directly.
- One concrete example of such a case is Preact’s event handler abstraction, which is often brought up when discussing the efficacy or delegated vs direct event handling. 
  - Preact’s renderer is already responsible for retaining a mirror tree in order to perform Virtual DOM diffing, which means there’s already a clear place to perform direct event handler binding during updates
- To minimize any invocation cost associated with `addEventListener()` and `removeEventListener()`, a single proxy listener is registered for all events that looks up the current listener for a given event when it is fired. 
  - This means “swapping” an event handler to a new function reference only updates the current handler reference and does not remove or re-add any event listeners.
# more-patterns
- [The Outbox Pattern](https://www.kamilgrzybek.com/blog/posts/the-outbox-pattern)
# discuss-oop
- ## 

- ## 

- ## 

- ## 🆚️ The biggest reason I prefer working in TypeScript over typed alternatives like C# or Java: Bare functions. 
- https://x.com/housecor/status/1907076979360157916
  - In C# and Java, everything has to be a class. 

- As of C# 12, bare functions, known in C# as "primary functions" are fully supported. That was released late 2023.

- ## I avoid OOP as much as possible nowadays
- https://twitter.com/0xglitchbyte/status/1772474741007220770
  - I wrote and worked in heavy OOP codebases, and found nothing but messes and layers of indirection
  - After a while, I got introduced to Data Oriented Design

- I always thought it was never really an either or decision. Some situations a class and inheritance is nice, some pure data is better. To me, common lisp got this right with being multi paradigm. Going wild either way usually works against clarity.

- OOP is a tool. Just don't abuse it. I'm looking at you Java and C# ...

- I had the same opinion... until I had to work with Unreal Engine. The fact that it's maybe the best engine out there has a lot to do with it being entirely OOP. I still don't think high of OOP, especially for hp tasks, however after my experience with UE, I'm not so sure anymore.
