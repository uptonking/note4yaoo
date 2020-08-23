---
tags: [js, lang, proposal]
title: lang-js-proposal
created: '2020-06-27T07:29:09.318Z'
modified: '2020-07-07T08:10:16.774Z'
---

# lang-js-proposal

## proposal-toc

- https://babeljs.io/docs/en/plugins
- https://github.com/babel/proposals

## guide

- deprecated
  - cancellable promise

## class fields

- stage 3
- https://github.com/tc39/proposal-class-fields
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields
- motivation
  - By declaring fields up-front, class definitions become more self-documenting; instances go through fewer state transitions, as declared fields are always present.
- Both static and instance public fields are writable, enumerable, and configurable properties.
  - As such, unlike their private counterparts, they participate in prototype inheritance.
- Public instance fields exist on every created instance of a class. 
  - By declaring a public field, you can ensure the field is always present, and the class definition is more self-documenting.
  - Public instance fields are added with `Object.defineProperty()` either at construction time in the base class (before the constructor body runs), or just after `super()` returns in a subclass.  
  - Fields without initializers are initialized to undefined
  - Like properties, field names may be computed.
  - When initializing fields this refers to the class instance under construction. 
    - Just as in public instance methods, if you're in a subclass you can access the superclass prototype using super.
- Public instance methods are methods available on class instances.
  - Public instance methods are added to the class prototype at the time of class evaluation using `Object.defineProperty()` . 
  - They are writable, non-enumerable, and configurable.
  - Inside instance methods, `this` refers to the instance itself. 
    - In subclasses, super lets you access the superclass prototype, allowing you to call methods from the superclass.
  - Use the `get` and `set` syntax to declare a public instance getter or setter.
- Public static fields are useful when you want a field to exist only once per class, not on every class instance you create. 
  - This is useful for caches, fixed-configuration, or any other data you don't need to be replicated across instances.
  - Public static fields are added to the class constructor at the time of class evaluation using `Object.defineProperty()` . They are accessed again from the class constructor.
  - Fields without initializers are initialized to undefined.
  - Public static fields are not reinitialized on subclasses, but can be accessed via the prototype chain.
  - When initializing fields, `this` refers to the class constructor. 
    - You can also reference it by name, and use `super` to get the superclass constructor (if one exists).
- Property assignment is frequently used to add new properties to an object. 
  - Definition: `Object.defineProperty(obj, propName, propDesc)`
  - Assignment: `obj.prop = value`
  - This post explained that that can cause problems. 
  - Hence, it is best to follow the simple rules:
    - If you want to create a new property, use definition.
    - If you want to change the value of a property, use assignment.
  - ref
    - https://2ality.com/2012/08/property-definition-assignment.html

## dynamic import

- stage 4
- https://github.com/tc39/proposal-dynamic-import
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#Dynamic_Imports
- motivation
  - you will need the code until a later time.
  - When the module you are importing does not exist at load time
  - When the import specifier string needs to be constructed dynamically.
    - Static import only supports static specifiers.
  - When the module being imported has side effects 
    - and you do not want those side effects unless some condition is true.
  - The existing syntactic forms for importing modules are static declarations. 
    - They accept a string literal as the module specifier, and introduce bindings into the local scope via a pre-runtime "linking" process. 
    - This is a great design for the 90% case, and supports important use cases such as static analysis, bundling tools, and tree shaking.
  - It's also desirable to be able to dynamically load parts of a JavaScript application at runtime. 
    - This could be because of factors only known at runtime (such as the user's language), for performance reasons (not loading code until it is likely to be used), or for robustness reasons (surviving failure to load a non-critical module). 
    - Truly dynamic code loading also enables advanced scenarios, such as racing multiple modules against each other and choosing the first to successfully load.
- To dynamically import a module, the `import` keyword may be called as a function. 
  - When used this way, it **returns a promise**.
  - This form also supports the `await` keyword
- Use dynamic import only when necessary. 
  - The static form is preferable for loading initial dependencies, and can benefit more readily from static analysis tools and tree shaking.
