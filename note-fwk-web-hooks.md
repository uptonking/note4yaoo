---
title: note-fwk-web-hooks
tags: [hooks, web]
created: '2020-11-14T18:57:59.777Z'
modified: '2020-12-08T13:29:40.625Z'
---

# note-fwk-web-hooks

# guide

- hooks的js实现
  - lighterhtml和neverland

# hooks-blog

## [TinyJSX](https://github.com/stanchino/tiny-jsx)

- TinyJSX is a lightweight UI JavaScript library for developing user interfaces using functional components.
- TinyJSX exposes an API which mimics the recent React Hooks implementation but is really small.
- TinyJSX supports only functional components.

``` JS
import TinyJSX from 'tiny-jsx';
import { render } from 'tiny-jsx/dom';
import useEffect from 'tiny-jsx/hooks/useEffect';
import useState from 'tiny-jsx/hooks/useState';

function Clock() {
  const [tick, setTick] = useState(0);
  useEffect(() => {
    const interval = setInterval(() => {
      setTick(tick + 1);
    }, 1000);
    return () => clearInterval(interval);
  }, [tick]);

  return (
    <div>Seconds: {tick}</div>
  );
}

render(<Clock />, document.body);
```

## [A Critique of React Hooks_202004](https://dillonshook.com/a-critique-of-react-hooks/)

1. More Stuff to Learn
  - The problem with learning about hooks is that they're not generally applicable knowledge about computing or programming. 
  - They're a React-specific thing. 
  - In 5-10 years when you're programming something completely different, your knowledge of hooks will be completely obsolete.

2. They Don't Interoperate With Class Components
  - you could create a HOC to wrap your component and pass down the hooks functionality. 
  - This creates a lot of boilerplate and doesn't compose well though. 
  - The only sustainable option is to suck it up and convert that class component to a FunctionComponent.  

3. Ecosystem Challenges
  - As a library consumer, what happens when you need to upgrade a library but it made the choice to only support hooks? 
  - As the ecosystem evolves and adopts hooks you'll be coerced more and more into using them. 
  - This is another argument for reducing your dependencies but that's a story for another day.

4. The Rules of Hooks Limit Your Design
  - In this case I think the best solution is to refactor all these hooks to not be hooks 
    - and just regular functions that take their dependencies explicitly so that you can call them inline like in the second example 
    - and the dependency array for useMemo is manageable.
  - These sorts of battles with how you have to organize your code in a world of hooks is common, 
  - and it can take a lot of iteration, thought, and time to come up with a design that feels good.

5. They Complicate Control Flow
  - Using a few useState hooks is pretty easy to understand, 
  - but once you start needing to use all the other kinds of hooks up and down the component tree, it becomes very difficult to follow the execution order of your code

6. In Conclusion
  - I'm not asking you to never use hooks or remove them from your project. 
  - As I said in the intro, I would still use hooks in a new project, and I think they do improve the prior situation of HOC's creating component hierarchies deeper than the Mariana Trench. 
  - But I also think they're not the "Computing Promised Land". It might be a while before we get there though.
  - So until then, just use them judiciously.
  - P. S. Library authors, please try to keep things simple!

- They break semantic of the function. 
  - Cant use loops, if-else ... Especially this is bad for juniors developers.

