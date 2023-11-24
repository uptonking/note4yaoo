---
title: lang-js-base-class-extends
tags: [class, ECMAScript, inheritance, js, lang, object-oriented-programming]
created: 2022-11-23T17:47:26.881Z
modified: 2022-11-23T17:48:48.839Z
---

# lang-js-base-class-extends

# guide

# prototype
- [Public class fields - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields)
  - Public fields are writable, enumerable, and configurable properties. 
  - As such, unlike their private counterparts, **they participate in ~~prototype~~ inheritance**.
# examples

# discuss

- ## 

- ## 

- ## I think classes make more sense for a component model than functions
- https://twitter.com/passle_/status/1727733249844064534
- Classes are okay *in general* for a component model, but if we’re talking about React, I don’t miss needing to use componentWillReceiveProps where we now use useEffect.
- Classes don't compose, which is kind of a deal breaker for components.
- Classes are fine, but I'm not sure coupling state instantiation and render was ever a good approach.

- ## Change my mind: The “this” keyword in JavaScript has gotten a bad wrap.
- https://twitter.com/jpschroeder/status/1712500964085670069
  1. It really isn’t hard to understand.
  2. It provides a native mechanism for instance data (like context).
  3. JavaScript has native tools for it like apply, bind, and arrow fns.

- I don't mind "this", especially with arrow funcs. 
  - But function params + closures to capture instance data are such nicer patterns for dealing with objects. 
  - "this" is only best for dealing with inheritance, which is not great.
- 
- 

- ## I'm beginning to think we will be "stuck" with class components in @Angular for the long term. 
- https://twitter.com/brandontroberts/status/1711110538103558207
  - This is not necessarily bad, but it shows that the community isn't very open to such a change, which is unfortunate.

- As long as Angular never has JSX.  Zoneless and server only routes will go a long way... ready for that
- i don't understand this sentiment tbh. jsx is the clean solution. separation of concern means separating state from view, NOT code from view. angular cuts the viewlayer in two, it looses scope and has to make up an arbitrary language, only to mend the two halves together again but now code is masked as html. it just never made any sense whatsoever and it clearly held it back.
  - code and the view logically belong together, there can be no separation between them because they both belong to the view layer. that was one thing react realized, hate it for everything else but not for solving templating.
- Zoneless is coming at some point. I dunno about server-only routes being a thing in Angular.
  - not necessarily like server components, just api routes or endpoints like Svelte, Solid Start, and all others, also need to separate server only code like load, serversideprops to not load extraneous js in the browser

- There are zero benefits to using classes but it adds a ton of ceremony and mental overhead.

- classes  aren't inherently bad, but Angular doesn't do them any favors, and React did classes real dirty.

- Classes are JS-native containers of behavior and state, which is exactly what components need.
  - The pain points I see with classes are around composition + multi inheritance. If you’re in a disciplined team familiar with OOP patterns you won’t see any issues. Otherwise, classes just tend to grow out of control. In general it’s easier to split up a function than a class
- Functional programming style is just more popular right now
-  I love class based for state containers, but for things like data pipelines and data manipulation, I really like FP

- I've never understood the resistance to class based components - it's the only way components are created everywhere other than the web, because it just makes sense. 

- Where else do you see classes being primarily used besides web components? React, Svelte, Vue, Solid? None use them primarily
- In the JavaScript ecosystem, Angular is the only one that nowadays is using classes heavily. A good portion of the ecosystem is using functional approaches instead. I don’t understand, why Angular is not there.

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

- ## No, js classes have never been just sugar, various things are better/different.
- https://twitter.com/WebReflection/status/1380809258095247360
- [JS classes are not “just syntactic sugar”](https://webreflection.medium.com/js-classes-are-not-just-syntactic-sugar-28690fedf078)

- ## You'll never convince me that: `fn({ // One thousand random things here })` Is better than a class.
- https://twitter.com/matthewcp/status/1380610388467793920
- This is so prevalence with web component libraries, and I just don't get it.
  - How is writing special object properties named "props" and "methods" any better than using plain class fields and methods? Just to avoid the class keyword? It's so weird.
- There’s no problem with classes per se, the problem is subclassing. 
  - A struct with a million random things is fine compared to a function with a million random things. 
  - The issue is wrangling covariance/contravariance, jumping between definitions of overridden methods, etc.
- You'll never convince me that 1, 000 random things in a class is better than 1, 000 random things in a function.
  - 1, 000 random things anywhere is bad.
- I like classes, as long as I don't do any inheritance with them.
  - What I don't like is the sea of `.this` that easily ends up being almost 50% of the code. I'd rather take a `<div>` soup or a HOC hell anytime.

- ## Classes were a good addition to JS. Private fields I'm more skeptical about—mostly because classes are not a good level for managing visibility, modules are.
- https://twitter.com/MarijnJH/status/1408004016752283648

- ## Some people still think that JavaScript classes are just sugar for prototypes, even though that was never actually true and is most definitely not true now.
- https://twitter.com/justinfagnani/status/1524481337855410176
- Class fields for instance
