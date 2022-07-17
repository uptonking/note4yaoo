---
title: note-fwk-template-engine
tags: [frontend, template-engine]
created: 2020-11-08T10:01:14.339Z
modified: 2020-12-08T13:29:35.248Z
---

# note-fwk-template-engine

# guide

- 常用模版引擎
  - handlebars、ejs、lit-html

# faq

## [随着前端 MVC， MVVM 框架的壮大，后端模版引擎是否可以退出历史舞台了？(https://www.zhihu.com/question/47189015)](https://www.zhihu.com/question/47189015)

- 前后端分离后，后端绝大部分时候不再需要输出HTML代码，取而代之的是JSON纯数据
  - 这个就是后端MVC中的V，已经足够简单，几乎不用写什么东西，所以，更多的精力放在MC上了。
  - 而此时的后端的V，却是前端的MV*中的M。至于如何把M表现为V，由前端决定。这样一来，相比之下，前端工作确实繁重了不少
- 模板引擎跟后端语言如Python、PHP还是相关联的。也就是能够更加方便地搭配使用。模板引擎的重点角色往往是简单数据携带及其简单处理
- server side render最起码有两点是mvvm做不到的吧
  1. 能极大提升首渲速度
  2. SEO
- 需要秒开首屏以及对seo有高要求的应用场景，前端渲染还有下面几个地方，不能完成，只能后端渲染：
  - 导出为.doc .docx .xls .xlsx .pdf
  - 自定义纸张的打印
  - 前端导出PDF是可以做到的 只是代码量....amcharts里看到导出PDF的js，真的是大。

- ### [现在还有学习模版引擎的必要吗？](https://www.zhihu.com/question/61523320/answers/updated)
- 模板引擎，其实只是一种利用一种占位符或者特定语法实现对某段字符串的处理的方法，原理并不复杂，学习一下也挺快。
- 现在的前端框架，大多都使用了模板引擎的思想。
  - 比如vue的template部分，react的jsx等
- 更简单的是es6直接提供了``的方法，可以直接用额，不特地去学也会学到的
- 模板技术太基础了，
  - 即便你以后不需要单独去使用他，也会在各种场合遇到，
  - 比如随便一个双向绑定框架都相当于内置了模板引擎，即便做个微信小程序也会用到，
  - 核心无非就是三样东西：插值、判断、循环，学习成本几乎为零，还纠结啥，花个十分钟看一下呗。
- 模板与数据的分离相比传统页面减轻了服务器的压力； 做单页应用（就那种后台系统，邮箱之类的单页页面）时模板是很重要的组成部分 像vue react angular 一般模板与数据是分开的，然后在浏览器端两者结合组成页面

- ### [有哪些好用的前端模板引擎？](https://www.zhihu.com/question/32524504)
- 严格的模板引擎的定义，输入模板字符串 + 数据，得到渲染过的字符串
  - 实现上，从正则替换到拼 function 字符串到正经的 AST 解析各种各样，但从定义上来说都是差不多的。
  - 字符串渲染的性能其实也就在后端比较有意义，毕竟每一次渲染都是在消耗服务器资源，但在前端，用户只有一个，几十毫秒的渲染时间跟请求延迟比起来根本不算瓶颈。
  - 倒是前端的**后续更新是字符串模板引擎的软肋**，因为用渲染出来的字符串整个替换 innerHTML 是一个效率很低的更新方式。
  - 所以这样的模板引擎如今在纯前端情境下已经不再是好的选择，意义更多是在于方便前后端共用模板。
- 相比之下 Angular 是 DOM-based templating，直接解析 live DOM 来提取绑定，如果是字符串模板则是先转化成 live DOM 再解析。数据更新的时候直接通过绑定做局部更新。
  - 其他 MVVM 如 Knockout, Vue, Avalon 同理。
  - 缺点是没有现成的服务端渲染，要做服务端渲染基本等于重写一个字符串模板引擎。
  - 不过其实也不难，因为 DOM-based 的模板都是合法的 HTML，直接用现成的 HTML parser 预处理一下，后面的工作就相对简单了。
