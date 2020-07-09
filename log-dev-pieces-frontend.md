---
attachments: [hello.txt]
tags: [log/dev]
title: log-dev-pieces-frontend
created: '2019-06-09T15:54:12.063Z'
modified: '2020-07-08T13:14:27.999Z'
---

# log-dev-pieces-frontend

## logging

- webpack的hmr热替换通常替换顶层App组件，子组件替换较难，因为会有状态共享、使用context等情况，并且hmr不保存状态
  - 适合react组件的热替换要用单独的工具库如react-hot-loader
  - 可以使用**Paint Flashing**工具高亮浏览器repaint的部分
  - Hot Module Replacement (HMR) exchanges, adds, or removes modules while an application is running, without a page reload. 
  - HMR is particularly useful in applications using a single state tree since components are "dumb" and will reflect the latest application state, even after their source is changed and they are replaced.
  - ref
    - https://apimirror.com/webpack~2/guides/hmr-react/index
    - https://developer.mozilla.org/en-US/docs/Tools/Paint_Flashing_Tool
- With paint flashing enabled, when you load a page, the entire screen flashes green because the browser has to paint everything. 
  - After the page has been rendered, the work is not done because things on the page can change. 
  - Each of these blinking animations requires the browser to paint a part of the screen, represented with a green rectangle.
- webpack编译react代码时，首页只显示html内容，js修改毫无作用
  - 可以通过`webpack --config ./webpack.config.js`的方式查看本次编译了哪些文件
  - 发现只编译了`src/index.js`的内容，没有编译config文件中`entry`指定的文件
  - 暂时的解决方法是根目录及src目录不要存放`index.js`文件，这样webpack才会编译entry配置的入口文件
- 副作用就是和本职无关的东西，函数的本职是接收参数，并返回值，多次同参调用都是确定的。我给你举几个前端世界里的副作用例子你体会体会：调接口获取数据、注册监听函数、手动操作DOM、 访问修改全局变量、打印log，使用 setTimeout 等
- console对象
  - 分级日志：console.log/info/debug/warn/error
  - 字符串占位符： `%s` 代表字符串， `%o` 代表对象， `%d` 代表数字
  - 设置样式：开头使用 `%c` , 如 `console.log('%cNull','color:gold;font-size:large')`
  - `console.dir` ：强制以JSON模式输出，如DOM会转换成json对象
  - `console.table` ：将对象属性或数组打印成表格更美观
  - `console.assert` ：仅当第一个参数为false时才打印第二个参数
  - `console.trace` ：打印调用栈
  - `console.time/End` ：打印代码执行时间
  - `console.memory` ：打印内存使用情况
  - `console.clear` ：清空控制台输出
  - `console.group` ： 分组输出，便于阅读
- 确保FMP（首次有效绘制） 尽可能的快速, 方法之一就是分阶段进行代码拆分
  - render loding-render-analytics
  - FMP所需的所有数据都可以在加载阶段获取其他代码的同时获取
  - http://www.alloyteam.com/2019/12/14174/
- RESTful APIs 缺点(GraphQL的优点)
  - 数据格式不规范
  - 猜谜游戏（如何判定一个失败的请求，400，401，还是404？）
  - 无意义的对话
  - 无合约协议
- 从输入页面URL到页面渲染完成大致流程
  - 解析URL
  - 浏览器本地缓存
  - DNS解析
  - 建立TCP/IP连接
  - 发送HTTP请求
  - 服务器处理请求并返回HTTP报文
  - 浏览器根据深度遍历的方式把html节点遍历构建DOM树
  - 遇到CSS外链，异步加载解析CSS，构建CSS规则树
  - 遇到script标签，如果是普通JS标签则同步加载并执行，阻塞页面渲染，如果标签上有defer/async属性则异步加载JS资源
  - 将dom树和CSS DOM树构造成render树
  - 渲染render树
