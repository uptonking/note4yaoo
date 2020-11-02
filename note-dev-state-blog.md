---
title: note-dev-state-blog
tags: [blog, dev, state]
created: '2020-11-02T05:18:43.747Z'
modified: '2020-11-02T05:19:40.469Z'
---

# note-dev-state-blog

## state-blog

### [State-based components with vanilla JS](https://gomakethings.com/state-based-components-with-vanilla-js/)

- State is data at a particular moment in time. 
  - It’s the present “state” of your data.
- If you’ve done simple DOM manipulation before, you’ve probably gone through the task of:
  - Getting an element from the DOM (using `querySelector()` or something similar), and then…
  - Adding content with `innerHTML`, or…
  - Using `classList` to add or remove classses, or…
  - Using `style` to update some styles.
- This works, but as your apps grow, it can be tedious to manage.
- Today’s more popular JavaScript frameworks, including React and Vue, use state and components to make managing the UI easier.
- With this approach, instead of targeting specific elements in the DOM and adjusting a class here or a style there, you treat your data, or state, as the single source of truth.
- Updated your state, render a fresh copy of the UI based on the new data, and move on. 
- You never have to think about which element in the DOM to target or how it needs to change.
- In the previous example, the state was a global object that any function can access.
- To give your code more structure, you might instead scope state to your component. 
  - This is how React, Vue, and other popular frameworks do things.

``` typescript
// This is a simple Component
var greeting = function () {
	return '<p>' + greeting.data.greeting + ', ' + greeting.data.name + '!</p>';
};

// This is the state
greeting.data = {
	greeting: 'Hello',
	name: 'there'
}

// We can render it like this
var app = document.querySelector('#app');
app.innerHTML = greeting();
```

- In this example, the data or state is a property of the component itself. 
  - The state is only accessible within (or is scoped to) the component.
- The nice thing about scoping state to a component like this is that you get out of the business of targeting individual elements and manipulating specific things within them.
- With a scoped component, you update your state and then render your template. You don’t need to hunt for individual items.
- Your data is the single source of truth, and it makes updating the UI easier and more consistent.

- [A stateful component helper function for vanilla JS](https://gomakethings.com/a-stateful-component-helper-function-for-vanilla-js/)
- I’m going to show you a small helper function that makes creating stateful components (and rendering them into the DOM) easier, without having to rely on a big framework or library. 

``` JS
// Create a clock component
var clock = new Component('#clock', {
  data: {
    time: new Date().toLocaleTimeString()
  },
  template: function(props) {
    return 'The time is ' + props.time;
  }
});

// Render the clock
clock.render();

// Update the clock once a second
window.setInterval(function() {
  clock.data.time = new Date().toLocaleTimeString();
  clock.render();
}, 1000);
```

### [Build a state management system with vanilla JavaScript_2018](https://css-tricks.com/build-a-state-management-system-with-vanilla-javascript/)

- https://github.com/hankchizljaw/vanilla-js-state-management

- Traditionally, we’d keep state within the DOM itself or even assign it to a global object in the window
- Libraries like Redux, MobX and Vuex make managing cross-component state almost trivial(微不足道的，不重要的)
- We’re creating the functionality that allows other parts of our application to subscribe to named events.
- Another part of the application can then publish those events, often with some sort of relevant payload.
- The PubSub pattern loops through all of the subscriptions and fires their callbacks with that payload.
- Let’s take a look at how our Store object keeps track of all of the changes. We’re going to use a Proxy to do this
- Usage of DOM Api will prevent possible SSR
