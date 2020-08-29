---
title: log-faq-dev-repeat
tags: [dev, faq, repeat]
created: '2019-08-01T16:03:46.394Z'
modified: '2020-08-18T06:14:25.248Z'
---

# log-faq-dev-repeat

## faq-not-yet

- 开发list组件和tree组件，是先开发list然后用多个list创建tree更好，还先开发tree然后用深度为2的tree创建list更好？
  - react-virtualized: List uses a Grid internally to render the rows
- Why it is important to cache DOM: http://jsperf.com/dom-caching-excercise

## hide dom elements: visibility vs display

- `visibility: hidden` does not cause a reflow on the document, while `display: none` does.
- `display:none` will remove the element from the document's normal flow and set the values for position/height/width to 0 on the element and its children. 
  - When the elements display property is changed to other value than `none` , it triggers a complete document re-flow, which can be a problem for big documents - and sometimes not-so-big documents being rendered on hardware with limited capabilities.
- If you are adding a lot of elements to a DOM, and you add them to the container with `visibility: hidden` , then you'll provoke a reflow for each one. 
  - On the other hand, you can add as many elements as you want with `display:none` and show them all at once provoking a single reflow. 
  - The performance taxing action is the the reflow.
  - 这里描述的是特殊场景，动态添加隐藏的div。
