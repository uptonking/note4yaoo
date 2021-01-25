---
title: log-faq-dev-common
tags: [dev, faq]
created: '2019-08-01T16:03:46.394Z'
modified: '2020-12-23T09:52:52.428Z'
---

# log-faq-dev-common

# faq-not-yet

- 没有电脑、没有网络、没有电的时候，你能做什么？

- 选用哪种state management方案更好？
  - 考虑直接用react context api，减少依赖
  - 一个开发者开发了多种方案(如jotai/zustand/react-tracked)，每种都有优缺点

- 哪些计算适合放在服务端，哪些计算适合放在客户端？
  - 行业案例: ssr, react-server-components

# 配置项过多时，如何处理更好，特别是针对组件或应用

- tips
  - search: component too many props/options
  - Too many options = bad software.
- 惯例优先原则/约定优于配置(convention over configuration)
  - 提供合理的默认值
  - opinionated的另外一个同义词是Convention over configuration，或者coding by convention
- 拆分出弱耦合的小组件，然后组合小组件
- 将部分紧密相关的配置项组合成一个大对象作为一个大的配置项，还要考虑方便替换该大配置对象的默认值
  - group by features
  - 类似component的`variant`属性，设计目的就是一次修改多个值
- 利用custom hooks，将配置项参数作为函数的参数，而不是组件自身的参数
  - 也称为 state reducer pattern

- It has too many configuration options and lacks configuration-by-convention dependency injection, one needs to look up all the services

