---
title: job-js-es6-latest
tags: [es6, job, js, latest]
created: 2021-10-10T09:56:40.369Z
modified: 2021-10-10T09:56:56.337Z
---

# job-js-es6-latest

# guide

# proxy使用场景

- 修改的是程序默认形为，就形同于在编程语言层面上做修改，属于元编程(meta programming)
- new Proxy(target, handler)
- Proxy其功能非常类似于设计模式中的代理模式
  - 拦截和监视外部对对象的访问
    - 通过使用Proxy实现观察者模式
  - 降低函数或类的复杂度
  - 在复杂操作前对操作进行校验或对所需资源进行管理



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
