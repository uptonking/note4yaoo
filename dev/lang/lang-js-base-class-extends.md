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

- ## 

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
