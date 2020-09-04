---
title: page-js-proto-prototype
tags: [js, lang]
created: '2020-09-04T03:36:05.137Z'
modified: '2020-09-04T03:36:47.938Z'
---

# page-js-proto-prototype

## guide 

- ref
  - [Inheritance and the prototype chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
  - [Object.prototype.__proto__](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/proto)
  - [Object.prototype.constructor]https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)
  - [Object prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)

## Inheritance and the prototype chain

- When it comes to inheritance, JavaScript only has one construct: objects. 
  - Each object has a private property([[Prototype]]) which holds a link to another object called its prototype. 
  - That prototype object has a prototype of its own, and so on until an object is reached with `null` as its prototype. 
  - By definition, `null` has no prototype, and acts as the final link in this prototype chain.
- Nearly all objects in JavaScript are instances of `Object` which sits on the top of a prototype chain.
- While this confusion is often considered to be one of JavaScript's weaknesses, the prototypal inheritance model itself is, in fact, more powerful than the classic model. 
  - It is, for example, fairly trivial(不重要的，普通的，微不足道的) to build a classic model on top of a prototypal model.

- JavaScript objects are dynamic "bags" of properties (referred to as own properties). 
  - JavaScript objects have a link to a prototype object. 

- When trying to access a property of an object, the property will not only be sought on the object but also on the prototype of the object, the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.
- Following the ECMAScript standard, the notation `someObject.[[Prototype]]` is used to designate the prototype of `someObject` . 
  - Since ECMAScript 2015, the [[Prototype]] is accessed using the accessors `Object.getPrototypeOf()` and `Object.setPrototypeOf()` . 
  - This is equivalent to the JavaScript property `__proto__` which is non-standard but de-facto(事实存在的但不一定合法的) implemented by many browsers.
  - __proto__常用来构成原型链，访问属性通过查找原型链实现
  - It should not be confused with the `func.prototype` property of functions, which instead specifies the [[Prototype]] to be assigned to all instances of objects created by the given function when used as a constructor. 
  - func.prototype用来指定将func作为构造函数的实例对象会共享的[[Prototype]]属性值，类似于定义了一个类型
  - The `Object.prototype` property represents the `Object` prototype object.

``` JS
// 原型链实例
class CC { constructor() {} }
let oo = new CC();

oo.__proto__ === CC.prototype //true
oo.__proto__.__proto__ === Object.prototype // true
oo.__proto__.__proto__.__proto__ === null // true
```

- Property Shadowing
  - Is there a 'b' own property on o? Yes, and its value is 2.
  - The prototype also has a 'b' property, but it's not visited. 
  - This is called Property Shadowing
- JavaScript does not have "methods" in the form that class-based languages define them. 
  - In JavaScript, any function can be added to an object in the form of a property. 
  - An inherited function acts just as any other property, including property shadowing as shown above (in this case, a form of method overriding).
  - When an inherited function is executed, the value of `this` points to the inheriting object, not to the prototype object where the function is an own property.
  - this指向当前元素，而不是指向prototype原型对象

- In JavaScript, functions are able to have properties. 
  - All functions have a special property named `prototype` . 
- We can use the `new` operator to create an instance of `doSomething()` based on this prototype.
- **Calling a function with the `new` operator returns an object that is an instance of the function**.
- `doSomething()` has a default `prototype` property, as demonstrated by the console. 
  - We can now use the `new` operator to create an instance of `doSomething()` based on this prototype. 
  - `var doSomeInstancing = new doSomething();`
  - As seen above, the `__proto__` of `doSomeInstancing` is `doSomething.prototype` .
  - When you access a property of `doSomeInstancing` , the browser first looks to see if `doSomeInstancing` has that property.
  - If `doSomeInstancing` does not have the property, then the browser looks for the property in the __proto__ of doSomeInstancing (a.k.a. `doSomething.prototype` ). 
  - If the __proto__ of doSomeInstancing has the property being looked for, then that property on the __proto__ of doSomeInstancing is used.
  - Otherwise, if the __proto__ of doSomeInstancing does not have the property, then the __proto__ of the __proto__ of doSomeInstancing is checked for the property. 
  - By default, the __proto__ of any function's prototype property is `window.Object.prototype`
  - `Object.prototype` has `null` as its prototype.

- A "constructor" in JavaScript is "just" a function that happens to be called with the new operator.

- ECMAScript 5 introduced a new method: `Object.create()` . 
  - Calling this method creates a new object. 
  - The prototype of this object is the first argument of the function

- Performance
  - The lookup time for properties that are high up on the prototype chain can have a negative impact on the performance, and this may be significant in the code where performance is critical. 
  - Additionally, trying to access nonexistent properties will always traverse the full prototype chain.
  - Also, when iterating over the properties of an object, every enumerable property that is on the prototype chain will be enumerated. 
  - `hasOwnProperty` is the only thing in JavaScript which deals with properties and does not traverse the prototype chain.
  - Note: It is not enough to check whether a property is `undefined` . The property might very well exist, but its value just happens to be set to `undefined` .

- Bad practice: Extension of native prototypes
  - One misfeature that is often used is to extend `Object.prototype` or one of the other built-in prototypes.
  - This technique is called monkey patching and breaks encapsulation. 
  - While used by popular frameworks such as Prototype.js, there is still no good reason for cluttering built-in types with additional non-standard functionality.
  - The only good reason for extending a built-in prototype is to backport the features of newer JavaScript engines, like `Array.forEach` .

