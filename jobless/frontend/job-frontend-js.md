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

## 如何理解原型？

- 构造函数：任何情况下创建一个函数，都会在内部为其创建一个prototype属性，该属性是一个指向原型对象的引用。使用原型对象可以允许上面定义的属性与方法被对象实例共享。
- 原型对象：原型对象会默认自动获得一个constructor属性，该属性是指回构造函数的引用。自定义构造函数的原型对象默认只会获得constructor属性，其余方法都继承自Object
- 原型对象的原型：原型对象本身是Object或父类的实例，它也有一个暴露为__proto__的属性指向父类构造函数的原型对象（隐式原型）。特别的，Object的原型对象是原型链的起点，其constructor指向Object()构造函数，同时Object原型对象的不再有原型，其不再具有__proto__
- 对象实例：每个被构造的实例内部也有__proto__，同样指向其构造函数原型对象

## new一个对象时发生了什么

- 在内存中创建一个新对象
- 新对象内部的[[Prototype]]特性被赋值为构造函数的prototype属性
- 构造函数内部的this被赋值为这个新对象（即this指向新对象）
- 执行构造函数内部的代码
- 如果构造函数返回非空对象，则返回该对象；否则，返回刚创建的新对象

## this

- this 是执行上下文中的一个属性，它指向最后一次调用这个方法的对象。 
- this的绑定在构建执行上下文时确定，在实际开发中，this 的指向可以通过四种调用模式来判断：
  - 默认绑定：当一个函数不是一个对象的属性时，直接作为函数来调用时，调用行为发生在全局上下文中，this 默认绑定到全局对象
  - 隐式绑定：被直接对象作为方法调用的函数，其上下文的 this 隐式绑定到该对象上
  - 显式绑定：通过 call()/apply()/bind() 把指定对象绑定到 this 上，叫做显式绑定
  - new 绑定：new 构造一个新对象时，构造函数内部的 this 会自动绑定到新建的对象上
- 绑定优先级：new绑定 > 显式绑定 > 隐式绑定 > 默认绑定

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

## array

- 对象的拷贝实际上只是在栈上多存了一个指向堆中实例的引用
- 深拷贝就是不仅新建一个引用，同时在堆上新开辟一块内存空间，存储一个和原始对象一样的对象，并让新引用指向该对象。
- JSON.parse(JSON.stringify(oldObj)); 
  - 无法深拷贝函数、正则对象；所有新对象constructor都会是Object；循环引用会报错

```JS
/** 深拷贝 */
function clone(parent) {
  // 存储循环引用
  let parents = [],
    children = [];

  function _clone(parent) {
    if (parent === null) return null;
    // 原始值，直接返回
    if (typeof parent != "object" || typeof parent != "function") return parent;

    let child, proto;
    // 确定具体对象类型
    let parentType = Object.prototype.toString.call(parent);
    if (parentType == "[object Array]") {
      // Array
      child = [];
    } else if (parentType == "[object RegExp]") {
      // RegExp
      child = new RegExp(parent.source, parent.flags);
      if (parent.lastIndex) child.lastIndex = parent.lastIndex;
    } else if (parentType == "[object Date]") {
      // Date
      child = new Date(parent.getDate());
    } else {
      // 其他对象
      // 获取parent原型配合create()而不是获取constructor配合new，避免创建冗余属性
      proto = Object.getPrototypeOf(parent);
      child = Object.create(proto);
    }

    // 是否有循环引用
    const index = parents.indexOf(parent);
    if (index != -1) {
      return children[index];
    }
    parents.push(parent);
    children.push(child);

    // for-in 遍历可迭代属性
    for (let item in parent) {
      child[item] = _clone(parent[item]);
    }

    return child;
  }

  return _clone(parent);
}

// 测试
function person(pname) {
  this.name = pname;
}

const Messi = new person("Messi");

function say() {
  console.log("hi");
}

const oldObj = {
  a: say,
  c: new RegExp("ab+c", "igum"),
  d: Messi,
};

oldObj.b = oldObj;

const newObj = clone(oldObj);
console.log(newObj.a, oldObj.a);
console.log(newObj.b, oldObj.b);
console.log(newObj.c, oldObj.c);
console.log(newObj.d.constructor, oldObj.d.constructor);
```

