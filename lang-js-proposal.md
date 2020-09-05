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
  - 实践结论
    - instance method会定义在MyClass.prototype，共享实例了方法
    - instance field会定义在MyClass.prototype.constructor(也就是MyClass)构造方法内，实例属性不共享
      - 如果共享实例属性，当实例属性值为数组等引用类型时，修改prototype上的属性会修改所有对象实例的属性
      - You have to initialize arrays and objects in the constructor, so that each instance gets its own object or array instance. Some style guidelines propose that you still create the property on the prototype, but initialize it with null. This has no benefit other than adding some conceptual structure (if such a word exists) to your code.
    - static field和method直接定义在MyClass构造函数上，直接访问
    - 装饰器都是运行在类创建时，而实例成员是在实例化一个类的时候才会执行的，所以没有办法获取对应的descriptor

``` JS
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
  - When initializing fields, `this` refers to the class instance under construction. 
    - Just as in public instance methods, if you're in a subclass you can access the superclass prototype using `super` .

- Public instance methods are methods available on class instances.
  - Public instance methods are added to the class prototype at the time of class evaluation using `Object.defineProperty()` . 
  - They are writable, non-enumerable, and configurable.
  - Inside instance methods, `this` refers to the instance itself. 
    - In subclasses, `super` lets you access the superclass prototype, allowing you to call methods from the superclass.
  - Use the `get` and `set` syntax to declare a public instance getter or setter.

- Public static fields are useful when you want a field to exist only once per class, not on every class instance you create. 
  - This is useful for caches, fixed-configuration, or any other data you don't need to be replicated across instances.
  - Public static fields are added to the class constructor at the time of class evaluation using `Object.defineProperty()` . They are accessed again from the class constructor.
  - Fields without initializers are initialized to `undefined` .
  - Public static fields are not reinitialized on subclasses, but can be accessed via the prototype chain.
    - `console.log(SubClassWithStaticField.baseStaticField)`
  - When initializing fields, `this` refers to the class constructor. 
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

## decorator

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
- There is a well defined order to how decorators applied to various declarations inside of a class are applied:
  1. Parameter Decorators, followed by Method, Accessor, or Property Decorators are applied for each instance member.
  2. Parameter Decorators, followed by Method, Accessor, or Property Decorators are applied for each static member.
  3. Parameter Decorators are applied for the constructor.
  4. Class Decorators are applied for the class
- 5种常用装饰器
- A **Class Decorator** is declared just before a class declaration. 
  - The class decorator is applied to the constructor of the class and can be used to observe, modify, or replace a class definition. 
  - A class decorator cannot be used in a declaration file, or in any other ambient(周围的) context (such as on a `declare` class).
  - The expression for the class decorator will be called as a function at runtime, with the constructor of the decorated class as its only argument.
  - If the class decorator returns a value, it will replace the class declaration with the provided constructor function.
  - NOTE: Should you choose to return a new constructor function, you must take care to maintain the original prototype. The logic that applies decorators at runtime will not do this for you.
- A **Method Decorator** is declared just before a method declaration. 
  - The decorator is applied to the Property Descriptor for the method, and can be used to observe, modify, or replace a method definition. 
- An **Accessor Decorator** is declared just before an accessor declaration. 
  - The accessor decorator is applied to the Property Descriptor for the accessor and can be used to observe, modify, or replace an accessor’s definitions. 
- A **Property Decorator** is declared just before a property declaration. 
- A **Parameter Decorator** is declared just before a parameter declaration. 
  - The parameter decorator is applied to the function for a class constructor or method declaration. 
  - 函数参数的装饰器也是像实例属性一样的，没有办法单独使用，毕竟函数是在运行时调用的，而无论是何种装饰器，都是在声明类时（可以认为是伪编译期）调用的。

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
