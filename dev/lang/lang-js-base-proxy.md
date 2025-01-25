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

- ## 

- ## my favorite JavaScript API is `Proxy` – it allows you to "spy" on any object property
- https://x.com/aidenybai/status/1880648594895901055
- Check out vue 3 ref and reactive. They used proxies to handle reactivity in vue and it works flawlessly.

- Proxy is indeed cool and useful. But note that its primary role is to break JS semantics, when needed.

- Why use `Reflect` for that use case? Why not `target[key]` directly?
  - With Reflect.get you simulate the default behavior if there was no proxy.
- In this case you can use target[key]. However get() has an extra argument that Reflect.get can utilize so the right invocation would be Reflect.get(...arguments) or Reflect.get(target, key, receiver). So in the example posted, Reflect.get doesn't do anything.

- Proxy object can act as a facade. You may use it as wrapper for a complex object to intercept/control access to its properties. This is how zone.js actually manages change detection in Angular.

- ## structuredClone doesn’t support proxies which means Vue’s ref or reactive values cannot be cloned.
- https://x.com/logaretm/status/1821882058718757278
  - toRaw won’t work either because of deep objects.
  - I started to like shallowRef more recently because of this among other things but you lose the deep reactivity that is usually (sometimes?) desired.

- ## One thing about Vue's Proxy-based reactivity system is that because it relies on replacing the `this` value *internally* to objects, it doesn't just break on private fields, but it breaks on arrow functions too.
- https://x.com/justinfagnani/status/1823564891049091414
  - this wasn't to pick on Vue, but to point out that proxies have some really sharp edges and fundamental limitations.
  - Private fields got a bad rap recently because of their interaction with some proxy-based systems, but I think proxies themselves are the main culprit.
  - And it'll break in many other cases where the original `this` value and the proxied `this` value can be confused, like if `this` is passed out of the constructor.
  - So don't blame private fields here, there's a more fundamental problem with this type of proxy system.

- The fundamental issue is that what we really need is Object.observe(), and instead we got proxies.
- Array, Map, & Set if not special-cased, but any collection especially useralnd. Mutable closure state. 
  - And any API backed by mutable state where you don't have a reference to the mutable object itself.
  - Closure state can't be observed by Vue-style proxies or Object.observe()

- The DOM is a big source of non-observable state that won't be fully signalized...

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
