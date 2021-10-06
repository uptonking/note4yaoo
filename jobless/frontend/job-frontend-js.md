---
title: job-frontend-js
tags: [frontend, job, js]
created: '2021-09-23T08:24:24.348Z'
modified: '2021-09-23T08:24:41.968Z'
---

# job-frontend-js

# guide

## js数据类型

- JavaScript 中有八（7+1）种基本的数据类型（七种基本数据类型，也称为原始类型，object 为复杂数据类型）
  - string：用于字符串
  - number：用于整数或浮点数，在 ±(2^53-1) 范围内的整数
  - boolean：用于 true 和 false
  - null：只有一个 null 值的独立类型
  - undefined：只有一个 undefined 值的独立类型
  - bigInt：用于任意长度的整数
  - symbol：用于唯一的标识符
  - object：用于更复杂的数据结构

## promise

- `Promise.all()` 必须全部resolve，有一个失败就立即reject
  - takes an iterable of promises as an input, and returns a single Promise that resolves to an array of the results of the input promises. 
  - This returned promise will resolve when all of the input's promises have resolved
  - It rejects immediately upon any of the input promises rejecting or non-promises throwing an error
  - 使用 Promise.all() 执行过个 promise 时，只要其中任何一个promise 失败都会执行 reject ，并且 reject 的是第一个抛出的错误信息，只有所有的 promise 都 resolve 时才会调用 .then 中的成功回调
  - 但大多数场景中，我们期望传入的这组 promise 无论执行失败或成功，都能获取每个 promise 的执行结果，为此，ES2020 引入了 Promise.allSettled()
  - 适合promise彼此相互依赖，其中任何一个被 reject ，其它都失去了实际价值

- Promise.allSettled() 
  - returns a promise that resolves after all of the given promises have either fulfilled or rejected, with an array of objects that each describes the outcome of each promise
  - In comparison, the Promise returned by Promise.all() may be more appropriate if the tasks are dependent on each other / if you'd like to immediately reject upon any of them rejecting.
  - 可以获取数组中每个 promise 的结果，无论成功或失败
  - 适合promise彼此不依赖，其中任何一个被 reject ，对其它都没有影响
  - 期望知道每个 promise 的执行结果

## js作用域和变量提升

- 普通var变量提升，会初始化为undefined
- 函数名变量提升，会立即初始化为函数对象

- Hoisting happens on every execution context. 
  - During the hoisting variable or function declarations are not moving to the top, they are just being written to the memory.

- Function hoisting means that functions are moved to the top of their scope.
  - function declaration `function a(){}` is hoisted first and it behaves like `var a = function () {}; `, hence in local scope `a` is created.
  - `var a` forces it into a local scope, and variable scope is through the entire function, so the global a variable is still 1 because you have declared a into a local scope by making it a function.

```JS
var a = 1;

function b() {
  a = 10;
  return;

  function a() {}
}
b();
alert(a); // 1

// ------- equals to -----------

var a = 1; //defines "a" in global scope
function b() {
  var a = function() {}; //defines "a" in local scope 
  a = 10; //overwrites local variable "a"
  return;
}
b();
alert(a); //alerts global variable "a"
```

```JS
var boo = 11

function foo() {
  console.log(boo)
  var boo = 10
}
foo() // undefined

// ------- equals to -----------

function foo() {
  var boo = undefined
  // "boo" is partially hoisted inside  
  // "boo" is written into the variable environment of the execution context
  // "foo()" will always look into the its variable environment first
  console.log(boo)
  boo = 10
}
```

- 执行优先级
  - 20: 成员访问.[]?. = new 有参构造(有括号即可，不一定要有实参) = 函数调用
  - 19: new 无参构造(无括号)
  - 17: 单+-! 号 = typeof = delete = await = void
  - 12: instanceof = in = ><
  - 7: &&
  - 6: ||
  - 5: ??
  - 4: ?:
  - 3: = +=
  - 2: yield yield*
  - 1 , 

```JS
new Foo().getName() // (new Foo()).getName();
new Foo.getName() // new(Foo.getName());
new Foo().getName() // new ((new Foo()).getName())
```

## valueOf vs toString (+号运算符) 类似java的自动拆箱装箱/隐式类型转换

### [Object.prototype.valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)

- returns the primitive value of the specified object.
- JavaScript automatically invokes it when encountering an object where a primitive value is expected.
- If an object has no primitive value,  `valueOf` returns the object itself.
- A (unary) plus sign can sometimes be used as a shorthand for `valueOf`, e.g. in `+new Number()`.

- The unary plus operator (`+`) precedes its operand and evaluates to its operand but attempts to convert it into a number, if it isn't already.
  - Although unary negation (`-`) also can convert non-numbers, unary plus is the fastest and preferred way of converting something into a number

```typescript
{}.valueOf(); // Uncaught SyntaxError: Unexpected token '.'
let aa = {};
aa.valueOf(); // {}
[].valueOf(); // []

// 单个+号默认是获取数值类型的原始值

+"5" // 5 (string to number)
+"" // 0 (string to number)
+"1 + 2" // NaN (doesn't evaluate)
+new Date() // same as (new Date()).getTime()
+"foo" // NaN (string to number)
+{} // NaN
+[] // 0 (toString() returns an empty string list)
+[1] // 1
+[1,2] // NaN
+new Set([1]) // NaN
+BigInt(1) // Uncaught TypeError: Cannot convert a BigInt value to a number
+undefined // NaN
+null // 0
+true // 1
+false // 0
```

### [Object.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

- returns a string representing the object.
- toString() method that is automatically called when the object is to be represented as a text value or when an object is referred to in a manner in which a string is expected.
- If this method is not overridden in a custom object, toString() returns "[object type]", where type is the object type.

