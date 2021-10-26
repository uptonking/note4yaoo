---
title: page-lang-js
tags: [js, lang]
created: '2020-08-28T07:27:16.385Z'
modified: '2020-08-28T07:27:31.736Z'
---

# page-lang-js

# [Properties in JavaScript: definition versus assignment](https://2ality.com/2012/08/property-definition-assignment.html)

- `Object.defineProperty(obj, propName, propDesc)`
  - The primary purpose of this function is to add an own (direct) property to obj, whose attributes (writable etc., see below) are as specified by propDesc. 
  - The secondary purpose is to change the attributes of a property, including its value.
- `obj.prop = value`
  - The primary purpose of such an expression is to change the value. 
  - Before performing that change, JavaScript consults the prototype chain of obj: 
    - If there is a setter somewhere in obj or in one of its prototypes,then the assignment is an invocation of that setter. 
  - Assignment has the side effect of creating a property if it doesn’t exist, yet – as an own property of obj, with default attributes.
- Assignment calls a setter in a prototype, definition creates an own property
- Read-only properties in prototypes prevent assignment, but not definition
  - You can make a property read-only, by only defining a getter.
  - We can, however, define something new and thus override proto’s property bar
  - A read-only property in a prototype prevents assignment from adding an own property with the same name, you need to use definition if you want to do so. 
  - That is, the assignment obj.foo = "b" does not auto-create the property foo if there is a read-only property with that name in one of obj’s prototypes. 
- The assignment operator does not change properties in prototypes
  - You can’t change proto.foo by assigning to obj.foo. 
    - Doing so creates a new own property
  - The rationale for this behavior is as follows: 
    - Prototypes can introduce properties whose values are shared by all of their descendants. 
    - If one decides to change such a property in a descendant, a new own property is created. 
    - That means one can make the change, but it is only local, it doesn’t affect the other descendants. 
    - In this light, the effects of getter-only properties and read-only properties make sense: prevent changes, by preventing the creation of an own property. 
  - What is the motivation for overriding prototype properties instead of changing them?
    - Methods: Allow methods to be patched, directly in the prototype, but prevent accidental changes via descendants of the prototype.
    - Non-method properties: The prototype provides shared default values for descendants. One can override these values via a descendant, but not change them. This is considered an anti-pattern and discouraged. It is cleaner to assign default values in constructors.
- Only definition allows you to create a property with arbitrary attributes
  - If you create an own property via assignment, it always has default attributes. 
  - If you want to specify arbitrary attributes, you must use definition. 
  - Note that that includes adding getters and setters to an object.
- The properties of an object literal are added via definition
  - It is for the same reason that `Object.create` receives property descriptors via its second argument.

``` JS
var obj = {
  foo: 123
};

// This is internally translated to a series of statements.
var obj = new Object();
Object.defineProperties(obj, {
  foo: {
    configurable: true,
    enumerable: true,
    value: 123,
    writable: true
  }
});
```

- Definition can be used to prevent accidental assignment by setting `writable: false, configurable: true,`
  - However, as attr is configurable, we can override it in an instance via property definition.
- Property assignment is frequently used to add new properties to an object. 
  - This post explained that that can cause problems. 
  - Hence, it is best to follow the simple rules:
    - If you want to create a new property, use definition.
    - If you want to change the value of a property, use assignment.
- In the comments, medikoo reminds us that using property descriptors to achieve #1 is slow. 
  - And I indeed often use assignment to create properties, because it’s also more convenient. 
  - Thankfully, esnext might make definition both faster and more convenient
  - There is a proposal for a “define properties” operator, an alternative to Object.defineProperties. 

- I work with descriptors over a year now. 
  - I've moved through different approaches over time, 
  - and now I feel they should be used only in specific cases.
  - First thing is that defining descriptors is magnitudes slower in some engines (V8 for sure), other case is that they clutter your code and logic. 
    - There's no need to overuse them. 
    - I would never use descriptors on internal objects, that you don't expose outside, objects are safe, no need to introduce extra rules.
  - Currently I use descriptors only if I need to define custom property on object I do not own (I don't want that property to be enumerable) 
    - and when I shim or extend native prototypes with other methods (by default all native methods and functions are defined as not enumerable and it's nice to keep that).

# Why I Don’t Use Classes

- [Why I Don’t Use Classes](https://spin.atomicobject.com/2020/03/12/why-i-dont-use-classes/)

- For context, my projects lately have been in full-stack Typescript, and what I value in writing software is highly influenced by the experiences in the Typescript ecosystem. 
- I also should note that I don’t actively avoid writing classes. 
- I just lean toward other solutions, typically functional solutions over object-orientated solutions

- I'm terrible at making good abstractions with classes. 
  - But typically, using inheritance and polymorphism to model a problem space evolves into a mess. 
  - First, classes end up having terrible method names if those methods are overriding base class methods. 
    - I’ve been fooled by too many method names that end up doing more than what they said they would.
    -  But I’ve found much more success creating groups of functions that don’t belong in a class. 
    -  And I can give them any name I want and split responsibilities into new functions as I please.
  - Secondly, I’ve noticed that classes have a tendency to grow large. 
    - They will collect pieces of functionality that need to live in the context of the class, usually to access the internal state of that class. 
    - This dependency on the internal state makes it difficult to break the methods up into logical chunks.
    - This usually isn’t a huge pain point, but teams I’ve been on have preferred using groups of functions in modules that have state passed to them. 
    - It tends to be easier to break large modules into smaller ones if needed.
- State contained and controlled by a class has been the cause of undesirably behaviors. 

- Alternatives to Classes
  - I like to use modules that expose groups of functions. 
  - These functions accept state and other dependencies. 
  - These modules tend to look like what my colleague Drew describes as the functional module pattern.
