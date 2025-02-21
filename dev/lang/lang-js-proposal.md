---
title: lang-js-proposal
tags: [js, lang, proposal]
created: 2020-06-27T07:29:09.318Z
modified: 2020-07-07T08:10:16.774Z
---

# lang-js-proposal

# guide
- communities
  - [TC39 - Specifying JavaScript.](https://tc39.es/)
  - [TC39 - Specifying JavaScript](https://es.discourse.group/)
# proposals-toc
- [finished proposals](https://github.com/tc39/proposals/blob/main/finished-proposals.md)

- https://babeljs.io/docs/en/plugins
  - https://github.com/babel/proposals
- [top tc39 proposals](https://github.com/search?o=desc&q=user%3Atc39&s=stars&type=Repositories)
  - pipeline-operator(|>), optional-chaining(?.), pattern-matching(case-when), observable, dynamic-import, bind-operator(::), object-rest-spread, decorators
  - [tc39 proposals stages](https://github.com/tc39/proposals)

- https://github.com/saadq/proposals.es /MIT/202111/ts/inactive
  - https://proposals.es/
  - A website for exploring ECMAScript proposals/champions/specs and more
  - 基于nextjs实现，每个proposal可在单独页面打开
# proposals-trending
- https://github.com/tc39/proposal-json-modules /s3
  - Proposal to import JSON files as modules
  - `import json from "./foo.json" assert { type: "json" };`

- https://github.com/tc39/proposal-import-attributes /s2
  - formerly known as Import Assertions, adds an inline syntax for module import statements to pass on more information alongside the module specifier
  - The specification of JSON modules was originally part of this proposal, but it was resolved during the July 2020 meeting to split JSON modules out into a separate Stage 3 proposal.

- https://github.com/tc39/proposal-temporal /s3
  - The JavaScript Temporal proposal has reached stage 3 in TC39. 
  - Proper Date & Time handling are coming!
  - `@internationalized/date` is a date library built by the React Aria team
    - https://twitter.com/devongovett/status/1641069934460510214
    - The API is inspired by Temporal, and eventually we will back it by Temporal when implemented in browsers. 

- https://github.com/tc39/proposal-shadowrealm /s3
  - [ES6 Realms API](https://gist.github.com/dherman/7568885)
  - A realm object abstracts the notion of a distinct global environment, with its own global object, copy of the standard library, and "intrinsics" (standard objects that are not bound to global variables, like the initial value of Object.prototype).
  - Extensible web: This is the dynamic equivalent of a same-origin `<iframe>` without DOM.
  - https://github.com/tc39/proposal-compartments /s1
    - Compartments are a mechanism for isolating and providing limited power to programs within a shared realm. 
    - Each compartment shares the intrinsics of a realm, but a different set of evaluators (eval, Function, and a new evaluator, Module) and a global object. 
    - Having a separate global object allows each compartment to be granted access to only those powerful objects it needs, its own isolated evaluators, powerless constructors, and shared prototypes.

- https://github.com/tc39/proposal-explicit-resource-management /s3
  - https://github.com/tc39/proposal-async-explicit-resource-management
  - This proposal intends to address a common pattern in software development regarding the lifetime and management of various resources (memory, I/O, etc.). 
  - This pattern generally includes the allocation of a resource and the ability to explicitly release critical resources.
  - `DisposableStack`

- https://github.com/tc39/proposal-iterator-helpers /s3
  - https://tc39.es/proposal-iterator-helpers
  - help with general usage and consumption of iterators in ECMAScript.

- https://github.com/tc39/proposal-async-iterator-helpers /s2
  - https://tc39.es/proposal-async-iterator-helpers/
  - Methods for working with async iterators in ECMAScript
  - This proposal was split out from proposal-iterator-helpers to resolve design questions related to concurrency
# proposals-finished
- https://github.com/tc39/proposal-class-static-block
  - provide a mechanism to perform additional static initialization during class definition evaluation.
# proposals-dead
- html import
- [proposal-bind-operator `::`](https://github.com/tc39/proposal-bind-operator)
  - [Is this proposal dead?](https://github.com/tc39/proposal-bind-operator/issues/53)

- ref
  - https://github.com/sudheerj/ECMAScript-features
  - https://kangax.github.io/compat-table/esnext/
  - [Rethinking JavaScript Infrastructure: Check out a (controversial) proposal to improve JavaScript Infrastructure.](https://cpojer.net/posts/rethinking-javascript-infrastructure)
# guide
- [ECMAScript-new-features-list](https://github.com/daumann/ECMAScript-new-features-list)

## [es2015/es6](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2015.md)

- scoping variables
- module
- class
- arrow functions
- generator function
- promise
- constants
- template literals
- map & set
- typed array
- symbol type as unique object property
- Rest parameter & Spread Operator
- destructuring assignment
- iterators & for-of
- proxy & relfecting
- formatting: number, date time

## [es2016](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2016.md)

- Array.prototype.includes
- Exponentiation Operator: 5 ** 2 (Math.pow(5, 2))

## [es2017](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2017.md)

- async function
- Object.entries, Object.values
- Object.getOwnPropertyDescriptors
- Trailing commas in function declarations and calls
- String padding

## [es2018](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2018.md)

- [object-rest-spread properties](https://github.com/tc39/proposal-object-rest-spread)
  - Rest properties used in variables declarations
  - Spread properties used in object literals
- Async iterators
- Promise.prototype.finally

## [es2019](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2019.md)

- Array.prototype.flat/flatMap
- Object.fromEntries
- String.prototype.trimStart/trimEnd
- Symbol.prototype.description
- Optional catch binding
- Array.prototype.sort() is required to be stable

- https://github.com/tc39/proposal-json-superset
  - A proposal to extend ECMA-262 syntax into a superset of JSON.

## [es2020](https://github.com/daumann/ECMAScript-new-features-list/blob/main/ES2020. MD)

- Private Class Variables `#message = "Howdy"`; 
- dynamic import: `import(my.js)`; 
- bigint
- optional chaining: `?.`
- Nullish Coalescing Operator: `??`解决`||`无法处理空字符串/0这类falsy value的问题
- `globalThis`: to provide a standard way of accessing the global this value across environments.
- Promise.allSettled
- String.matchAll
- import.meta
- `for..in` order: loop over the properties of an object in the order in which they were defined

## [es2021](https://github.com/daumann/ECMAScript-new-features-list/blob/main/ES2021. MD)

- String.prototype.replaceAll
- Logical Assignment Operators (&&= ||= ??=)
- Numeric Separators (1_000)
- `Promise.any` & AggregateError
- `WeakRef`s & FinalizationRegistry

## [es2022](https://github.com/daumann/ECMAScript-new-features-list/blob/main/ES2022. MD)

- Class field declarations
- `.at()` method on built-in indexables
- `Object.hasOwn`; 
- RegExp Match Indices
- Top-level await
- Ergonomic brand checks for private fields

## [es2023](https://github.com/daumann/ECMAScript-new-features-list/blob/main/ES2023. MD)

- `array.findLast`; 
- Hashbang Grammar #!/usr/bin/env node
- Use symbols in WeakMap/WeakSet/WeakRef collections and registries
- Change Array by copy: .toSorted, .toSpliced

## esX-deprecated

- cancellable promise

## more-proposals

- https://github.com/rbuckton/proposal-enum /201805/stage0
  - Enums provide a finite domain of constant values that are regularly used to indicate choices, discriminants, and bitwise flags.
  - [Alternative enum proposal · Issue #1 · rbuckton/proposal-enum](https://github.com/rbuckton/proposal-enum/issues/1)
  - https://github.com/Jack-Works/proposal-enum

## stage3/4

# class fields
- stage 3
  - https://github.com/tc39/proposal-class-fields
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields
- motivation
  - By declaring fields up-front, class definitions become more self-documenting; instances go through fewer state transitions, as declared fields are always present.
- Both static and instance public fields are writable, enumerable, and configurable properties.
  - As such, unlike their private counterparts, they participate in prototype inheritance.
  - 实践结论
    - instance method会定义在MyClass.prototype，共享实例了方法
    - instance field会定义在MyClass.prototype.constructor(也就是MyClass)构造方法内，实例属性不共享
      - 如果共享实例属性，当实例属性值为数组等引用类型时，修改prototype上的属性会修改所有对象实例的属性
      - You have to initialize arrays and objects in the constructor, so that each instance gets its own object or array instance. Some style guidelines propose that you still create the property on the prototype, but initialize it with null. This has no benefit other than adding some conceptual structure (if such a word exists) to your code.
    - static field和method直接定义在MyClass构造函数上，直接访问
    - 装饰器都是运行在类创建时，而实例成员是在实例化一个类的时候才会执行的，所以没有办法获取对应的descriptor

```JS
// class示例
class Model {
  // 实例方法
  method1() {}
  // 实例属性
  method2 = () => {}

  // 静态方法
  static method3() {}
  // 静态属性
  static method4 = () => {}
}

// 转译成es5版本
function Model() {
  // 实例属性仅在实例化时赋值
  this.method2 = function() {}
}

// 实例方法被定义在原型链上
Object.defineProperty(Model.prototype, 'method1', {
  value: function() {},
  writable: true,
  enumerable: false, // 设置不可被枚举
  configurable: true
})

// 静态属性被定义在构造函数上，且是默认的可被枚举
Model.method4 = function() {}

// 静态方法被定义在构造函数上
Object.defineProperty(Model, 'method3', {
  value: function() {},
  writable: true,
  enumerable: false, // 设置不可被枚举
  configurable: true
})
```

- A public field declarations define fields on instances with the internals of `Object.defineProperty` (which we refer to in TC39 jargon as [[Define]] semantics), rather than with `this.field = value;` (referred to as [[Set]] semantics).
  - The choice between [[Set]] and [[Define]] is a design decision contrasting different kinds of expectations of behavior: Expectations that the field will be created as a data property regardless of what the superclass contains, vs expectations that the setter would be called. 
  - Following a lengthy discussion, TC39 settled on [[Define]] semantics, finding that it's important to preserve the first expectation. 
  - As a mitigation, the decorators proposal provides the tools to write a decorator to make a public field declaration use [[Set]] semantics.

- Public instance fields exist on every created instance of a class. 
  - By declaring a public field, you can ensure the field is always present, and the class definition is more self-documenting.
  - Public instance fields are added with `Object.defineProperty()` either at construction time in the base class (before the constructor body runs), or just after `super()` returns in a subclass.  
  - Fields without initializers are initialized to `undefined`
  - Like properties, field names may be computed.
  - When initializing fields `this` refers to the class instance under construction. 
    - Just as in public instance methods, if you're in a subclass you can access the superclass prototype using `super` .

- Public instance methods are methods available on class instances.
  - Public instance methods are added to the class prototype at the time of class evaluation using `Object.defineProperty()` . 
  - They are writable, non-enumerable, and configurable.
  - Inside instance methods `this` refers to the instance itself. 
    - In subclasses, `super` lets you access the superclass prototype, allowing you to call methods from the superclass.
  - Use the `get` and `set` syntax to declare a public instance getter or setter.

- Public static fields are useful when you want a field to exist only once per class, not on every class instance you create. 
  - This is useful for caches, fixed-configuration, or any other data you don't need to be replicated across instances.
  - Public static fields are added to the class constructor at the time of class evaluation using `Object.defineProperty()` . They are accessed again from the class constructor.
  - Fields without initializers are initialized to `undefined` .
  - Public static fields are not reinitialized on subclasses, but can be accessed via the prototype chain.
    - `console.log(SubClassWithStaticField.baseStaticField)`
  - When initializing fields `this` refers to the class constructor. 
    - You can also reference it by name, and use `super` to get the superclass constructor (if one exists).

- Public static methods aren't called on instances of the class. Instead, they're called on the class itself. 
  - These are often utility functions, such as functions to create or clone objects.
  - The static methods are added to the class constructor with `Object.defineProperty()` at class evaluation time. 
  - These methods are writable, non-enumerable, and configurable.
  - another way to write static method: `Class.method = function () { /* code */ }`
- Property assignment is frequently used to add new properties to an object. 
  - Definition: `Object.defineProperty(obj, propName, propDesc)`
  - Assignment: `obj.prop = value`
  - This post explained that that can cause problems. 
  - Hence, it is best to follow the simple rules:
    - If you want to create a new property, use definition.
    - If you want to change the value of a property, use assignment.
  - ref
    - https://2ality.com/2012/08/property-definition-assignment.html
# private methods
- stage 3
  - https://github.com/tc39/proposal-private-methods
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields

- The class fields proposal provides private fields for classes and instances, and this proposal builds on that by adding private methods and accessors (getter/setters) to JavaScript. 
- To make methods, getter/setters or fields private, just give them a name starting with `#` .
# decorator
- stage 2
  - https://github.com/tc39/proposal-decorators
  - The decorators champion(支持者、拥护者) group is considering a redesign of the proposal as "static decorators".
  - [Javascript装饰器的妙用](https://juejin.im/post/6844903635168526343)
- motivation
  - This decorators proposal aims to improve on past proposals by working towards twin(双重的、同时发生的) goals:
    - It should be easy not just to use decorators, but also to write your own.
    - Decorators should be fast, both generating good code in transpilers, and executing fast in native JS implementations.
  - Decorators make class declarations programmable.
  - This proposal enables the basic functionality of the JavaScript original decorators proposal (e.g., most of what is available in TypeScript decorators), 
    - as well as two additional capabilities of the previous Stage 2 proposal which were especially important: access to private fields and methods, and registering callbacks which are called during the constructor.
- There's a set of built-in decorators that serve as the basic building blocks.
  - @wrap: Replace a method or the entire class with the return value of a given function
  - @register: Call a callback after the class is created
  - @expose: Call a callback given functions to access private fields or methods after the class is created
  - @initialize: Run a given callback when creating an instance of the class
- Decorators can be defined in JavaScript by composing other decorators
  - A `decorator @foo { }` declaration defines a new decorator. 
    - These are lexically scoped and can be imported and exported.
  - Decorators cannot be treated as JavaScript values; 
    - they may only be applied in classes, composed, exported, imported, etc.
  - As part of this, decorators have `@` as part of their name; 
    - `@decorator` names form a separate namespace.
  - Decorators can only be composed in rather fixed ways, making them more statically analyzable.
- Sometimes, certain code outside of a class may need to access private fields and methods.
  - Decorators can make this possible by giving someone access to a private field or method.

- A Decorator is a special kind of declaration that can be attached to a class declaration, method, accessor, property, or parameter. 
- Decorators use the form `@expression` , where `expression` must evaluate to a function that will be called at runtime with information about the decorated declaration.
- A Decorator Factory is simply a function that returns the expression that will be called by the decorator at runtime.
  - 装饰器工厂是返回装饰器函数的高阶函数
- Multiple decorators can be applied to a declaration `@f @g x`
  - is equivalent to `f(g(x))`
  - 装饰器是可以同时应用多个的，最内层的最先执行
- There is a well defined order to how decorators applied to various declarations inside of a class are applied:
  1. Parameter Decorators, followed by Method, Accessor, or Property Decorators are applied for each instance member.
  2. Parameter Decorators, followed by Method, Accessor, or Property Decorators are applied for each static member.
  3. Parameter Decorators are applied for the constructor.
  4. Class Decorators are applied for the class
- **5种常用装饰器**
- A **Class Decorator** is declared just before a class declaration. 
  - The class decorator is applied to the constructor of the class and can be used to observe, modify, or replace a class definition. 
  - A class decorator cannot be used in a declaration file, or in any other ambient(周围的) context (such as on a `declare` class).
  - 类装饰器会在class定义前调用，如果函数有返回值，则会认为是一个新的构造函数来替代之前的构造函数。
  - 函数接收一个参数：
    - constructor之前的构造函数
  - The expression for the class decorator will be called as a function at runtime, with the constructor of the decorated class as its only argument.
  - If the class decorator returns a value, it will replace the class declaration with the provided constructor function.
  - NOTE: Should you choose to return a new constructor function, you must take care to maintain the original prototype. The logic that applies decorators at runtime will not do this for you.
- A **Property Decorator** is declared just before a property declaration. 
  - 类成员上的 @Decorator 应该是应用最为广泛的一处了，函数，属性，get、set访问器，这几处都可以认为是类成员。
  - 在TS文档中被分为了Method Decorator、Accessor Decorator和Property Decorator，实际上使用类似。
  - 关于这类装饰器，会接收如下三个参数：
    - 如果装饰器挂载于静态成员上，则会返回构造函数，如果挂载于实例成员上则会返回类的原型
    - 装饰器挂载的成员名称
    - 成员的描述符，也就是 `Object.getOwnPropertyDescriptor` 的返回值
  - Property Decorator不会返回第三个参数，但是可以自己手动获取

前提是静态成员，而非实例成员，因为装饰器都是运行在类创建时，而实例成员是在实例化一个类的时候才会执行的，所以没有办法获取对应的descriptor

- A **Method Decorator** is declared just before a method declaration. 
  - The decorator is applied to the Property Descriptor for the method, and can be used to observe, modify, or replace a method definition. 
- An **Accessor Decorator** is declared just before an accessor declaration. 
  - The accessor decorator is applied to the Property Descriptor for the accessor and can be used to observe, modify, or replace an accessor’s definitions. 
- A **Parameter Decorator** is declared just before a parameter declaration. 
  - The parameter decorator is applied to the function for a class constructor or method declaration. 
  - 函数参数的装饰器也是像实例属性一样的，没有办法单独使用，毕竟函数是在运行时调用的，而无论是何种装饰器，都是在声明类时（可以认为是伪编译期）调用的。
  - 函数参数装饰器会接收三个参数：
    - 类似属性装饰器，类的原型或者类的构造函数
    - 参数所处的函数名称
    - 参数在函数中形参中的位置（函数签名中的第几个参数）
# dynamic import
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
