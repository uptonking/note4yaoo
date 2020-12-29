---
title: lang-js
tags: [js, lang]
created: '2019-06-09T05:36:13.734Z'
modified: '2020-07-14T09:26:50.808Z'
---

# lang-js

## tips

- all in js as frontend

## js guide

- js vm bytecode
- Replace `arr.filter().map()` with `arr.reduce()`
  - 可以减少遍历次数
- Object.assign修改属性值的性能
- https://github.com/airbnb/javascript

## faq

- js复制数组方法的性能比较
  - `b = [...a]`
  - `b = a.slice()`
- `new Date()` vs `performance.timing`
  - Navigation Timing API gives us a more accurate measure  
- eval vs template literals
  - template literals are parsed at compile time
  - the argument to eval only gets parsed at runtime, when eval is executed.
  - eval can get a dynamically built argument, while a template literal is literal: it cannot be stored as a template variable. A tag function does not actually get a template variable as argument, but the parsed components of it, which are known at compile-time.
- setTimeout添加的异步任务队列和requestAnimationFrame每帧执行的任务队列是一个吗
  - ？？？
  - 参考 https://stackoverflow.com/questions/43050448/when-will-requestanimationframe-be-executed
- 写js时候，需要用到严格模式（use strict）吗
  - 现在严格模式都不算严格， 还是容易写出安全隐患，还要搭配使用eslint
  - 虽然严格模式会失去js很多原有的灵活性啊，但是有利于js正式化
  - 对于ES6来说模块始终以严格模式被解析, 但这一点过去对于非ES6目标在生成的代码中并没有遵循
  - 从TypeScript 1.8开始, 输出的模块总会为严格模式
- 使用apply/call方法时第一个参数传入null有什么用
  - 第一个参数指定了函数体内this对象的指向
  - 在使用call和apply的时候，如果传入的第一个参数是null，在非严格模式下，函数体内的this会默认指向宿主对象，在浏览器环境里就是window，在严格模式下this还是null
  - 参考 https://www.cnblogs.com/snandy/archive/2012/03/01/2373243.html
- js连等赋值A=B=C的原理
  - 赋值云算符是右结合的，从右边开始向左边赋值
  - 真正的运算规则是 B = C; A = B; 左右持有的是右边对象的引用
  - 实例分析

``` js
      var a = { n: 1 };
      a.x = a = { n: 2 }; // a.x指向之前的地址是因为.运算符优先于=赋值运算符
      console.log(a.x); // 输出undefined 
```

    1. 在执行前，会先将a和a.x中的a的引用地址都取出来，此值他们都指向{n:1}
    2. 在内存中创建一个新对象{n:2}
    3. 执行a={n:2}，将a的引用从指向{n:1}改为指向新的{n:2}
    4. 执行a.x=a，此时a已经指向了新对象，而a.x因为在执行前保留了原引用，所以a.x的a依然指向原先的{n:1}对象，所以给原对象新增一个属性x，内容为{n:2}也就是现在a
    5. 语句执行结束，原对象由{n:1}变成{n:1,x:{n:2}}，而原对象因为无人再引用他，所以被GC回收，当前a指向新对象{n:2}
    6. 所以执行a.x，自然就是undefined了
  - 结论
    - 少用连等符号，会出现全局变量
- js虚拟机和jvm有什么关系
  - JS的虚拟机有JSC、spidermonkey、v8等，跟JVM没有什么直接的联系
  - V8的team leader是Lars Bak，jvm的Hotspot正是Lars Bak领导开发的
  - 在V8出现之前，JS引擎的技术比较原始，正是Lars Bak率先将JVM中先进的技术带到了JS引擎中的，如分代式GC、机器码直接生成等
- 若在js函数内部不使用var直接定义一个变量并赋值，则在函数外部能访问吗
  - 可以访问
  - 示例

``` js
  function sayA() {

    var a = 'aaa';
    b = 'bbb';
    console.log('===', a + b);

  }
  console.log(a); // error, not defined
  console.log(b); // bbb
```

- 跨window传递数据的方法
  - `window.opener`

## data type

### Boolean

- The `Boolean()` constructor is used to create `Boolean` objects.
- The Boolean object is an object wrapper for a boolean value.
- The value passed as the first parameter is converted to a boolean value, if necessary. 
- If the value is omitted or is 0, -0, null, false, NaN, undefined, or the empty string (""), the object has an initial value of `false` . 
- All other values, including any object, an empty array ([]), or the string "false", create an object with an initial value of `true` .
- Do not use a Boolean object to convert a non-boolean value to a boolean value. 
  - To perform this task, instead, use Boolean as a function, or a double NOT operator

``` JS
var x = Boolean(expression); // use this...
var x = !!(expression); // ...or this
var x = new Boolean(expression); // don't use this!

var myFalse = new Boolean(false); // initial value of false
var g = Boolean(myFalse); // initial value of true
var myString = new String('Hello'); // string object
var s = Boolean(myString); // initial value of true
```

- If you specify any object, including a Boolean object whose value is `false` , as the initial value of a Boolean object, the new Boolean object has a value of `true` .

- `array.filter(Boolean)` 中的Boolean的作用
  - 这里的Boolean是一个function，最终只保存结果为true的项目
  - `arrayOfSheeps.filter(Boolean).length`
  - `arrayOfSheeps.filter(function(x){return Boolean(x)}).length`

### WeakMap

