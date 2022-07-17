---
title: lang-js-typescript-pattern
tags: [lang, pattern, typescript]
created: 2021-03-22T14:42:21.776Z
modified: 2021-03-22T14:43:12.866Z
---

# lang-js-typescript-pattern

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

``` typescript

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
