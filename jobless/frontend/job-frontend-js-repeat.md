---
title: job-frontend-js-repeat
tags: [frontend, job, js, repeat]
created: '2021-09-21T19:54:16.072Z'
modified: '2021-09-23T08:17:23.261Z'
---

# job-frontend-js-repeat

# guide

# faq

## 如何理解原型？

- `Ctr.prototype` 显式原型: explicit prototype property
  - 每一个函数在创建之后都会拥有一个名为 `prototype` 的属性，这个属性指向函数的原型对象。
  - **显式原型的作用：用来实现基于原型的继承与属性共享**

- `obj.__proto__` 隐式原型: implicit prototype link
  - js中任意对象都有一个内置属性[[prototype]]，在ES5之前没有标准的方法访问这个内置属性，但是大多数浏览器都支持通过 `__proto__` 来访问。
  - **对象的隐式原型指向创建这个对象的构造函数(constructor)的prototype**
  - ES5中有了对于这个内置属性标准的Get方法 `Object.getPrototypeOf()` .
  - **隐式原型的作用：构成原型链查找属性，同样用于实现基于原型的继承**

- `Object.prototype` 这个对象是个例外，它的 `__proto__` 值为 `null`.
- 修改对象的隐式原型影响范围一般较大，要避免，可以使用`Object.create(obj)` .

- 构造函数：任何情况下创建一个函数，都会在内部为其创建一个prototype属性，该属性是一个指向原型对象的引用。使用原型对象可以允许上面定义的属性与方法被对象实例共享。
- 原型对象：原型对象会默认自动获得一个constructor属性，该属性是指回构造函数的引用。自定义构造函数的原型对象默认只会获得constructor属性，其余方法都继承自Object
- 原型对象的原型：原型对象本身是Object或父类的实例，它也有一个暴露为__proto__的属性指向父类构造函数的原型对象（隐式原型）。特别的，Object的原型对象是原型链的起点，其constructor指向Object()构造函数，同时Object原型对象的不再有原型，其不再具有__proto__
- 对象实例：每个被构造的实例内部也有__proto__，同样指向其构造函数原型对象

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

function aa() {}

aa.__proto__ === Function.prototype // true
aa.prototype === Function.prototype // false
aa.prototype.__proto__ === Object.prototype // true

let aaObj = new aa();
aaObj.constructor === aa // true
aaObj.__proto__ === aa.prototype // true
```

```JS
// 关于类与继承

class A {}
class B extends A {}

B.__proto__ === A // true
B.prototype.__proto__ === A.prototype // true

// 继承实现的原理
// Object.setPrototypeOf(B.prototype , A.prototype) // B 的实例继承 A 的实例
// Object.setPrototypeOf (B, A)  // B 的实例继承 A 的静态属性

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
// a.__proto__ === A.prototype  // true
// A.prototype.__proto__ === Object.prototype  // true
a.a();
a.b(); // Uncaught TypeError: a.a is not a functionI
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

## new新建对象时发生了什么

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