- WeakMap is a collection of key/value pairs where the keys are weakly referenced
  - fast keyed access to value
  - not prevent keys from garbage collection
  - keys are not enumerable
  - keys must be objects
- WeakMaps are ideal for preventing memory leaks when keeping DOM nodes as keys
- There are various use cases when you don't control the keys' garbage collection, and WeakMaps are the way to ensure you're not leaking memory. 

## mdn docs

### 函数参数

- 在JavaScript高级程序设计中，第4.1.3节传递参数这一节中，作者说的是ECMAScript中所有函数的参数都是按值传递的
- Primitive parameters (such as a number) are passed to functions by value; 
  - the value is passed to the function, but if the function changes the value of the parameter, this change is not reflected globally or in the calling function.
- If you pass an object (i.e. a non-primitive value, such as Array/user-defined object) as a parameter and the function changes the object's properties, that change is visible outside the function, as shown in the following example

``` JS
function f1(a) {
  alert(a);
  a = 1; //修改形参a  使用arguments[0] = 1修改效果一样
  alert(1 === a);
  alert(1 === arguments[0]);
}
f1(10);
// 函数f1定义了参数a，调用时传参数10，先弹出10，修改a为1，弹出两次true，a和arguments[0]都为1了。
```

### window.postMessage()

- method safely enables cross-origin communication between Window objects; e.g., between a page and a pop-up that it spawned
- Normally, scripts on different pages are allowed to access each other if and only if the pages they originate from same origin
- window.postMessage() provides a controlled mechanism to securely circumvent this restriction
- Broadly, one window may obtain a reference to another (e.g., via targetWindow = window.opener), and then dispatch a MessageEvent on it with targetWindow.postMessage(). 
- The receiving window is then free to handle this event as needed. 
- The arguments passed to window.postMessage() (i.e., the “message”) are exposed to the receiving window through the event object.

### this

- `this` is a property of an execution context (global, function or eval) that, 
  - in non–strict mode, is always a reference to an object 
  - and in strict mode can be any value.
- In the global execution context(outside of any function),  `this` refers to the global object whether in strict mode or not.
  - You can always easily get the global object using the global globalThis property, regardless of the current context in which your code is running.
- Inside a function, the value of `this` depends on how the function is called.
- in non-strict mode, because the value of this is not set by the call, this will default to the global object, which is window in a browser.
- In strict mode, however, if the value of this is not set when entering an execution context, it remains as undefined
- To set the value of this to a particular value when calling a function, use call(), or apply()
  - es5 introduces `bind()`
  - In arrow functions, this retains the value of the enclosing lexical context's this
- In most cases, the value of `this` is determined by how a function is called (runtime binding). 
  - It can't be set by assignment during execution, and it may be different each time the function is called.
- **When a function is called as a method of an object, its `this` is set to the object the method is called on**.

