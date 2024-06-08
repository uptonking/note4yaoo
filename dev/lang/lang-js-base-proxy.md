---
title: lang-js-base-proxy
tags: [ECMAScript, js, lang, proxy]
created: 2022-11-23T17:49:32.485Z
modified: 2022-11-23T17:49:54.052Z
---

# lang-js-base-proxy

# guide

- cons
  - [Vue3 解构赋值失去响应式引发的思考](https://zhuanlan.zhihu.com/p/543010554)

- [Proxy和Reflect的要注意的问题与局限性 - 掘金](https://juejin.cn/post/7004452888638554125)
  - 在开发时假如对一个对象做代理时，对代理的所有管理也需要再进行一层代理，原对象对原对象，代理对代理
# examples

# more

# discuss
- ## 

- ## 

- ## 

- ## JavaScript proxies that just trap everything to forward somewhere else (like a worker or a server) are starting to seem like a really bad idea to me.
- https://x.com/justinfagnani/status/1798939691313758706
  - They interact really badly with all kinds of duck-typing / brand-checking code because they behave like they have every property.
  - I suppose that private fields (and ergonomic brand checks) could help here, if you or your library code can adopt them.
  - But I think I'd rather just define a real client class, maybe with decorators, that only forwards known properties and methods.

- ## [Vue3.0里为什么要用 Proxy API 替代 defineProperty API ？](https://vue3js.cn/interview/vue3/proxy.html)
- Object.defineProperty只能遍历对象属性进行劫持
  - Proxy直接可以劫持整个对象，并返回一个新对象
  - Proxy有多达13种拦截方法, 不限于apply、ownKeys、deleteProperty、has等等，这是Object.defineProperty不具备的
- 数组API方法无法监听到
  - Proxy可以直接监听数组的变化（push、shift、splice）
- 检测不到对象属性的添加和删除
- 需要对每个属性进行遍历监听，如果嵌套对象，需要深层监听，造成性能问题

- ## Working with (JavaScript) Proxies is kind of a pain
- https://twitter.com/brian_d_vaughn/status/1443202951368089601
  - Can't detect them. Can't iterate over them (in some cases).

- ## now that IE/Edge (legacy) are gone, I am using Proxy all over and one of the most compelling cases is the one-off cache through a Map
- https://twitter.com/WebReflection/status/1528013495924666370

```JS
const speedy = new Proxy(new Map, {
  get(map, key) {
    if (!map.has(key)) {
      map.set(key, compute(key));
    }
    return map.get(key);
  }
});
```

- ## is it a good practice to use Proxy objects in your app, or I should let that shit to library authors?
- https://twitter.com/hhg2288/status/1602323703198523394
- I don’t like them, they feel a bit convoluted and aren’t that performant either.
  - Greg who made Shelf tried to add them to the Shelf library but found they were slowing things down significantly.
- if the problem can be solved more simply I wouldn’t touch them. I have yet to run into a problem in app code that proxies are the obvious answer for 
