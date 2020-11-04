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

### [How to create a state-based UI component with vanilla JS_202005](https://gomakethings.com/how-to-create-a-state-based-ui-component-with-vanilla-js/)

- With State-based UI, you use your state or data to create your UI.
- Rather than trying to target and manipulate elements in the DOM when the user does things, you update your data object. 
  - Then, in a template, you say, “If the data looks like this, do this. If it looks like that, do that instead.”
  - Then, you can render the HTML string into the UI using the innerHTML property.

``` JS
var template = function(props) {
  return `
		<h1>${props.heading}</h1>
		<ul>
			${props.todos.map(function (todo) {
				return `<li>${todo}</li>`;
			}).join('')}
		</ul>`;
};

var app = document.querySelector('#app');
// Returns an HTML string
app.innerHTML = template(data);
```

- The approach above works, but it would be nice to have a component we can use over-and-over again with different elements, data, and templates.
- Let’s start by creating a new component using a constructor pattern
- In our constructor function, we’ll accept a selector for the element to render our template into, our data, and our template.

``` JS
var Rue = function(options) {
  this.elem = document.querySelector(options.selector);
  this.data = options.data;
  this.template = options.template;
};
Rue.prototype.render = function() {
  this.elem.innerHTML = this.template(this.data);
};

var app = new Rue({
  selector: '#app',
  data: {
    heading: 'My Todos',
    todos: ['Swim', 'Climb', 'Jump', 'Play']
  },
  template: function(props) {
    return `
			<h1>${props.heading}</h1>
			<ul>
				${props.todos.map(function (todo) {
					return `<li>${todo}</li>`;
				}).join('')}
			</ul>`;
  }
});
app.render();

// Add a new item to the data
app.data.todos.push('Take a nap... zzzzz');
// Render an updated UI
app.render();
```

### [State based UI vs. manual DOM manipulation_201901](https://gomakethings.com/state-based-ui-vs.-manual-dom-manipulation/)

- State is data at a particular moment in time. 
  - It’s the present “state” of your data.
- What’s wrong with manual DOM manipulation?

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