- globalThis
  - Historically, accessing the global object has required different syntax in different JavaScript environments. 
  - On the web you can use `window/self/frames` - but in Web Workers only `self` will work. 
  - In Node.js none of these work, and you must instead use `global`
  - The `this` keyword could be used inside functions running in non–strict mode, but `this` will be `undefined` in Modules and inside functions running in strict mode. 
  - The `globalThis` property provides a standard way of accessing the global this value (and hence the global object itself) across environments. 
    - Unlike similar properties such as window and self, it's guaranteed to work in window and non-window contexts.
    - in global scope the `this` value is `globalThis`
    - In many engines globalThis will be a reference to the actual global object
    - but in web browsers, due to iframe and cross-window security considerations, it references a Proxy around the actual global object (which you can't directly access). 
    - This distinction is rarely relevant in common usage, but important to be aware of.

- `Object()`
  - The Object constructor creates an object wrapper for the given value
  - If the value is null or undefined, it will create and return an empty object, otherwise, it will return an object of a Type that corresponds to the given value.
  - If the **value is an object already**, it will return the value.

``` js
  const a = { aa: 1 };
  Object(a) === a //true
  Object('a') === 'a' //false
  Object(1) === 1 //false
```

- `arr.slice()`
  - arr.slice(); // [0, end]
  - arr.slice(begin); 
  - arr.slice(begin, end)     
  - 方法返回一个新的数组对象，这一对象是一个由begin和end（不包括end）决定的原数组的浅拷贝
  - 原始数组不会被改变
- `array.splice(start[, deleteCount[, item1[, item2[, ...]]]])`
  - start 指定修改的开始位置（从0计数）
  - deleteCount 整数，表示要移除的数组元素的个数
  - item1, item2, .. 要添加进数组的元素, 从start位置开始
  - 返回由被删除的元素组成的一个数组，如果只删除了一个元素，则返回只包含一个元素的数组，如果没有删除元素，则返回空数组
  - splice()与slice()的作用是不同的，splice()会直接对数组进行修改
- `arr.reverse()`
  - reverse 方法颠倒数组中元素的位置，并返回该数组的引用
- `Object.assign(target, ...sources)`
  - method is used to copy the values of all enumerable own properties from one or more source objects to a target object. It will return the target object.
  - shallow copies property values. If the source value is a reference to an object, it only copies that reference value.

### setTimeout vs setInterval

- 相同点
  - setTimeout和setInterval的回调函数，都是经过n毫秒后被添加到队列中，而不是过n毫秒后立即执行
      - 表示的是何时将定时器的代码添加到异步队列，而不是何时执行代码
      - 真正何时执行代码的时间是不能保证的，取决于何时被主线程的事件循环取到并执行
- 使用动画方面
  - setInterval只执行一次，并且定时器的ID始终不变，setTimeout需要执行多次，并且每次执行都会生成新的ID
  - setTimeout迭代式方法的调用方式，压栈、出栈都不是轻量级的任务
  - setTimeout自身消耗了部分性能
- setInterval受单线程影响可能出现时间不精确现象，如果函数的执行时间超过设置的间隔时间，会出现函数小于间隔时间而执行或无间隔执行的情况
- 如果用setTimeout来模拟setInterval，这样函数执行的间隔时间就会保证（>=设置时间）

### setTimeout

- ref
  - https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout
  - https://www.jeffjade.com/2016/01/10/2016-01-10-javacript-setTimeout/
- `var timeoutID = scope.setTimeout(function[, delay, arg1, arg2, ...]);`
- `setTimeout()` method of the WindowOrWorkerGlobalScope mixin (and successor to Window.setTimeout()) sets a timer which executes a function or specified piece of code once the timer expires.
- The returned timeoutID is a *positive integer value* which identifies the timer created by the call to setTimeout()
- use cases
  - 替换setInterval来实现定时任务
  - 防止事件持续触发
  - 延时生效，如 on keyup paste cut
  - 调整事件的发生顺序
  - 分割耗时任务
  - setTimeout和setInterval返回的整数值是连续的(一定环境下，比如浏览器控制台，或者js执行环境等)，也就是说，setTimeout方法返回的整数值将比第一个的整数值大1。利用这一点，可以写一个函数，取消当前所有的setTimeout。
- 问题
  - 当线程中没有执行任何同步代码的前提下才会执行异步代码，setTimeout是异步代码，所以setTimeout只能等js空闲才会执行。若主线程有个死循环，死循环是永远不会空闲的，所以setTimeout也永远不会执行
- setTimeout(0) vs window.postMessage vs MessagePort.postMessage
  - using window.postMessage is a preferred way
  -  While setTimeout is waiting to invoke it's callback, it's *non-blocking*. 
  - The call is simply added to a queue. At some point in the future the callback fires and the call is removed from that queue.
  - setTimeout callback is within a closure. As soon as setTimeout invokes the callback, it becomes eligible for garbage collection.
  - using a 15 minutes timeout function might be problematic for debugging and maintaining.
  - The 60 second timer is implemented by magic in the OS: it basically adds no CPU load during the 60 seconds it is waiting.
- setTimeout and setInterval share the same pool of IDs, and that clearTimeout and clearInterval can technically be used interchangeably. 
- a timeout ID will never be reused by a subsequent call to setTimeout() or setInterval() on the same object (a window or a worker). However, different objects use separate pools of IDs.
- Code executed by setTimeout() is called from an execution context separate from the function from which setTimeout was called. The usual rules for setting the this keyword for the called function apply, and if you have not set this in the call or with bind, it will default to the global (or window) object in non-strict mode, or be undefined in strict mode.
- A common way to solve the problem is to use a wrapper function that sets this to the required value
- Arrow functions are a possible alternative, too
- Passing a string instead of a function to setTimeout() has the same associated problems as using `eval` .
- A string passed to setTimeout is evaluated in the global context, so local symbols in the context where setTimeout() was called will not be available when the string is evaluated as code.
- Reasons for delays longer than specified
  - In modern browsers, setTimeout()/setInterval() calls are throttled to a minimum of once every 4 ms when successive calls are triggered due to callback nesting (where the nesting level is at least a certain depth), or after certain number of successive intervals.
      - 4 ms is specified by the HTML5 spec and is consistent across browsers released in 2010 and onward. Prior to (Firefox 5.0 / Thunderbird 5.0 / SeaMonkey 2.2), the minimum timeout value for nested timeouts was 10 ms.
  - To reduce the load (and associated battery usage) from background tabs, timeouts are throttled to firing no more often than once per second (1, 000 ms) in inactive tabs.
      - Firefox 50 no longer throttles background tabs if a Web Audio API AudioContext is actively playing sound
  - Since Firefox 55, tracking scripts (e.g. Google Analytics) have been subject to further throttling. When running in the foreground, the throttling minimum delay is still 4ms. In background tabs, however, the throttling minimum delay is 10 seconds, which comes into effect 30 seconds after a document has first loaded.
  - timeout can also fire later when the page (or the OS/browser itself) is busy with other tasks
      - even though setTimeout was called with a delay of zero, it's placed on a queue and scheduled to run at the next opportunity; not immediately
- In WebExtension background pages, timers don't work properly. This is because background pages don't actually stay loaded all the time: the browser can unload them if they are not being used, and restore them when they are needed
- Browsers store the delay as a 32-bit signed integer internally. This causes an integer overflow when using delays larger than 2, 147, 483, 647 ms (about 24.8 days), resulting in the timeout being executed immediately
- clearTimeout
- setTimeout、setInternal、setImmediate这些方法在浏览器内一般是由浏览器内部实现，而Node.js中，这些方法都是由Timers模块提供的
  - 在Node.js里，这些定时器相关的函数是由基础库实现的，底层通过 C++ 在 libuv 的基础上包裹了一个 timer_wrap 模块，这个模块提供了 Timer 对象，实现了在 runtime 层面的定时功能

### setInterval

- ref
  - https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval
- 问题
  - setInterval每隔100ms往队列中添加一个事件；100ms后，添加T1定时器代码至队列中，主线程中还有任务在执行，所以等待，some event执行结束后执行T1定时器代码；又过了100ms，T2定时器被添加到队列中，主线程还在执行T1代码，所以等待；又过了100ms，理论上又要往队列里推一个定时器代码，但由于此时T2还在队列中，所以T3不会被添加，结果就是此时被跳过；这里我们可以看到，T1定时器执行结束后马上执行了T2代码，所以并没有达到定时器的效果
  - 使用setInterval时，某些间隔会被跳过，可能多个定时器会连续执行
  - 每个setTimeout产生的任务会直接push到任务队列中；而setInterval在每次把任务push到任务队列前，都要进行一下判断(看上次的任务是否仍在队列中)
  - 可以**用setTimeout模拟setInterval**来规避掉上面的缺点
  - 示例：一秒后立即输出5个5

``` js
  for (var i = 0; i < 5; i++) {

    setTimeout(function() {
      console.log(i);
    }, 1000);

  }
```

  - 每个setTimeout都由定时触发器线程负责计时，计时完毕后，添加到事件队列中(即：事件触发线程)，等待JS引擎线程空闲后，再来依次执行
  - 首先JS引擎线程要运行for循环，在每次循环中都会调用一个setTimeout函数，每个setTimeout计时结束后都会将其回调函数添加到事件队列中。等for循环结束后（即JS引擎线程空闲后），才开始按顺序执行事件队列中的函数。每次循环都会在一秒后将回调函数添加到事件队列中，但由于两次相邻的循环时间是短到可以忽略不计的，所以表面看上去一秒后立即执行了5次回调函数

### requestAnimationFrame

- ref
  - https://developer.mozilla.org/en-US/docs/Web/API/Window/requestAnimationFrame
  - https://jinlong.github.io/2013/06/24/better-performance-with-requestanimationframe/
- `window.requestAnimationFrame()` method tells the browser that you wish to perform an animation and requests that the browser calls a specified function to update an animation before the next repaint.
- The method takes a callback as an argument to be invoked before the repaint.
- Your callback routine must itself call requestAnimationFrame() if you want to animate another frame at the next repaint.
- The number of callbacks is usually *60 times per second*, but will generally match the display refresh rate in most web browsers as per W3C recommendation
- requestAnimationFrame() calls are paused in most browsers when running in background tabs or hidden <iframe>s in order to improve performance and battery life
- The callback method is passed a single argument, a `DOMHighResTimeStamp` , which indicates the current time (based on the number of milliseconds since time origin)

### es6的class

- js生成对象的传统方法是通过构造函数

``` js
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function() {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
```

- ES6的class只是语法糖，ES5的构造函数Point，对应ES6的Point类的构造方法

``` js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
typeof Point // "function"
Point === Point.prototype.constructor // true
```

- 一个类必须有constructor方法，若没有显式定义，一个空的constructor()会被默认添加
- **constructor方法默认返回实例对象**，即this
- 类的所有实例共享一个原型对象
- 实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）
- 类的方法内部如果含有this，它默认指向类的实例
- 类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上static关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为 `静态方法`
- 如果在实例上调用静态方法，会抛出一个错误，表示不存在该方法
- **如果静态方法包含this关键字**，这个this指的是类，而不是实例
- 父类的静态方法，可以被子类继承
- 实例属性除了定义在constructor()方法里面的this上面，也可以定义在类的最顶层
- 利用new.target可以写出不能独立使用、必须继承后才能使用的类
- 子类**可继承**父类的实例属性、实例方法、静态属性、静态方法
  - 当静态属性是引用类型时，子类和父类指向的同一个地址，父类如果变化子类也会变化
  - es5和es6实现继承的方式是不同的, 前者通过原型链实现对父类原型方法、原型属性的继承，通过构造函数的调用实现对实例方法、实例属性的调用，后者通过extends关键字实现继承
  - es5中静态方法、静态属性是无法通过继承下来的，只能通过赋值传递，但es6可以
- 子类必须在constructor()中调用super()， 否则新建实例时会报错。这是因为**子类没有自己的this对象**，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象
- ES5继承
  - 实质是先创造子类的实例对象this，然后再将父类的方法添加到this, 类似 `Parent.apply(this)`
- ES6继承
  - 实质是先创造父类的实例对象this(所以必须先调用super)， 然后再用子类的构造函数修改this 

## dev tips

- spread operator `...` vs `Object.assign()`
  - The main difference is that spreading defines new properties, while `Object.assign()` sets them.
  - First,  `Object.assign()` triggers setters, spread doesn’t
  - Second, you can stop `Object.assign()` from creating own properties via inherited read-only properties, but not the spread operator
  - Both spread and `Object.assign()` only consider own enumerable properties
  - ref
    - [ES2018: Rest/Spread Properties](https://2ality.com/2016/10/rest-spread-properties.html)
- Object vs Map
  - Objects have been used as Maps historically
  - The keys of an Object are String and Symbol, whereas they can be any value for a Map, including functions, objects, and any primitive.
  - keys in Map are *ordered* while keys added to object are not. 
      - Thus, when iterating over it, a Map object returns keys in order of insertion.
      - Note that in the ECMAScript 2015 spec objects do preserve creation order for string and Symbol keys, so traversal of an object with only string keys would yield the keys in order of insertion
  - You can get the *size* of a Map easily with the size property, while the number of properties in an Object must be determined manually
  - A Map is an *iterable* and can thus be directly iterated, whereas iterating over an Object requires obtaining its keys in some fashion and iterating over them.
  - An Object has a prototype, so there are default keys in the map that could collide with your keys if you're not careful. 
      - As of ES5 this can be bypassed by using Object.create(null), but this is seldom done.
  - A Map may perform better in scenarios involving frequent addition and removal of key pairs
  - ref
      - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map
- 逻辑运算符的玄学
  - `const aa = undefined || false;` // false
  - `const bb = false || undefined;` // undefined
- js复制数组的方式
  - 浅拷贝
  - `arr2=[...arr1]`
  - `arr1.slice()`
  - `arr1.concat()`
  - `Array.from(arr1)`
  - `Array.prototype.push.apply(arr2,arr1);`
  - 使用数组遍历赋值

``` js
  arr1.forEach(function(value, index) {

    arr2[index] = value;

  })

  let arr2 = arr1.map(function(item) {

    return item;

  });

  for (var a in arr1) {

    arr2[a] = arr[a];

  }
```

  - 深拷贝
  - `arr2=JSON.parse(JSON.stringify(array1));`
      - 数组中的项如果是undefined，那么转换后将变为null
      - 如果数组的项为对象，则对象之间不可相互引用。若存在循环引用，则无法JSON序列化
- js遍历对象属性几种方法的区别
  - `for-in` 是es3中就存在的最早用来遍历对象（集合）的方法
      - 会输出自身以及原型链上**可枚举**的属性
      - 不同的浏览器对for in属性输出的顺序可能不同
      - 如果仅想输出自身的属性可以借助hasOwnProperty滤掉原型链上的属性
  - `Object.keys(obj)`
      - 用来获取对象自身**可枚举**的属性键
      - Object.keys的效果和for in+hasOwnProperty的效果是一样的
  - `Object.getOwnPropertyNames(obj)`
      - 可以获取所有的键值，包括不可枚举的属性
- js执行原理
  - 浏览器（或者说JS引擎）执行JS的机制是基于事件循环
    - 由于JS是单线程，所以同一时间只能执行一个任务，其他任务就得排队，后续任务必须等到前一个任务结束才能开始执行
    - Node的事件循环和浏览器的略有差异
    - 有一个事件循环，但是任务队列可以有多个，整个script代码放在了macrotask queue中，setTimeout也放入macrotask queue，但promise.then放到了另一个任务队列microtask queue中
  - 为了避免因为某些长时间任务造成的无意义等待，JS 引入了异步的概念，用另一个线程来管理异步任务
  - 同步任务直接在主线程队列中顺序执行，而异步任务会进入另一个任务队列，不会阻塞主线程。等到主线程队列空了（执行完了）的时候，就会去异步队列查询是否有可执行的异步任务了（异步任务通常进入异步队列之后还要等一些条件才能执行，如ajax请求、文件读写），如果某个异步任务可以执行了便加入主线程队列，以此循环
- JS的定时器目前有三个：setTimeout、setInterval和setImmediate
  - 定时器也是一种异步任务，浏览器通常有一个独立的定时器模块，定时器的延迟时间就由定时器模块来管理，当某个定时器到了可执行状态，就会被加入主线程队列
  - `setTimeout(fn, x)`表示延迟x毫秒之后执行fn，严格来说是加入异步任务队列。延迟的时间严格来说总是大于x毫秒。
    - 使用时要注意setTimeout()内fn中变量的作用域问题，以及循环内使用setTimeout()的问题
    - `setTimeout(func, 0)` 并不会立刻执行，仍会先加入异步任务队列
    - 不要频繁使用，会导致程序执行的生命周期混乱和意想不到的问题，Promise和Generator也能实现异步编程
  - 多个定时器如不及时清除（clearTimeout），会存在干扰，使延迟时间更加难确定
  - HTML5规范规定最小延迟时间不能小于4ms，若x小于4，会被当做4来处理。不过不同浏览器的实现不一样，比如Chrome可以设置1ms，IE11是4ms

- 函数的length属性可以获取函数的形参个数，arguments.length得到实参个数
- 模块
  - ES6标准发布后，module成为标准，使用是以 `export` 导出模块，以 `import` 导入模块
  - 常用的node模块中，采用的是CommonJS规范，使用 `module.exports` 导出模块，使用 `require` 导入模块
  - es6的default可以看成as的语法糖
  - import是编译期的，require是运行期的
  - 前端早期没有模块加载规范，只能通过html中的script标签引入js
      - 命名问题：所有文件的方法都是挂载到global上，会污染全局，要考虑命名冲突
      - 依赖问题：script按顺序加载，如果文件间有依赖，要考虑加载.js文件的书写顺序
      - 网络问题：如果文件过多，所需请求次数会增多，增加加载时间
  - CommonJS
      - 主要运行于服务器端，一个单独的文件就是一个模块，同步加载模块
      - 暴露3个全局对象
          - require():用来加载模块
          - exports：用来导入模块的属性或方法
          - module：包含当前模块的导出信息，有id、uri等属性
  - AMD && Require.js
      - 主要运行于浏览器端，一个单独的文件就是一个模块，模块和模块的依赖可以被异步加载
      - 该规范是在RequireJs的推广过程中逐渐完善的
      - 模块功能主要的几个命令
          - define(id?, dependencies?, factory)用来定义模块
          - require用于输入其他模块提供的功能
          - return用于规范模块的对外接口
          - define.amd属性是一个对象，此属性的存在来表明函数遵循AMD规范
  - CMD && Sea.js
      - 主要在浏览器中运行，也可以在Node.js中运行
      - 主要是Sea.js推广中形成的，一个文件就是一个模块
      - CMD推崇依赖就近，延迟执行，通过require引入，只有运行到此处，模块才会加载
      - 常用命令
          - define(function(require, exports, module) {}
  - UMD && webpack
      - 主要用来解决CommonJS模式和AMD模式代码不能通用的问题，还支持传统全局变量
      - 常用命令
          - (function (root, factory) {
          - if (typeof define === 'function' && define.amd) {
          - } else if (typeof module === 'object' && module.exports) {
  - ES6 Module && ES6
      - ECMAScript2015标准确定的一种新的模块加载方式
      - 支持浏览器，支持node
      - 可以和Commonjs模块混合使用
          - CommonJS输出的是一个值的拷贝,ES6模块输出的是值的引用,加载的时候会做静态优化
          - CommonJS模块是运行时加载确定输出接口，ES6模块是编译时确定输出接口
      - 常用命令
          - import 
          - export
  - 参考
      - https://www.cnblogs.com/weiqinl/p/9940549.html
      - https://juejin.im/post/5b7d2f45e51d4538826f4c28
- js对象的属性
  - writable
  - enumerable
  - configurable

- js闭包
  - 「函数」和「函数内部能访问到的变量」（也叫环境）的总和，就是一个闭包
      - https://zhuanlan.zhihu.com/p/22486908
  - 将外部作用域中的局部变量封闭起来的函数对象称为闭包
  - 被封闭起来的变量与封闭它的函数对象有相同的生命周期。
  - 返回函数的函数
  - 能读取函数内部的变量
  - 应用场景
      - 保护函数内的变量安全：如迭代器、生成器
      - 在内存中维持变量：如果缓存数据、柯里化
  - 闭包的特点很鲜明，闭包内，变量无法释放，无法被直接访问；闭包可以被延迟执行

- 函数中的this
  - this的指向是由它所在函数调用的上下文决定的，而不是由它所在函数定义的上下文决定的
  - 由于函数可以在不同的运行环境执行，所以需要有一种机制，能够在函数体内部获得当前的运行环境（context）。所以，this就出现了，它的设计目的就是在函数体内部，指代函数当前的运行环境。
  - 例子

``` js
  var name = "The Window";
  var object = {
    name: "My Object",
    getNameFunc: function() {

      console.log(this.name); // my object

      return function() {

        console.log(this.name); // the window

        return this.name;
      };
    }
  };
  const v = object.getNameFunc()();
  console.log(v); // the window
```

  - object.getnameFunc() 返回的匿名闭包函数被全局变量所引用，其中的this指向全局变量，当执行时打印The Window 。
  - 闭包的两个作用：一个是可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。

- js equals
  - `==` ：普通相等，比较运算符，两边值类型不同的时候，先进行类型转换，再比较；
  - `===` ：全等，严格比较运算符，不做类型转换，类型不同就是不等；
  - `Object.is()` 是ES6新增的用来比较两个值是否严格相等的方法，与===的行为基本一致。
- window.location.assign(url) ： 加载 URL 指定的新的 HTML 文档，支持返回上个页面
- window.location.replace(url) ： 通过加载 URL 指定的文档来替换当前文档 ，不支持返回
- Object.assign()与spread operator扩展运算符 区别
- 扩展运算符支持遍历数组
- 扩展运算符 is A proposal, not standardized, Literal, not dynamic.
  - 动态示例 `options = Object.assign.apply(Object, [{}].concat(sources))`
- core-js
  - core-js是babel-polyfill的底层依赖，用ES3实现了大部分的ES2017原生标准库

- HTTP cookies
- An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser. 
- The browser may store it and send it back with the next request to the same server. 
- Typically, it's used to tell if two requests came from the same browser — keeping a user logged-in, for example. 
- It remembers stateful information for the stateless HTTP protocol.
- Cookies are mainly used for three purposes:
  - Session management
    - Logins, shopping carts, game scores, or anything else the server should remember
  - Personalization
    - User preferences, themes, and other settings
  - Tracking
    - Recording and analyzing user behavior
- 浏览器在发送请求之前，首先会根据请求url中的域名在cookie列表中找所有与当前域名一样的cookie，然后再根据指定的路径进行匹配，
  - 如果当前请求在域匹配的基础上还与路径匹配那么就会将所有匹配的cookie发送给服务器，这里要注意的是最大匹配和最小匹配问题，有些cookie服务器在发送之前会有意扩大当前页面cookie的匹配范围，此时这些被扩大范围的cookie也会一起发送给服务器。

- XMLHttpRequest与fetch   
- XMLHttpRequest是对象，fetch()是window的一个方法
- 服务器返回400、500错误码时并不会 reject，只有网络错误这些导致请求不能完成时，fetch 才会被 reject 
- 在默认情况下fetch不会接受或者发送cookies，需要设置 `fetch(url, {credentials: 'include'})`
- 所有的IE浏览器都不会支持 fetch()方法
- fetch不支持JSONP
- fetch不支持progress事件
- fetch不支持超时timeout处理

- 函数去抖（debounce）与 函数节流（throttle）
  -  以下场景往往由于事件频繁被触发，因而频繁执行DOM操作、资源加载等重行为，导致UI停顿甚至浏览器崩溃

   - 拖拽组件时的mousemove事件
   - window对象的resize、scroll事件
   - 射击游戏中的mousedown、keydown事件
   - 文字输入、自动完成的keyup事件

  - 实际上对于window的resize事件，实际需求大多为**停止改变大小n毫秒后再执行**后续处理；而其他事件大多的需求是**以一定的频率执行**后续处理。针对这两种需求就出现了debounce和throttle两种解决办法
- js debounce 去抖
  - 当调用动作n毫秒后，才会执行该动作，若在这n毫秒内又调用此动作则将重新计算执行时间
  - 示例

``` js
  var debounce = function(idle, action) {

    var last
    return function() {
      var ctx = this,
        args = arguments
      clearTimeout(last)
      last = setTimeout(function() {
        action.apply(ctx, args)
      }, idle)
    }

  }
```

- js throttle 节流   
  - 预先设定一个执行周期，当调用动作的时刻大于等于执行周期则执行该动作，然后进入下一个新周期
  - 示例

``` js
  var throttle = function(delay, action) {

    var last = 0
    return function() {
      var curr = +new Date()
      if (curr - last > delay) {
        action.apply(this, arguments)
        last = curr
      }
    }
  }
```

  - 函数节流和函数去抖都是通过减少实际逻辑处理过程的执行来提高事件处理函数运行性能的手段，并没有实质上减少事件的触发次数
- js事件性能考虑  
  - debounce：强制函数在某段时间内只执行一次
  - throttle：强制函数以固定的速率执行   
  - 在处理一些高频率触发的DOM事件的时候，它们都能极大提高用户体验
  - throttle和debounce均是通过减少实际逻辑处理过程的执行，来提高事件处理函数运行性能的手段，并没有实质上减少事件的触发次数

## ECMAScript

- 函数绑定运算符 两个冒号 ::  [doc](http://es6.ruanyifeng.com/#docs/function)
  - 双冒号左边是一个对象，右边是一个函数，该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面。
  - 如果双冒号左边为空，右边是一个对象的方法，则等于将该方法绑定在该对象上面
  - 如果双冒号运算符的运算结果还是一个对象，就可以采用链式写法
- js的函数调用  
  - 定义function f1(a, b){}  
  - 单参数也可以调用 f1(c)  
- 模块化开发不推荐使用css和html，可以都写在js中

## tool

- webpack
  - 前端资源模块化管理和打包工具  
  - 通过 loader 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等
  - 4个核心概念
    - entry：webpack创建应用程序所有依赖的关系图(dependency graph)，图的起点被称之为入口起点(entry point)。
      - 入口起点告诉webpack从哪里开始，并根据依赖关系图确定需要打包的内容。
      - 可以将应用程序的入口起点认为是根上下文(contextual root)或app第一个启动文件。
    - output：告诉 webpack 在哪里打包应用程序，webpack 的 output 属性描述了如何处理归拢在一起的代码(bundled code)。  
      - 通过 output.filename 和 output.path 属性，来告诉 webpack bundle 的名称，以及我们想要生成(emit)到哪里。
    - loader：loader用于对模块的源代码进行转换
      - loader可以使你在import或"加载"模块时预处理文件，定义loader时，要定义在 module.rules 中，loader 有两个目标         
      - test: 识别出(identify)应该被对应的 loader 进行转换(transform)的那些文件 
      - use: 转换这些文件，从而使其能够被添加到依赖图中（并且最终添加到 bundle 中）
    - plugins：插件目的在于解决loader无法实现的其他功能  
- js模块化 CommonJS、AMD、UMD  
  - CommonJS NodeJS  

``` js
var $ = require('jquery');
module.exports = myFunc;
```

  - AMD requirejs、dojo   

``` js
require(['math'], function(math) { math.add(2, 3); });
define(['jquery'], function($) { return myFunc; });
```

  - UMD  

``` js
      (function(root, factory) {
        if (typeof define === 'function' && define.amd) {
          // AMD
          define(['jquery'], factory);
        } else if (typeof exports === 'object') {
          // Node, CommonJS之类的
          module.exports = factory(require('jquery'));
        } else {
          // 浏览器全局变量(root 即 window)
          root.returnExports = factory(root.jQuery);
        }
      }(this, function($) {
        //    方法
        function myFunc() {};

        //    暴露公共方法
        return myFunc;
      }));
```

  - CMD seajs
  - es6
- UMD的实现很简单： 
  1. 先判断是否支持Node.js模块格式（exports是否存在），存在则使用Node.js模块格式。
  2. 再判断是否支持AMD（define是否存在），存在则使用AMD方式加载模块。
  3. 前两个都不存在，则将模块公开到全局（window或global）。
- js自执行函数  
  - 因为JavaScript里括号()里面不能包含语句，用括号将函数括住，解析器在解析function关键字的时候，会将相应的代码解析成function表达式，而不是function声明。

``` js
  // 下面2个括弧()都会立即执行
  (function() { /* code */ }()); // 推荐使用这个  
  (function() { /* code */ })(); // 但是这个也是可以用的  

  // 由于括弧()和JS的&&，异或，逗号等操作符是在函数表达式和函数声明上消除歧义的
  // 所以一旦解析器知道其中一个已经是表达式了，其它的也都默认为表达式了
  // 不过，请注意下一章节的内容解释
  var i = function() { return 10; }();
  true && function() { /* code */ }();
  0,
  function() { /* code */ }();

  // 如果你不在意返回值，或者不怕难以阅读
  // 你甚至可以在function前面加一元操作符号
  ! function() { /* code */ }();
  ~ function() { /* code */ }(); -
  function() { /* code */ }(); +
  function() { /* code */ }();

  // 还有一个情况，使用new关键字, 也可以用，但我不确定它的效率
  new function() { /* code */ }
  new function() { /* code */ }() // 如果需要传递参数，只需要加上括弧()
```

- core-js：为es5、es6提供polyfill   

## react

- 优点
  - React的理念是界面**组件化**，在桌面开发中叫控件，可复用性强，开发效率高
  - 但这个组件的含义与Web Components并无明显联系，Web Components是底层标准，而上层框架的实现是足可以抹平这个差异的
  - **Virtual DOM**让组件的渲染输出不局限于浏览器，能实现服务端渲染
      - vdom的性能只能说不低，现在vue和angular都引入了vdom
  - 自上而下的单向数据流，方便追踪状态数据和定位问题
  - react架构设计开放，组件生态丰富
- 缺点
  - react组件中js和html混写，与HTML+CSS+JS的分离思想有一定冲突
  - 并不是一个完整的框架，基本都需要加上ReactRouter和Flux才能写大型应用
  - 组件对框架依赖过重，移植到其他框架的组件不方便
- 使用体验
  - 技术只是手段，每个框架都有擅长的使用场景
  - react只是View层，对于其他的部分并没有规定，可以在vue/angular/backbone中使用
  - 强调只从this.props和this.state生成HTML，所以非常的functional programming
  - 脱离了Flux，在解决大规模UI的问题上React本身并没有拿出比MVVM更优的方案
  - 而结合Flux看的话，MVVM上也可以用Flux的思想，MVVM框架如果加上合适的优化，并不会比React慢，比如Vue的track by

## 样式处理

### css modules

### css in js

#### styled-components

- 使用模板字符串
- 样式写在js文件里，可以使用变量，更加灵活
- SSR类框架处理CSS Modules变量相当棘手，使用styled-components更方便
- 无法分离成独立的css
- 优点: 
  - 1. 接触到的css in js方案中最贴近 css语法的工具。很方便的从 lesa sass 等方案迁移过来。
  - 2. 支持父子，伪类等语法，可以很方便的更改样式权重。想要复写特定组件样式只需要增加很少一部分 BEM class就行。
  - 3. 作用域隔离，这是所有css in js 的优点，但其天然契合 react，让写组件样式辛福感提升了一个台阶。
- 缺点
  - 1. 没法使用 css 预处理框架的全局变量，目前虽然可以通过 style-variable 和 js-object 互转的plugin 解决，但需要使用 ThemeProvider 注入到全局 context 中，个人非常不喜欢。
  - 2. 没法使用postcss，无法自动补全浏览器前缀，css代码压缩，postcss既不是预处理器也不是后处理器
  - 3. js 体积增大，目前没有类似 ExtractCssPlugin 的工具解决这问题。

``` js
import styled from 'styled-components';
import styles from './style.less';

const Wrapper = styled(div)
`
border: 1px dashed ${props => props.color}; 
width: 100%; 
`;

const Header = (props) => {
  return (
    <div>

    {/* 直接看 jsx，看不出来 Wrapper 的原始标签是 div */}
    <Wrapper color="#000">使用 styled-component </Wrapper>
    <div className={styles.Wrapper}>使用 CSS Modules</div>

  </div>
  );
};

// 链接：https://www.zhihu.com/question/266625289/answer/321576411
```

## resources

- https://github.com/designmodo/html-website-templates

## WebAssembly

- 典型应用场景
  - 扩展浏览器端视音频处理能力
  - 游戏计算
- 90%的应用场景都不需要WebAssembly
  - https://www.infoq.cn/article/ytxfUWloi2wi00cQY-8a
  - js问题
    - 语法太灵活导致开发大型项目困难
    - 性能不能满足一些场景的需要
  - TypeScript是JavaScript的一个严格超集，并添加了可选的静态类型和使用看起来像基于类的面向对象编程语法操作Prototype，TypeScript最终仍然是被编译成JavaScript在浏览器中执行
  - 在2008年，Google推出了JavaScript引擎V8，首次通过JIT技术提升JavaScript的执行速度，并且它真的做到了
    - Web应用中，性能瓶颈大部分的原因已经不在JavaScript，而在于DOM。浏览器中通常会把DOM 和JavaScript独立实现，这两个模块相互访问的时候，都是通过接口访问。由于JavaScript单线程的特性，这种访问只能是单工的
    - 为了减少js访问dom的次数，可以使用Virtual Dom，Web Worker 
    - JIT执行时，可以根据代码编译进行优化，代码运行时，不需要每次都翻译成二进制汇编代码，V8就是这样优化JavaScript性能的
  - 为了进一步提升JIT优化效率，Mozilla 推出了asm.js。asm.js也是强类型的JavaScript，但是他的语法则是JavaScript的子集，是为了JIT性能优化而专门打造的，其他大厂都觉得asm.js的思路不错，于是联合起来共建WebAssembly生态
  - WebAssembly是一份字节码标准，以字节码的形式依赖虚拟机在浏览器中运行，可以依赖Emscripten等编译器将C++/Golang/Rust/Kotlin等强类型语言编译成为WebAssembly字节码.wasm 文件。
    - WebAssembly并不是Assembly（汇编），它只是看起来像汇编
  - 鉴于V8的强大性能，90%的应用场景下你不需要WebAssembly
  - 如何提高JS代码性能
    - 声明变量时提供默认类型，加快JIT介入
    - 不要轻易改变变量的类型
    - Node.js像Java一样也存在JIT预热？