- `visibility: hidden` acts like `opacity: 0` + `pointer-events: none` . 
- `display: none` acts like `Element.remove()` .
- ref
  - [Performance differences between visibility:hidden and display:none](https://stackoverflow.com/questions/11757016/performance-differences-between-visibilityhidden-and-displaynone)

## 对象解构时，特别地，对react函数组件的props参数解构时，是在参数处解构更好，还是在函数体内解构更好？

``` JS
// 在参数处解构，变量默认是let
function MyComponent({ name, age, height }) {
  // do stuff here
}

function MyComponent(props) {
  // 在函数体内解构，变量被指定为const
  const { name, age, height } = props
  // do stuff here
}

<MyComponent name="bob" age={25} height = {175} haspets={false}/>
```

- 在函数内解构，除了可以获取各prop参数变量外，还方便使用整体的props对象
- 在参数处解构，更直观的写法，便于第三方插件如doc-gen提取参数默认值
  - 解构多层嵌套对象的深层属性时，要考虑提取参数的意义与困难度
- 使用 `arguments[0]` 也可以获取整体props对象，但箭头函数没有 `this` , `super` , `arguments` , `new.target` ，且箭头函数不能用作构造函数
- One of the differences I can think of, and I suppose the most important, is that on the second case, while you are destructing your props object in function body, you are using `const` on declaration.
  - In that way, you can no longer change these values on your MyComponent, while on your first case you could easily modify them.
  - 对react组件来说，props不能改变，推荐只用const解构，但对普通函数参数解构时，要考虑用let
- ref
  - [Different ways of destructuring props in react](https://stackoverflow.com/questions/59586876/different-ways-of-destructuring-props-in-react)
  - [ES6 destructuring function parameter - naming root object](https://stackoverflow.com/questions/29051011/es6-destructuring-function-parameter-naming-root-object)

## when should I use class

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

## In js, what does `this` refer to?

- `this` is a property of an execution context (global, function or eval) that, in non–strict mode, is always a reference to an object 
  - and in strict mode can be any value.

- A function's `this` keyword behaves a little differently in JavaScript compared to other languages. 
- It also has some differences between strict mode and non-strict mode.
- In most cases, the **value of `this` is determined by how a function is called (runtime binding)**. 
- It can't be set by assignment during execution, and it may be different each time the function is called. 
- ES5 introduced the `bind()` method to set the value of a function's this regardless of how it's called, 
- and ES2015 introduced arrow functions which don't provide their own this binding (it retains the this value of the enclosing lexical context).

- In the global execution context (outside of any function), `this` refers to the global object( `window` ) whether in strict mode or not.
- You can always easily get the global object using the global `globalThis` property, regardless of the current context in which your code is running.

- Inside a function, the value of `this` depends on how the function is called.
- Since the following code is not in strict mode, and because the value of `this` is not set by the call, `this` will default to the global object, which is `window` in a browser

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
- To set the value of this to a particular value when calling a function, use `call()` , or `apply()` . 
  - The first parameter is the object to use as 'this', subsequent parameters are passed as arguments in the function call
  - Note that in non–strict mode, with call and apply, if the value passed as this is not an object, an attempt will be made to convert it to an object. 
  - Values null and undefined become the global object. 
  - Primitives like 7 or 'foo' will be converted to an Object using the related constructor, so the primitive number 7 is converted to an object as if by new Number(7) and the string 'foo' to an object as if by new String('foo')

- The behavior of `this` in classes and functions is similar, since classes are functions under the hood.
- Within a class constructor, `this` is a regular object. 
  - All non-static methods within the class are added to the prototype of `this`
  - Static methods are not properties of this. They are properties of the class itself.
- For derived classes, derived constructors have no initial `this` binding. 
- Calling `super()` creates a this binding within the constructor, like evaluating `this = new Base();`
- Referring to this before calling super() will throw an error.
- Derived classes must not return before calling super(), unless they return an Object or have no constructor at all. 

- Calling `f.bind(someObject)` creates a new function with the same body and scope as `f` , but where `this` occurs in the original function, in the new function it is permanently bound to the first argument of `bind` , regardless of how the function is being used.

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

- In arrow functions, `this` retains the value of the enclosing lexical context's `this` . In global code, it will be set to the global object
- If `this` arg is passed to `call` , `apply` , or `bind` on invocation of an arrow function, it will be ignored. 
  - You can still prepend arguments to the call, but the first argument (thisArg) should be set to null

- **When a function is called as a method of an object, its `this` is set to the object the method is called on**.
  - In the following example, when `o.f()` is invoked, inside the function `this` is bound to the `o` object.
  - Note that this behavior is not at all affected by how or where the function was defined.
  - This demonstrates that it matters only that the function was invoked from the `f` method member of object `o` .
  - `this` is only affected by the most immediate member reference

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

- If the method is on an object's prototype chain, `this` refers to the object the method was called on, as if the method were on the object.

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

- this in classes
  - Just like with regular functions, the value of `this` within methods depends on how they are called. 
  - Sometimes it is useful to override this behavior so that `this` within classes always refers to the class instance. 
  - To achieve this, `bind` the class methods in the constructor
  - Classes are always strict mode code. Calling methods with an undefined `this` will throw an error.

``` JS
class Car {
  constructor() {
    this.sayBye = this.sayBye.bind(this);
  }
  sayHi() {
    console.log( `Hello from ${this.name}` );
  }
  sayBye() {
    console.log( `Bye from ${this.name}` );
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

- tips
  - Don't use this
    - You actually don't want to access `this` in particular, but the object it refers to. 
    - That's why an easy solution is to simply create a new variable that also refers to that object. 
    - The variable can have any name, but common ones are `self` and `that` .
  - Explicitly set this of the callback 
    - use `bind`
 

- ref
  - [mdn this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
  - [How to access the correct `this` inside a callback?](https://stackoverflow.com/questions/20279484/how-to-access-the-correct-this-inside-a-callback)

## js对象内的属性如何引用同一对象的另一个属性

- 如果不介意在对象字面量外写的话

``` js
    var a = {
      p1: [1]
    }
    a.p2 = a.p1
```

- 如果要在对象字面量内写的话，可以使用访问器属性

``` js
    var a = {
      p1: [1],
      // p2: a.p1//this.p1  // 都是错的
      get p2() { return this.p1 },
      set p2(v) { this.p1 = v }
    }
    a.p1 === a.p2 //true
    a.p2 = 1;
    a.p1; // 1
```

- 对象字面量里this和a都是从作用域链中去寻找的
  - ES6之前只有两个作用域，全局或函数，
  - 在这里，没有函数，就是全局作用域，所以 this 和 a 就会从当前全局作用域中去寻找

``` js
    var a = { p1: 111 };
    var a = {
      p1: [1],
      p2: a.p1
    }
    a.p2 //111
```

## Can a JavaScript object property refer to another property of the same object?

- Unfortunately, no. 
- The `{}` syntax initiates creation of a new object, but until the object is created, it isn't assigned to the carousel variable. 
- Also, the `this` value can only change as a result of a function call. 
- If your "several more properties" are all going to depend only on slider, then you could get around with something like this:

``` JS
      var slider = $('.slider');
      var carousel = {
        panes: slider.children.length(),
        something: slider.something_else,
      };
      carousel.slider = slider;

      var a, b;
      var foo = {
        a: a = 5,
        b: b = 6,
        c: a + b
      };
```

- Not with object literals (this has the same value during constructing of the literal that it did before-hand). But you can do  

``` JS
      var carousel = new(function() {
        this.$slider = $('#carousel1 .slider');
        this.panes = this.$slider.children().length;
      })();

      var foo = new function() {
        this.a = 5;
        this.b = 6;
        this.c = this.a + this.b;
      };

      var foo = function() {
        var a = 5;
        var b = 6;
        var c = a + b;

        return {
          a,
          b,
          c
        }
      }();
```

- The `get` syntax binds an object property to a function that will be called when that property is looked up.

``` js
      var foo = {
        a: 5,
        b: 6,
        get c() {
          return this.a + this.b;
        }
      }
      console.log(foo.c) // 11
```

- eg1: assign the return value of init() to foo. you have to `return this` .

``` js
      var foo = {
        a: 5,
        b: 6,
        init: function() {
          this.c = this.a + this.b;
          //delete this.init
          return this;
        }
      }.init();
```

- eg2: separate

``` js
      var foo = {
        a: 5,
        b: 6
      };
      foo.c = foo.a + foo.b;
```

- eg3: once, more 

``` js
      var foo = function(o) {
        o.c = o.a + o.b;
        return o;
      }({ a: 5, b: 6 });

      function buildFoo(a, b) {
        var o = { a: a, b: b };
        o.c = o.a + o.b;
        return o;
      }
```

- eg4: es6 class

``` js
      class Foo {
        constructor() {
          this.a = 5;
          this.b = 6;
          this.c = this.a + this.b;
        }
      }
      const foo = new Foo();
```

## js function declaration vs function expression(named/anonymous)

- 匿名函数表达式无法递归调用自身(arguments.callee无法在严格模式)，具名可以
- 调试时的可读性
- Availability (scope) of the function，函数或变量会自动提升hoist
  - one difference that concerns me is when the machine creates the function object. Which in the case of declarations is before any statement is executed but after a statement body is invoked (be that the global code body or a sub-function's), and in the case of expressions is when the statement it is in gets executed. 
- `(function(){}).name === ""` ，匿名函数表达式会返回true
  - Both have a name property
- In Google's V8 and Firefox's Spidermonkey there might be a few microsecond JIST compilation difference, but ultimately the result is the exact same.
- If we declare the variable as function funcName(){}, then the immutability of the variable is the same as declaring it with var。
  - function expression can be const
  - function declaration name can be reassigned, too
- Function Declarations are only allowed to appear in Program or FunctionBody. Syntactically, they can not appear in Block ( `{ ... }` ) — such as that of if, while or for statements. This is because Blocks can only contain Statements, not SourceElements, which Function Declaration is. 
  - The only way Expression is allowed directly within Block is when it is part of ExpressionStatement. 
  - However, ExpressionStatement is explicitly defined to not begin with "function" keyword, and this is exactly why Function Declaration cannot appear directly within a Statement or Block (note that Block is merely a list of Statements).
- ref
  - http://kangax.github.io/nfe/
  - https://stackoverflow.com/questions/336859/var-functionname-function-vs-function-functionname

## 数组对象能添加自定义属性吗？ 可以

- `var arr=[1,2,3]; arr.count=3;`
- console.log(arr)得到 `[1, 2, 3, b: 33]`
- arr.length得到3
- 可以借助此方法对数组插值，参考styled-system的responsive array prop value

## Is it possible to have a comment inside a es6 template string?

- comment in expression interpolation  

``` js
  const fields = `
    id, ${ /* post id */'' }
    message, ${ /* post status/message */'' }
    created_time
  `;
```

- parse comment in tag function  

``` js
  const commented = (strings, ...values) => {
    const pattern = /\/{2}.+$/gm; // basic idea

    return strings.map(
        (str, i) =>
 `${str}${values[i] !== undefined ? values[i] : ''}`
      )
      .join('')
      .replace(pattern, '');
  };

  const d = 10;
  const fields = commented `
    ${d}
    id, // post ID
    ${d}
    message, // post/status message
    created_time, // ...
    permalink_uri,
    type
  `;
```

## firefox与chrome滚动条样式不一致，应该如何处理

- 结论
  - 选择1：放弃自定义滚动条，使用系统默认的，各操作系统实现的滚动条不一致
  - 选择2：remove scrollbars
    - 使用箭头导航，add some arrows to scroll the content
    - 放弃滚动条，使用分页
- 可参考perfect-scrollbar(MIT)实现跨浏览器样式一致的滚动条
  - https://mdbootstrap.com/snippets/jquery/filipkapusta/765760
  - No manipulation on DOM tree
  - Use plain scrollTop and scrollLeft
  - 最外层的(竖直)滚动条问题仍未解决，firefox是自动隐藏且收窄的
- 自定义滚动条样式时要注意
  - scrollbar styling is part of the OS
  - 在触摸板上向上滑动时，页面顶部会逐渐隐藏，此时滚动条下移
  - 直接向上拖动滚动条时，页面顶部已隐藏的部分逐渐显示，与上面相反
- ref
  - https://stackoverflow.com/questions/47138603/scroll-issue-on-firefox-vs-webkit-browsers-side-navigation-text-truncate-and
  - https://www.zhihu.com/question/278165453
  - chrome支持滚动条的样式修改，但是又有多少网站去改变了滚动条的样式呢？为什么这几个相关的css私有伪元素，为什么一直没有被w3c标准采纳？
    - 换个样式，并不能让操作变得更方便。而样式方面的问题，用户完全可以按照自己的喜好选择操作系统中的主题
    - Every other browser, with the exception of chrome, uses the default OS UI for the scrollbar, which means, the scrollbars will look almost the same regardless which browser you use.
      - In Windows is a thick gray scrollbar with two buttons on the edges that work for going up/down.  
      - In OSX for instance, scrollbar never appear, until you scroll, and it looks like a discrete rectangle moving downward to the page you are scrolling.  
      - In contrast chrome uses a customized scrollbar instead of the default so it looks consistent in every OS it uses.

## 前后端分离导致的单点登录不可用如何解决

- 使用json web token，每个请求都带身份认证id