- 浏览器加载与渲染的时间概念 
  - P：首次绘制。用于标记导航之后浏览器在屏幕上渲染像素的时间点。这个不难理解，就是浏览器开始请求网页到网页首帧绘制的时间点。这个指标表明了网页请求是否成功。
  - FCP：首次内容绘制。FCP标记的是浏览器渲染来自DOM第一位内容的时间点，该内容可能是文本、图像、SVG甚至canvas元素。
  - FMP：首次有效绘制(First Meaningful Paint)。这是一个很主观的指标。根据业务的不同，每一个网站的有效内容都是不相同的，有效内容就是网页中"主角元素"。对于视频网站而言，主角元素就是视频。对于搜索引擎而言，主角元素就是搜索框。
  - TTI：可交互时间。用于标记应用已进行视觉渲染并能可靠响应用户输入的时间点。应用可能会因为多种原因而无法响应用户输入：①页面组件运行所需的JavaScript尚未加载完成。②耗时较长的任务阻塞主线程
  - 根据devtool时间轴的结果
    - 虽然CSR(客户端渲染)配合预渲染方式（loading、骨架图）可以提前FP、FCP从而减少白屏问题，但无法提前FMP
    - SSR(服务端渲染)将FMP提前至js加载前触发，提前显示网页中的"主角元素"。SSR不仅可以减少白屏时间还可以大幅减少首屏加载时间。
  - ref
    - https://www.zhihu.com/question/308792091
    - https://zhuanlan.zhihu.com/p/90746589
- lodash引用方式
  - `import { cloneDeep } from 'lodash';`
    - 70.9KB
  - `import cloneDeep from 'lodash/cloneDeep';`
    - 17.8KB
  - `import { cloneDeep } from 'lodash-es';`
    - 14.6KB
  - Because static analysis in a dynamic language like JavaScript is hard, there will occasionally be false positives. 
    - Lodash is a good example of a module that looks like it has lots of side-effects, even in places that it doesn't. 
    - You can often mitigate those false positives by importing submodules (e.g. `import map from 'lodash-es/map'` rather than `import { map } from 'lodash-es'` ).
- named import和namespace import都可以被webpack v5和rollup进行tree shaking
  - default import对于多属性的对象，无法进行tree shaking
  - https://blog.csdn.net/qq_34629352/article/details/104258640
  - https://webpack.js.org/guides/tree-shaking/
  - Note that any imported file is subject to tree shaking. This means if you use something like css-loader in your project and import a CSS file, it needs to be added to the side effect list so it will not be unintentionally dropped in production mode
- $ and $$ will work on any web page (if jQuery is not included also) on Google Chrome, Firefox and Safari browsers where $ returns first element of selector passed.
    - `$` is `document.querySelector()`
    - `$$` is `document.querySelectorAll()`
    - `$x()` Returns an array of elements that match the specified XPath.
    - Warning: These functions only work when you call them from the Chrome DevTools Console. They won't work if you try to call them in your scripts.
    - They are native functions of Google Chrome and Firefox browsers, you can see $ and $$ definition in Safari as well.
    - https://developers.google.com/web/tools/chrome-devtools/console/utilities
- js对象内的属性引用同一对象的另一个属性
    - 如果不介意在对象字面量外写的话

    

``` 
    var a = {
       p1: [1]
    }
    a.p2 = a.p1
    ```

    - 如果要在对象字面量内写的话，可以使用访问器属性

    

``` 
    var a = {
        p1: [1],
        // p2: a.p1//this.p1  // 都是错的
        get p2(){return this.p1},
        set p2(v){this.p1=v}
    }
    a.p1 === a.p2 //true
    a.p2=1;
    a.p1; // 1
    ```

    - 对象字面量里this和a都是从作用域链中去寻找的，ES6之前只有两个作用域，全局或函数，在这里，没有函数，就是全局作用域，所以 this 和 a 就会从当前全局作用域中去寻找

    