```typescript

// {}.toString()  // Uncaught SyntaxError: Unexpected token '.'
let aa = {};
aa.toString(); // [object Object]
[].toString(); // '' 空字符串
[1,2].toString(); // 1,2 数组转字符串默认没有方括号
null.toString(); // Uncaught TypeError: Cannot read properties of null
null+''; // null
undefined.toString(); // Uncaught TypeError: Cannot read properties of undefined
undefined+''; //undefined

Number(); // 0
Number(''); // 0

({valueOf: () => 1, toString: () => "f"})+""    // "1" 
`${({valueOf: () => 1, toString: () => "f"})}`  // "f"

'a' === String('a')      // true
'a' === new String('a')  // false
```

### [obj.toString() vs String(obj)](https://stackoverflow.com/questions/3945202)

- `value.toString()` will cause an error if value is `null` or `undefined`. 
  - `String(value)` should not.
- The `String` constructor called as a function would be roughly equivalent to: `value +''; `

- when converting from Object-to-String, the following steps are taken:
  - If available, execute the `toString` method.
    - If the result is a primitive, return result, else go to Step 2.
  - If available, execute the `valueOf` method.
    - If the result is a primitive, return result, else go to Step 3.
  - Throw `TypeError`.

### The addition operator ( `+` ) 自动类型转换

- produces the sum of numeric operands or string concatenation.

```JS
var x = {
  toString: function() { return "foo"; },
  valueOf: function() { return 42; }
};
console.log("x=" + x); // x=42
console.log("x=" + x.toString()); // x=foo

Symbol("foo").toString() // Symbol(foo)
String(Symbol("foo")) // Symbol(foo)
Symbol("foo") + "" // Uncaught TypeError: Cannot convert a Symbol value to a string
`${Symbol("foo")}` // Uncaught TypeError: Cannot convert a Symbol value to a string
```

- Type coercion(强迫), or implicit type conversion, enables weak typing and is used throughout JavaScript. 
  - Most operators (with the notable exception of the strict equality operators `===` and `!==`), and value checking operations (eg. if(value)...), will coerce values supplied to them, if the types of those values are not immediately compatible with the operation.
  - The precise mechanism used to coerce a value depends on the expression being evaluated.
- The **addition(`+`) operator will first ensure both operands are primitives**, which, in this case, involves calling the `valueOf` method.
  - 遇到+号运算符，会先将两边操作数转为原生类型，自动调用ToPrimitive，若不给hint，默认先调用valueOf()，若返回值不为原生类型，再调用toString()
  - The `toString` method is not called in this example because the overridden `valueOf` method on object `x` returns a primitive value. 
  - Then, because one of the operands in the question is a string, both operands are converted to strings. This process uses the abstract, internal operation `ToString` (note: capitalized), and is distinct from the `toString` method on the object (or its prototype chain).

- The purpose of `valueOf` is to retrieve the primitive value associated with an object (if it has one). 
  - If an object does not have an underlying primitive value, then the object is simply returned.
- If `valueOf` is invoked against a primitive, then the primitive is auto-boxed in the normal way, and the underlying primitive value returned. 
  - Note that for strings, the underlying primitive value (ie. the value returned by `valueOf`) is the string representation itself.
- For most operations, JavaScript will silently attempt to convert one or more operand(s) to the required type. 
  - This kind of implicit type conversion is called type coercion, and it is the basis of JavaScript's loose (weak) type system.
  - The complicated rules behind this behavior are intended to move the complexity of typecasting into the language itself, and out of your code.
- **When attempting to convert non-primitive types to primitives to be operated upon, the abstract operation `ToPrimitive` is called** with an optional "hint" of 'number', or 'string'. 
  - If the hint is omitted, the default hint is 'number' (unless the `@@toPrimitive` method has been overridden). 
  - If the hint is 'string', then `toString` is tried first, and `valueOf` second if `toString` did not return a primitive. Else, vice-versa. 
- The hint depends on the operation requesting the conversion.
  - The addition(`+`) operator supplies no hint, so `valueOf` is tried first. 
  - The subtraction(`-`) operator supplies a hint of 'number', so `valueOf` is tried first. 
  - The only situations I can find in the spec in which the hint is 'string' are: `Object#toString` or `ToPropertyKey`
- **The addition operator will first use `ToPrimitive` to ensure each operand is a primitive**; 
  - then, if either operand is a string, it will then deliberately invoke the abstract operation `ToString` on each operand, to deliver the string concatenation behavior we expect with strings. 
  - If, after the `ToPrimitive` step, both operands are not strings, then arithmetic addition is performed.
- Unlike addition, the subtraction operator does not have overloaded behavior, and so will invoke `toNumeric` on each operand having first converted them to primitives using `ToPrimitive`

```typescript
 1  +  1   //  2 
'1' +  1   // '11'   Both already primitives, RHS converted to string, '1' + '1',   '11'
 1  + [2]  // '12'   [2].valueOf() returns an object, so `toString` fallback is used, 1 + String([2]), '1' + '2', 12
 1  + {}   // '1[object Object]'    {}.valueOf() is not a primitive, so toString fallback used, String(1) + String({}), '1' + '[object Object]', '1[object Object]'
 2  - {}   // NaN    {}.valueOf() is not a primitive, so toString fallback used => 2 - Number('[object Object]'), NaN
+'a'       // NaN    `ToPrimitive` passed 'number' hint), Number('a'), NaN
+''        // 0      `ToPrimitive` passed 'number' hint), Number(''), 0
+'-1'      // -1     `ToPrimitive` passed 'number' hint), Number('-1'), -1
+{}        // NaN    `ToPrimitive` passed 'number' hint', `valueOf` returns an object, so falls back to `toString`, Number('[Object object]'), NaN
 1 + 'a'   // '1a'    Both are primitives, one is a string, String(1) + 'a'
 1 + {}    // '1[object Object]'    One primitive, one object, `ToPrimitive` passed no hint, meaning conversion to string will occur, one of the operands is now a string, String(1) + String({}), `1[object Object]`
 1 - 'a'   // NaN    Both are primitives, one is a string, `ToPrimitive` passed 'number' hint, 1-Number('a'), 1-NaN, NaN
 1 - {}    // NaN    One primitive, one is an object, `ToPrimitive` passed 'number' hint, `valueOf` returns object, so falls back to `toString`, 1-Number([object Object]), 1-NaN, NaN
[] + []    // ''     Two objects, `ToPrimitive` passed no hint, String([]) + String([]), '' (empty string)
[] - []    // 0      Two objects, `ToPrimitive` passed 'number' hint => `valueOf` returns array instance, so falls back to `toString`, Number('')-Number(''), 0-0, 0

let date = new Date();
date.valueOf(); // 1632449848133
date.toString(); // 'Fri Sep 24 2021 14:34:47 GMT+0800 (China Standard Time)'
date + ''; // 'Fri Sep 24 2021 14:34:47 GMT+0800 (China Standard Time)'

```

