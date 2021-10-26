---
title: lib-fwk-reef-blog-state
tags: [blog, reef, state]
created: '2020-11-04T17:58:48.042Z'
modified: '2020-12-08T13:26:42.816Z'
---

# lib-fwk-reef-blog-state

# [State-Based UI series](https://gomakethings.com/series/state-based-ui/)

- Here’s my complete series on building a reactive state-based UI library. 
- It gets into how today’s most popular frameworks work under-the-hood.

## [How to create a state-based UI component with vanilla JS_202005](https://gomakethings.com/how-to-create-a-state-based-ui-component-with-vanilla-js/)

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
  - 将状态数据、dom模版封装在一个组件模块中更容易复用
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

## [How to create a reactive state-based UI component with vanilla JS Proxies_202005](https://gomakethings.com/how-to-create-a-reactive-state-based-ui-component-with-vanilla-js-proxies/)

## [How to batch UI rendering for better performance_202005](https://gomakethings.com/how-to-batch-ui-rendering-in-a-reactive-state-based-ui-component-with-vanilla-js/)

## [DOM diffing with vanilla JS_202005](https://gomakethings.com/dom-diffing-with-vanilla-js/)

## [State-based components with vanilla JS_201807](https://gomakethings.com/state-based-components-with-vanilla-js/)

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

## [State based UI vs Manual DOM Manipulation_201901](https://gomakethings.com/state-based-ui-vs.-manual-dom-manipulation/)

- State is data at a particular moment in time. 
  - It’s the present “state” of your data.
- Manual DOM manipulation
  - Let’s say you have a really simple list-making app. 
  - It lets you add items to a list and literally nothing else.

``` HTML
<form id="add-to-list">
  <label for="list-item">What do you want to add to your list?</label>
  <input type="text" id="list-item">
  <button>Add to your list</button>
</form>

<ul id="list"></ul>
```

``` JS
document.addEventListener('submit', function(event) {

  // Make sure our #add-to-list form was the one submitted
  if (!event.target.matches('#add-to-list')) return;

  // Prevent default
  event.preventDefault();

  // Get the list item
  var item = event.target.querySelector('#list-item');
  if (!item || item.length < 1) return;

  // Add it to the DOM
  var list = document.querySelector('#list');
  var li = document.createElement('li');
  li.textContent = item.value;
  list.appendChild(li);

  // Clear the input
  item.value = '';
  item.focus();

}, false);
```

- What’s wrong with manual DOM manipulation?
  - For simple apps like this, manual DOM manipulation is a perfectly valid way to do things.
  - But things get really complicated, really quickly once you start adding more features and functionality.
  - Every time a user clicks a button—to add a new item, delete an item, edit an item, and so on—you would need to target specific elements in the DOM an manipulate them. 
  - There’s a lot of ways for things to go wrong.

- With a state-based UI approach, you store all of the data in a JavaScript object.
  - Then, you use JavaScript to build the DOM based on the current data state.
  - You don’t bother trying to figure out what needs to change in the DOM. 
  - You instead say, “given our data, this is how the DOM should look.” 
  - Then you render an updated layout.
  - This is how frameworks like React and Vue work. But you don’t need a 30kb framework to do this.

## [State-based UI with vanilla JS_201902](https://gomakethings.com/state-based-ui-with-vanilla-js/)

- To make state-based ui, we need three things:
  - A data object.
  - A template for how the UI should look based on different data states.
  - A function to render the template into the DOM.
- This is, at a high level, how bigger JS frameworks like React and Vue work, too. 
- We’ll be pulling out some of their conventions and approaches into small vanilla JS helper functions instead.

- The original starting markup had an empty unordered list that we added list items to.
- With a state-based UI approach, we’ll add the unordered list dynamically only if there are list items to show.
- Otherwise, we’ll display a welcome message to the user.
- For our super simple app, we only need one property in our data object: listItems. 
  - By default, it will be an empty array that will eventually hold our list items.
- When working with dynamic data, the template should be a function that returns a string. 
  - When called it, it will use the data object to create a markup string.
- Now, we’re ready to render our UI into the DOM.
  - Inside our `render()` function, we’ll find the #list element in the DOM. 
  - Then we’ll set its `innerHTML` to the output of our `template()` function.

``` JS
var data = {
  listItems: []
};

var template = function() {
  // If there are no list items
  if (data.listItems.length < 1) return '<p><em>You do not have any list items yet. Try adding one with the form above.</em></p>';

  // If there are
  return '<ul>' + data.listItems.map(function(item) {
    return '<li>' + item + '</li>';
  }).join('') + '</ul>';
};

var render = function() {
  var list = document.querySelector('#list');
  if (!list) return;
  list.innerHTML = template();
};

document.addEventListener('submit', function(event) {
  // Make sure the submitted form was for our list items
  if (!event.target.matches('#add-to-list')) return;

  // Stop the form from submitting
  event.preventDefault();

  // Get the list item
  var item = event.target.querySelector('#list-item');
  if (!item || item.length < 1) return;

  // Update the data and UI
  data.listItems.push(item.value);
  render();

  // Clear the field and return to focus
  item.value = '';
  item.focus();

}, false);
```

- Now we’re ready to add some interactivity.
- Like with the manual approach, we still need our event listener. 
  - But instead of manually injecting elements into the DOM, we’ll add items to our data object and render the UI again.
  - One thing about this approach is that while sighted users can see when things in the UI change, someone using a screen reader might not know about them.

- When using `innerHTML` with user-provided or third-party data, you can expose yourself to cross-siting scripting attacks. There are two ways to fix this:
  - Strip all HTML out of the user data using a helper function.
  - Use a library like `DOMPurify` to remove malicious code in your template.
- If the third-party content can have markup in it, option two is your best bet. 

- The state-based UI approach makes it much easier to bolt in features.
  - For example, let’s say we wanted to save our data to `localStorage`. 
  - In the `render` method, we can save our updated state every time a new render happens.
- Before our initial render, we can check for data in localStorage and update the data object with it.

``` JS
var render = function() {
  // Render the UI
  var list = document.querySelector('#list');
  if (!list) return;
  list.innerHTML = template();

  // Save to localStorage
  localStorage.setItem('list', JSON.stringify(data));
};
```
