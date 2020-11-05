---
title: note-dev-state-blog
tags: [blog, dev, state]
created: '2020-11-02T05:18:43.747Z'
modified: '2020-11-02T05:19:40.469Z'
---

# note-dev-state-blog

## state-blog

### [Build a state management system with vanilla JavaScript_2018](https://css-tricks.com/build-a-state-management-system-with-vanilla-javascript/)

- https://github.com/hankchizljaw/vanilla-js-state-management
- https://github.com/hankchizljaw/beedle
  - /306Star/MIT/201006/js
  - A tiny library inspired by Redux & Vuex to help you manage state in your JS apps
  - Beedle creates a central store that enables you predictably control 

- Traditionally, we’d keep state within the DOM itself or even assign it to a global object in the window
- Libraries like Redux, MobX and Vuex make managing cross-component state almost trivial(微不足道的，不重要的)
- We’re creating the functionality that allows other parts of our application to subscribe to named events.
- Another part of the application can then publish those events, often with some sort of relevant payload.
- The PubSub pattern loops through all of the subscriptions and fires their callbacks with that payload.
- Let’s take a look at how our Store object keeps track of all of the changes. We’re going to use a Proxy to do this
- Usage of DOM Api will prevent possible SSR

### [Stateful Components in Vanilla JS](https://yamagata-developers-society.github.io/blog/stateful-components-vanilla-js/)

- Today I’d like to show you how to create stateful components with vanilla JavaScript, and demonstrate 
  - You don’t need to download any library to apply the amazing concepts used by React.js in your JavaScript programming.
- Even though we can’t benefit from React’s virtual DOM or setState({}) method, this is a powerful way to think and program — and there is no external dependency to worry about!
- What are the benefits?
  - Write organized, reactive code without the increased bundle size
  - Simplify DOM manipulations and state logic
  - Improve the versatility and strength of your standard JavaScript coding!

- [demo on jsfiddle](https://jsfiddle.net/jzft0o7r/)

``` HTML
<div class="App__container" id="app">
  <div>Count: <span id="display">0</span></div>

  <button onclick="incCountUp()">+Count</button>
</div>
```

``` CSS
.App__container {
  padding: 15px;
}

.Score {
  font-size: 28px;
}

.text-error {
  color: red;
}

.text-success {
  color: green;
  font-size: 40px;
}
```

``` JS
const display = document.getElementById("display");

const state = {
  count: 0,
}

// Components

const counter = count => {
  let classname = "text-error";

  if (count > 10) {
    classname = "text-success";
  }

  return (
    `<p class="Counter">Count: <span class="${classname}">${count}</span></p>`
  );
};

// Render Methods

function renderCount() {
  display.innerHTML = counter(state.count);
}

// Update methods

function incCountUp() {
  let newCount = state.count + 1;
  state.count = newCount;

  renderCount();
}

renderCount();
```

### [Observer vs Pub-Sub pattern](https://hackernoon.com/observer-vs-pub-sub-pattern-50d3b27f838c)

- The `observer pattern` is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.
- The Subject in the Observer Pattern is like a Publisher and the Observer can totally be related to a Subscriber 
- and Yes, the Subject notifies the Observers like how a Publisher generally notify his subscribers. 
- That’s why most of the Design Pattern books or articles use ‘Publisher-Subscriber’ notion to explain Observer Design Pattern. 
- But there is another popular Pattern called ‘Publisher-Subscriber’ and it is conceptually very similar to the Observer pattern. 
- In `Publisher-Subscriber` pattern, senders of messages, called publishers, do not program the messages to be sent directly to specific receivers, called subscribers.
- This means that the publisher and subscriber don’t know about the existence of one another. 
- There is a third component, called broker or message broker or `event bus`, 
  - which is known by both the publisher and subscriber, 
  - which filters all incoming messages and distributes them accordingly.
- In other words, pub-sub is a pattern used to communicate messages between different system components without these components knowing anything about each other’s identity. 
- how does the broker filter all the messages?  
  - Most popular methods are: Topic-based and Content-based

- Let’s list out the differences as a quick Summary:
  - In the Observer pattern, the Observers are aware of the Subject, also the Subject maintains a record of the Observers. 
    - Whereas, in Publisher/Subscriber, publishers and subscribers don’t need to know each other. 
    - They simply communicate with the help of message queues or broker.
  - In Publisher/Subscriber pattern, components are loosely coupled as opposed to Observer pattern.
  - Observer pattern is mostly implemented in a synchronous way, i.e. the Subject calls the appropriate method of all its observers when some event occurs. 
    - The Publisher/Subscriber pattern is mostly implemented in an asynchronous way (using message queue).
  - Observer pattern needs to be implemented in a single application address space. 
    - On the other hand, the Publisher/Subscriber pattern is more of a cross-application pattern.

- Despite the differences between these patterns, some might say that Publisher-Subscriber pattern is a variation of Observer pattern because of the conceptual similarity between them. And it won’t be wrong at all. Don’t need to take the differences religiously. 