- [reddit: A Critique of React Hooks ](https://news.ycombinator.com/item?id=22995928)
- Hooks are an elegant & clever idea but they can be difficult to use in practice. 
  - You really need to understand in detail how closures work. 
  - Manually managing your dependency graph and memoizing in all the right places is harder than the old class-based model in my experience.
- How objects work: 
  - there's a lookup table for methods and properties associated with your instance to find them by name (or call signature, or whatever).
- How hooks work: 
  - there's a lookup array associated with your instance (yes, an instance of an object—read the code if you're skeptical, and besides functions are objects in JS anyway so even if I'm wrong, which I'm not, I'm technically right) to find properties and methods by reference order(!?!)
  - Hooks are just a crippled implementation of objects with weird syntax. 
  - In a language that already has non-crippled ones built in with less-weird syntax.
- It's storing all the hooked-in functions (methods) and variables (properties) outside the function and associating them with the relevant React view object instance at run-time, which is effectively the hooks' "this". 
  - Unless the code's change substantially and in very fundamental ways since it was introduced. 
  - It doesn't bring to mind closures, at least as I read it. 
  - It very much brings to mind object/class-system implementations.
- I don't think FP purity is the point of hooks, the advantage is the ability to compose them, more easily than HOCs.

## [How to Create Hooks In Javascript – A Beginner’s Guide_202009](https://code-boxx.com/create-javascript-hooks/)

- Hooks are usually used to intercept(拦截；阻拦) procedures, and possibly change the way they act. 
- But hooks are not natively supported in Javascript, we can only simulate hooks using functions and events

- In computer programming, the term hooking covers a range of techniques used to 
  - alter or augment the behaviour of an operating system, of applications, or of other software components 
  - by intercepting function calls or messages or events passed between software components.

- We can add a hook before the AJAX call to disable the submit button, to prevent the user from submitting multiple times.
  -  We can also add another hook after the AJAX call to show the results of the process, to re-enable the submit button.
- We could have just created a single simple function to do all of these. 
  - Why go through all the trouble to create so many functions, so much of all these roundabout useless hooks thing?
  - The keywords here are reusability, extensibility, and flexibility. 
  - The AJAX function here is a common core function – We use it whenever we need to do an AJAX call to the server, and it could be shared among hundreds of other functions; 
  - We do not want to modify this core function, but to extend the usability of it, which is where hooks step in.

- Isn’t the above example the same as a callback or event? 
- Well yes, these 3 are relatives but totally different ideas altogether:
  - Events are fired when certain things happen – Mouse click, keyboard press, finished loading, etc.
  - Callbacks are functions that we put into another function to complete a certain task.
  - Hooks intercept the process and may interrupt the normal process.
- Javascript does not have a native hook implementation.
  - So the only “hook” that we can “build” in Javascript is achieved with events and/or callbacks.

- We are simply inserting `if` to simulate a hook where it is required, and creating the respective “hook functions”.

``` JS
// (A) "HOOKED" AJAX FUNCTION
function doAJAX(url) {
  // (A1) BEFORE HOOK
  if (typeof before == "function") { before(); }

  // (A2) DO AJAX CALL
  var xhr = new XMLHttpRequest();
  xhr.open('POST', url);

  // (A3) AFTER HOOK - SERVER RESPONSE
  if (typeof after == "function") { xhr.onload = after; }
  xhr.send();
}

// (B) CREATE HOOKS
function before() {
  document.getElementById("demoA").style.color = "red";
}

function after() {
  document.getElementById("demoA").innerHTML = this.response;
}

// (C) GO!
doAJAX("1b-dummy.html");
```

- using custom events to simulate hooks.

``` JS
// (A) "HOOKED" AJAX FUNCTION
function doAJAX(url) {
  // (A1) BEFORE HOOK
  window.dispatchEvent(new CustomEvent('b4ajax'));

  // (A2) DO AJAX CALL
  var xhr = new XMLHttpRequest();
  xhr.open('POST', url);

  // (A3) AFTER HOOK - SERVER RESPONSE
  xhr.onload = function() {
    window.dispatchEvent(new CustomEvent('aftajax', { detail: this.response }));
  };
  xhr.send();
}

// (B) SET HOOKS
window.addEventListener("b4ajax", function() {
  document.getElementById("demoA").style.color = "red";
});
window.addEventListener("aftajax", function(evt) {
  document.getElementById("demoA").innerHTML = evt.detail;
});

// (C) GO!
doAJAX("1b-dummy.html");
```

- Hooks are not natively available in Javascript. 
  - We can only simulate “hook-like” behaviors using various techniques. 

- we simply introduce another var hooks hook handler, and that will do all the magic to “queue” the hook functions and organize them properly.

``` JS
// (A) MULTIPLE HOOKS HANDLER
// Credits to https://jsbin.com/joxigabeyi/edit?js,console
var hooks = {
  // (A1) CURRENT HOOK QUEUE
  queue: {},

  // (A2) ADD FUNCTION TO QUEUE
  add: function(name, fn) {
    // name : name of function to add hook to
    // fn : function to call

    if (!hooks.queue[name]) { hooks.queue[name] = []; }
    hooks.queue[name].push(fn);
  },

  // (A3) CALL A HOOK
  call: function(name, ...params) {
    // name : name of function to add hook to
    // params : parameters

    if (hooks.queue[name]) {
      hooks.queue[name].forEach(fn => fn(...params));
      delete hooks.queue[name];
    }
  }
};

// (B) "HOOKED" AJAX FUNCTION
function doAJAX(url) {
  // (B1) BEFORE HOOK
  hooks.call("beforeAJAX");

  // (B2) DO AJAX CALL
  var xhr = new XMLHttpRequest();
  xhr.open('POST', url);

  // (B3) AFTER HOOK - SERVER RESPONSE
  xhr.onload = function() {
    hooks.call("afterAJAX", this.response);
  };
  xhr.send();
}

// (C) SET HOOKS
hooks.add("beforeAJAX", function() {
  document.getElementById("demoA").style.color = "blue";
});
hooks.add("beforeAJAX", function() {
  document.getElementById("demoA").style.background = "lightblue";
});
hooks.add("afterAJAX", function(res) {
  document.getElementById("demoA").innerHTML = res;
});
hooks.add("afterAJAX", function() {
  document.getElementById("demoA").innerHTML += "FOO BAR!";
});

// (D) GO!
doAJAX("1b-dummy.html");
```

- HOOKS VS CALLBACK VS EVENTS
  - Events are fired when something happens, 
    - and we write blocks of code to deal with the situation.
  - A callback is a function that is passed into another function to complete the routine.
  - Hooks are interceptors. 
    - They interrupt the normal process 
    - and we usually place them before the function starts, or just before the function ends

## [Javascript Hook System](https://coderwall.com/p/tfmxya/javascript-hook-system)

- I have written a little hook/plugin system for Javascript 
  - as I needed to have a base class which other developers could then hook their functions into prior to other functionality running.
  - https://github.com/mailpoet/WP-JS-Hooks
    - A lightweight JavaScript event manager for WordPress
    - Vanilla JS with no dependencies
    - Hooks with lower integer priority are fired first.
    - Utilizes insertion sort for keeping priorities correct. Best Case: O(n), worst case: O(n^2)

``` JS
var ClassName = function() {
  //Construct Stuff
}

ClassName.prototype.hooks = new Array();

ClassName.prototype.setHook = function(hook, args) {
  // {Hook Name : { Func: args }}
  InstanceOfClass.hooks.push({ 'hook': hook, 'args': args });
}

ClassName.prototype.getHook = function(hook) {

  var hookArray = InstanceOfClass.getHooks();

  for (var i in hookArray) {

    if (hookArray[i].hook == hook) {
      var argsKeys = Object.keys(hookArray[i].args);
      return InstanceOfClass[argsKeys[0]].apply(ClassName, hookArray[i].args);
    }
  }
  return null;
}

ClassName.prototype.getHooks = function() {
  return InstanceOfClass.hooks;
}

// ====== Usage ======

ClassName.prototype.preMethod = function() {
  var InstanceOfClass = new ClassName();

  InstanceOfClass.setHook('MY_HOOK', { 'SomeOtherMethod', [params] });
}

ClassName.prototype.myMethod = function() {
  var InstanceOfClass = new ClassName();

  // Will fire off the method by hook
  InstanceOfClass.getHook('MY_HOOK');
}
```

## [Reactive UI’s with VanillaJS – Part 1: Pure Functional Style](https://css-tricks.com/reactive-uis-vanillajs-part-1-pure-functional-style/)

- Part1: Pure Functional Style
- Part2: [Class Based Components](https://css-tricks.com/reactive-uis-vanillajs-part-2-class-based-components/)

- In this pair of posts, I delve(探索；探究) into a middle ground: writing reactive-style UI’s in plain old JavaScript – no frameworks, no preprocessors.

- If you’ve ever used a templating engine like Handlebars or Swig, their syntax looks pretty similar to function-style React code.
- In this pair of posts, our target use case is websites that might otherwise be static, but would benefit from JavaScript-based rendering were it not for the overhead of setting up a framework like React. Blogs, forums, etc.

# ref

- [Emulating React and JSX in Vanilla JS](https://www.toptal.com/javascript/emulating-react-jsx-in-vanilla-javascript)
  - Working directly with the DOM works and gets the job done, 
  - but it also makes constructing the page very verbose, especially when we need to add HTML attributes and nest nodes. 
  - So, the idea would be to capture some of the benefits of working with technologies like JSX and make our lives simpler. 
  - The advantages we are trying to replicate are the following:
    - Write code in HTML syntax so that the creation of DOM elements becomes easy to read and modify.
    - Since we aren’t using an equivalent of virtual DOM like in the case of React, we need to have an easy way to indicate and keep track of the nodes we are interested in.
  - The idea is simple but powerful
    - we send the function the HTML we want to create as a string, 
    - in the HTML string we add a `var` attribute to the nodes we want to have references created for us. 
    - The second parameter is an object in which those references will be stored. 
    - If not specified we will create a “nodes” property on the returned node or document fragment (in case the highest hierarchy node is more than one).
  - The function works in three steps:
    - Create a new empty node and use innerHTML in that new node to create the entire DOM structure.
    - Iterate over the nodes and if the var attribute exists, add a property in the scope object that points to the node with that attribute.
    - Return the top node in the hierarchy, or a document fragment in case there are more than one.
  - This approach also separates building the DOM structure and inserting the data into separate steps 
    - which helps with keeping the code organized and well structured. 
    - This enables us to separately create the DOM structure and fill-in (or update) the data when it becomes available.
  - you can also use hyperHTML which uses native DOM
- [PHP Hooks – The Complete Beginner’s Guide_201902](https://code-boxx.com/php-hooks-beginners-guide/)
  - PHP does not implement the use of hooks natively; 
  - Wordpress, Drupal, and whatever package that you use has their own version of a “simulated hook”. 