- 前端框架里面也有在前端解析字符串模板到静态AST再生成 live DOM 做局部更新的，比如 Ractive 和  @郑海波 的 Regular。
  - 这一类的实现因为解析到 AST 的这步已经在框架内部完成了，所以做服务端渲染几乎是现成的，另外也可以在构建时进行预编译。
- 然后说说 React，JSX 根本就不是模板，它就是带语法糖的手写 AST，并且把语法糖的处理放到了构建阶段。
  - 因为运行时不需要解析，所以 virtual DOM 可以每次渲染都重新生成整个 AST，在客户端用 diff + patch，在服务端则直接 serialize 成字符串。
  - 所有其他 virtual DOM 类方案同理。
  - 像 virtual-dom，mithril 之类的连语法糖都不带。
- 最后说下我的看法：
  - 如果是静态内容为主，那就直接服务端渲染好了，首屏加载速度快。
  - 如果是动态的应用界面，那就不应该用拼模板的思路去做，而是用做应用的架构（MV*，组件树）思路去做。

- underscore.template这种东西不叫模板引擎，他还不够格来配上“引擎”这两个字，充其量就是一个模板函数
- 我们团队自己用的模板引擎都前后有3个版本，现在我正在思考第4个版本应该有的特性
- **前端模板引擎需要有开发时的透明性**
  - 所谓透明性即指我在搭建好开发环境后，随手写代码随手刷新浏览器就能看到最新的效果，而不需要额外地执行任何命令或有任何的等待过程
  - 所以一切依赖编译过程的模板引擎并不适合前端使用，编译只能是模板引擎的一个特性，而不能是使用的前提
  - 更严格地说，使用FileWatch等手段进行文件变更检测并自动编译也不在我的考虑范围之内，因为这会造成额外的等待，像我这种手速极快的人可能编译速度跟不上
  - 前端的模板引擎应该是具备可在纯前端环境中解析使用的能力的
- **前端模板引擎要有良好的运行时调试能力**
  - 前端并不像后端，任何错误都可以有严格的日志记录和调用堆栈以供分析
  - 前端很难做到完全的错误处理和跟踪，这也导致前端必然存在需要直接在线上排查问题的情况
  - 就需要模板引擎提供良好的调试能力
  - 一般来说，编译后生成的函数的调试能力是弱于原先手动编写的模板片断的，因为自动生成的函数基本不具备可读性和可断点跟踪性
  - 因此在这一点上，一个供前端使用的模板引擎应该具备在特定情况下从“执行编译后函数获取HTML”换回“解析原模板再执行函数获取HTML”的模式，
  - 即应该支持在两种模式间切换或者更好地，一个强大的前端模板引擎编译生成的函数，可以使用Source Map或其它自定义的手段直接映射回原模板片段，不过现在并没有什么模板引擎实现了这一功能
- **前端模板引擎要对文件合并友好**
  - 在提供编译功能的模板引擎中，我们可以使用编译的手段将模板变为JavaScript源码，再在JavaScript的基础上做文件合并
  - 但是如果我们出于上文所说的调试能力等原因希望保留原模板片段，那就需要模板引擎本身支持模板片段合并为一个文件了
  - 需要实现对文件合并的支持，最好的办法就是让模板的语法是基于“片段”的
- **前端模板引擎要担负XSS的防范**
  - 前端对XSS的防范比较合适的方法是使用“默认转义”的白名单式策略
  - 基于此，一个合理的模板引擎是必须支持默认转义的，即所有数据的输出都默认经过escape的逻辑处理，将关键符号转为对应的HTML实体符号，以从根源上杜绝XSS的入侵路径
  - 当然并不是所有的内容都必须经过转义的，在系统中免不了有对用户输入富文本的需求，因此需要支持特定的语法来产生无转义的输出
- **前端模板引擎要支持片段的复用**
- **前端模板引擎要支持数据输出时的处理**
- **前端模板引擎要支持动态数据**
- **前端模板引擎要与异步流程严密结合**
- **前端模板引擎要支持不同的开发模式**
- **前端模板引擎要有实例间的隔离**

