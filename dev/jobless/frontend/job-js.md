---
title: job-js
tags: [frontend, job, js]
created: 2021-09-23T08:24:24.348Z
modified: 2021-10-10T09:30:51.190Z
---

# job-js

# guide

## function 函数

- `func.length` 属性，正式形参的个数，要排除rest参数和带默认值的参数
  - `length` is a property of a function object, and indicates how many arguments the function expects, i.e. the number of formal parameters.
  - This number excludes the rest parameter and only includes parameters before the first one with a default value
  - `arguments.length` is local to a function and provides the number of arguments actually passed to the function.

## 箭头函数

- 箭头函数没有`this`，其`this`需从外部作用域获取，因此取决于箭头函数定义位置的上下文
- 箭头函数不能使用 `arguments`、`super` 和 `new.target`，也不能用作构造函数。
- 此外也没有 `prototype` 属性

## 柯里化

- 柯里化其实是函数式编程的一个过程，在这个过程中能把一个带有多个参数的函数转换成一系列的嵌套函数
- 柯里化可以实现：
  - 参数复用: 在新函数中继续接收剩余参数
  - 延迟执行: 在参数收集齐后再执行函数

## this

- [this的四种绑定规则(优先级由上到下依次递增)](https://juejin.cn/post/6844903688897576974)
- 默认绑定
  - 独立函数调用时， this 指向全局对象，
  - 如果使用严格模式，那么全局对象无法使用默认绑定， this 绑定至 undefined 并抛错（TypeError: this is undefined）
- 隐式绑定
  - 当函数作为引用属性被添加到对象中，隐式绑定规则会把函数调用中的 this 绑定到这个上下文对象
- 显示绑定
  - 运用apply call 方法，在调用函数时候绑定this，也就是指定调用的函数的this值
- new绑定
  - 使用new操作符的时候的this绑定

- this是执行上下文中的一个属性，它指向最后一次调用这个方法的对象。
- this的绑定在构建执行上下文时确定，在实际开发中，this的指向可以通过四种调用模式来判断：
  - 默认绑定：当一个函数不是一个对象的属性时，直接作为函数来调用时，调用行为发生在全局上下文中，this默认绑定到全局对象
  - 隐式绑定：被直接对象作为方法调用的函数，其上下文的 this 隐式绑定到该对象上
  - 显式绑定：通过 call()/apply()/bind() 把指定对象绑定到 this 上
  - new绑定：new构造一个新对象时，构造函数内部的 this 会自动绑定到新建的对象上
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
  - Java使用new实例化对象后，Java对象不会像JS中的函数上下文一样立即消失，同时private又保证了变量对外隐藏，之后只要使用calc.add()就能实现计算

- [Closures vs. classes for encapsulation?](https://stackoverflow.com/questions/8729714)
- The reasons to avoid closures is overhead.
  - Your get and set functions are trivially 20x slower than properties. 
  - Your closures also have a large memory overhead that is `O(N)` with the number of instances.

- there aren't any real classes in javascripts, we just mimic them with closures.
  - Because closures must reference the environment in which they were created (this is how they can use the private internal state data), they are more costly than just using a public function. 
  - So if you have a static method that doesn't require the internal state, you should add it to Class1 instead by using the `prototype` keyword
  - This way, the static method can be used through the prototype chain without using up extra memory with unnecessary closures. 

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

## 运算符

- `==`比较
  - 如果两个值类型相同，再进行三个等号(===)的比较
  - 如果两个值类型不同，也有可能相等，需根据以下规则进行类型转换再比较
    - 如果一个是null，一个是undefined，那么相等
    - 如果一个是字符串，一个是数值，把字符串转换成数值之后再进行比较
  - 字符串和数字之间的相等比较，将字符串转换为数字之后再进行比较。
  - 其他类型和布尔类型之间的相等比较，先将布尔值转换为数字后，再应用其他规则进行比较。
  - null 和 undefined 之间的相等比较，结果为真。其他值和它们进行比较都返回假值
  - 如果一个操作值为 NaN，则相等比较返回 false（NaN 本身也不等于 NaN）

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
