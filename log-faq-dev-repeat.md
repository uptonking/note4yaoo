---
title: log-faq-dev-repeat
tags: [dev, faq, repeat]
created: '2019-08-01T16:03:46.394Z'
modified: '2020-07-09T13:24:25.794Z'
---

# log-faq-dev-repeat

## not-yet

- 开发组件list和tree组件，是先开发list然后用多个list创建tree更好，还先开发tree然后用深度为2的tree创建list更好？
- Why it is important to cache DOM: http://jsperf.com/dom-caching-excercise

## 对象解构时，特别地，对react函数组件的props参数解构时，是在参数处解构更好，还是在函数体内解构更好？

- 在函数内解构，除了可以获得各属性prop变量外，还方便使用整体的props
- 在参数处解构，更直观的写法，便于第三方插件如doc-gen提取参数默认值
  - 解构多层嵌套对象的深层属性时，要考虑提取参数的意义与困难度
- 使用 `arguments[0]` 也可以获得props对象，但箭头函数没有 `this` - `super` - `arguments` - `new.target` ，且箭头函数不能用作构造函数
- One of the differences I can think of, and I suppose the most important, is that on the second case, while you are destructing your props object in function body, you are using `const` on declaration.
  - In that way, you can no longer change these values on your MyComponent, while on your first case you could easily modify them.
  - 对react组件来说，props不能改变，推荐只用const解构，但对普通函数参数解构时，要考虑用let
