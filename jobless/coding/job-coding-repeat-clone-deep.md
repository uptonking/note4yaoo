---
title: job-coding-repeat-clone-deep
tags: [coding, job, repeat]
created: 2021-10-04T17:43:08.859Z
modified: 2021-10-04T19:03:41.234Z
---

# job-coding-repeat-clone-deep

# guide

# 手写深拷贝
- `JSON.stringify()`缺点
  - 序列化循环引用会抛出异常
  - 无法序列化函数
  - 无法序列化特殊内置对象
    - 如RegExp
    - 序列化Map/Set会丢失内容，始终是{}
    - 序列化Date对象默认丢失timezone同时变成字符串 // "2021-10-03T13:42:01.550Z"
  - 忽略Symbol、undefined，因为不符合json规范
    - 忽略值为undefined的属性
    - Symbol类型的属性key也会被忽略
  - Infinity, NaN 都会序列化为 'null'

- `JSON.parse(JSON.stringify(oldObj))`; 
  - 无法深拷贝函数、正则对象；循环引用会报错
  - 所有新对象constructor都会是Object

```JS
/**
 * * 深拷贝一个比较标准的实现，跑通了大部分lodash测试用例。
 * - 但没有处理特殊类型对象，如Map； 注意 `typeof null` 也是 object
 * * 1. 返回循环引用的对象 copied.get(val)
 * * 2. 创建新内置对象、[]或{}，并放入记录循环引用的映射表
 * * 3. 遍历参数对象，递归地拷贝参数对象的属性值对象
 */
function cloneDeep(value) {

  // 不能用 {}，因为key只能是String或Symbol
  // const copied = {};
  const copied = new WeakMap();

  function _cloneDeep(val) {
    if (val === null) return null;

    if (typeof val === 'object') {

      if (copied.get(val)) {
        return copied.get(val);
      }

      const newVal = Array.isArray(val) ? [] : {};

      copied.set(val, newVal);

      Object.keys(val).forEach((key) => {
        newVal[key] = _cloneDeep(val[key]);
      });

      return newVal;
    } else {
      return val;
    }
  }

  return _cloneDeep(value);
}
```

```JS
/**
 * * 在上一个的基础上，实现了拷贝 特殊内置类型；
 * - 还实现了保留原对象的原型对象
 * 
 */
function cloneDeep2(value) {
  const nativeTypes = [Date, RegExp, Set, Map, WeakSet, WeakMap];

  const copied = new WeakMap();

  function _cloneDeep(val) {
    if (val === null) return null;

    if (typeof val === 'object') {
      if (copied.get(val)) {
        return copied.get(val);
      }

      let newVal;
      // newVal = Array.isArray(val) ? [] : {};

      if (nativeTypes.includes(val.constructor)) {
        newVal = new val.constructor(val);
        copied.set(val, newVal);

        return newVal;
      }

      // 不直接创建空对象的目的：克隆的结果和之前保持相同的所属类，同时也兼容了数组的情况
      // let newObj = new val.constructor();

      // 创建其他对象，保持属性配置
      const valDesc = Object.getOwnPropertyDescriptors(val);
      newVal = Object.create(Object.getPrototypeOf(val), valDesc);

      copied.set(val, newVal);

      Object.keys(val).forEach((key) => {
        newVal[key] = _cloneDeep(val[key]);
      });

      return newVal;
    } else {
      return val;
    }
  }

  return _cloneDeep(value);
}
```

- 对于数组arr, 若手动添加新属性`arr.ext='ext'`，不同的遍历方法得到的结果不同
  - `JSON.stringify()`时新属性ext会丢失，得到 '["a", "b", "c"]'
  - for-of会获取到数组元素值，但获取不到添加的ext属性
  - for-in遍历可以获取到ext属性和值，0, 1, 2, ext
  - Object.keys()会获取到ext

- `typeof operand` / `typeof(operand)` 表达式的值只有8种
  - 5种基本类型：'string', 'number', 'boolean', 'undefined', 'bigint'
  - 3种非基本类型：object, function, symbol

- 为什么 `typeof null` 会返回 object ？
  - 因为在js的设计中，object的前三位标志是000，而 null 在32位表示中也全是0，因此，typeof null 也会打印出object

- mozilla文档描述了Date()作为构造函数有4种使用方法
  - new Date()
  - new Date(value) // integer milliseconds since 1970
  - new Date(dateString)
  - new Date(year, monthIndex, day, hours, minutes, seconds, milliseconds)
