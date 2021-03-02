---
title: thread-lang-js-ts
tags: [js, lang, typescript]
created: '2021-01-28T14:33:59.037Z'
modified: '2021-01-28T14:34:20.579Z'
---

# thread-lang-js-ts

# pieces

- ## 

- ## All JavaScript functions should only be allowed to take one argument. 
- https://twitter.com/swyx/status/1198632709834326021
  - Take an object if you need to pass more than one piece of data.
  - Order independent
  - More Greppable codebase
  - Low cost of adding API
  - predictable pointfree JS
  - you already do this in @Reactjs as "props"
- i've been calling this the "Single All The Way" rule
  - there's a backend version of this too
  - Someone already coin the term for this philosophy, it's called RORO (Retrieve Object, Return Object). 
- In that way you lose currying unless you implement one that works with object
- Note that if the object is not persisted/wrapped in a closure, V8 will optimize that away. It’s pretty amazing. 
  - There are quite few more rules to it, so using multiple args might be better for performance sometimes.
- controversial controversial opinion: object destructuring should not be done in the function's params
  - I like destructuring in the arguments, but one pro to the latter form is that they're consts and the destructured ones are not (and, apparently controversial, but I think everything should be const unless you plan on reassigning it).
- I’m applying this rule when a function has more than 2 arguments, but applying to _every_ function is like too much.
- But React components are called with two arguments.
- This is where I love named params in swift. Wish JS had that.
- I’ve mostly only use positional args for either construction/dependency closure or in cases where partial application is expected.
  - Though an argument can be made that partial application is better served by a function that returns a function in many cases.
- Deno (typescript runtime) has it in their style guide of 3 args max, with the 3rd arg being an object if more than 3 properties are required.
- Yup, the 1 argument is better, especially the bigger the codebase is. Same reasoning applies to C#.
- Except lots of built in callbacks take two.

- ## I’m starting to have an opinion that *every* JS/TS function that takes more than one argument should take an object instead
- https://twitter.com/tlakomy/status/1362828075390631936
  - Better IDE support, code completion and you’ll never screw up the order of arguments
- I still prefer two args when there is a main argument and I put the rest in the second. eg: `format(code, options)` .
  - I hate losing myself in custom types for each function param object