- Here are all 4 ways to extend the prototype chain
  - New-initialization(Recommended)
    - Supported in every browser imaginable (support goes all the way back to IE 5.5!). 
      - Also, it is very fast, very standard, and very JIST-optimizable
    - In order to use this method, the function in question must be initialized.
      - During this initialization, the constructor may store unique information that must be generated per-object.
      - However, this unique information would only be generated once, potentially leading to problems.
      - Additionally, the initialization of the constructor may put unwanted methods onto the object.
      - However, both these are generally not problems at all (in fact, usually beneficial) if it is all your own code and you know what does what where.
  - Object.create
    - Allows the direct setting of __proto__ in a way that is one-time-only so that the browser can better optimize the object. 
      - Also allows the creation of objects without a prototype via Object.create(null).
    - The slow object initialization can be a performance black hole if using the second argument because each object-descriptor property has its own separate descriptor object. 
  - Object.setPrototypeOf
    - Allows the dynamic manipulation of an objects prototype
    - Should-be-deprecated and ill-performant.
  - __proto__
    - Setting __proto__ to something that is not an object only fails silently. It does not throw an exception.
    - Grossly deprecated and non-performant.

``` JS
// 推荐使用基于new的原型链
function foo() {}
foo.prototype = {
  foo_prop: "foo val"
};

function bar() {}

var proto = new foo;

proto.bar_prop = "bar val";
bar.prototype = proto;

var inst = new bar;

console.log(inst.foo_prop);
console.log(inst.bar_prop);
```

- JavaScript is a bit confusing for developers coming from Java or C++, as it's all dynamic, all runtime, and it has no classes at all. 
  - **It's all just instances (objects)**. 
  - Even the "classes" we simulate are just a function object.
- `function A(){}` has a special property called `prototype` .
  - This special property works with the JavaScript `new` operator. 
  - The reference to the prototype object is copied to the internal [[Prototype]] property of the new instance.
  - For example, when you do `var a1 = new A()` , JavaScript (after creating the object in memory and before running function `A()` with `this` defined to it) sets `a1.[[Prototype]] = A.prototype` . 
  - When you then access properties of the instance, JavaScript first checks whether they exist on that object directly, and if not, it looks in [[Prototype]]. 
  - This means that all the stuff you define in `prototype` is effectively shared by all instances, and you can even later change parts of `prototype` and have the changes appear in all existing instances, if you wanted to.
- In short, `prototype` is for types, while `Object.getPrototypeOf()` /[[Prototype]]/__proto__ is the same for instances.
- [[Prototype]] is looked at recursively, until it's found or `Object.getPrototypeOf` returns `null` .

- The __proto__ getter function exposes the value of the internal [[Prototype]] of an object. 

``` 
// So, when you call
var o = new Foo();

// JavaScript actually just does
var o = new Object();
o.[[Prototype]] = Foo.prototype;
Foo.call(o);
```

## Object prototypes

- Prototypes are the mechanism by which JavaScript objects inherit features from one another.
- JavaScript is often described as a prototype-based language — to provide inheritance, objects can have a prototype object, which acts as a template object that it inherits methods and properties from.
- An object's prototype object may also have a prototype object, which it inherits methods and properties from, and so on. 
  - This is often referred to as a prototype chain, and explains why different objects have properties and methods defined on other objects available to them
- In JavaScript, a link is made between the object instance and its prototype (its `__proto__` property, which is derived from the `prototype` property on the constructor), and the properties and methods are found by walking up the chain of prototypes.
- Note: It's important to understand that there is a distinction between an object's prototype (available via `Object.getPrototypeOf(obj)` , or via the deprecated `__proto__` property) and the `prototype` property on constructor functions.
  - The former is the property on each instance, and the latter is the property on the constructor. 
  - That is, `Object.getPrototypeOf(new Foobar())` refers to the same object as `Foobar.prototype` .
- We want to reiterate(重申、反复地说) that the methods and properties are not copied from one object to another in the prototype chain. 
  - They are accessed by walking up the chain as described above.
- Before ECMAScript 2015, there wasn't officially a way to access an object's prototype directly — the "links" between the items in the chain are defined in an internal property, referred to as [[Prototype]] in the specification for the JavaScript language.
  - Most modern browsers, however, do offer property available called `__proto__` , which contains the object's constructor's `prototype` object
  - Since ECMAScript 2015, you can access an object's prototype object indirectly via `Object.getPrototypeOf(obj)` .

- Every constructor function has a `prototype` property whose value is an object containing a `constructor` property. 
  - This `constructor` property points to the original constructor function.

``` JS
// 构造函数的原型对象的constructor属性，指向构造函数自身
function f() {}
f.prototype.constructor === f // true
```

## Object.prototype.constructor

- The `constructor` property returns a reference to the `Object` constructor function that created the instance object. 
  - Note that the value of this property is a reference to the function itself, not a string containing the function's name.
- All objects (with the exception of objects created with `Object.create(null)` ) will have a `constructor` property. 
- Objects created without the explicit use of a constructor function (such as object- and array-literals) will have a `constructor` property that points to the Fundamental `Object` constructor type for that object.

``` JS
let o = {}
o.constructor === Object // true

let o = new Object
o.constructor === Object // true

let a = []
a.constructor === Array // true

let a = new Array
a.constructor === Array // true

let n = new Number(3)
n.constructor === Number // true
```