- Note that the `Date` intrinsic object is unique, in that it is the only intrinsic to override the default `@@toPrimitive` method, in which the default hint is presumed to be 'string' (rather than 'number').
  - The reason for having this, is to have Date instances translate to readable strings by default

## this

- this 是执行上下文中的一个属性，它指向最后一次调用这个方法的对象。 
- this的绑定在构建执行上下文时确定，在实际开发中，this 的指向可以通过四种调用模式来判断：
  - 默认绑定：当一个函数不是一个对象的属性时，直接作为函数来调用时，调用行为发生在全局上下文中，this 默认绑定到全局对象
  - 隐式绑定：被直接对象作为方法调用的函数，其上下文的 this 隐式绑定到该对象上
  - 显式绑定：通过 call()/apply()/bind() 把指定对象绑定到 this 上，叫做显式绑定
  - new 绑定：new 构造一个新对象时，构造函数内部的 this 会自动绑定到新建的对象上
- 绑定优先级：new绑定 > 显式绑定 > 隐式绑定 > 默认绑定

```JS
// 箭头函数内没有自己的this，使用外部this
const fn = () => {
  this.x = 'z';
};

const b = { x: 'y' };
fn.call(b); // 设置window.x = 'z'
console.log(b); // {x:'y'}

// --------- 不用箭头函数 -------

function fn2() {
  this.x = 'z';
};

const b2 = { x: 'y' };
fn2.call(b2); // 设置b2.x
console.log(b2); // {x:'z'}
```

## 闭包

- 当一个函数可以访问到其他函数作用域中自由变量时，即构成闭包，创建闭包的最常见的方式就是在一个函数内创建另一个函数，创建的函数可以访问到当前函数的局部变量。
- 闭包的意义就是“隐藏变量”，对外隐藏状态。
  - 当前函数能够访问到外部函数词法环境中的变量，甚至在外部函数执行上下文已经离开执行栈时，此时外部函数的变量称为当前函数的“私有变量”，而外部函数的词法环境也会被一致保存在内存中

- 使用场景
- 实现装饰器函数：
  - 比如防抖和节流装饰器，外部 decorator 中的 timer 被返回的 wrapper 函数所引用着，timer 变成了一个私有变量，只有调用 wrapper 才能改变计时器的状态
- 解决循环中多个闭包共享词法作用域的问题：
  - 典型的场景就是 for 循环中使用 var 声明 i，通过 setTimeout 打印时，为了实现每次输出值的不同，使用更多的闭包解决这个问题；
  - 构造一个立即执行函数，构成计时器回调的闭包，这个立即构造函数中的 i 就成了私有变量，对外隐藏，只有回调执行时才能访问
- 私有变量与特权函数：
  - 对于构造函数内不想被外界直接访问修改的变量，同时又需要操作，通过this提供特权函数，让特权函数构成闭包，其具备访问外部构造函数中私有变量的能力

### 为什么Java没有闭包？

- 其实Java处处是闭包，比如对象、内部类等
  - Java使用new实例化Add对象后，Java对象不会像JS中的函数上下文一样立即消失，同时private又保证了变量对外隐藏，之后只要使用calc.add()就能实现计算

