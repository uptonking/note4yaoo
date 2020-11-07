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
- The Store is our central object.
- Let’s take a look at how our Store object keeps track of all of the changes. 
  - We’re going to use a Proxy to do this
  - If we add a `get` trap, we can monitor every time that the object is asked for data. 
  - Similarly with a `set` trap, we can keep an eye on changes that are made to the object.
  - when a mutation runs something like `state.name = 'Foo'` , this trap catches it before it can be set and provides us an opportunity to work with the change or even reject it completely. 
- There’s a lot going on there, but I hope you’re starting to see how this is all coming together and importantly, how we’re able to maintain state centrally, thanks to Proxy and Pub/Sub.
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

//  start with a simple object, which will represent the initial state of our data
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

// Render Function
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

### [What is state? Why do I need to manage it?](https://egghead.io/articles/what-is-state-why-do-i-need-to-manage-it)

- When it comes to client-side JavaScript applications, I like to think of state as “the outcome of all of the actions that the user has taken since the page loaded”.
- This isn’t an all-encompassing way of thinking about state, 
  - as other agents might affect state — the server might set some variables, a service worker might do something in the background, etc. 
  - However, I found it a useful place to start when I was building my understanding.
- when we manage our state, we create an explicit data structure (in my case, an object with a key named ‘errors’) to record the outcomes of the user’s actions.
- State management libraries provide us with tools for creating these data structures, and updating them when new actions occur. 
  - For example, with Redux, your state is stored as a JavaScript object. 
  - With MobX, it’s stored as an Observable. 
  - If you use React’s component state, your state could be a string, or a number, or anything you like.

- Without a state management system, how do we know what the state of our application is? 
  - We look at the DOM. We can check DOM elements to see if they have certain classes (‘active’, ‘error’), or to check whether certain elements exist.
- With a state management system, to find out what the state of our application is, 
  - we check our state data structure. 
  - The DOM should reflect the data, but the data is the Source Of Truth.

- **Why would I want to use state management tools?**
  - For me, the key to understanding state management was when I realised that there is always state. 
  - Whether or not I’m managing it, with an interactive web application, there is always state — users perform actions, and things change in response to those actions.
  - State management makes the state of your app tangible(可触摸到的，可感知的，具体的) in the form of a data structure that you can read from and write to. 
  - It makes your ‘invisible’ state clearly visible for you to work with.
  - Rather than looking at the DOM and deducing(推断、追溯) state based on what is there and what is not, an explicit data structure is much easier to understand.
  - When you’re creating larger and more complex JavaScript applications, having explicit data to work with in a predictable way is a huge boon to developers. 
  - It’s much easier to reason about and manipulate, and it’s less bug-prone (though of course, you can still create a lot of bugs with any code you write with a state management system).

- Some bonus benefits to understanding state management
  - Before working with JavaScript frameworks, I had never thought of the actions that a user makes as a holistic(整体的，全面的) group of causes and effects. 
    - The way I had written JavaScript before, it was just a bunch of one-off operations that manipulated the DOM and may or may not have had any relation to each other.
  - I also never saw ‘state’ and the DOM as separate entities from each other — to me, they were the same thing. 
    - In the DOM, there is an error message, so the state is that there is an error message.
  - By separating out the data (there is an error message) from the effects (an error message is displayed on the screen), I found myself thinking about my code in a much more declarative way, which was extremely powerful as I learned more and took a a dive into functional programming.


## ref

- [Simple State Management With Vanilla JS](https://viktorfejes.com/article/simple-state-management-with-vanilla-js)
  - The most important part is that the state shouldn't be updated through its properties but rather using the state.setState() method. 
  - This way it's easy to know using the stateChange() function when the state updates.
