---
title: dev-log-faq-lang-js
tags: [faq, js]
created: '2020-11-07T11:48:30.544Z'
modified: '2021-03-29T19:18:55.989Z'
---

# dev-log-faq-lang-js

# faq-not-yet

- [是否应该在production里使用typescript的decorator？](https://www.zhihu.com/question/404724504)
  - decorator提案已有三版草案，尤其第三版是对前两版的推倒重来
  - 前两版是类似于python decorator的语义，第三版是静态语义，类似于弱化的宏
  - 但是这三版都无法推进到 stage 3（主要的障碍来自于引擎厂商）
  - 现在TypeScript所实现的 decorator，基于第一版的草案
    - 现在TS团队拒绝投入精力到与 decorator 相关的任何改进
    - Vue 3放弃了class component而转向 composition API，也有部分原因源于 decorator 前景不明
  - [TypeScript装饰器(Decorators)具体做了什么工作）](https://www.zhihu.com/question/68257128)
    - Angular使用的根本不是装饰器（Decorator），而是注解（Annotation）
    - 装饰器的定位是通过对应的装饰函数，修改内容本身的定义，从而实现不同的行为。
    - 而注解并不产生任何行为，仅仅添加附加内容，需要相应的Scanner读取并识别其中的内容，从而使得Scanner自身产生不同的行为。
    - Angular是通过装饰器来模拟了注解的功能

# 

# .js vs .jsx

- The distinction between .js and .jsx files was useful before Babel, but it’s not that useful anymore.
  - There are other syntax extensions (e.g. Flow). What would you call a JS file that uses Flow? .flow.js? What about JSX file that uses Flow? .flow.jsx? What about some other experimental syntax? .flow.stage-1.jsx?
  - Most editors are configurable so you can tell them to use a JSX-capable syntax scheme for .js files. Since JSX (or Flow) are strict supersets of JS, I don’t see this as an issue.

- It's a bit concerning that many devs insist on putting JSX inside .js files "just because it's common practice" 
- https://twitter.com/youyuxi/status/1362049928139321348
  - The reason Vite requires .jsx extension for JSX processing is because in most cases plain .js files shouldn't need full AST transforms to work in the browser. Allowing JSX in .js files means every served file must be full-AST-processed just in case it contains JSX.
- Try .tsx

- ref

# In js, what does `this` refer to?

- tips
  - Don't use this
    - You actually don't want to access `this` in particular, but the object it refers to. 
    - That's why an easy solution is to simply create a new variable that also refers to that object. 
    - The variable can have any name, but common ones are `self` and `that` .
  - Explicitly set this of the callback 
    - use `bind`

- `this` is a property of an execution context (global, function or eval) that, 
  - in non–strict mode, is always a reference to an object 
  - and in strict mode can be any value.

- A function's `this` keyword behaves a little differently in JavaScript compared to other languages. 
  - It also has some differences between strict mode and non-strict mode.
- In most cases, the **value of `this` is determined by how a function is called (runtime binding)**. 
- It can't be set by assignment during execution, and it may be different each time the function is called. 
- ES5 introduced the `bind()` method to set the value of a function's this regardless of how it's called, 
  - and ES2015 introduced arrow functions which don't provide their own `this` binding 
  - (it retains the `this` value of the enclosing lexical context).

- In the global execution context (outside of any function),  `this` refers to the global object( `window` ) whether in strict mode or not.
  - You can always easily get the global object using the global `globalThis` property, regardless of the current context in which your code is running.

- **Inside a function, the value of `this` depends on how the function is called**.
- Since the following code is not in strict mode, and because the value of `this` is not set by the call,  `this` will default to the global object, which is `window` in a browser

``` JS
function f1() {
  return this;
}
// In a browser:
f1() === window; // true
// In Node:
f1() === globalThis; // true
```

- In strict mode, however, if the value of `this` is not set when entering an execution context, it remains as `undefined`
- To set the value of `this` to a particular value when calling a function, use `call()` , or `apply()` . 
  - The first parameter is the object to use as 'this', subsequent parameters are passed as arguments in the function call
  - Note that in non–strict mode, with call and apply, if the value passed as this is not an object, an attempt will be made to convert it to an object. 
  - Values null and undefined become the global object. 
  - Primitives like 7 or 'foo' will be converted to an Object using the related constructor, so the primitive number 7 is converted to an object as if by new Number(7) and the string 'foo' to an object as if by new String('foo')

- The behavior of `this` in classes and functions is similar, since classes are functions under the hood.
- Within a class constructor,  `this` is a regular object. 
  - All non-static methods within the class are added to the prototype of `this`
  - Static methods are not properties of `this`. 
    - They are properties of the class itself.
- For derived classes, derived constructors have no initial `this` binding. 
- Calling `super()` creates a `this` binding within the constructor, like evaluating `this = new Base(); `
- Referring to this before calling super() will throw an error.
- Derived classes must not return before calling super(), unless they return an Object or have no constructor at all. 

- Calling `f.bind(thisArg,arg1,arg2)` creates a new function with the same body and scope as `f` , 
  - but where `this` occurs in the original function, 
  - in the new function it is permanently bound to the first argument of `bind` , regardless of how the function is being used.
  - The `bind()` function creates a new bound function, which is an exotic(奇异的) function object (a term from ECMAScript 2015) that wraps the original function object. 
    - Calling the bound function generally results in the execution of its wrapped function.

``` JS
function f() {
  return this.a;
}

var g = f.bind({ a: 'azerty' });
console.log(g()); // azerty

var h = g.bind({ a: 'yoo' }); // bind only works once!
console.log(h()); // azerty

var o = { a: 37, f: f, g: g, h: h };
console.log(o.a, o.f(), o.g(), o.h()); // 37,37, azerty, azerty
```

- In arrow functions,  `this` retains the value of the enclosing lexical context's `this` .
  -  In global code, it will be set to the global object
- If `this` arg is passed to `call/apply` , or `bind` on invocation of an arrow function, it will be ignored. 
  - You can still prepend arguments to the call, but the first argument (thisArg) should be set to `null`

- **When a function is called as a method of an object, its `this` is set to the object the method is called on**.
  - In the following example, when `o.f()` is invoked, inside the function `this` is bound to the `o` object.
  - **Note that this behavior is not at all affected by how or where the function was defined**.
  - This demonstrates that it matters only that the function was invoked from the `f` method member of object `o` .
  - the `this` binding is only affected by the most immediate member reference

``` JS
var o = {
  prop: 37,
  f: function() {
    return this.prop;
  }
};
console.log(o.f()); // 37

function independent() {
  return this.prop;
}
o.f1 = independent;
console.log(o.f1()); // 37

o.b = { g: independent, prop: 42 };
console.log(o.b.g()); // 42
```

- If the method is on an object's prototype chain,  `this` refers to the object the method was called on, as if the method were on the object.

``` JS
var o = { f: function() { return this.a + this.b; } };
var p = Object.create(o);
p.a = 1;
p.b = 4;
console.log(p.f()); // 5
```

- A function used as getter or setter has its `this` bound to the object from which the property is being set or gotten.

``` JS
function sum() {
  return this.a + this.b + this.c;
}
var o = {
  a: 1,
  b: 2,
  c: 3,
  get average() {
    return (this.a + this.b + this.c) / 3;
  }
};
Object.defineProperty(o, 'sum', {
  get: sum,
  enumerable: true,
  configurable: true
});

console.log(o.average, o.sum); // 2, 6
```

- When a function is used as a constructor (with the `new` keyword), its `this` is bound to the new object being constructed.
  - While the default for a constructor is to return the object referenced by `this` , it can instead return some other object 
  - if the return value isn't an object, then the `this` object is returned
  - If the function has a return statement that returns some other object, that object will be the result of the `new` expression. 

``` JS
function C2() {
  this.a = 37;
  return { a: 38 };
}
o = new C2();
console.log(o.a); // 38
```

- When a function is used as an event handler, its `this` is set to the element on which the listener is placed 
  - (some browsers do not follow this convention for listeners added dynamically with methods other than addEventListener()).
- When the code is called from an inline `on-event` handler, its this is set to the DOM element on which the listener is placed
  - Note however that only the outer code has its `this` set this way
  - the inner function's `this` isn't set so it returns the global/window object (i.e. the default object in non–strict mode where `this` isn't set by the call).

``` HTML
<button onclick="alert((function() { return this; })());">
  Show inner this
</button>
```

- this in classes
  - Just like with regular functions, the value of `this` within methods depends on how they are called. 
  - Sometimes it is useful to override this behavior so that `this` within classes always refers to the class instance. 
  - To achieve this,  `bind` the class methods in the constructor
  - Classes are always strict mode code. Calling methods with an undefined `this` will throw an error.

``` JS
class Car {
  constructor() {
    this.sayBye = this.sayBye.bind(this);
  }
  sayHi() {
    console.log(`Hello from ${this.name}`);
  }
  sayBye() {
    console.log(`Bye from ${this.name}`);
  }
  get name() {
    return 'Ferrari';
  }
}
class Bird {
  get name() {
    return 'Tweety';
  }
}

const car = new Car();
const bird = new Bird();

// The value of 'this' in methods depends on their caller
car.sayHi(); // Hello from Ferrari
bird.sayHi = car.sayHi;
bird.sayHi(); // Hello from Tweety

// For bound methods, 'this' doesn't depend on the caller
bird.sayBye = car.sayBye;
bird.sayBye(); // Bye from Ferrari
```

- ref
  - [mdn this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
  - [How to access the correct `this` inside a callback?](https://stackoverflow.com/questions/20279484/how-to-access-the-correct-this-inside-a-callback)

# js: prototype vs __proto__

- prototype 显式原型: explicit prototype property
  - 每一个函数在创建之后都会拥有一个名为 `prototype` 的属性，这个属性指向函数的原型对象。
  - 通过 `Function.prototype.bind` 方法构造出来的函数是个例外，它没有prototype属性
  - **显式原型的作用：用来实现基于原型的继承与属性的共享**
  - ECMAScript does not use classes such as those in C++, or Java. 
    - Instead objects may be created in various ways including via a literal notation or via constructors which create objects 
      - and then execute code that initialises all or part of them by assigning initial values to their properties. 
    - Each constructor is a function that has a property named `prototype` that is used to implement prototype-based inheritance and shared properties.
    - Objects are created by using constructors in `new` expressions; for example, new Date(2009,11) creates a new Date object. ----ECMAScript Language Specification
- __proto__ 隐式原型: implicit prototype link
  - js中任意对象都有一个内置属性[[prototype]]，在ES5之前没有标准的方法访问这个内置属性，但是大多数浏览器都支持通过 `__proto__` 来访问。
  - 隐式原型指向创建这个对象的函数(constructor)的prototype
  - ES5中有了对于这个内置属性标准的Get方法 `Object.getPrototypeOf()` .
  - **隐式原型的作用：构成原型链，同样用于实现基于原型的继承**
    - 举个例子，当我们访问obj这个对象中的x属性时，如果在obj中找不到，那么就会沿着__proto__依次查找。
  - Every object created by a constructor has an implicit reference (called the object’s `prototype` ) to the value of its constructor’s `prototype` ----ECMAScript Language Specification
  - The `__proto__` property of `Object.prototype` is an accessor property (a getter function and a setter function) that exposes the internal [[Prototype]] (either an object or null) of the object through which it is accessed.
  - The `__proto__` getter function exposes the value of the internal [[Prototype]] of an object. 
    - For objects created using an object literal, this value is `Object.prototype` .
    - For objects created using array literals, this value is `Array.prototype` . 
    - For functions, this value is `Function.prototype` . 
    - For objects created using `new fun` , where `fun` is one of the built-in constructor functions provided by JavaScript (Array, Boolean, Date, Number, Object, String, and so on — including new constructors added as JavaScript evolves), this value is always `fun.prototype` .
  - The `__proto__` setter allows the [[Prototype]] of an object to be mutated.
    - Changing the [[Prototype]] of an object is, by the nature of how modern JavaScript engines optimize property accesses, a **very slow** operation, in every browser and JavaScript engine
    - The effects on the performance of altering inheritance are subtle(不易察觉的，不明显的) and far-flung(广泛的), and are not limited to simply the time spent in `obj.__proto__ = ...` statements, but may extend to any code that has access to any object whose [[Prototype]] has been altered.
    - If you care about performance you should avoid setting the [[Prototype]] of an object. 
    - Instead, create a new object with the desired [[Prototype]] using `Object.create()` .
- `Object.prototype` 这个对象是个例外，它的 `__proto__` 值为 `null`

- __proto__的指向
  - 根据ECMA定义 'to the value of its constructor’s "prototype" ' ----指向创建这个对象的函数(构造函数)的显式原型
  - JS中对象被创建的方式，一眼看过去似乎有三种方式：（1）对象字面量 `{}` 的方式 （2） `new` 的方式 （3）ES5中的 `Object.create()`
  - 但是我认为本质上只有一种方式，也就是通过 `new` 来创建。
  - 首先字面量的方式是一种为了开发人员更方便创建对象的一个语法糖，本质就是 `var o = new Object(); o.xx = xx; o.yy=yy; `
  - 再来看 `Object.create()` , 这是ES5中新增的方法，在这之前这被称为原型式继承，
    - 从实现代码 return new F() 中我们可以看到，这依然是通过new来创建的。
    - 不同之处在于由 Object.create() 创建出来的对象没有构造函数，其实这里说它没有构造函数是指在 Object.create() 函数外部我们不能访问到它的构造函数，然而在函数内部实现中是有的
    - 因此由Object.create(o)创建出来的对象它的隐式原型指向o

``` JS
// 模拟object.create(o)
function object(o) {
  function F() {}
  F.prototype = o;
  return new F()
}
//以下是用于验证的伪代码，f就是object.create(o)创建出的对象
var f = new F();
//于是有
f.__proto__ === F.prototype //true
//又因为
F.prototype === o; //true
//所以
f.__proto__ === o;
```

- `Array.prototype` 也是一个对象，对象就是由 `Object()` 这个构造函数创建的，因此 `Array.prototype.__proto__ === Object.prototype` 为true，
  - 或者也可以这么理解，所有的内建对象都是由Object()创建而来。
  - `Foo.prototype.__proto__ === Object.prototype` //true 理由同上
- 如果构造函数带返回值且为对象，则该对象直接赋给变量，那么当然 `__proto__` 属性指向该对象的prototype咯。
  - 但一般来说，当函数作为构造器使用，不应该带返回值。

- instanceof
  - instanceof的左值一般是一个对象，右值一般是一个构造函数，用来判断左值是否是右值的实例
  - 它的内部实现原理是这样
  - 也就是沿着L的__proto__一直寻找到原型链末端，直到等于R.prototype为止

``` JS
//设 L instanceof R 
//通过判断
L.__proto__.__proto__..... === R.prototype？
//最终返回true or false
Function instanceof Object // true 
Object instanceof Function // true 
Function instanceof Function //true
Object instanceof Object // true
Number instanceof Number //false
```

- misc
  - __proto__是每个对象都有的一个属性，而prototype是函数才会有的属性。
  - __proto__指向的是当前对象的原型对象，而prototype指向的，是以当前函数作为构造函数构造出来的对象的原型对象。
- ref
  - [js中__proto__和prototype的区别和关系？](https://www.zhihu.com/question/34183746)

# es6 class extends vs node util.inherits

- Since the class and extends keywords are only syntactic sugar on top of prototypal inheritance, 
  - the answer simply is: Yes, you can replace `util.inherits` by `extends` and keep the same behavior.
- Of course, there are minor things to watch out for, 
  - e.g. you need to make sure to call the `super` constructor in your derived class's constructor, 
  - whereas with `util.inherits` you had to call the constructor function and `apply` it to `this`. 
  - But effectively, these things are only other syntactic constructs, semantically, they are equivalent.

- ref
  - [Can i replace util.inherits with es6's extend keyword?](https://stackoverflow.com/questions/44226524/can-i-replace-util-inherits-with-es6s-extend-keyword)

# when should I use es6 class

- es6的class提供了一个class实现的标准，之前无标准而较乱
- Opinionated take: 
  - Class inheritance, getters and setters makes your modules overly complex and hard to debug. 
  - Should have complicated syntax to discourage use, ES6 made it too easy.
- ref
  - [Why use classes instead of functions?](https://stackoverflow.com/questions/6480676/why-use-classes-instead-of-functions)

  - [5 reasons not to use ES6 classes in React](https://blog.krawaller.se/posts/5-reasons-not-to-use-es6-classes-in-react/)
    - Inconsistent context
    - No mixin support
    - Inconsistent state handling
    - Inconsistent definition
    - Dealing with super

  - [Not Awesome: ES6 Classes](https://github.com/petsel/not-awesome-es6-classes)
    - Instead of ES6 classes, you should consider factory functions, object composition, and/or prototypal inheritance via the use of prototypes, object literals, Object.create(), Object.assign(), etc. while avoiding constructors and the `new` keyword altogether.

## [Built in Constructor functions in Javascript (可以省略new)](https://stackoverflow.com/questions/9745729/built-in-constructor-functions-in-javascript)

- Because some built-in functions are just defined to act this way. 
- For example see ES5 15.2.1.1 for `Object`:
  - When the `Object` function is called with no arguments or with one argument value, the following steps are taken:
    - If value is `null/undefined` or not supplied, create and return a new Object object exactly as if the standard built-in Object constructor had been called with the same arguments (15.2.2.1).
    - Return `ToObject(value)`.
  - They test whether they have been called with `new` or not and if not act like they'd have been called with `new`.
  - You can implement this yourself:
    - `Foo()` and `new Foo()` will act the same way

``` JS
function Foo() {
  if (!(this instanceof Foo)) {
    return new Foo();
  }
  // do other init stuff
}
```

- Since your example is an Object type of built-in function, as it is answered above it is the same for this type, it does not work the same way for most of the other built-in functions such as `Number()`. 
  - You should be very careful when invoking them with the `new` keyword or not. 
  - Because by default the `new` keyword with a function constructor returns an object, not a primitive type directly. 
  - So you can not, for example, check strict equality on two variables that one of them is declared and assigned using `new Number()` , and the other is with `Number()`

``` JS
var num1 = Number(26);
var num2 = new Number(26);

num1 == num2; // returns true
num1 === num2; // returns false
```

- The `Object()` constructor behaves identically with and without the `new` keyword. That's just how it works.
  - Note that `Array()` and `new Array()` work the same way too
  - Doing some more testing I see that behavior happens with all factory constructors (String, Date, RegExp, etc.) 
  - Every factory constructor has its own behavior when it's called as a function. 
    - For instance, the `Date` constructor returns the date as a string (and not a `Date` object) when called as a function.
  - Precisely. The only way to know what happens is to read the spec (or a derivative work that tries to be more accessible :-). 
    - And again, most constructors in the wild (not part of the spec) probably don't implement specific non-construction behaviors (unless they say they do!).

- ref
  - [JavaScript: using constructor without operator 'new'](https://stackoverflow.com/questions/1928342/javascript-using-constructor-without-operator-new)

## call constructor function without new keyword. 使用构造函数代替类

- Here's a pattern I've come across that really helps me.
- It doesn't use a `class`, but it doesn't require the use of `new` either.

``` JS
const Foo = x => ({
  x,
  hello: () => `hello ${x}`,
  increment: () => Foo(x + 1),
  add: ({ x: y }) => Foo(x + y)
})

console.log(Foo(1).x) // 1
console.log(Foo(1).hello()) // hello 1
console.log(Foo(1).increment().hello()) // hello 2
console.log(Foo(1).add(Foo(2)).hello()) // hello 3
```

- This deserves points. 
  - I really wonder whether adding `class` to JS was an improvement. This shows what JS code should look like. 
  - For people wondering why there is no `this` anywhere, the created object is just using the `x` that was passed in to the 'constructor' (arrow function). 
  - Whenever it needs to be mutated, it returns a new object. The objects are immutable. 
- The problem with technique is that each time `Foo` is invoked, it has to create all methods again. 
  - With classes, the `prototype` methods are efficiently shared between instances without having to re-create then per instance. 
  - Because the methods are re-created, you use up more memory as well. 
  - For production purposes, it is better to use something similar to the answer by Tim and use a method to create a new class.
- my answer is similar to the one here except it doesn't create new functions each time.

``` JS
const assoc = (prop, value, obj) =>
  Object.assign({}, obj, {
    [prop]: value
  })

const reducer = ($values, accumulate, [key, val]) => assoc(key, val.bind(undefined, ...$values), accumulate)

const bindValuesToMethods = ($methods, ...$values) =>
  Object.entries($methods).reduce(reducer.bind(undefined, ...$values), {})

const prepareInstance = (instanceMethods, staticMethods = ({})) => Object.assign(
  bindValuesToMethods.bind(undefined, instanceMethods),
  staticMethods
)

// Let's make our class-like function
const Right = prepareInstance(RightInstanceMethods, RightStaticMethods)

const RightInstanceMethods = ({
  chain: (x, f) => f(x),
  map: (x, f) => Right(f(x)),
  fold: (x, l, r) => r(x),
  inspect: (x) => `Right(${x})`
})

const RightStaticMethods = ({
  of: x => Right(x)
})
```

- ref
  - [ES6: call class constructor without new keyword](https://stackoverflow.com/questions/30689817/es6-call-class-constructor-without-new-keyword)

## Please stop using classes in JavaScript

- Binding issues. 
  - As class constructor functions deal closely with `this ` keyword, 
  - it can introduce potential binding issues, especially if you try to pass your class method as a callback to an external routine (hello, React devs)
- Performance issues. 
  - Because of classes' implementation, they are notoriously difficult to optimize at runtime. 
- Private variables. 
  - One of the great advantages and the main reasons for classes in the first place, private variables, is just non-existent in JS.
- Strict hierarchies. 
  - Classes introduce a straight top-to-bottom order and make changes harder to implement, which is unacceptable in most JS applications.
- **Because the React team tells you not to**. 
  - While they did not explicitly deprecate the class-based components yet, they are likely to in the near future.
  - One of the design constraints and motivations for hooks was to represent a component being multiple states concurrently. That's something classes cannot express properly. 使用class组件对并发操作状态不友好
  - 想象一下这种场景，一个组件的render函数结构基本一致，但是它的数据层states可能会根据环境条件有不同的变化逻辑（相似的state结构，但是计算state的逻辑不同）

    - 这种情况下用class写就免不了大量的if else，
    - 但是hooks就可以把每种条件下的state变化逻辑抽离出来，
    - hooks比class组件更优雅的实现了states的多态

- Using a standard function+object+prototype chain "classes" is a good way to learn how JS works, but hiding all that behind the class sugar is too much abstraction to me.
  - Main benefit I get out of ES6 classes is defining the shape of data I am dealing with, so I can talk and think about it in precise terms. 
  - When I say "Customer", I know exactly what fields and properties that entails (and IDE will help me remember it too).
  - Member functions and inheritance are less useful for the reasons you stated in your article. 
  - Any kind of business code I prefer to keep in pure functions or service objects, that are given class based objects to manipulate. 
  - Code and data kept mostly separate.
- Before es6 class, I worked with projects that had different class implementations in them, all with their own ups and downs. Now everyone tends to use the ES2015 version and things are much clearer.
- proposed private field in js may not be better than typescript class.
- ref
  - https://everyday.codes/javascript/please-stop-using-classes-in-javascript/
  - https://dev.to/smalluban/do-we-really-need-classes-in-javascript-after-all-91n

# function declaration vs function expression(named vs anonymous)

- namedFunc pros
  - funcExpression难以递归调用自身(arguments.callee无法在严格模式)，具名可以
  - 调试时的可读性更好
  - usecase
    - 用在class中时常需要bind(this)
    - I prefer function because python and java both use it and I don’t get confused.

- funcExpression pros
  - 更好的scoped，namedFunc总是提升，而箭头函数是先声明再使用
  - 方便动态修改调用的函数
  - usecase
    - Arrow functions are especially meant to be placed inline, anonymously. 函数能写为一行时常用
    - 箭头函数常用作事件监听器函数
    - 箭头函数内部没有自己的局部this

- Availability (scope) of the function，函数或变量会自动提升hoist
  - one difference that concerns me is when the machine creates the function object. Which in the case of declarations is before any statement is executed but after a statement body is invoked (be that the global code body or a sub-function's), and in the case of expressions is when the statement it is in gets executed. 
- `(function(){}).name === ""` ，匿名函数表达式会返回true
  - Both have a name property
- In Google's V8 and Firefox's Spidermonkey there might be a few microsecond JIST compilation difference, but ultimately the result is the exact same.
- If we declare the variable as `function funcName(){}` , then the immutability of the variable is the same as declaring it with var。
  - function expression can be const
  - function declaration name can be reassigned, too
- Function Declarations are only allowed to appear in Program or FunctionBody. Syntactically, they can not appear in Block ( `{ ... }` ) — such as that of if, while or for statements. This is because Blocks can only contain Statements, not SourceElements, which Function Declaration is. 
  - The only way Expression is allowed directly within Block is when it is part of ExpressionStatement. 
  - However, ExpressionStatement is explicitly defined to not begin with "function" keyword, and this is exactly why Function Declaration cannot appear directly within a Statement or Block (note that Block is merely a list of Statements).
- ref
  - http://kangax.github.io/nfe/
  - https://stackoverflow.com/questions/336859/var-functionname-function-vs-function-functionname

# essentials

## Map vs Object

- Object is similar to Map
  - both let you set keys to values, retrieve those values, delete keys, and detect whether something is stored at a key. 
  - For this reason (and because there were no built-in alternatives), Object has been used as Map historically.
- However, there are important differences that **make Map preferable in certain cases**:
1. A Map does not contain any keys by default. It only contains what is explicitly put into it.
  - An Object has a prototype, so it contains default keys that could collide with your own keys if you're not careful.
  - As of ES5, this can be bypassed by using `Object.create(null)` , but this is seldom done.
2. A Map's keys can be any value (including functions, objects, or any primitive).
  - The keys of an Object must be either a String or a Symbol.
3. The keys in Map are ordered. Thus, when iterating over it, a Map object returns keys in order of insertion.
  - The keys of an Object are not ordered.
  - Since ECMAScript 2015, objects do preserve creation order for string and Symbol keys. 
  - In JavaScript engines that comply with the ECMAScript 2015 spec, iterating over an object with only string keys will yield the keys in order of insertion.
4. The number of items in a Map is easily retrieved from its `size` property.
  - The number of items in an Object must be determined manually.
5. A Map is an iterable, so it can be directly iterated.
  - Iterating over an Object requires obtaining its keys in some fashion and iterating over them.
6. Performs better in scenarios involving frequent additions and removals of key-value pairs.
  - Object is NOT optimized for frequent additions and removals of key-value pairs.
- ref
  - [mdn: Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
  - [Maps vs Objects in ES6, When to use?](https://stackoverflow.com/questions/32600157/maps-vs-objects-in-es6-when-to-use)

## for-in vs for-of

- Both `for...in` and `for...of` statements iterate over something. 
  - The main difference between them is in what they iterate over.
- The `for...in` statement iterates over the enumerable properties of an object, in an arbitrary order.
  - for-in遍历集合的属性，在遍历数组arr时会打印0, 1, 2, prop
- The `for...of` statement iterates over values that the iterable object defines to be iterated over.
  - for-of遍历集合的值，在遍历数组arr时会打印arr[0], arr[1], ...
- tips
  - Don't use for..in for Array iteration

- ref
  - [Difference between for...of and for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
