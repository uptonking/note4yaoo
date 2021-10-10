---
title: job-coding-repeat-everytime
tags: [coding, job, repeat]
created: '2021-10-04T14:16:22.069Z'
modified: '2021-10-04T14:43:10.710Z'
---

# job-coding-repeat-everytime

> 练习 [2020年中大厂前端面试总结](https://wangyaxing.cn/blog/interview/%E9%9D%A2%E7%BB%8F/2020-%E9%9D%A2%E8%AF%95.html)
> [手写代码系列](https://wangyaxing.cn/blog/jsCode/)
> 超高频：面过的公司每家都问到了

# guide

# 防抖 debounce

- 不管事件触发频率多高，一定在事件触发n秒后才执行
- 使用场景
  - window 的 resize、scroll
  - mousedown、mousemove
  - keyup、keydown
  - 调整浏览器窗口大小时，resize次数过于频繁，造成计算过多，此时需要一次到位，就用到了防抖
  - 登录、发短信等按钮避免用户点击太快，以致于发送了多次请求，需要防抖
  - 文本编辑器实时保存，当无任何更改操作一秒后进行保存

- 非立即执行
  - 多次触发事件，只会在最后一次触发事件后等待设定的wait时间结束时执行一次
- 立即执行
  - 多次触发事件，第一次会立即执行函数，之后在设定wait事件内触犯的事件无效，不会执行。
  - 立即执行是第一次触发事件就执行然后n秒内不再执行，非立即执行是最后一次触发事件才执行，每次触发事件都会取消上一次的setTimeout任务

```js
/**
 * * 非立即执行版，每次事件触发后，若存在timer就 clearTimeout，重新创建任务
 */
function debounce(fn, wait) {
  let timer;

  return function(...args) {
    const that = this;

    if (timer) clearTimeout(timer);

    timer = setTimeout(() => {

      fn.apply(that, args);
    }, wait)
  }
}

// * 立即执行版
function debounce2(fn, wait, immediate) {
  let timer = null;

  return function(...args) {
    const that = this;

    // 每次触发事件时都取消之前的定时器
    if (timer) clearTimeout(timer);

    // 第一次会立即执行函数，之后在设定wait内触发事件无效，不会执行
    if (immediate) {
      const callNow = !timer;

      // 第一次触发后timer就存在，
      timer = setTimeout(() => {
        timer = null;
      }, wait);

      // 第一次触发才执行，之后等待wait毫秒timer清空了才会再次执行
      if (callNow) fn.apply(that, args);
    } else {
      timer = setTimeout(() => {
        fn.apply(that, args)
      }, wait)
    }

  }
}
```

# 节流 throttle
- 不管事件触发频率有多高，只在单位时间内执行一次。
- 使用场景
  - resize/scroll 事件，每隔一秒计算一次位置信息等
  - 浏览器播放事件，每个一秒计算一次进度信息等
  - input框实时搜索并发送请求展示下拉列表，没隔一秒发送一次请求 (也可做防抖)

```JS
/**
 * * 每次事件触发后，若存在timer则不执行，执行事件后timer=null
 */
function throttle(fn, wait) {
  let timer;

  return function(...args) {
    const that = this;

    // 计时器存在就返回
    if (timer) return;

    timer = setTimeout(() => {

      fn.apply(that, args);

      // 节流重在开关锁 timer=null
      timer = null;
    }, wait)

  }
}

// 基于时间戳实现
function throttle(fn, wait) {
  let prevTime = 0;

  return function(...args) {
    const that = this;

    const nowTime = Date.now();
    if (nowTime - prevTime < wait) return;

    fn.apply(that, args);
    prevTime = nowTime;

  }
}

// 立即执行版; https://juejin.cn/post/6844904071028228103
function throttle(fn, wait, immediate) {
  let timer;

  return function(...args) {
    const that = this;

    if (timer) return;

    if (immediate) {
      const callNow = !timer;

      timer = setTimeout(() => {
        timer = null;
      }, wait)

      if (callNow) fn.apply(that, args)
    } else {

      timer = setTimeout(() => {

        fn.apply(that, args);

        // 节流重在开关锁 timer=null
        timer = null;
      }, wait)
    }

  }
}
```

# curry 函数柯里化
- 要判断当前传入函数的参数个数 (args.length) 是否大于等于原函数所需参数个数 (fn.length) ，
  - 如果是，则执行当前函数；
  - 如果是小于，则返回一个函数。
- `fn.length` 可以获取到函数的正式形参数量，不包括rest参数和带默认值的参数

```JS
function curry2(fn, ...args) {
  return args.length >= fn.length ?
    fn(...args) :
    (...args2) => curry2(fn, ...args, ...args2);
}

// 测试表明，不用apply也能正常返回偏函数

function curry(fn) {
  return function curryCore(...args) {
    if (args.length >= fn.length) {
      // return fn.apply(this, args);
      return fn(...args);
    }

    return function(...args2) {
      // return curryCore.apply(this,args.concat(args2));
      return curryCore(...args, ...args2);
    };
  };
}

function sum(a, b, c) {
  return a + b + c;
}

const s = curry(sum);

s(1)(2)(3);
```

# new 创建新对象的过程

```JS
/**
 * * 手动实现new创建新对象的过程。
 * https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/71
 * 1. 在内存中创建新对象
 * 2. 新对象内部的[[Prototype]]指向构造函数的原型对象
 * 3. 构造函数内部的this指向新对象
 * 4. 执行构造函数内部代码
 * 5. 如果构造函数返回非空对象，则返回该对象，否则返回第1步创建的对象
 * - 这里的constructor其实是，`[].shift.call(arguments)`
 */
function _newObjectFactory(constructor, ...args) {
  const obj = new Object();

  // const obj = Object.create(constructor.prototype);
  Object.setPrototypeOf(obj, constructor.prototype);

  // 将构造函数内部的this绑定到新对象，并执行构造函数
  const newObj = constructor.apply(obj, args);

  // if (temp && ['object', 'function'].includes(typeof temp)) {
  //   return temp;
  // }

  // return obj;
  return typeof newObj === 'object' ? newObj : obj;
}
```

# 手写继承

## 组合式继承

- 思路是使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承
  - 既通过在原型上定义方法实现了函数复用，又能够保证每个实例都有它自己的属性

- 特点
  - 父类新增在构造函数上面的方法，子类都能访问到
  - 创建子类实例时，可以向父类传递参数
- 缺点
  - 调用了两次父类构造函数，生成了两份实例

```JS
// * 组合式继承
// https://juejin.cn/post/6844903569317953543
// 本方法很明显执行了两次父类的构造函数
// 子类仍旧无法传递动态参数给父类！
// 父类的构造函数被调用了两次。

function Parent1() {
  this.p1 = 'parent1';
}

Parent1.sayHello = function() {
  console.log('hello');
};

function Child(...args) {
  Parent1.apply(this, args);
  this.c1 = 'child1';
}

Child.prototype = new Parent1();
Child.prototype.constructor = Child;

const chd1 = new Child1();
console.log('chd1, ', chd1);
```

## 寄生组合式继承

- 所谓寄生组合式继承，即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。
  - 不必为了指定子类型的原型而调用超类型的构造函数
  - 使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型

```JS
// * 寄生组合式继承
// 子类继承了父类的属性和方法，同时属性没有被创建在原型链上，因此多个子类不会共享同一个属性。
// 子类可以传递动态参数给父类！
// 父类的构造函数只执行了一次！
// 但是子类想要在原型上添加方法，必须在继承之后添加，否则将覆盖掉原有原型上的方法。

function Child(...args) {
  Parent1.apply(this, args);
  this.c1 = 'child1';
}

/** 类似Object.create, 可以不用创建父类，直接利用已有实例作为模板 */
function object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}

function inheritPrototype(child, parent) {
  // 继承父类原型对象
  // const p = Object.create(parent.prototype);
  const p = object(parent.prototype);
  // 重写子类的原型对象
  child.prototype = p;
  // 将父类原型和子类原型合并，并赋值给子类的原型，实现允许在子类原型上添加新方法
  // copy原型链上可枚举的方法，如果子类本身已经继承自某个类，仍不能满足要求。
  // child.prototype = Object.assign(p, child.prototype);

  // 更新构造函数的指向
  child.prototype.constructor = child;
}

// 通过类似Object.create创建对象，然后更新Child.prototype和对象constructor的指向
inheritPrototype(Child1, Parent1);
const chd2 = new Child1();
console.log('chd2, ', chd2);
```

# setTimeout

```JS
/**
 * * 手写 setTimeout，思路是基于 `requestAnimationFrame` 和计算时间差实现
 * `Date.now()` method returns the number of milliseconds elapsed since 1970-01-01T00:00:00Z.
 */
function _setTimeout(fn, delay, ...args) {
  const start = Date.now();

  let timer;
  let now;

  const loop = () => {
    timer = requestAnimationFrame(loop);

    now = Date.now();

    if (now - start >= delay) {
      fn.apply(this, args);
      cancelAnimationFrame(timer);
    }
  };

  requestAnimationFrame(loop);

  return timer;
}
```

```js
// 使用 setTimeout 实现 setInterval

setTimeout(function fn() {
  console.log('在setTimeout中调用自身，就形成了setInterval');
  setTimeout(fn, 1000);
}, 1000);

setTimeout(function() {
  console.log('我被调用了');
  setTimeout(arguments.callee, 100);
}, 100);
```