- 扁平化
- reduce
- map
- 基于队列，非递归

- 判断Array类型
  - Array.isArray(arr)
  - arr.constructor === Array
  - arr instanceof Array

- 数组去重
  - [... new Set(arr)]

## map vs object

- Object只能使用数值、字符串或符号作为键，且会被转换为字符串，
  - Map可使用任何数据类型作为key ，且保持该类型
- Map实例会维护键值对的插入顺序，因此可以根据插入顺序执行迭代操作
- Weak主要形容弱映射中的key是弱的——GC随时会回收弱映射的key，但是只要key存在，value就不会被回收

## js继承

- 原型链继承
- 寄生式继承

- class关键字，类实际就是函数，但是类语法明确了存在于实例、原型、类上的成员
  - ES6使用extends关键字继承，可以继承类或者普通的构造函数，其背后依旧基于“寄生式组合继承”

- ES6继承与ES5继承对比
  - ES5的继承是先创建子类对象，将之替换为父类的this
    - ES6继承父类的this对象，然后在子类对其使用this进行加工
  - ES5原型链中子类原型是父类实例，子类构造函数和父类构造函数无直接关系，因此需要使用call()
    - ES6具有双重继承关系：除了原型对象间继承，子类本身是父类构造的实例

## js内存模型

- JS引擎将内存空间分为两块：堆（heap）与栈（stack）
- JS中的原始数据类型值通常都存储在栈中（Number String Null Undefined Boolean Symbol）
- 引用类型的数据都被存储在堆中（Object）
- 当使用原始数据值运算时，我们就是在操纵栈中的数据；
  - 但JS不允许直接访问堆空间，我们只能在栈中保存指向堆中数据的引用/指针/地址，
  - 在操作对象时，实际上是在操作对象的引用而不是实际的对象
- 函数本身作为对象，在被声明后就创建在了堆上
  - 当函数被调用，引擎会在执行栈上创建函数的上下文
  - 函数中的基本类型数据会直接被存放在栈空间上
  - 函数中的引用类型数据会存放在堆空间上，但为了使用堆上的数据，函数上下文会在栈中保存一个指向堆上数据的引用，实际上该过程刚才已经存在——全局上下文在栈上保存了一个指向函数的引用，函数对象本身存在堆上等待调用
  - 函数执行结束，则它的上下文出栈，栈空间被回收，如果堆中对象不再被使用，则堆空间会被垃圾回收程序重新回收

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
- JS最常用的GC策略是标记清理（mark-and-sweep）：该策略主要在维护一个可达性图，“可达”值是那些以某种方式可访问或可用的值。它们一定是以某种方式被使用的，不应该被回收。
- 标记清理：JS的GC程序会定期执行以下“垃圾回收”步骤，更新可达值并回收不可达的内存空间
  - 垃圾收集器找到所有的根，并“标记”它们【“根”指固有的可达值的基本集合，比如当前上下文的局部变量和参数、全局变量等，它们显然不可回收，因此作为根】
  - 遍历并“标记”根引用的对象
  - 再遍历并标记对象引用的内容。所有被遍历到的对象都会被记住，以免将来再次遍历到同一个对象
  - 重复直到所有可达的（从根部）引用都被访问到，没有被标记的对象都会被删除
- 引用计数（reference counting）策略使用较少。其思路是对每个值记录它被引用的次数。声明变量并给它赋一个引用值（对象）时，这个值的引用数为1。
  - 引用计数无法解决循环引用问题，循环引用会导致两个对象的引用值至少为一，即便函数执行完毕
- 优化
  - 分代
  - 增量
  - 闲时回收