``` 
    var a={p1:111};
    var a = {
        p1: [1],
        p2: a.p1
    }
    a.p2 //111
    ```

    - The `get` syntax binds an object property to a function that will be called when that property is looked up.
        - 语法： `{get prop() { ... } }` 或 `{get [expression]() { ... } }`
        - prop is the name of the property to bind to the given function.
        - you can also use expressions for a computed property name to bind to the given function.
        - It is not possible to simultaneously have a getter bound to a property and have that property actually hold a value, although it is possible to use a getter and a setter in conjunction to create a type of pseudo-property.
        - If you want to remove the getter, you can just delete it: `delete obj.latest;`
        - While using the get keyword and Object.defineProperty() have similar results, there is a subtle difference between the two when used on classes.
        - When using get the property will be defined on the instance's prototype, while using Object.defineProperty() the property will be defined on the instance it is applied to.
    - js定义了两种不同的属性
        - 如何区分属性的类型？
            - 通过 `Object.getOwnPropertyDescriptor()` 查看属性的描述符。有 `value` 的是数据属性，没有的是访问器属性
            - 数据属性存储值，访问器属性不存储值
            - value和set/get不能共存。因为有了set/get同时又有value，读写不明确
            - 访问器属性的功能用自定义函数也能实现，但es5原生支持更简洁
    - 数据属性主要有四个特性描述对象属性行为
        - [ ] [[Configurable]]: 默认为true。表示能否通过delete删除属性来重新定义属性，或者能否把属性改为可访问属性；
        - [x] [[Enumerable]]: 默认为true。表示能否通过for-in循环返回属性；
        - [ ] [[Writable]]: 默认为true。表示能否修改属性的值；
        - [ ] [[Value]]: 默认为underfined。表示包含属性的数据值。读写属性之都从这个位置进行；
    - 访问器属性不包含数据值。访问器属性不能直接定义，必须通过Object.defineProperty()定义。但包含一对getter和setter函数
        - [ ] [[Configurable]]: 默认为true。表示能否通过delete删除属性来重新定义属性，或者能否把属性改为可访问属性；
        - [ ] [[Enumerable]]: 默认为true。表示能否通过for-in 循环返回属性；
        - [ ] [[Get]]: 默认为underfined。表示读取属性时调用的函数；
        - [ ] [[Set]]: 默认为underfined。表示写入属性时调用的函数；
