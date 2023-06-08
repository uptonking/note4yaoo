---
title: job-js-prototype-class
tags: [frontend, job, js]
created: 2021-10-10T09:08:20.137Z
modified: 2021-10-10T09:31:04.461Z
---

# job-js-prototype-class

# guide

# 如何理解原型？
- `Ctr.prototype` 显式原型: explicit prototype property
  - 每一个函数在创建之后都会拥有一个名为 `prototype` 的属性，这个属性指向函数的原型对象。
  - **显式原型的作用：用来实现基于原型的继承与属性共享**

- `obj.__proto__` 隐式原型: implicit prototype link
  - js中任意对象都有一个内置属性`[[Prototype]]`，在ES5之前没有标准的方法访问这个内置属性，但是大多数浏览器都支持通过 `__proto__` 来访问。
  - **对象的隐式原型指向创建这个对象的构造函数(constructor)的prototype**
  - ES5中有了对于这个内置属性标准的Get方法 `Object.getPrototypeOf()` .
  - **隐式原型的作用：构成原型链查找属性，同样用于实现基于原型的继承**

- `Object.prototype` 这个对象是个例外，它的 `__proto__` 值为 `null`.
- 修改对象的隐式原型影响范围一般较大，要避免，可以使用`Object.create(obj)` .

- 构造函数：任何情况下创建一个函数，都会在内部为其创建一个prototype属性，该属性是一个指向原型对象的引用。使用原型对象可以允许上面定义的属性与方法被对象实例共享。
- 原型对象：原型对象会默认自动获得一个constructor属性，该属性是指回构造函数的引用。自定义构造函数的原型对象默认只会获得constructor属性，其余方法都继承自Object
- 原型对象的原型：原型对象本身是Object或父类的实例，它也有一个暴露为__proto__的属性指向父类构造函数的原型对象（隐式原型）。特别的，Object的原型对象是原型链的起点，其constructor指向Object()构造函数，同时Object原型对象的不再有原型，其不再具有__proto__
- 对象实例：每个对象实例内部也有__proto__，同样指向其构造函数原型对象

```JS
var a = function() { this.b = 3; }
var c = new a(); // 创建一个新对象，构造函数中this指向新对象
a.prototype.b = 9;
var b = 7;
a(); // 这里再次设置window.b
console.log(b); // 3
c // {b: 3}
a.prototype // {b:9, constructor}

Function.prototype.__proto__ === Object.prototype // true

Array.constructor === Function //true
Function.constructor === Function //true

function aa() {}

aa.constructor === Function // true
aa.constructor.prototype === Function.prototype // true
aa.__proto__ === Function.prototype // true
Object.getPrototypeOf(aa) === Function.prototype // true
aa.prototype === Function.prototype // false
aa.prototype.__proto__ === Object.prototype // true
aa.prototype.constructor === aa // true，注意此时不能是箭头函数定义

let aaObj = new aa();
aaObj.constructor === aa // true
aaObj.__proto__ === aa.prototype // true
```

```JS
// 关于类与继承
// 👀 注意aa和ss属性都不在prototype上
class A { aa = '11';
  static ss = 'ss'; }
class B extends A { bb = '22' }

// 可以将class作为function来分析结果
A.__proto__ === Function.prototype // true
A.prototype.__proto__ === Object.prototype // true

// 👇🏻 继承实现的原理
B.__proto__ === A // true
B.prototype.__proto__ === A.prototype // true

// 继承实现的原理，子类没有自己的this对象，会继承父类this对象，并加工
// Object.setPrototypeOf(B.prototype, A.prototype) // B的实例继承A的实例
// Object.setPrototypeOf(B, A)  // B的实例继承A的静态属性

class A extends Object {}
A.__proto__ === Object // true
A.prototype.__proto__ === Object.prototype // true

class A {}
A.__proto__ === Function.prototype // true
A.prototype.__proto__ === Object.prototype // true
```

```JS
Function.prototype.a = () => alert(1);
Object.prototype.b = () => alert(2);

function A() {};
var a = new A();

// 查找属性时会沿着原型链查找
a.__proto__ === A.prototype // true
A.prototype.__proto__ === Object.prototype // true
a.__proto__.__proto__ === Object.prototype // true

a.a(); // Uncaught TypeError: a.a is not a function
a.b(); // 2
```

```JS
const prototype1 = {};
const object1 = Object.create(prototype1);

object1.__proto__ === prototype1 // true
object1.__proto__ === Object.prototype // false
object1.__proto__.__proto__ === Object.prototype // true

{}.toString(); // 不能直接调用字面量的方法，Uncaught SyntaxError: Unexpected token '.

// {} would instead be equivalent to Object.create(Object.prototype).
let oo = {};
oo.constructor.prototype === Object.prototype; // true
oo.__proto__ === Object.prototype; // true
oo.constructor === Object; // true

let aa = Object.create(null); // aa 没有toString等基础原型方法
```