- There is a pattern for that, its name is RORO (receive an object, return an object)
  - [Javascript RORO pattern - A nice way to write more readable functions](https://www.tinyblog.dev/blog/2020-07-13-javascript-roro-pattern/)
  - Receive an Object, Return and Object
  - functions should always accept an object as their parameters and they should always return an object as their result.
  - Receiving an Object as standard for all the functions I write is something I started doing after learning Python and getting experience with kwargs, which I greatly enjoyed since it made it so easy to know what was going into a function
  - I personally get a lot less utility of Return an Object than I do Receive an Object. 
  - Multiple return items are pretty nice, but I find that most functions I write only concern themselves with a single thing.
- One potential downside is that if you do not make the object properties readonly, the incoming object is mutable. 
  - This is not the case with non-object parameters since they are passed by value, not by reference.
- I find the pattern of having a max of two args a good balance: first is required and the second is optional. 
- Been doing this for years. 
  - The only exceptions are extremely rare: functions which implement unary or binary operators, which by definition are future proof. 
  - Another advantage in @typescript : it naturally encourages using named interfaces, making them readable and composable.
- I often follow this pattern as well, much more predictable for end user/third party and you can build in default behavior for undefined configuration options
- only downside is having to repeat every argument twice for TS declarations
- better for extending APIs without breakages as well. it’s the closest thing we have to named function parameters (yet)
  - I am absolutely of the same opinion. Also the extension or modification is much easier.
- Every time I don't make a function that accepts an object, I find myself regretting it so hard in the future 
- In @PixiJS we've been doing more of this. There are some APIs with perplexingly long args for historical reasons.
  - I only favor args when it really the logical order is baked-in, eg. setPosition(x, y) 
- The main advantage of the object arg is that it's super easy to refactor. 
  - Imagine you need to change the order, or add some optional arg
- I would prefer a python way. They have positional and named arguments at the syntax level.

- ## Totally shocked that there's no refactoring to reorder arguments in VS Code for TypeScript.
- https://twitter.com/BenLesh/status/1366543595172470786
  - I get that with type overloads and rest args it's tricky
- Not a problem if you avoid positional arguments altogether and use a single object instead.
  - That's fine for apps, but unfortunately if you're developing a library that needs to be memory sensitive and lower level, you probably don't want to do that.
  - I agree that for hot code GC pressure can be a consideration to opt for positional arguments over POJOs at each call site.
- I would love so much that TypeScript have a transpiled named parameters feature

- ## Performance tip: if you're working with *large* objects (10KB and larger), it'll be way faster to parse them as JSON strings rather than consuming them directly in your JavaScript as objects
- https://twitter.com/mgechev/status/1366259446154989569
  - because json grammar is uch simpler than js grammar
  - json can be parsed more efficiently than js.
- not for GTA apparently

- ## is there a way to wait for N promises on tests?
- https://twitter.com/sseraphini/status/1365297469911937025
  - I have a test that will receive N messages and process each of them using an async code
  - so I need to wait N process to be processed to do some assertion
- Promise.all() or Promise.allSettled() might be work.
- `await new Promise(setImmediate)` .
  - will this awaits a single promise or all the pending promises?
  - This awaits all promises that are to be resolved in the same event loop

- ## I just realized ternary operator is called that way because it handles THREE things at once
- https://twitter.com/vishwajeetv/status/1365121673922543622
- Personally I am not fan of the reduced readability introduced by ternary operator. I avoided them for years, and even today I use it sparingly. 
  - If else is much more readable and maintainable.
  - Short expressions *should* use the ternary operator.
  - The problem is that if/else is not an expression, but a statement

- ## I think most JS libraries that vend some kind of observable value could just use async iterables instead of an actual observable library.
- https://twitter.com/justinfagnani/status/1360793286781247491
  - Clients mostly need to be able to subscribe and unsubscribe to new values. 
  - The rest isn't strictly needed and a client can pipe the async iterable into their library of choice if they really want.
  - No need for clients to read about rxjs/wonka/zen-observable or whatever is used.
- I think the platform should have added a simple type like observables, instead of a heavy complicated type like AsyncIterables.
  - A promise allocation for each event?
  - No cancellation other than not iterating, ignoring the next event, or rejecting the next event and handling it?
- It always surprised that Angular 2+ went all in on RxJS, while other frameworks could perfectly live with only promises.
  - IMO the choice for RXJS causes a way too high learning curve. 
  - And also are error prone because unsubscribe is sometimes automatically but not always.
- I disagree with things like react being able to live with only promises. 
  - You end up building your own ad-hoc chains in likely buggy async/await code and probably doing it in some complex hook with race conditions or difficult to debug code. 
  - I don't use rxjs but I see the appeal.

- ## Babel gave us an incredibly flexible ecosystem of plugins and presets. TypeScript (as a language) limits you to using whatever language features they choose to implement.
- https://twitter.com/mjackson/status/1361525113175171072
  - It’s always trade-offs when it comes to engineering, but what a price for type safety!
- TS is usually pretty good about implementing features at Stage 3

- ## Writing app TypeScript is *way* easier than writing library TypeScript
- https://twitter.com/tannerlinsley/status/1361159377051262977
- I have written a couple bits of app-level TS that were fairly complex and resembled "lib"-style TS, but it was an internal abstraction that bordered on lib-like.
  - [Thoughts as a Library Maintainer](https://blog.isquaredsoftware.com/2019/11/blogged-answers-learning-and-using-typescript/)
- TS keeps your app consistent. Found a better way to structure some object? Change it and TS tells you all the places you need to fix its usage.
- Generics come in handy quite a lot, but I never reach for them right away. 
  - I just write the code I need and always try to think about how to avoid `any` , and if I end up factoring out reusable stuff at all, generics tend to emerge as the right solution.
- Needing generics in app code tends to be rare. 
  - Typescript is fantastic for defining API boundaries such as component props.
- In our team, we start types without genetics, but add them if we need more reusable parts, and more type safety around those parts. 
  - We try to communicate intent rather than expectation.

- ## Don’t use `delete` to remove a property from an object.
- https://twitter.com/SimonHoiberg/status/1357998820106399744
  - Instead, use the rest operator to create a new copy without the given property.
- Because `delete` mutates the original object, and the spread operator creates a ref to the original, it doesn't mutate it.
- How you will cover eslint error? Age variable is defined but not used.
  - `{ age: _age, ...other}` . Adding _ in front of a variable name tells the linter that it's ok if the variable in not being used
- The object will mutate when you add new properties or modify existing properties, so why decry(批评) only `delete` ?
  - If you want to avoid mutating object, use `Object.freeze()` ?

- ## Did you know that there was a time pre-ES5 where undefined could be globally redefined?
- https://twitter.com/oliverjumpertz/status/1357421013303259142
  - This is where the void operator came in handy. 
  - It forces an expression to return the primitive undefined instead of any overridden value.
- Saw void 0 today generated by TS, was a bit surprised
  - Yea, void 0 is the idiomatic way to enforce undefined

- ## does anyone know if using Symbol, instead of direct properties, is either faster or slower, *especially* in NodeJS or, in general, v8?
- https://twitter.com/WebReflection/status/1356911723920445440
- It made no difference
  - In this benchmark, symbols are 3.2 times slower

- ## I wish JavaScript import statements were written in reverse order so that autocomplete worked properly.
- https://twitter.com/markdalgleish/status/1356404787244195840
  - e.g. from 'lodash' import { debounce }
- Seems like a nice improvement at first glance, but I’m wondering how imports with side-effects could look
  - `from "./styles.css" import *` ; 

- ## Trick—JavaScript superclass that can’t be instantiated 
- https://twitter.com/rauschma/status/1356134928707153920
- why is this pattern useful, when we have structural typing and interfaces? 
  - This is when you do OOP-style abstract superclasses: You want the subclasses to be instantiated, but not the superclass.

- ## Yet again I'm reminded that JavaScript class fields are a bad design
- https://twitter.com/justinfagnani/status/1355665301979897860
  - Define semantics means you can't meta-program over them like other class members, and you can't override them with accessors.
  - Class fields should have been sugar for accessors.
  - ES Classes in general feel like an opportunity to carve out some static niche and forgo metaprogramming altogether.
  - Which really limits them. The list opportunity here is that they don't need to have false equivalences to object literals because they aren't.
- A similar issue is happening for decorators as a decorator won’t be able to convert a field to an accessor unless you prefix with prop, as in: `@example prop field` . 
  - I wonder if this could lead to some `prop field` as sugar to set accessors without the decorator.
  - It’s a workaround and honest I’d just prefer the decorator without prop but that’s the much we can do in the consensus model.

- ## In JavaScript, there are no classes.
- https://twitter.com/SimonHoiberg/status/1355453046617108484
  - t’s syntactical sugar added to please developers from other languages such as Java or C#.
  - Most of the time, they don’t serve a good purpose, and are not really useful.
  - Instead, use modules.
- don’t you think classes help maintain order and principles of programming that have been established over a longer period of time?
- The singleton pattern would like to have a word with you.

- ## Don't use functions as callbacks unless they're designed for it
- https://twitter.com/jaffathecake/status/1355188620932608006
- [Don't use functions as callbacks unless they're designed for it](https://jakearchibald.com/2021/function-callback-risks/)
- Here's the problem:

``` JS
// Convert some numbers into human-readable strings:
import { toReadableNumber } from 'some-library';

// We think of:
const readableNumbers = someNumbers.map(toReadableNumber);
// …as being like:
const readableNumbers = someNumbers.map((n) => toReadableNumber(n));
// …but it's more like:
const readableNumbers = someNumbers.map((item, index, arr) =>
  toReadableNumber(item, index, arr),
);
```

- Everything works great until `some-library` is updated, then everything breaks.
- `toReadableNumber` wasn't designed to be a callback to `array.map`, so the safe thing to do is create your own function that is designed to work with `array.map`
- **The same issue, but with web platform functions**

``` JS
// A promise for the next frame:
const nextFrame = () => new Promise(requestAnimationFrame);

// this is equivalent to:
const nextFrame = () =>
  new Promise((resolve, reject) => requestAnimationFrame(resolve, reject));
```

- **Option objects can have the same gotcha**

``` JS
const controller = new AbortController();
const { signal } = controller;

// it's best to create an object that's designed to be addEventListener options:
el.addEventListener('mousemove', callback, { signal });
el.addEventListener('pointermove', callback, { signal });
el.addEventListener('touchmove', callback, { signal });
// el.addEventListener(name, callback, options);

// Later, remove all three listeners:
controller.abort();

// code below works today, but it might break in future.
const controller = new AbortController();
el.addEventListener(name, callback, controller);
```

- Watch out for functions being used as callbacks, and objects being used as options, unless they were designed for those purposes. 
  - Unfortunately it isn't something TypeScript warns about

- I guess that's probably more relevant when passing your own class functions as callbacks. Anyway, great advice!
  - yes that's a gotcha too, but thankfully it tends to obviously fail straight away

- ## Don't destructure deep properties. Put more on the right side. Use dot notation.
- https://twitter.com/tannerlinsley/status/1354948274281566208
  - Reserve it for smaller functions and variable namespaces.
  - It can *feel* like a productivity hack, but time and experience have taught me the opposite.
  - If you do too much of it unnecessarily, you might find yourself *re*structuring a lot, eg. Taking those same variables and reforming them into functions or other structures. 
  - It's much easier to spread an object than it is to type it all out again.
- I'm saying this because I am literally in the middle of a painful refactor caused mostly by this issue. I only have my yester-self to blame, too. Live and learn, right?
  - I'd add that when you destructure too much - especially down into primitives - then you discard your data model and pass props 1 by 1. When the structure changes, there'd be multiple places to change. If you keep your data model and pass it down, refactors will be cheaper.
- I dislike destructuring because ts won't narrow down the type.
- Destructuring also makes project wide search harder.
  - I want to find if user dot id is used. If I search for the whole term, destructured cases will be missed. If I search only for id, the search will have lot of other results like post id, item id.
  - You can destructure and alias

- ## Using TypeScript without classes feels suboptimal, like I'm using it for something it wasn't designed for. TypeScript really shines with classes and static methods.
- https://twitter.com/BenLesh/status/1354541556234137600
- [To clarify: I'm not advocating programming with classes. ](https://twitter.com/mjackson/status/1354524449706414080)
  - I typically avoid them. There is 1 class in the codebase I'm currently working on, and it's a React class because there is no hook for React error boundaries 
  - I'm just saying, TypeScript seems designed for them.
- That's interesting.
  - I view TS as just a type system on top of JavaScript
  - Classes in TS are just interfaces.
  - TS is all just interfaces, types, and function signatures. 
  - In my head, the actual "class" is a runtime thing.
  - So functions and classes feel pretty much the same to me.
  - Totally agree with everything you said here. I think about it the same way.
  - But there are a few spots where I wish TS had better support for working with functions, like typing a whole module of functions, for example. I could easily do it w/ a class, but not w/ a module.
  - What is a "module of functions"?
  - Just talking about JavaScript modules. There is no way to type all the exports of a module in TypeScript.
  - namespaces are nice for that but unfortunately discouraged because of tree shaking issues (i think...)
  - referring to ECMAScript Modules.
  - Modules =/= Classes.  You can have a javascript file that exports only functions.
- I find it exactly the opposite. 
  - I use plain functions and values 90% of the time with TS and classes only when I really need to (mostly for perf). 
  - Generics are easier to manage with functions too.
  - I do the same thing. There are 0 classes in the codebase I'm currently working on, but sometimes it feels like things would be easier if there were. For example, typing a whole module would be easier using static methods on a class.
  - I don't see how this is different than just plain typed functions?
  - You can't get a type for the whole module, just each individual function.
  - 但是可以通过单独的文件专门导出一个文件中所有的export，虽然可行，但增加了文件数量
  - Clever, but there’s no way to open up a new module and say “this module is one of these” (ie implements an interface)