- [Closures vs. classes for encapsulation?](https://stackoverflow.com/questions/8729714)
- The reasons to avoid closures is overhead.
  - Your get and set functions are trivially 20x slower than properties. 
  - Your closures also have a large memory overhead that is `O(N)` with the number of instances.

- there aren't any real classes in javascripts, we just mimic them with closures.
  - Because closures must reference the environment in which they were created (this is how they can use the private internal state data), they are more costly than just using a public function. 
  - So if you have a static method that doesn't require the internal state, you should add it to Class1 instead by using the `prototype` keyword
  - This way, the static method can be used through the prototype chain without using up extra memory with unnecessary closures. 

## 箭头函数

- 箭头函数没有`this`，其`this`需从外部作用域获取，因此取决于箭头函数定义位置的上下文
- 箭头函数不能使用 `arguments`、`super` 和 `new.target`，也不能用作构造函数。此外也没有 `prototype` 属性

## Object 对象

- 对象属性的特征
  - [[Configurable]]：属性是否可通过 delete 删除并重新定义，默认 true
  - [[Enumerable]]：属性是否可通过 for-in 或 Object.keys() 枚举，默认 true
  - [[Writable]]：属性是否可被修改，默认 true
  - [[Value]]：属性值，默认 undefined
- Object.keys()返回一个由一个给定对象的自身可枚举属性组成的数组
  - 作为对比 for-in 循环则会遍历对象自身+其原型链上可枚举属性，每次获取的索引都是字符串类型
- Object.freeze()
  - 冻结对象，使其不能被修改（冻结一层）
  - 不能新增、删除、修改属性
  - 对象 [[prototype]] 不可修改
- Object.seal()
  - 不能新增属性
  - 现有属性标记为不可配置，即不可删除
  - 已有可写属性可以修改
  - 对象 [[prototype]] 不可修改
- Object.preventExtensions()
  - 不能新增属性
  - 可删除已有属性
  - 对象 [[prototype]] 不可修改
  - 其余属性都可修改
- 从限制的严格性来说：Object.preventExtensions() [不可增，可删可改] < Object.seal() [不可增不可删，可改] < Object.freeze() [不可增不可删不可改] 

## 数字处理

- JS 的 Number 类型遵循的是 IEEE 754 标准，使用的是 64 位固定长度来表示
- 0.1 转换为 IEEE 754 标准，转换过程主要经历 3 个过程：
  - 将 0.1 转换为二进制表示：乘2取整，自上而下，得到0.00011
  - 将转换后的二进制通过科学计数法表示：0.00011=1.1001*10-4
  - 将通过科学计数法表示的二进制转换为 IEEE 754 标准表示
    - 求阶码
    - 求尾数
- 0.1+0.2 计算结果不等于0.3，而是 0.30000000000000004
  - 解决方法：
  - 放大，先各放大100倍，求和后除以100
  - 使用 Number. EPSILON，小于该值的即认为是机器误差，可认为结果正确

```JS
function numbersequal(a, b) {
  return Math.abs(a - b) < Number.EPSILON;
}

var a = 0.1 + 0.2， b = 0.3;
console.log(numbersequal(a, b)); //true
```

- 基于 IEEE754 的 JS 能够安全存储的整数范围在 (-2^53, 2^53)之间。
  - 后端返回的数据一般都是 JSON 格式的字符串，当其中的超过区间的字符串数字经过 JSON.parse() 转换为数字后可能出错
- 以前需要使用外部库，如 JSON-bigint，现在可以使原生 bigInt 类型，借助 JSON.parse() 的 reviver 函数，判断在不安全值时转换为 bigInt 值，注意使用 reviver 后需要针对所有值都有返回值

```JS
console.log(
  JSON.parse(
    '{ "id": 9007199254740995, "name": "Jack", "age": 18 }',
    (k, v) => {
      if (typeof v == "number" && !Number.isSafeInteger(v)) return BigInt(v);
      else return v;
    }
  )
);
```

## 类型转换

```JS
String(null); // 'null'
String(undefined); // 'undefined'
String(1e21); // '1e+21'
String([null]); // ''
String([1, undefined, 3]); // '1,,3'
String([]); // ''
String({}); // '[object Object]'

Number(null); // 0
Number(undefined); // NaN
Number("10a"); // NaN
Number(""); // 0
Number(true); // 1
Number(false); // 0
Number(["1"]); // 1
Number([]); // 0
Number({}); // NaN

Boolean(Infinity); // true

[] == [] //false： 类型相同， 但是堆上不同对象， false
[] == ![] // true： 右侧由 false 转为 0， 左侧 toPrimitive() 转为 0
[] == 0 // true： 同上 
  [] == "" // true： 左侧 toPrimitive() 转为 "" 和右侧相等
```

## 运算符

- `==`比较
  - 如果两个值类型相同，再进行三个等号(===)的比较
  - 如果两个值类型不同，也有可能相等，需根据以下规则进行类型转换再比较
    - 如果一个是null，一个是undefined，那么相等
    - 如果一个是字符串，一个是数值，把字符串转换成数值之后再进行比较
  - 字符串和数字之间的相等比较，将字符串转换为数字之后再进行比较。
  - 其他类型和布尔类型之间的相等比较，先将布尔值转换为数字后，再应用其他规则进行比较。
  - null 和 undefined 之间的相等比较，结果为真。其他值和它们进行比较都返回假值
  - 如果一个操作值为 NaN ，则相等比较返回 false（ NaN 本身也不等于 NaN ）

## 事件循环 浏览器端

- JS 作为单线程执行的语言，程序的执行流依靠执行栈控制，
  - 当主线程遇到异步任务时，会将异步任务放入任务队列，而非执行栈；
  - 在执行栈中的同步任务全部执行结束后，主线程会去任务队列中取出就绪的异步任务（计时器回调不会在计时未结束时执行），执行它们的回调函数，而异步任务又分为宏任务和微任务：
- 宏任务：script( 整体代码)、setTimeout、setInterval、I/O、UI交互事件、setImmediate(Node.js 环境)
- 微任务：Promise、MutationObserver、process.nextTick(Node.js 环境)
- 整体的执行流程：
  - 执行同步代码，这是宏任务
  - 执行栈为空，执行所有微任务
  - 必要时渲染 UI
  - 进行下一轮的 EventLoop ，执行宏任务队列中队首任务的异步代码
- 在浏览器中，setTimeout()/setInterval() 的每调用一次定时器的最小间隔是4ms，这通常是由于函数嵌套导致，或者是由于已经执行的 setInterval 的回调函数阻塞导致的。
  - 例如：setTimeout(fn, 0)只能指定某个任务在主线程最早有空闲时尽快执行

## 异步

- promise本身可以抽象一个异步操作，同时具有状态来表示异步操作的完成情况，状态可被resolve()和reject()改变。
  - Promise虽然摆脱了回调地狱，但是then的链式调用也会带来额外的阅读负担
  - Promise传递中间值非常麻烦，而async/await几乎是同步的写法，非常优雅
- ES6之前使用异步返回值的操作都需要放在回调函数中，异步结果作为回调参数，回调成为闭包
- new Promise执行程序是同步任务，会被放到主进程中去立即执行。
  - then()函数是异步任务，当promise状态落定时，回调才会进入异步队列

- ES6中使用异步返回值的操作都需要放在处理程序中，ES8的async/await旨在解决利用异步结构组织代码
  - 错误处理友好，async/await可以用成熟的try/catch，Promise的错误捕获非常冗余
  - 调试友好，Promise的调试很差，由于没有代码块，你不能在一个返回表达式的箭头函数中设置断点，如果你在一个.then代码块中使用调试器的步进(step-over)功能，调试器并不会进入后续的.then代码块，因为调试器只能跟踪同步代码的『每一步』
- 带async关键字的函数会返回一个promise对象，如果里面没有await，执行起来等同于普通函数；
  - await 要在 async 函数的内部，等待其右侧的表达式完成。
  - await会迫使异步函数让出主线程，阻塞async内后续的代码，先去执行async外的代码。
  - 等外面的同步代码执行完毕，才会执行里面的后续代码。就算await的不是promise对象，是一个同步函数，也会等这样操作

## 柯里化

- 柯里化其实是函数式编程的一个过程，在这个过程中能把一个带有多个参数的函数转换成一系列的嵌套函数
- 柯里化可以实现：
  - 参数复用: 在新函数中继续接收剩余参数
  - 延迟执行: 在参数收集齐后再执行函数

```JS
function curry(func) {
  // 返回一个包装器
  return function curried(...args) {
    // 参数足够，直接返回func调用
    if (args.length >= func.length) {
      return func.apply(this, args);
    } else {
      // 参数不够，返回偏函数
      return function(...args2) {
        return curried.apply(this, args.concat(args2));
      }
    }
  };
}

function sum(a, b, c) {
  return a + b + c;
}

let curried_sum = curry(sum);
console.log(curried_sum(1)(2)(3));
```

# es6新特性
- 常用新特性
  - let, const
  - 箭头函数
  - class
  - rest operator ...
  - Symbol
  - Map, Set
  - 迭代器；for-of
  - promise

- 根据规范，对象属性键只能是字符串类型或者Symbol类型
  - “隐藏” 对象属性
    - Symbol作为键的属性不会出现在 for-in/of 循环，防止被意外使用或重写，且该键只能用中括号访问
  - 系统Symbol
    - JavaScript使用了许多系统 Symbol，可以用来改变一些内置行为。
    - 例如使用 Symbol.iterator 来进行迭代操作，使用 Symbol.toPrimitive 来设置 对象原始值的转换 等等。

- 可迭代协议：Iterable 接口
  - JS许多内置类型都是可迭代的：String、Array、Map、Set、arguments对象、NodeList 等。
- 实现 Iterable 接口要求同时满足两点：
  - 否支持迭代的判断：ES中要求暴露一个属性作为“默认迭代器”，而且这个属性必须使用特殊的Symbol.iterator 作为键
  - 创建迭代器的能力：Symbol.iterator 必须引用一个迭代器工厂函数，调用工厂函数要能返回一个新迭代器
- 迭代器协议：Iterator 接口
  - 迭代器是一种一次性使用的对象，用于迭代与其关联的可迭代对象
  - 迭代器使用 next() 在可迭代对象中遍历数据，成功调用后返回 IteratorResult 对象
  - IteratorResult 对象：包含两个属性 done 和 value

```JS
let num = 1;
let obj = {};

// 这两种类型没有实现迭代器工厂函数
console.log(num[Symbol.iterator]); // undefined
console.log(obj[Symbol.iterator]); // undefined

let str = 'abc';
let arr = ['a', 'b', 'c'];
let map = new Map().set('a', 1).set('b', 2).set('c', 3);
let set = new Set().add('a').add('b').add('c');
let els = document.querySelectorAll('div');

// 这些类型都实现了迭代器工厂函数
console.log(str[Symbol.iterator]); // f values() { [native code] }
console.log(arr[Symbol.iterator]); // f values() { [native code] }
console.log(map[Symbol.iterator]); // f values() { [native code] }
console.log(set[Symbol.iterator]); // f values() { [native code] }
console.log(els[Symbol.iterator]); // f values() { [native code] }

let arr = ['foo', 'bar'];
console.log(arr[Symbol.iterator]); // f values() { [native code] }

// 获取迭代器
let iter = arr[Symbol.iterator]();
console.log(iter); // ArrayIterator {}
// 执行迭代
console.log(iter.next()); // { done: false, value: 'foo' }
console.log(iter.next()); // { done: false, value: 'bar' }
```

- 尾调用优化
  - ES6可执行优化，因为引擎可以发现 innerFunction() 的返回值就是 outerFunction() 的返回值，计算内层返回值之前可以放心弹出外层函数上下文。
  - 现在只要满足条件，就可以只保留一个函数上下文
- 尾调用优化的条件
  - 代码在严格模式下执行
  - 外部函数的返回值是对尾调用函数的调用
  - 尾调用函数返回后不需要执行额外的逻辑
  - 尾调用函数不是引用外部函数作用域中自由变量的闭包

```JS
function outerFunction() {
  return innerFunction(); // 尾调用
}
```

- WeakSet 的成员只能是对象，而不能是其他类型的值。WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用
- WeakMap只接受对象作为键名（ null 除外），不接受其他类型的值作为键名。Weak 主要形容弱映射中的 key 是弱的——GC随时会回收弱映射的key 指向对象，但是只要 key 存在，value 就不会被回收

## babel原理

- Babel就是一个编译器，执行了和其他编译器类似的编译工作：
- 解析（parse）
  - 将代码字符串解析成抽象语法树
- 变换（transform）
  - 对抽象语法树进行变换操作。实现代码转换的重点在变换阶段
  - Babel会对 AST 进行DFS，在遍历结点的过程中，如果遇到了不支持的语法，Babel 会对其进行变换，相当于修改 AST 结点。
  - Babel会维护一个 Visitor 对象，这个对象定义了用于获取 AST 中具体节点的方法，由 Visitor 判断并进行变换操作。
- 重建（rebuild）
  - 根据变换后的抽象语法树再生成字节码

## string

- 字符串字面量 (通过单引号或双引号定义) 和 直接调用 String 方法(没有通过 new 生成字符串对象实例)的字符串都是基本字符串
  - 当基本字符串需要调用一个字符串对象才有的方法或者查询值的时候(基本字符串是没有这些方法的)，JS会自动将基本字符串转化为字符串对象并且调用相应的方法或者执行查询

- 字符串可以使用类似数组索引下标的方式来访问字符元素
  - 如 aa = 'string'; aa[1] === 't'

- [`string.charAt(x)` or `string[x]`](https://stackoverflow.com/questions/5943726)
- There is a difference when you try to access an index which is out of bounds or not an integer.
  - string[x] returns the character at the xth position in string if x is an integer between 0 and string.length-1, and returns `undefined` otherwise.
  - string.charAt(x) converts x to an integer and then returns the character at the that position if the integer is between 0 and string.length-1, and returns an empty string otherwise.
- Word of caution: using either syntax for emojis or any other unicode characters past the Basic Multilingual Plane BPM (AKA the "Astral Plane") "😃".charAt(0) will return an unusable character
  - using either syntax for emojis will return an unusable character
  - That’s why Array.from("😃")[0] or [..."😃"][0] should be used in this case. 

```JS
// They can give different results in edge cases.
'hello' [NaN] // undefined
'hello'.charAt(NaN) // 'h'

'hello' [true] //undefined
'hello'.charAt(true) // 'e'
```

## number

```JS
NaN === NaN // false; 但作为Map的key时是被认为相等的
```

## array

- 扁平化
  - reduce，递归
  - map，递归
  - 基于队列，非递归

- 判断Array类型
  - Array.isArray(arr)
  - arr.constructor === Array
  - arr instanceof Array

- 数组去重
  - [... new Set(arr)]

- indexOf vs includes
  - [NaN].indexOf(NaN) // -1，因为indexOf使用的是严格相等
  - NaN].includes(NaN) // true

- indexOf vs findIndex
  - indexOf() expects a value
  - findIndex() expects a callback; good for objects

- 不要再forEach里面return，因为forEach循环无法终止

### `concat vs ...rest` ([...arr1, ...arr2] vs arr1.concat(arr2))

- concat不会改变arr1和arr2，返回的也是新数组，a new Array instance.
- 最大的区别是rest操作符可读性好，测试leetcode快排算法时结尾用展开语法更快
- rest还能展开字符串、对象等
- the only honest answer is that "it depends". 
  - Browsers change all the time
- concat will preserve the empty slots in the array while the Spread will replace them with undefined values.

- 虽然concat保留了空位置，但比较起来却是相等的，都等于`undefined`

```JS
var x = [],
  y = [];

x[1] = "a";
y[1] = "b";

var usingSpread = [...x, ...y];
var usingConcat = x.concat(y);

console.log(usingSpread); // [ undefined, "a", undefined, "b"]
console.log(usingConcat); // [ empty, "a",empty , "b"] 

console.log(1 in usingSpread); // true
console.log(1 in usingConcat); // true

usingSpread[0] === usingConcat[0] // true
usingConcat[0] === undefined // true
```

- 在常见使用场景中，concat不会修改数组
  - arr1.push(...arr2)使用rest经常需要修改已有数组

```JS
const arr1 = ["dog", "cat", "hamster"];
const arr2 = ["bird", "snake"];

arr1.push(arr2);
arr1 // ['dog', 'cat', 'hamster', Array(2)]

arr1.push.apply(arr1, arr2);
arr1 // ['dog', 'cat', 'hamster', 'bird', 'snake']

// When we invoke the function, we pass it all the values in the array using the spread syntax 
arr1.push(...arr2); // ['dog', 'cat', 'hamster', 'bird', 'snake']
```

- Spread syntax is not an operator and therefore does not have a precedence.
  - It is part of the array literal and function call (and object literal) syntax.
  - Similarly, rest syntax is part of the array destructuring and function parameter (and object destructuring) syntax.

- [Array.prototype.push.apply](https://stackoverflow.com/questions/35638511)
- `arr1.push.apply(arr1, arr2); `的计算逻辑
  - `arr1.push === Array.prototype.push` // true
  - Function.prototype.apply(thisArg, argsArray)，apply的第2个参数会自动展开然后传递给函数  
  - When you use `apply()`, it will take the array that you have supplied as the second argument and convert it to multiple arguments.
- [Difference between using a spread syntax (...) and push.apply](https://stackoverflow.com/questions/39716216)
- Both `Function.prototype.apply` and the `...` spread syntax may cause a stack overflow when applied to large arrays
  - `apply: Maximum call stack size exceeded` 异常信息
  - 因为 JavaScriptCore engine 引擎限制了函数参数列表的长度为65536，但是chrome的v8引擎测试表明支持参数数量大于65536
  - Use `Array.prototype.concat` instead. Besides avoiding stack overflows,  `concat` has the advantage that it also avoids mutations. Mutations are considered harmful, because they can lead to subtle side effects.
  - But that isn't a dogma(教条). If you are within a function scope and perform mutations to improve performance and relieve garbage collection you can perform mutations, as long as they aren't visible in the parent scope.

- [Does spread operator affect performance?](https://stackoverflow.com/questions/55843097)
  - Yes, spreading a variable which refers to an object into another object requires the interpreter to look up what the variable refers to, and then look up all the enumerable own properties (and the associated values) of the object that gets spreaded so as to insert into the new object. 
  - But, on modern computers, and on modern JS engines, the processing power required is next to nothing; 
- beware of using spread with an `array.reduce()`. I suspect it leads to O(n^2) behavior or worse.

```JS
let phoneBook = inputs.reduce((acc, entry) => {
  let [name, phone] = entry.trim().split(' ');

  // ! 不要用展开运算符，返回的是在循环内创建的新对象
  return { ...acc, [name]: phone };
}, {});

let phoneBook = inputs.reduce((acc, entry) => {
  let [name, phone] = entry.trim().split(' ');

  // 返回的是同一个acc对象
  acc[name] = phone;

  return acc;
}, {});
```

- [spread operator vs array.concat()](https://stackoverflow.com/questions/48865710)
- To sum it up, when your arguments are possibly non-arrays, the choice between concat and ... depends on whether you want them to be iterated.
  - `concat` makes no attempt to iterate the generator and appends it as a whole, while `...` nicely fetches all values from it.
  - ES6 provides a way to override it with `Symbol.isConcatSpreadable`; 
- Performance-wise `concat` is faster, probably because it can benefit from array-specific optimizations, while `...` has to conform to the common iteration protocol. 

## Map vs Object

- 区别
  - Map对象默认不包含键值对
    - Object原型对象上的默认属性会添加到普通对象上
    - 但Object.create(null)也可以实现类似Map的效果
  - Map的key的类型可以是任意类型，包括对象、函数、symbol、数字
    - Object的key必须是String或Symbol
  - Map对象的keys会保持插入顺序
    - Object的keys的顺序以前没有在规范中规定保持插入顺序
    - obj的遍历机制很复杂
    - `for-in` includes only enumerable string-keyed properties，还会遍历原型对象上的kv
    - `Object.keys` includes only own, enumerable, string-keyed properties; 这里不包含原型对象上的kv
    - `Object.getOwnPropertyNames` includes own, string-keyed properties even if non-enumerable;
  - Map对象的size很容易获得
    - 获取Object的属性数量必须遍历和过滤
  - Map默认实现了 iterator protocol 
    - Object需要自己实现 Object.keys/entries
    - for-in可遍历obj及其原型链上的可迭代属性，会忽略Symbol，
  - Map在插入、删除操作较多时性能较好
    - Object没有针对插入删除进行优化
  - Map序列化默认会丢失所有内容，总是{}
    - Object对象默认提供了序列化和反序列化的方法，但有限制

- for-in遍历
  - only iterates over enumerable, non-Symbol properties.
  - 可遍历原型对象上的属性
  - for...in loop iterates over the properties of an object in an arbitrary order 
    - 而数组的遍历一般按索引顺序，所以最好不要使用for-in遍历数组
  - for-in遍历数组会遍历手动添加的属性
  - for-in为遍历对象而设计

- [es6 Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- holds key-value pairs and remembers the original insertion order of the keys
- Key equality is based on the sameValueZero algorithm.

- Object只能使用数值、字符串或符号作为键，且会被转换为字符串，
  - Map可使用任何数据类型作为key，且保持该类型
- Map实例会维护键值对的插入顺序，因此可以根据插入顺序执行迭代操作
- Weak主要形容弱映射中的key是弱的——GC随时会回收弱映射的key，但是只要key存在，value就不会被回收

- Object.isSealed
  - 让这个对象变的不能添加新属性，且所有已有属性会变的不可配置。属性不可配置的效果就是属性变的不可删除，以及一个数据属性不能被重新定义成为访问器属性
  - 但属性的值仍然可以修改。
- Object.isFrozen
  - 属性不能被修改。

## Map/Set

- 弱引用与强引用相对，是指不能确保其引用的对象不会被垃圾回收器回收的引用。 
  - 一个对象若只被弱引用所引用，则被认为是不可访问（或弱可访问）的，并因此可能在任何时刻被回收。
  - 我们默认创建一个对象：const obj = {}，就默认创建了一个强引用的对象，我们只有手动将obj = null，它才会被垃圾回收机制进行回收，如果是弱引用对象，垃圾回收机制会自动帮我们回收。
  - weakMap.set(obj, 'i can be auto recycled'); 
  - obj = null; 
  - weakMap和obj是弱引用关系，当obj断开时，obj对应的val会被自动回收

- WeakSet与Set的区别
  - 成员都是对象
  - 成员都是弱引用，可以被垃圾回收机制回收，可以用来保存 DOM 节点，不容易造成内存泄漏
  - 不能遍历；而Set可遍历

- WeakMap
  - 只接受对象最为键（null除外），不接受其他类型的值作为键
  - 不能遍历，没有keys()/entries()等方法
  - 没有size属性，没有clear()方法
  - 键名是弱引用，键值可以是任意的，键名所指向的对象可以被垃圾回收，此时键名是无效的；

- [从【垃圾回收机制】的角度认识【Map与WeakMap】的区别](https://zhuanlan.zhihu.com/p/266054976)
- JavaScript最常用垃圾回收策略是"标记清理（mark-and-sweep）"
  - 遍历空间下所有的对象，并标记活着的，有被引用的并且最终可以到达根（window/global）的对象。
  - 在垃圾回收阶段的时候，将没有标记进行清除。
- 当WeakMap对象的key键所对应引用地址的 **key引用断开**或**key引用指向的地址内容发生变化**
  - 引用断开，WeakMap表现出“自动”删掉了对应value
- 所以weakMap也还是遵循垃圾回收机制对吗？栏主有没有试过多个引用指向weakMap的key，将一个引用断开，weakMap的键值是否还在内存中？
  - 只要Key的引用还在当前空间的时候，这个键值就还在。
  - 不管“复制”多少份key，只要他们引用还存在变量里面，那么垃圾回收机制并不会收回他们
- 你上面的例子 因为变量注册在最外层，不会被垃圾回收机制自动回收 所以会有用，在函数体内函数上下文执行了一般会自动释放，所以使用Map 和 WeakMap ，并没什么区别

```JS
const wm = new WeakMap();
// 给 WeakMap实例 赋值一个 占领内存足够大的 键值对
wm.set(key, new Array(114514 * 19));
global.gc();

// 此时把 key键 的引用进行断开，并观察内存占用情况
key = null;
// key = new Array(); 
global.gc();
```

- ES2021 推出了 WeakRef ，能实现保留对另一个对象的弱引用，而不会阻止该弱引用对象被GC回收

## es6 class

- 类使用在前，定义在后，这样会报错，因为 ES6 不会把变量声明提升 到代码头部。
  - 这种规定的原因与继承有关，必须保证子类在父类之后定义。

- 类的方法内部如果含有 this ，它将默认指向类的实例 。 
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

## js继承

- 原型链继承
- 寄生式继承

- class关键字，类实际就是函数，但是类语法明确了存在于实例、原型、类上的成员
  - ES6使用extends关键字继承，可以继承类或者普通的构造函数，其背后依旧基于“寄生式组合继承”

- ES6继承 vs ES5继承
  - ES5的继承是先创造子类的实例对象this，然后再将父类的方法添加到 this 上面 (`Parent.apply(this)`)。
    - ES6的继承机制完全不同，实质是先创造父类的实例对象 this （所以必须先调用 `super()` 方法），然后再用子类的构造函数修改 this 。
    - 因为es6子类没有自己的 this 对象，而是继承父类的 this 对象，然后对其进行加工。
    - super 虽然代表了父类 A 的构造函数，但是返回的是子类 B 的实例，即 super 内部的 this 指的是 B，因此 `super()` 在这里相当于`A.prototype.constructor.call(this)`;
    - ES6规定，通过 super 调用父类的方法时， super 会绑定子类的 this
  - ES5原型链中子类原型是父类实例，子类构造函数和父类构造函数无直接关系，因此需要使用call()
    - ES6具有双重继承关系：除了原型对象间继承，子类本身是父类构造的实例

- ref
  - [深入JavaScript继承原理](https://juejin.cn/post/6844903569317953543)

## js内存模型

- JS引擎将内存空间分为两块：堆（heap）与栈（stack）
- JS中的原始数据类型值通常都存储在栈中（Number String Null Undefined Boolean Symbol）
- 引用类型的数据都被存储在堆中（Object）
- 当使用原始数据值运算时，我们就是在操纵栈中的数据；
  - 但JS不允许直接访问堆空间，我们只能在栈中保存指向堆中数据的引用/指针/地址，在操作对象时，实际上是在操作对象的引用而不是实际的对象
- 函数本身作为对象，在被声明后就创建在了堆上
  - 当**函数被调用，引擎会在执行栈上创建函数的上下文**
  - 函数中的基本类型数据会直接被存放在栈空间上
  - 函数中的引用类型数据会存放在堆空间上，但为了使用堆上的数据，函数上下文会在栈中保存一个指向堆上数据的引用，实际上该过程刚才已经存在——全局上下文在栈上保存了一个指向函数的引用，函数对象本身存在堆上等待调用
  - **函数执行结束，则它的上下文出栈，栈空间被回收**，如果堆中对象不再被使用，则堆空间会被垃圾回收程序重新回收

## js执行机制

- JavaScript作为一门解释性语言，每次执行程序时，解释器都需要边解释边执行
- v8对JS程序的编译执行大致分为四个阶段：
- 词法分析
  - 对代码逐行进行分词(tokenizing/lexing)操作，在此期间引擎可以进行变量登记，其中包括变量声明、函数声明、形参声明等，输出有意义的词法单元(tokens)
  - var声明会为变量分配内存并初始化为undefined，赋值在执行阶段进行
  - let/const声明不会初始化变量，保持uninitialized
  - 函数声明则会直接在内存中创建函数对象并直接初始化为该函数对象
- 语法分析
  - 分词结束后，引擎将对tokens进行语法分析（parsing），得到一棵AST，如果语法分析出错则会停止后续操作直接报错
- 代码生成阶段
  - 这一阶段解释器会根据AST生成字节码（bytecode），v8引擎还会将字节码优化为CPU可执行的机器码

- 执行阶段
- 执行阶段是开发者可直接面对的场景，通常调试js程序可以看到一个调用栈，调用栈是什么？栈里的每一帧是什么，是什么时候放进去的？
- 调用栈里的每个栈帧是一个执行上下文（execution context），JS程序执行时会生成不止一个上下文，不同的执行上下文会遵循LIFO顺序被存入一个栈结构——调用栈
- 执行栈控制着JS程序的执行流：
  - 开始执行任何代码前，全局上下文是最先创建的上下文，被压入栈底，之后进行“词法分析-语法分析-代码生成-执行”
  - 当引擎执行到函数时会创建新的函数上下文入栈，对函数体中代码进行“词法分析-语法分析-代码生成-执行”，执行到子函数时重复上述入栈到执行的步骤。
  - 当函数执行完，执行栈会弹出当前函数上下文，将控制权返还给之前的执行上下文

- 为什么会存在变量、函数提升和暂时性死区？
  - 对于var变量声明，构建上下文时会给标识符分配内存空间，初始化为undefined。执行阶段，在声明语句之前访问var变量会读取到undefined，不会报错
  - 对于let/const变量声明，保持uninitialized。如果代码中在声明语句前访问，会报引用错误（未初始化）
  - 对于函数，会在内存里创建函数对象，并且直接初始化为该函数对象

- 可执行上下文中的词法环境中含有outer，通过这个引用获取外部词法环境的变量、声明等，这些引用串联起来一直指向全局的词法环境，形成了作用域链
- 作用域链是一个包含指针的列表，每个指针指向了一个执行栈中上下文的词法环境组件

- 闭包三种定义
- MDN：函数和函数内部所能访问到变量的总和
- 红宝书：引用了另一个函数作用域中变量的函数
- 你不知道的JS：当函数可以记住并访问所在的词法作用域，即使函数是在当前词法作用域之外执行，这时产生闭包
- 闭包通常是在嵌套函数中实现

## js垃圾回收

- 浏览器发展中，主要有两种GC策略：标记-清理 & 引用计数

- JS最常用的GC策略是标记清理（mark-and-sweep）
  - 该策略主要在维护一个可达性图，“可达”值是那些以某种方式可访问或可用的值。它们一定是以某种方式被使用的，不应该被回收。

- 标记清理：JS的GC程序会定期执行以下“垃圾回收”步骤，更新可达值并回收不可达的内存空间
  - 垃圾收集器找到所有的根，并“标记”它们【“根”指固有的可达值的基本集合，比如当前上下文的局部变量和参数、全局变量等，它们显然不可回收，因此作为根】
  - 遍历并“标记”根引用的对象
  - 再遍历并标记对象引用的内容。所有被遍历到的对象都会被记住，以免将来再次遍历到同一个对象
  - 重复直到所有可达的（从根部）引用都被访问到，没有被标记的对象都会被删除

- 引用计数（reference counting）策略使用较少。
  - 其思路是对每个值记录它被引用的次数。声明变量并给它赋一个引用值（对象）时，这个值的引用数为1。
  - 引用计数无法解决循环引用问题，循环引用会导致两个对象的引用值至少为一，即便函数执行完毕

- 优化
  - 分代
  - 增量
  - 闲时回收