- ref
  - [Different ways of destructuring props in react](https://stackoverflow.com/questions/59586876/different-ways-of-destructuring-props-in-react)
  - [ES6 destructuring function parameter - naming root object](https://stackoverflow.com/questions/29051011/es6-destructuring-function-parameter-naming-root-object)

## 使用js时要不要用class? Please stop using classes in JavaScript

- Binding issues. 
  - As class constructor functions deal closely with `this ` keyword, 
  - it can introduce potential binding issues, especially if you try to pass your class method as a callback to an external routine (hello, React devs)
- Performance issues. 
  - Because of classes' implementation, they are notoriously difficult to optimize at runtime. 
- Private variables. 
  - One of the great advantages and the main reasons for classes in the first place, private variables, is just non-existent in JS.
- Strict hierarchies. 
  - Classes introduce a straight top-to-bottom order and make changes harder to implement, which is unacceptable in most JS applications.
- **Because the React team tells you not to**. 
  - While they did not explicitly deprecate the class-based components yet, they are likely to in the near future.
  - One of the design constraints and motivations for hooks was to represent a component being multiple states concurrently. That's something classes cannot express properly. 使用class组件对并发操作状态不友好
  - 想象一下这种场景，一个组件的render函数结构基本一致，但是它的数据层states可能会根据环境条件有不同的变化逻辑（相似的state结构，但是计算state的逻辑不同）
    - 这种情况下用class写就免不了大量的if else，
    - 但是hooks就可以把每种条件下的state变化逻辑抽离出来，
    - hooks比class组件更优雅的实现了states的多态
- Using a standard function+object+prototype chain "classes" is a good way to learn how JS works, but hiding all that behind the class sugar is too much abstraction to me.
  - Main benefit I get out of ES6 classes is defining the shape of data I am dealing with, so I can talk and think about it in precise terms. 
  - When I say "Customer", I know exactly what fields and properties that entails (and IDE will help me remember it too).
  - Member functions and inheritence are less useful for the reasons you stated in your article. 
  - Any kind of business code I prefer to keep in pure functions or service objects, that are given class based objects to manipulate. 
  - Code and data kept mostly separate.
- Before es6 class, I worked with projects that had different class implementations in them, all with their own ups and downs. Now everyone tends to use the ES2015 version and things are much clearer.
- proposed private field in js may not be better than typescript class.
- ref
    - https://everyday.codes/javascript/please-stop-using-classes-in-javascript/
    - https://dev.to/smalluban/do-we-really-need-classes-in-javascript-after-all-91n

## js对象内的属性如何引用同一对象的另一个属性

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

``` js 

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

``` js
      var carousel = new (function()
        {
              this.$slider =  $('#carousel1 .slider');
              this.panes = this.$slider.children().length;
        })();
      
      var foo = new function () {
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

## js function declaration vs function expression(named/anonymous)

- 匿名函数表达式无法递归调用自身(arguments.callee无法在严格模式)，具名可以
- 调试时的可读性
- Availability (scope) of the function，函数或变量会自动提升hoist
  - one difference that concerns me is when the machine creates the function object. Which in the case of declarations is before any statement is executed but after a statement body is invoked (be that the global code body or a sub-function's), and in the case of expressions is when the statement it is in gets executed. 
- `(function(){}).name === ""` ，匿名函数表达式会返回true
  - Both have a name property
- In Google's V8 and Firefox's Spidermonkey there might be a few microsecond JIST compilation difference, but ultimately the result is the exact same.
- If we declare the variable as function funcName(){}, then the immutability of the variable is the same as declaring it with var。
  - function expression can be const
  - function declaration name can be reassigned, too
- Function Declarations are only allowed to appear in Program or FunctionBody. Syntactically, they can not appear in Block ( `{ ... }` ) — such as that of if, while or for statements. This is because Blocks can only contain Statements, not SourceElements, which Function Declaration is. 
  - The only way Expression is allowed directly within Block is when it is part of ExpressionStatement. 
  - However, ExpressionStatement is explicitly defined to not begin with "function" keyword, and this is exactly why Function Declaration cannot appear directly within a Statement or Block (note that Block is merely a list of Statements).
- ref
  - http://kangax.github.io/nfe/
  - https://stackoverflow.com/questions/336859/var-functionname-function-vs-function-functionname

## 数组对象能添加自定义属性吗？ 可以

- `var arr=[1,2,3]; arr.count=3;`
- console.log(arr)得到 `[1, 2, 3, b: 33]`
- arr.length得到3
- 可以借助此方法对数组插值，参考styled-system的responsive array prop value

## Is it possible to have a comment inside a es6 template string?

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

## firefox与chrome滚动条样式不一致，应该如何处理

- 结论
  - 选择1：放弃自定义滚动条，使用系统默认的，各操作系统实现的滚动条不一致
  - 选择2：remove scrollbars
    - 使用箭头导航，add some arrows to scroll the content
    - 放弃滚动条，使用分页
- 可参考perfect-scrollbar(MIT)实现跨浏览器样式一致的滚动条
  - https://mdbootstrap.com/snippets/jquery/filipkapusta/765760
  - No manipulation on DOM tree
  - Use plain scrollTop and scrollLeft
  - 最外层的(竖直)滚动条问题仍未解决，firefox是自动隐藏且收窄的
- 自定义滚动条样式时要注意
  - scrollbar styling is part of the OS
  - 在触摸板上向上滑动时，页面顶部会逐渐隐藏，此时滚动条下移
  - 直接向上拖动滚动条时，页面顶部已隐藏的部分逐渐显示，与上面相反
- ref
  - https://stackoverflow.com/questions/47138603/scroll-issue-on-firefox-vs-webkit-browsers-side-navigation-text-truncate-and
  - https://www.zhihu.com/question/278165453
  - chrome支持滚动条的样式修改，但是又有多少网站去改变了滚动条的样式呢？为什么这几个相关的css私有伪元素，为什么一直没有被w3c标准采纳？
    - 换个样式，并不能让操作变得更方便。而样式方面的问题，用户完全可以按照自己的喜好选择操作系统中的主题
    - Every other browser, with the exception of chrome, uses the default OS UI for the scrollbar, which means, the scrollbars will look almost the same regardless which browser you use.
      - In Windows is a thick gray scrollbar with two buttons on the edges that work for going up/down.  
      - In OSX for instance, scrollbar never appear, until you scroll, and it looks like a discrete rectangle moving downward to the page you are scrolling.  
      - In contrast chrome uses a customized scrollbar instead of the default so it looks consistent in every OS it uses.

## 前后端分离导致的单点登录不可用如何解决

- 使用json web token，每个请求都带身份认证id
