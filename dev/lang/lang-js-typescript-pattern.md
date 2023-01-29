---
title: lang-js-typescript-pattern
tags: [lang, pattern, typescript]
created: 2021-03-22T14:42:21.776Z
modified: 2021-03-22T14:43:12.866Z
---

# lang-js-typescript-pattern

# guide

- [JavaScript Patterns Workshop](https://javascriptpatterns.vercel.app/patterns)
  - rendering, performance, react
# [Declaration Merging](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)
- “declaration merging” means that the compiler merges two separate declarations declared with the same name into a single definition. 
  - This merged definition has the features of both of the original declarations. 
  - Any number of declarations can be merged; it’s not limited to just two declarations.
- The simplest, and perhaps most common, type of declaration merging is interface merging. 
  - At the most basic level, the merge mechanically joins the members of both declarations into a single interface with the same name.
- Non-function members of the interfaces should be unique.
  - The compiler will issue an error if the interfaces both declare a non-function member of the same name, but of different types.
  - For function members, each function member of the same name is treated as describing an overload of the same function. 

- classes can not merge with other classes or with variables

- For information on mimicking class merging, see the Mixins in TypeScript section.

- Although JavaScript modules do not support merging, you can patch existing objects by importing and then updating them.

```typescript
// observable.ts
export class Observable<T> {
  // ... implementation left as an exercise for the reader ...
}

// map.ts
import { Observable } from "./observable";
declare module "./observable" {
  interface Observable<T> {
    map<U>(f: (x: T) => U): Observable<U>;
  }
}
Observable.prototype.map = function (f) {
  // ... another exercise for the reader
};

// consumer.ts
import { Observable } from "./observable";
import "./map";
let o: Observable<number>;
o.map((x) => x.toFixed());

```

# string

# object

# data-type

# function

- ## [TypeScript Function Syntaxes](https://kentcdodds.com/blog/typescript-function-syntaxes)

- ts基础用法小结
- Function declarations
- Function Expression
- Optional/Default params
- Rest params
- Object properties and Methods
- Classes
- Modules
- Overloads
- Generators
- Async
- Generics
- Type Guards
- Assertion functions
- Conclusion

```typescript

// Simple type for a function, use =>
type FnType = (arg: ArgType) => ReturnType
// Every other time, use :
type FnAsObjType = {
  (arg: ArgType): ReturnType
}
interface InterfaceWithFn {
  fn(arg: ArgType): ReturnType
}
```

- Given the choice between type, interface, and declare function, I think I prefer type personally, unless I need the extensibility that interface offers. 
  - I'd only really use declare if I really did want to tell the compiler about something that it doesn't already know about (like a library).
# expression
- https://github.com/Dkendal/pattern-match.js
  - Provides pattern matching features typically found in functional languages like Elixir/Erlang, ML, F#, etc.
# class
- ## Drastically simplifying all of the construction and inference of route configs in @tan_stack Router using... Classes.
- https://twitter.com/tannerlinsley/status/1617936251147161600
  - In JS, this would be a very trivial amount, but most of that was strictly TS meta typings, so it's like... a big win.
- Strangely, i'm not surprised. 
  - I almost also used classes for "crazy" advanced inference in my project.
  - I'm not sure if you used the same pattern, but i find using classes as a "workaround" for advanced inference (especially for nested objects) a bit strange.