- 首先要区分出（传统的）string-based模板引擎和（新潮的）dom-based模板引擎。
- string based模板引擎的目标是输出字符串，
  - 几乎是所有时候，它的输入也是字符串，也就是所谓的模板。
  - string based模板引擎当中应用最广泛的，我猜是PHP的Smarty模板引擎
  - string based模板引擎的输出并不一定是要HTML，其实你想输出什么都可以，
    - 比如用来生成过CSS文件
    - 但是类似Jade这类的引擎，它基本上就只能输出标记语言，比如HTML/XML了，它就是为此而设计的。
- dom-based模板引擎，通常输出就直接是dom了
  - 很多dom-based模板引擎也可以很方便的挂载string输出端，从而在服务端也能输出
  - 输入也不一定，可能就是已经存在的DOM树（比如AngularJS直接写在页面上的时候），可能是字符串（如AngularJS使用字符串模板的时候）也可能是它们自己定义的某种语言（比如React之于JSX）
  - 前者需要先把字符串解析为语法树；后者就相当于给你一点语法糖，直接让你写一个AST了。
  - 有了AST，再在其中寻找出来一些“模板语法”，比如变量binding啊、比如循环、条件啊什么的。
  - dom-based模板引擎基本上不考虑输出HTML/XML以外的东西。
- 相比之下dom-based模板引擎可以实现像Matt-Esch/virtual-dom 这类的东西，
  - 在数据更新的时候实现最小操作，并不像string-based模板引擎那样，可能改了一个值就要重新生成巨大的一部分字符串。
- 个人认为，在浏览器端，string-based模板引擎的应用场景越来越有限，string-based模板引擎对现在提倡的组件化开发其实是挺不友好的。

# popular

- https://github.com/mde/ejs
  - http://ejs.co/
  - /5.1kStar/Apache2/202009/js
  - Embedded JavaScript templates
  - Client-side support
    - When `true`, compiles a function that can be rendered in the browser without needing to load the EJS Runtime (ejs.min.js).
    - includes do not work unless you use an include callback
  - Complies with the Express view system
- https://github.com/handlebars-lang/handlebars.js
  - https://handlebarsjs.com/guide/
  - /15.8kStar/MIT/202011/js
  - Handlebars let you build semantic templates effectively
  - Handlebars is largely compatible with Mustache templates.
  - syntax of Handlebars.js templates is a superset of Mustache templates.

# pieces

- [用20行代码带你了解模板引擎实现原理](https://zhuanlan.zhihu.com/p/267830144)
  - 模板引擎就是将数据（data）和模板（template）合并然后生成 HTML 文本。
  - 使用 ejs 的语法来实现一个模板引擎，整个代码实现只有 20 行。

# discuss

- ## [differences between handlebars.java and handlebars.js](https://github.com/jknack/handlebars.java/issues/346)
- handlebars.java is a server side template engine (like freemarker, velocity, etc..)
- That's all handlebars.java is about, just a template engine for Java.
- Now, if your app does a lot of JavaScript or MVC on the browser... people usually choose a template engine for the browser: handlebars.js (mustache.js, jade, haml, etc...)
- On such apps, handlebars.java let's you use/reuse templates in the server and browser. 
- This is the main goal of handlebars.java: "reuse the templates". 
- Here there aren't so much difference the same template works at server side (handlebars.java) and/or client side (handlebars.js). 
- Another issue that people want to solved too "is to reuse the helpers" again at server and client sides. 
  - This one is more tricky and handlebars.java does something on this point but it not always work.
  - What does it? It let you define your helpers in javascript and being executed in Java through Rhino.
  - This feature works good most of the times, but not always.
- Handlebars.js doesn't look in the context stack for missing attributes in the current scope (this is consistent with the Mustache Spec).
  - Hopefully, you can turn-off the context stack lookup in Handlebars.java by qualifying the attribute with this.

# ref

- [Comparison of web template engines](https://en.wikipedia.org/wiki/Comparison_of_web_template_engines)