- [A component with 500+ possible variants feels too much imho.](https://twitter.com/apixelpusher/status/1336875440972181510)
  - 本次讨论没有提出解决方案
  - If I’ve learned anything that past two weeks of focusing on standing up a library quickly it’s to not over-complicate variants or have too many of them for a single component. It’s not useful to force people to waste time parsing a ton of options in a bunch of select inputs.
  - I think this might be true for a lot of components, but a button in a reasonably complex design system? That's easily 500+ (1000+ depending on complexity) variations in the code component. How are you all doing this? Split by size (or w/e), even if that's not true in code?
    - `<Button>` props:
      * Size (several)
      * With icon (left or right)
      * Prominence (primary, secondary, tertiary, etc)
      * Visual style (default, success, danger, brand, etc—we had a lot lol) 
      * Automatic width vs sized to container
      * Some others I'm missing heh

- [What do you get when you put too many props on a component instead of breaking it into smaller components? Prop soup](https://twitter.com/NerdCowboy/status/966027592506617856)
  - if you want the most flexibility, compound components are the way to go imo. 
  - It allows you to create a wrapper component where you can pass in an object like you're saying AND you can create custom functionality elsewhere when you need it.

- [Hick’s Law predicts that the time and the effort it takes to make a decision increases with the number of options.](https://twitter.com/InfoKaaswell/status/1261675520271548418)
  - The more choices, the more time users take to make their decisions.
  - Trello's 3rd signup step has a dropdown with 15 options.
  - That makes it hard to pick one:
  - In a travel booking app like Airbnb, having too many options can lead to a paradox(矛盾的人/事) of choice (and a churn!):
  - Duolingo's list of lessons can sometimes be overwhelming
  - Zapier showed too many navigation links during their upgrade flow which distracts you from crucial checkout steps
  - Find an area where you have a lot of options or a lot of repetitions.
  - Try to either reduce the number of options or find ways to hide items.
  - If you can't minimize the options, try to put them in an easily skimmable order and make sure the items are familiar; else, it won't work.

- ref
  - [Avoid soul-crushing components](https://epicreact.dev/soul-crushing-components/)
    - The beauty of patterns like compound components, state reducers, prop getters, controlled props, etc. is that you can have your simple API and a simple implementation at the same time.
  - [7 code smells in your React components_202011](https://dev.to/awnton/7-code-smells-in-react-components-5f66)
  - [The State Reducer Pattern with React Hooks](https://kentcdodds.com/blog/the-state-reducer-pattern-with-react-hooks)
  - [Sometimes tools are too flexible.](https://twitter.com/sebmck/status/1142090256096743425)

# [event-loop异步模型为什么比多线程模型在IO密集场景中更高效？](https://www.zhihu.com/question/67751355/answers/updated)

- 因为event loop模型可以不使用IO线程，而是使用操作系统提供的IO复用/异步IO/事件驱动IO
  - 就比如ngx，在linux上，ngx用的是边沿触发的epoll，这是典型的IO复用，ngx是没有专门的IO线程的。
  - 所以并不是event loop模型更高效，而是异步IO复用比多线程同步IO额外开销更低。
- event loop模型的优点是，
  - event loop更贴近异步IO复用的模型，因此开发效率更高。
  - 单线程模型能够避免多线程带来的同步问题，既提高了开发效率，又避免了同步开销
- 最著名的event-loop的程序莫过于redis和nginx ，而两个恰好都是 single-threaded，一个进程占满一个核。
  - 有些应用中请求处理可能需要一定的 CPU 时间，那么可能会分到另外的线程去计算，为的也是保证 I/O 这一个线程能够不被阻塞。
- 用更轻量的用户级线程替换OS线程，然而根据资料，JVM最初就是LWT，但后来却改为了OS线程
  - 用户线程的问题主要在于操作系统无法提供足够的支持，
  - 因为从操作系统的角度来看，一个时间只有一个线程在运行而已。
  - Linux 以线程为调度单位，不管多少个用户线程都在这一个核上运行；
  - 一旦这个OS线程被抢占或挂起了（比如 blocking syscall），所有的用户线程都被一起挂起。
  - 这也回到了为什么在处理 I/O 的时候，用 event-loop + non-blocking I/O 要好过 multi-threading + blocking I/O 的原因：防止OS线程被 blocking I/O强制挂起。
- vert.x也面临着一个选择问题，是继续reactive呢，还是coroutine方向
  - 有一个问题就是问你是继续坚持reactive(rxjava2)的方向呢，还是走向coroutine(kotlin)方向

# 函数式编程 vs 面向对象的编程 (FP vs OOP)

- FP优点
  - 方便复用
  - 方便测试
  - 编译体积小，一般无需polyfill
- FP缺点
- FP案例
  - lodash/fp

- OOP优点
- OOP缺点

- ref
  - [为什么这两年函数式编程又火起来了？](https://www.zhihu.com/question/30190384/answers/updated)
    - 可以把oo语言加入lambda map folder reduce...
    - 函数式和过程式的区别是思维方式，而不在于语法。
    - 函数式的思维在于抽象流程，过程式的思维在于抽象主体。

# 最新消息事件的实现: push vs pull/poll

- 场景1：Producer速率大于Consumer速率
  - 采取Pull的方式只需要降低Consumer的访问频率即可
- 场景2：强调消息的实时性
  - 采用Push的方式时，一旦消息到达，服务端即可马上将其推送给消费端，这种方式的实时性显然是非常好的
- 场景3：Pull的长轮询
  - Pull模式存在的问题：由于主动权在消费方，消费方无法准确地决定何时去拉取最新的消息
  - 长轮询的优化方法，用以平衡Pull/Push模型各自的缺点。
  - 长轮询的基本方式是：消费者如果尝试拉取失败，不是直接return，而是把连接挂在那里 wait，服务端如果有新的消息到来，把连接拉起，返回最新消息。
- 场景4：部分或全部Consumer不在线
  - 在消息系统中，Producer和Consumer是完全解耦的
  - Producer发送消息时，并不要求Consumer一定要在线，对于Consumer也是同样的道理，这也是消息通信区别于RPC通信的主要特点

- Advantages of SSE over Websockets:
  - Transported over simple HTTP instead of a custom protocol
  - Can be poly-filled with javascript to "backport" SSE to browsers that do not support it yet.
  - Built in support for re-connection and event-id
  - Simpler protocol
  - No trouble with corporate firewalls doing packet inspection
- Advantages of Websockets over SSE:
  - Real time, two directional communication.
  - Native support in more browsers
- Ideal use cases of SSE:
  - Stock ticker streaming
  - twitter feed updating
  - Notifications to browser
- SSE gotchas:
  - No binary support
  - Maximum open connections limit
- ref
  - [Push 和 Pull 的区别](https://cloud.tencent.com/document/product/406/4791)
  - [WebSockets vs. Server-Sent events/EventSource](https://stackoverflow.com/questions/5195452/websockets-vs-server-sent-events-eventsource)
  - [Is it recommended to use Server Sent Events for pushing notifications by continuous querying of the database?](https://stackoverflow.com/questions/60156197/is-it-recomended-to-use-server-sent-events-for-pushing-notifications-by-continuo)

# 存取器getter-setter(setXxx) vs 公共变量 

- A difference between using a getter or setter and using a standard function is that getters/setters are automatically invoked on assignment. 
  - So it looks just like a normal property but behind the scenes you can have extra logic (or checks) to be run just before or after the assignment.
  - Direct property access is a perfectly fine way to do things when you don't need getter or setter special logic.
  - 能实现相同的功能，但提供的api不同，给开发者更大的灵活性

- getter-setter优点
  - getters and setter can have validation in them, fields can't
  - using getter you can get subclass of wanted class.
  - getters and setters are polymorphic, fields aren't
  - debugging can be much simpler, because breakpoint can be placed inside one method not near many references of that given field.
  - they can hide implementation changes
- getter usecase
  - The value is computed. 可计算属性
  - You are proxying a value from another object. 返回自身私有属性或封装的另一个对象的属性。
- setter usecase
  - You need to validate the incoming value.
  - You need to do something every time a value changes, like trim, concat

- ref
  - [Are `getter` and `setter` necessary in JavaScript?](https://stackoverflow.com/questions/34805099/are-getter-and-setter-necessary-in-javascript)
  - [Why use getters and setters in JavaScript?](https://stackoverflow.com/questions/42342623/why-use-getters-and-setters-in-javascript)

# 设计函数时，要不要统一用一个大的参数对象作为唯一参数？

- 优点
  - 无需关心参数顺序、方便加减参数数量
  - 方便实现高阶函数
- 缺点
  - 需要额外步骤解构出常用变量
  - 参数对象过多可能导致性能问题。 
    - Not only do you mess up JIT optimization and code minimization, but your code also becomes less performant. 
    - It makes no sense to be allocating new objects for each function invocation (or possibly mutating previous ones).
  - The problem with multi argument function, in most cases is the fact that our function is responsible for too many things. 
    - Creating one big object as an argument solves readability of this function call, but still keeps this function in the wrong shape.
    - Other thing is currying and partial application which is very handy, even sometimes it is must have. And your idea blocks that fully. 
- 总结
  - I think we should avoid functions with many arguments. 
  - But there is no silver bullet solution, and what you are proposing is a solution only for small variety of problems.
- ref
  - [Always pass one argument to your JavaScript function](https://levelup.gitconnected.com/always-pass-one-argument-to-your-javascript-function-4140d909937e)

# Should interface names begin with an “I” prefix?

- do if you like.
- In many ways, consistency is more important than convention. 
- It doesn't matter as long as you pick a style and stick with it!

# 对象解构时，特别地，对react函数组件的props参数解构时，是在参数处解构更好，还是在函数体内解构更好？

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
- 使用 `arguments[0]` 也可以获取整体props对象，但箭头函数没有 `this/super/arguments/new.target` ，且箭头函数不能用作构造函数
- One of the differences I can think of, and I suppose the most important, is that on the second case, while you are destructing your props object in function body, you are using `const` on declaration.
  - In that way, you can no longer change these values on your MyComponent, while on your first case you could easily modify them.
  - 对react组件来说，props不能改变，推荐只用const解构，但对普通函数参数解构时，要考虑用let
- ref
  - [Different ways of destructuring props in react](https://stackoverflow.com/questions/59586876/different-ways-of-destructuring-props-in-react)
  - [ES6 destructuring function parameter - naming root object](https://stackoverflow.com/questions/29051011/es6-destructuring-function-parameter-naming-root-object)

# js对象内的属性如何引用同一对象的另一个属性

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

# js数组对象能添加自定义属性吗？ 可以

- `var arr=[1,2,3]; arr.count=3;`
- console.log(arr)得到 `[1, 2, 3, b: 33]`
- arr.length得到3
- 可以借助此方法对数组插值，参考styled-system的responsive array prop value

# Is it possible to have a comment inside a es6 template string?

- 需要自己规定注释格式及解析方式
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

# session vs jwt(json web token)

- 前后端分离导致的单点登录不可用如何解决

- 使用json web token，每个请求都带身份认证id