- import lodash
    - import { has } from 'lodash-es'; 
        - tree shakable, but CommonJS modules are not 
    - import has from 'lodash/has';
        -  lodash holds all it's functions in a single file, so rather than import the whole 'lodash' library at 100k, it's better to just import lodash's has function which is maybe 2k.
        - 'lodash/has' isn't a separate package. There's a file called has.js in the root of the regular 'lodash' package, and import has from 'lodash/has' (or const has = require ('lodash/has) will load that file. 
    - import { has } from 'lodash';
- 前端定时器
    - setTimeout()，精确度不高，可能有延迟执行的情况发生，且因为动用了红黑树，所以消耗资源大； 
    - setImmediate()，消耗的资源小，也不会造成阻塞，但效率也是最低的。
        - 目前只支持IE10以上, 速度比setTimeOut执行延迟快一些
    - process.nextTick()，效率最高，消费资源小，但会阻塞CPU的后续调用；
    - 关于Event Loop和任务队列,除了script整体代码，micro-task的任务优先级高于macro-task
        - macro-task: script (整体代码)，setTimeout, setInterval, setImmediate, I/O, UI rendering.
            - script(整体代码) ，可以理解为待执行的所有代码
        - micro-task: process.nextTick, Promise(原生)，Object.observe，MutationObserver
        - 执行过程
            - 第一步script整体代码被执行，创建各种macro-task,执行micro-task的部分
            - 第二步执行其他micro-task,优先级process.nextTick高于Promise
            - 第三步来执行macro-task. setTimeout的优先级高于setImmediate(一般情况,若timeout延迟大,后者可能先执行) 
            - 不同版本的node执行结果可能不同
    - ref https://segmentfault.com/a/1190000008595101
- webpack module vs chunk vs bundle
  - Webpack has three closely related terms - module, chunk, and bundle. 
  - A module is a piece of JS code that encapsulates data and provides functionality. Modules can depend on one another and thus, form a dependency graph. 
  - In the webpack bundling process, a few modules form a chunk. 
  - A bundle is an output file, produced by the bundling process. In most cases, each chunk emits exactly one bundle.
- webpack-hmr

``` 
const server = http.createServer(app);
let currentApp = app;
console.log(currentApp === app); // Returns true 

if (process.env.NODE_ENV !== 'production') {

    if (module.hot) {
         module.hot.accept('./server', () => {
             console.log(currentApp === app); // Returns false 

        })
    }
}
```

-  live reloading vs and hot module replacement/hot reloading vs React Fast Refresh
    - Live Reload - Triggers an app wide reload that listens to file changes
    - Hot Module Replacement - Is the same as Live Reload with the difference that it only replaces the modules that have been modified, hence the word Replacement. 
        - The advantage of hmr is that it doesn't lose your app state e.g. your inputs on your form fields, your currently selected tab etc.
    - Hot Reloading is just short for Hot Module Replacement.
    - webpack-hmr的原理
        - Hot Module Replacement is a core capability offered by Webpack. Webpack's compiler offers a `module.hot.accept()` API. Your application code can register callbacks to run when certain files have been recompiled. Here's how the process works:
            - Your Webpack config needs to include the HMR client code as an `entry` point in addition to your actual application entry file. This adds a small piece to the client bundle, which will open a websocket connection back to the Webpack dev server.
            - Your client application code calls `module.hot.accept("./someFileName", callbackToRunWhenThatFileIsRecompiled)` .
            - Webpack's dev server watches your files for changes, and recompiles source files when you hit save
            - The dev server sends a message to the client, announcing that those files have been recompiled, and including the new versions of the code
            - The client runs any `module.hot.accept` callbacks that match that file's path
        - What happens in that callback is up to you, but normal usage is to re-import the changed file and swap out the affected code, such as a React component or a Redux reducer. If you use this "plain HMR" approach in your own application, you would generally only have one or two calls to module.hot.accept(), such as one for your root component file and one for your root Reducer file. 
    - React-Hot-Loader uses the Webpack HMR API in a very powerful, but complex way. RHL transforms your code as it is compiled to add "proxy" components that wrap around anything that looks like a React component. Those "proxy" components insert their own `module.hot.accept()` calls at a much finer-grained level, to try to catch updates to each specific React component file instead of letting the updates "bubble up" to the root component file. The "proxy" components also try to manage the component state for the "real" components, so that when the "real" components get swapped out, the component state is carried over.
        - Unfortunately, there's a lot of edge cases involved, and that causes a lot of problems. Variations in build config can cause RHL to not work right. This is one of the reasons why Dan Abramov originally stopped working on RHL and started Create-React-App - to provide a stable, consistent, and known build environment as a potential baseline for later revisiting the idea of making advanced hot reloading widely available
        - I personally advise that people not use React-Hot-Loader, and instead stick with "plain HMR". With "plain HMR", updates to your component tree will not keep component state between reloads, but the implementation is much simpler and more reliable. Also, Redux goes great with plain HMR, as any data that's kept in Redux is still there when you reload the component tree from edits, and so the app will re-render based on that Redux state.
    - ref
        - https://blog.isquaredsoftware.com/2017/08/blogged-answers-webpack-hmr-vs-rhl/
- Can a JavaScript object property refer to another property of the same object?
    - Unfortunately, no. The `{}` syntax initiates creation of a new object, but until the object is created, it isn't assigned to the carousel variable. Also, the `this` value can only change as a result of a function call. If your "several more properties" are all going to depend only on slider, then you could get around with something like this:

    

``` 
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

    

``` 
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

    

``` 
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

    

``` 
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

    

``` 
      var foo = {
          a: 5,
          b: 6
      };
      foo.c = foo.a + foo.b;
    ```

    - eg3: once, more 

    

``` 
      var foo = function(o) {
          o.c = o.a + o.b;
          return o;
      }({a: 5, b: 6});
      
      function buildFoo(a, b) {
          var o = {a: a, b: b};
          o.c = o.a + o.b;
          return o;
      }
    ```

    - eg4: es6 class

    

``` 
      class Foo {
        constructor(){
          this.a = 5;
          this.b = 6;
          this.c = this.a + this.b;
        }  
      }
      const foo = new Foo();
    ```

- Please stop using classes in JavaScript
    - Binding issues. As class constructor functions deal closely with `this ` keyword, it can introduce potential binding issues, especially if you try to pass your class method as a callback to an external routine (hello, React devs)
    - Performance issues. Because of classes' implementation, they are notoriously difficult to optimize at runtime. 
    - Private variables. One of the great advantages and the main reasons for classes in the first place, private variables, is just non-existent in JS.
    - Strict hierarchies. Classes introduce a straight top-to-bottom order and make changes harder to implement, which is unacceptable in most JS applications.
    - Because the React team tells you not to. 
        - While they did not explicitly deprecate the class-based components yet, they are likely to in the near future.
        - One of the design constraints and motivations for hooks was to represent a component being multiple states concurrently. That's something classes cannot express properly.使用class组件对并发操作状态不友好
        - 想象一下这种场景，一个组件的render函数结构基本一致，但是它的数据层states可能会根据环境条件有不同的变化逻辑（相似的state结构，但是计算state的逻辑不同），这种情况下用class写就免不了大量的if else，但是hooks就可以把每种条件下的state变化逻辑抽离出来，hooks比class组件更优雅的实现了states的多态
    - Using a standard function+object+prototype chain "classes" is a good way to learn how JS works, but hiding all that behind the class sugar is too much abstraction to me.
        - Main benefit I get out of ES6 classes is defining the shape of data I am dealing with, so I can talk and think about it in precise terms. 
        - When I say "Customer", I know exactly what fields and properties that entails (and IDE will help me remember it too).
        - Member functions and inheritence are less useful for the reasons you stated in your article. 
        - Any kind of business code I prefer to keep in pure functions or service objects, that are given class based objects to manipulate. 
        - Code and data kept mostly separate.
    - Before es6 class, I worked with projects that had  different class implementations in them, all with their own ups and downs. Now everyone tends to use the ES2015 version and things are much clearer.
    - proposed private field in js may not be better than typescript class.
    - ref
        - https://everyday.codes/javascript/please-stop-using-classes-in-javascript/
        - https://dev.to/smalluban/do-we-really-need-classes-in-javascript-after-all-91n
- node require json文件
    - Node.js中推崇非阻塞I/O，但是require一个模块时却是同步调用的，这会带来性能上的开销，但并不是每次require都很耗时，因为在require成功之后会缓存起来，在此加载时直接从缓存读取，并没有额外开销。
    - 当通过.json的方式加载文件时，固然方便，但大量使用时会导致这些数据被缓存。大量数据会驻留在内存中，导致GC频繁和内存泄漏。
- npm list -g -depth=0
    - 列出本地已安装的包
- npx
    - npm从5.2版开始，增加了npx命令，现已集成进npm，不需单独安装
    - npx想要解决的主要问题，就是调用项目内部安装的模块
    - 若要调用Mocha，一般只能在项目脚本和package.json的scripts字段里面，如果想在命令行下调用，必须 `node-modules/.bin/mocha --version`
    - npx让项目内部安装的模块用起来更方便 `npx mocha --version`
    - npx的原理就是运行的时候，会到node_modules/.bin路径和环境变量$PATH里面，检查命令是否存在
    - 由于npx会检查环境变量$PATH，所以系统命令也可以调用 `npx ls -ll`
- REPL 交互式编程环境 (Read-Eval-Print-Loop) 
    - jShell
    - python 
    - babel-node(有babel-cli提供)
- targe=_blank
    - 当一个外部链接使用了target=_blank的方式，这个外部链接会打开一个新的浏览器tab。此时，新页面会打开，并且和原始页面占用**同一个进程**(UI进程)。
    - 这也意味着，如果这个新页面有任何性能上的问题，比如有一个很高的加载时间，这也将会影响到原始页面的表现。
    - 如果你打开的是一个同域的页面，那么你将可以在新页面访问到原始页面的所有内容，包括document对象(window.opener.document)。
    - 如果你打开的是一个跨域的页面，你虽然无法访问到document，但是你依然可以访问到location对象。
- node依赖
    - dependencies
        - 是最常用普通业务依赖
    - devDependencies
        - 开发环境依赖，常用来指定打包、测试工具
    - peerDependencies
        - 比较适合插件库来声明所依赖的核心库，将依赖提升到根目录避免重复下载
        - 指定当前包（也就是你写的包）兼容的宿主版本
        - 可以避免类依赖库被重复下载
            - 如果用户显式依赖了核心库，则可以忽略各插件的peerDependency声明
            - 如果用户没有显式依赖核心库，则按照插件peerDependencies中声明的版本将库安装到项目根目录中
            - 当用户依赖的版本、各插件依赖的版本之间不相互兼容，貌似会报错让用户自行修复
    - optionalDependencies
        - 可选依赖，它们即使安装失败，npm仍然继续运行
    - bundleDependencies
        - 在发布时会将指定的包打包到最终的发布包里
        - undleDependencies节点的功能跟dependencies节点是一样的，区别在于，当需要构建项目并发布版本时，bundleDependencies节点下的依赖会被包含在构建结果中，不需要另外npm install来安装了
    - 参考
        - https://github.com/SamHwang1990/blog/issues/7
- html a标签属性 rel='nofollow'
    - 告诉搜索引擎不要此网页上的链接或不要追踪此特定链接
    - 使用场景
        - 屏蔽广告/付费链接的权重
        - 屏蔽恶意用户
        - 划分优先级
    - rel="noopener noreferrer"可以取消传递相关信息
- The main difference between Cyan and Teal is that the Cyan is a color visible between blue and green; subtractive (CMY) primary color and Teal is a low-saturated color, a bluish-green to dark medium, similar to medium blue-green and dark cyan.
- 语言地区代码的构成，如en-US, zh-CN
    - The syntax and registry of HTTP language tags is the same as that defined by RFC 1766 
    - a language tag is composed of 1 or more parts: A primary language tag and a possibly empty series of subtags
    - any two-letter primary-tag is an ISO-639 language abbreviation and any two-letter initial subtag is an ISO-3166 country code.
    - 参考 https://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html
- 渐进式图片  
    - JPEG、GIF和PNG这三种图像格式都提供了一种功能，让图像能够更快地显示图像可以以一种特殊方式存储，显示时先大概显示图像的草图，当文件全部下载后再填充细
- file-loader will copy files to the build folder and insert links to them where they are included. 
- url-loader will encode entire file bytes content as base64 and insert base64-encoded content where they are included. So there is no separate file.
- The url-loader works like the file-loader, but can return a DataURL if the file is smaller than a byte limit.
- 获取数组中随机元素
    - ` arr[Math.floor(Math.random()*(arr.length))]`
- `performance.now()` vs `date.now()`
    - performance.now() returns the number of milliseconds, with microseconds in the fractional part and is more precise in orders of magnitude. 精度更高，不依赖系统时间，但在大型循环中使用会明显感觉慢，输出的是相对于performance.timing.navigationStart(页面初始化)的时间
        - Use cases include benchmarking and other cases where a high-resolution time is required such as media (gaming, audio, video, etc.)
        - performance.now() is only available in newer browsers (including IE10+).可能会有兼容性问题
    - Date.now() returns the number of milliseconds elapsed since Unix epoch(1 January 1970 00:00:00 UTC) and is dependent on system clock.会因为系统时间的变化而改变，准确性有时不能保证
        - Use cases include same old date manipulation ever since the beginning of JavaScript.
- typescript typeof

``` 
let bar = {a: 0};
let TypeofBar = typeof bar;  // the value "object"
type TypeofBar = typeof bar; // the type {a: number}
```

- Object.prototype.hasOwnProperty.call(obj, attrName); 
    - obj.hasOwnProperty(prop)判断一个属性是定义在对象本身而不是继承自原型链
        - 调用的是js中Object对象原型上的hasOwnProperty()方法
    - js没有将hasOwnProperty作为一个敏感词，所以我们很有可能将对象的一个属性命名为hasOwnProperty，这样一来就无法再使用对象原型的hasOwnProperty 方法来判断属性是否是来自原型链，解决方法有几种
        - ({}).hasOwnProperty.call(foo, 'bar'); // true
        - Object.prototype.hasOwnProperty.call(foo, 'bar');
- TypeScript 3.0在JSX命名空间中引入了一个新的类型别名 `LibraryManagedAttributes`
    - 这是一个辅助类型，用于告诉TypeScript某个JSX标记可以接受哪些属性
    - TypeScript 3.0 adds support for a new type alias in the JSX namespace called LibraryManagedAttributes. 
    - This helper type defines a transformation on the component’s Props type, before using to check a JSX expression targeting it; thus allowing customization like: how conflicts between provided props and inferred props are handled, how inferences are mapped, how optionality is handled, and how inferences from differing places should be combined.
    - The default-ed properties are inferred from the defaultProps property type. If an explicit type annotation is added, e.g. static defaultProps: `Partial<Props>` ; the compiler will not be able to identify which properties have defaults
    - Use static defaultProps: `Pick<Props, "name">` as an explicit type annotation instead
- As of NPM 2.0.0, importing local dependencies is supported natively.
    - `"bar": "file:../foo/bar"`
- npm main vs module
    - 当我们在不同环境下 `import` 一个npm包时，到底加载的是npm包的哪个文件？
        - 由于我们使用的模块规范有ESM和CommonJS两种，为了能在node环境下原生执行 ESM 规范的脚本文件，.mjs文件就应运而生。当存在 index.mjs 和 index.js 这种同名不同后缀的文件时， `import './index'` 或者 `require('./index')` 是会优先加载 index.mjs 文件
        - `main` : 定义了npm包的入口文件，browser环境和node环境均可使用
        - `module` : 定义npm包的ESM规范的入口文件，browser环境和node环境均可使用
        - `browser` : 定义npm包在browser环境下的入口文件
        - 实际上的优先级是 `browser=browser+mjs > module > browser+cjs > main`
            - webpack会根据这个顺序去寻找字段指定的文件，直到找到为止
    - 最早的npm包都是基于CommonJS规范(name,version,main)，当require('package1')的时候，就会根据main字段去查找入口文件
        - ES2015后，js拥有了ES Module，相较于之前的模块化方案更优雅，并且ES模块也是官方标准（JS 规范），而CommonJS模块是一种特殊的传统格式，利用ES Module的特性可以提高打包的性能，其中提升一个便是 tree shaking
        - CommonJS规范的包都是以 `main` 字段表示入口文件了，如果使用ES Module的也用main字段，就会对使用者造成困扰
        - webpack从版本2开始也可以识别 `module` 字段。打包工具遇到 package1 的时候，如果存在 module 字段，会优先使用，如果没找到对应的文件，则会使用 main 字段，并按照 CommonJS 规范打包
        - tree-shaking的功能就是把我们JS中无用的代码给去掉，如果把打包工具通过入口文件，产生的依赖树作为tree，tree-shaking就是把依赖树中用不到的代码shaking掉
- html所有元素通用的title属性，可以作为鼠标悬浮提示，可以用来作为input前类似label的提示，可以作为a11y的补充(对键盘导航影响大)
- tsc vs babel
    - I'd probably roll plain tsc for a lib. Output the js, .d.ts and source maps into the same folder (different from source folder).
    - Babel for "endpoint" code since one would use things like HMR, useful babel plugins, etc
- ts definitions downloaded does not match the component, 定义过时了，不匹配
    - https://stackoverflow.com/questions/44043492/override-typescript-types-in-v2-2-2-downloaded-from-npm-types/44046969#44046969
    - tsconfig.json > paths: './typings/*
    - https://stackoverflow.com/questions/44067014/error-ts7016-could-not-find-a-declaration-file-for-module-implicitly-has'
    - 将tsconfig.json的noImplicitAny设为any
- babel [7.0] Deprecate env option in .babelrc #5276
    - https://github.com/babel/babel/issues/5276
    - Options specific to a certain environment are merged into and overwrite non-env specific options.
    - Because it's JS you could do this in a lot of ways
- IOS环境下的按钮都是经过美化的，但通常我们在设计web app的时候不需要这些看上去老土的样式，所以，去除这些显得很有必要
    - `-webkit-appearance` 会将webkit浏览器中的元素默认样式去除
    - 会导致无法获取checkbox值,给这个元素重新赋上-webkit-appearance:checkbox就不会报错了
- typescript interface extends vs `&` intersect
    - the most significant is the difference in how members with the same property key are handled when present in both types.
    - extends above results in an error because the derriving interface declares a property with the same key as one in the derived interface but with an incompatible signature.
    - intersection types can contain conflicting types
    - ref
        - https://stackoverflow.com/questions/52681316/difference-between-extending-and-intersecting-interfaces-in-typescript
        - https://stackoverflow.com/questions/42735611/why-can-intersection-types-contain-conflicting-types