# new新建对象时发生了什么
1. Creates a blank, plain JavaScript object.
2. Adds a property to the new object (`__proto__`) that links to the `constructor` function's `prototype` object 
3. Binds the newly created object instance as the `this` context 
   - (i.e. all references to `this` in the constructor function now refer to the object created in the first step).
4. Returns `this` if the function doesn't return an object.

- 在内存中创建一个新对象
- 新对象内部的[[Prototype]]特性被赋值为构造函数的prototype属性
- 构造函数内部的this被赋值为这个新对象（即this指向新对象）
- 执行构造函数内部的代码
- 如果构造函数返回非空对象，则返回该对象；否则，返回刚创建的新对象
# class
- 类使用在前，定义在后，这样会报错，因为ES6不会把变量声明提升到代码头部。
  - 这种规定的原因与继承有关，必须**保证子类在父类之后定义**。

- 类的方法内部如果含有this ，它将默认指向类的实例 。 
  - 但是，必须非常小心， 一旦单独使用该方法，很可能会报错。
  - 如果将这个方法提取出来单独使用， this 会指向该方法运行时所在的环境
  - 方法1: 在构造函数中bind
  - 方法2: 方法的定义使用箭头函数
  - 方法3: 创建对象实例时，创建并返回Proxy对象，代理对象的处理器中在获取方法时，先bind方法再返回

- new.target内置属性，可以在构造函数中获取new命令所作用的构造函数
  - `new.target` pseudo-property lets you detect whether a function or constructor was called using the `new` operator. 
  - In constructors and functions invoked using the `new` operator,  `new.target` returns a reference to the constructor or function. 
  - In normal function calls,  `new.target` is `undefined`.
  - Class 内部调用 new.target ，返回当前 Class
  - 子类继承父类时 ηew . target 会返回子类。
  - 可以写出不能独立使用而必须继承后才能使用的类：在父类和子类构造函数中分别检查new.target

- 私有方法的实现

```JS
// 💡️ 方法1: 将私有方法移出模块，不可访问私有方法，但仍可直接访问私有值

class C1 {

  getPrivate(args) {
    getPrivateImpl.call(this, args);
  }
}

function getPrivateImpl(args) {
  return this.val = args;
}

// 💡️ 方法2: 将私有方法命名为一个Symbol值

const privateFn = Symbol('privateFn');
const privateVal = Symbol('privateVal');

class C2 {

  getPrivate(args) {
    this[privateFn](args);
  }

  [privateFn](args) {
    this[privateVal] = args;
  }
}

function getPrivateImpl(args) {
  return this.val = args;
}
```

# js继承
- 原型链继承
- 寄生式继承

- class关键字，类实际就是函数，但是类语法明确了存在于实例、原型、类上的成员
  - ES6使用extends关键字继承，可以继承类或者普通的构造函数，其背后依旧基于“寄生式组合继承”

- ES6继承 vs ES5继承
  - ES5的继承是先创造子类的实例对象this，然后再将父类的方法添加到 this 上面 (`Parent.apply(this)`)。
  - ES6的继承机制完全不同，实质是先创造父类的实例对象 this（所以必须先调用 `super()` 方法），然后再用子类的构造函数修改 this 。
    - 因为es6子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。
    - super虽然代表了父类 A 的构造函数，但是返回的是子类 B 的实例，即 super 内部的 this 指的是 B，因此 `super()` 在这里相当于`A.prototype.constructor.call(this)`;
    - ES6规定，通过 super 调用父类的方法时， super 会绑定子类的 this
  - ES5原型链中子类原型是父类实例，子类构造函数和父类构造函数无直接关系，因此需要使用call()
    - ES6具有双重继承关系：除了原型对象间继承，子类本身是父类构造的实例

- ref
  - [深入JavaScript继承原理](https://juejin.cn/post/6844903569317953543)
# `Object.create(proto, propertiesObject)`

- creates a new object, using an existing object as the prototype of the newly created object.

```JS
function objectCreate(o) {

  function F() {}

  F.prototype = o;

  return new F();
}

const newObj = objectCreate(obj);
```

- 当修改newOBj.constructor.prototype的属性的时候，旧的o.constructor.prototype就不会被修改

- [Object.create 内部为什么要用一个中间函数来实现？](https://www.zhihu.com/question/272240823)
  - 动态修改继承关系会严重降低性能（现代浏览器优化失效），所以用 ES6 的 `Reflect.setPrototypeOf` 也一样不可取。