- 但其实还有第5种 `new Date(dateObj)` 创建date对象的方法
  - [Calling the Date constructor with a Date object](https://stackoverflow.com/questions/32364860)
  - from the relevant portion of the ECMAScript 6 spec:
    - If `Type(value)` is Object and value has a `[[DateValue]]` internal slot, then Let tv be thisTimeValue(value).
  - But, the ES5 spec is not the same and will do a conversion to a string when you do what you're doing which will then be parsed as a string by the constructor.
  - es6相当于直接 new Date(d1.getTime()); 
  - es5相当于直接 new Date(Date.parse(d1.toString())); 
  - Firefox seems to be following ES5.1 behaviour at the moment and Chrome ES6.0
- 实测 `new RegExp(reObj)` 也能创建一个正则对象

```JS
JSON.stringify({ b: undefined }) // {}

JSON.stringify(function() {}) // undefined
```

- 实际上克隆函数是没有实际应用场景的，两个对象使用在内存中处于同一个地址的函数也是没有任何问题的，
  - 我特意看了下lodash对函数的处理，如果发现是函数的话就会直接返回了
- 通过prototype来区分下箭头函数和普通函数，箭头函数是没有prototype
- `new Function(arg1, ... , argN, functionBody)`; 
  - 如 `new Function('a', 'b', 'return a + b')`; 
- 可以直接使用`eval`和函数字符串来重新生成一个箭头函数，注意这种方法是不适用于普通函数的。

```JS
/**
 * * 箭头函数对象使用eval()生成；
 * * 对普通函数对象，取出参数、函数体，通过new Function(...args, body)生成
 */
function cloneFunction(func) {
  //  { 中间是任意字符或换行 }
  const bodyReg = /(?<={)(.|\n)+(?=})/m;
  // ( 任意字符 ) {
  const paramReg = /(?<=\().+(?=\)\s+{)/;

  // 函数源码文本
  const funcString = func.toString();

  if (func.prototype) {
    // console.log('普通函数');
    // exec返回的是第一个匹配值
    const param = paramReg.exec(funcString);
    const body = bodyReg.exec(funcString);

    if (body) {
      // console.log('匹配到函数体：', body[0]);
      if (param) {
        const paramArr = param[0].split(',');
        // console.log('匹配到参数：', paramArr);
        return new Function(...paramArr, body[0]);
      } else {
        return new Function(body[0]);
      }
    } else {
      return null;
    }
  } else {
    // 直接生成箭头函数对象
    return eval(funcString);
  }
}
```

- 实现参考
  - [浅拷贝和深拷贝](https://wangyaxing.cn/blog/jsCode/%E6%B5%85%E6%8B%B7%E8%B4%9D%E5%92%8C%E6%B7%B1%E6%8B%B7%E8%B4%9D.html)
  - [百度：什么是浅拷贝和深拷贝？如何实现 Object 的深拷贝](https://github.com/sisterAn/JavaScript-Algorithms/issues/55)
  - [如何写出一个惊艳面试官的深拷贝?](https://juejin.cn/post/6844903929705136141)
  - [Javascript 经典面试之深拷贝VS浅拷贝](https://segmentfault.com/a/1190000023751381)
  - [实用函数 深拷贝](https://www.yuque.com/nepjnq/fgeemd/xz22uy#AdRRt)
# 浅拷贝和深拷贝
- JS数据类型分为基本数据类型和引用数据类型
  - 基本数据类型：变量名和值都储存在栈内存中；
  - 引用数据类型：变量名储存在栈内存中，值储存在堆内存中，栈中保存的是对象在堆内存中的地址，堆内存中会提供一个引用地址指向堆内存中的值，而这个引用地址是储存在栈内存中的。

- 对象的浅拷贝只是在栈上多存了一个指向堆中实例的引用
- 浅拷贝的实现
  - 直接赋值，修改对象后，浅拷贝的对象也会改变
  - 浅拷贝第一层属性值
    - let obj2 = { ...obj }
    - Object.assign(target, source)
    - 在循环中利用赋值浅拷贝第一层属性值

```JS
let obj2 = { ...obj };
let obj2 = Object.assign({}, obj); // returns the modified target object.

let obj2 = {};
for (let i in obj) {
  if (!obj.hasOwnProperty(i)) break; // 这里使用 continue 也可以
  obj2[i] = obj[i];
}
```

- 深拷贝就是不仅新建一个引用，同时在堆上新开辟一块内存空间，存储一个和原始对象一样的对象，并让新引用指向该对象。
# 手写深比较

```JS
/**
 * * 手写深比较
 * * 思路
 * * a. 直接比较 ===
 * * b. 比较非null的对象的Object.keys()属性数量
 * * c. for in循环里面递归比较各属性值
 */
function deepEquals(o1, o2) {
  if (o1 === o2) return true;

  if (
    typeof o1 === 'object' &&
    typeof o2 === 'object' &&
    o1 != null &&
    o2 != null
  ) {
    if (Object.keys(o1) !== Object.keys(o2)) {
      return false;
    }

    // for-in可处理数组的情况
    for (const p in o1) {
      if (!deepEquals(o1[p], o2[p])) return false;
    }

    return true;
  }

  return false;
}
```
