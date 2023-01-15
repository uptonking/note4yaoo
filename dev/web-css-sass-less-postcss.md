---
title: web-css-sass-less-postcss
tags: [css, less, postcss, sass, styling, web]
created: 2020-10-06T12:03:25.728Z
modified: 2021-02-25T17:48:40.857Z
---

# web-css-sass-less-postcss

# guide

- css书写tips
  - 趋势是每个组件的css样式能独立使用，不需要单独引入reset样式和theme变量

- css预处理器的技术选型
  - 参考知名项目或大公司项目的选择，如google、microsoft、alibaba
  - 比较开发工具的下载量
  - 比较辅助项目及应用项目的流行度

- css预处理器的使用
  - 目的是提高开发者的效率
  - 定义变量: sass用 `$` , less用 `@`
  - @mixin指令定义一个可复用mixin，@include指令使用mixin
  - sass is the older syntax， scss(sassy css) is the new syntax as of Sass 3
    - 主要区别是scss有行尾分号，有花括号包围kv

- css缺点
  - 无局部模块，命名会全局污染
  - 无嵌套书写
  - 无变量(旧版css)

# sass

- who is using #sass
  - bootstrap.v4
  - google-material-components-web
  - ibm-carbon-components
  - github-primer-css
  - microsoft-fluentui-react

- 为什么使用Sass而不是Less
  - Sass研发有一些成熟的框架，比如说Compass，而且有很多框架也在使用Sass，比如说Foundation
  - 就国外讨论的热度来说，Sass绝对优于LESS。
  - 就学习教程来说，Sass的教程要优于LESS。
  - Sass是成熟的CSS预处理器之一，而且有一个稳定，强大的团队在维护。
  - Scss对sass语法进行了改良，Sass 3就变成了Scss(sassy css)。与原来的语法兼容，只是用{}取代了原来的缩进。
  - bootstrap 4的版本，使用的就是Scss，而之前的3使用的是less

- sass cons
  - sass内置函数有限，没有充分利用js灵活计算的优势，参考treat.js和polished

# postcss

- PostCSS的主要功能只有两个
  - 第一个就是把CSS解析成JavaScript可以操作的 抽象语法树结构（Abstract Syntax Tree，AST），
  - 第二个就是调用插件来处理AST并得到结果。
- PostCSS一般不单独使用，而是与已有的构建工具进行集成。
  - PostCSS与主流的构建工具，如 Webpack完成集成之后，选择满足功能需求的 PostCSS插件并进行配置。
- 使用postcss插件可以转换最新的css语法特性，类似babel
  - 可以书写最新的css语法，然后利用postcss插件转换
  - 不建议使用自定义的css语法，因为.css/.scss后缀的文件ide会报错，而.pcss文件不够流行

- [GitHub now supports PostCSS syntax highlight.](https://twitter.com/Qodesmith/status/1039592898076008450)
  - Use `.pcss` file file extension and `pcss` for code block examples in Markdown
  - Where can I find info on the `.pcss` extension? Is it the same syntax as css?
    - `.pcss` is a convention for a style sheet which supposed to be processed by PostCSS and usually has non-standard syntax or features, or standard syntax which isn't supported in all browsers yet. 
    - It could be a regular CSS as well.
    - Yep, it is just a convetion without proper description (because PostCSS plugins are very different)

## postcss vs sass

- postcss更/过于灵活，它对自定义css语法没有统一的规定，需要查看当前项目依赖的插件
  - 而sass内置了最常用的扩展css功能的语法
  - 主流ide可以支持sass文件跳转到@import的依赖文件，但postcss不支持
  - 可以参考babel和typescript对语法支持的关系

- the biggest difference between Sass and PostCSS:
  - Sass comes with a whole bunch of functionality out of the box, even if you don’t need some of that functionality. 
  - PostCSS allows you to choose which functionality you’d like to add (and they have a pretty amazing choice of independently created plugins).

- ref
  - https://www.npmtrends.com/sass-vs-postcss-vs-node-sass-vs-postcss-loader
    - vs2021: postcss >> postcss-loader > node-sass > sass(dart-sass)
  - https://www.npmtrends.com/typescript-vs-@babel/preset-typescript
    - vs2021: ts: 17m, babel-ts: 7m
  - [Switching from SASS to PostCSS](https://dev.to/michaeldscherr/switching-from-sass-to-postcss-4p0c)

## postcss-plugins

- https://github.com/postcss/postcss-scss
  - A SCSS parser for PostCSS.
- https://github.com/jonathantneal/postcss-sass
  - 依赖sass
- https://github.com/AleshaOleg/postcss-sass
  - 不依赖sass，Not all Sass syntax supported. 

# less

- who is using #less
  - ant-design.v4
  - bootstrap.v3

- ## [An Introduction To LESS, And LESS Vs Sass]https://www.smashingmagazine.com/2011/09/an-introduction-to-less-and-comparison-to-sass/)
- LESS and Sass share a lot of similarities in syntax, including the following:
  - Mixins -. Classes for classes.
  - Parametric mixins -. Classes to which you can pass parameters, like functions.
  - Nested Rules -. Classes within classes, which cut down on repetitive code.
  - Operations -. Math within CSS.
  - Color functions -. Edit your colors.
  - Namespaces -. Groups of styles that can be called by references.
  - Scope -. Make local changes to styles.
  - JavaScript evaluation -. JavaScript expressions evaluated in CSS.
- The main difference between LESS and Sass is the way in which they are processed. 
  - LESS is a JavaScript library and is, therefore, processed client-side.
  - Sass, on the other hand, runs on Ruby and is processed server-side. 
- A lot of developers might not choose LESS because of the additional time needed for the JavaScript engine to process the code and output the modified CSS to the browser.
  - The way I get around it is to use LESS only during the development process. 
    - Once I’m finished, I copy and paste the LESS output into a minifier and then into a separate CSS file to be included in place of the LESS files. 
  - Another option is to use LESS.app to compile and minify your LESS files. 
  - Both options will minimize the footprint of your styles, as well as avoid any problems that might result from the client’s browser not running JavaScript. 
- Maybe when LESS has a companion like Compass for Sass, it will become as powerful as Sass.

## less vs sass

- Less will work on both client side and Server side. SCSS will only work on Server side.
  - less是通过客户端处理的，sass是通过服务端处理，相比较之下前者解析会比后者慢一点
- Less环境较Sass简单
  - Sass的安装需要安装Ruby环境，Less基于JavaScript，是需要引入Less.js来处理代码输出css到浏览器，
  - 也可以在开发环节使用Less，然后编译成css文件，直接放在项目中。
- Less使用较Sass简单，Sass功能比Less更强大
  - sass有变量和作用域，变量有全局和局部之分，并且有优先级
  - sass有函数的概念，@function和@return以及函数参数（还有不定参）
  - 逻辑控制，if，while，for
  - 数据结构，list，map

## css预处理器简介

- 都提供了语法糖，最终经过预处理工具转换成css
- sass
  - 使用场景：bootstrap4, foundation
  - 特点
    - 无大括号，使用缩进
    - 支持变量$作用域
    - 支持函数
    - 支持流程控制
    - 支持数据结构$list, $map
  - 编译需要ruby
  - node-sass国内安装不流畅
  - 讨论度更高，资料更全
  - since2007
- less
  - 使用场景：bootstrap3，ant-design，七牛pd团队
  - 特点
    - 有大括号
    - 支持变量@
    - 不支持函数
  - 编译基于node
  - since2009
- scss
  - 使用场景：
  - 特点
    - 有大括号
    - **兼容css**
  - 就是sass 3
- stylus
  - 使用场景：
  - 特点
    - 支持缩进和大括号
  - since2010
- postcss
  - 使用场景：
  - 特点
- 预处理器使用建议
  - CSS中不建议用@import导入css，因为会增加http请求。但CSS预处理器中的导入和CSS的有很大区别，它是将不同css是在语义上导入，最终编译结果会生成一个CSS文件

# ref

- [Bootstrap 4 alpha release blog](https://blog.getbootstrap.com/2015/08/19/bootstrap-4-alpha/)
  - Moved from Less to Sass. 
    - Bootstrap now compiles faster than ever thanks to Libsass, and we join an increasingly large community of Sass developers.
- [Bootstrap 4 will be in SCSS. And if you care, v5 will likely be in PostCSS](https://mobile.twitter.com/mdo/status/591364406816079873)
  - reasons: more people use SCSS, libsass is crazy fast, syntax more explicitly clear, and I'm lazy and use SCSS at GitHub.
- [该使用SASS还是LESS?](https://www.zhihu.com/question/24375983/answers/updated)
- [国内互联网前端用LESS的还是SASS的多一些?](https://www.zhihu.com/question/22285654/answers/updated)
- [国内CSS预处理器 Less、Sass、Stylus 的实践代表分别有哪些？](https://www.zhihu.com/question/26810568/answers/updated)
- [Sass vs Less](https://zhuanlan.zhihu.com/p/51316352)
- [Sass vs. Less_2012](https://css-tricks.com/sass-vs-less/)
  - Slightly longer answer: Sass is better on a whole bunch of different fronts, 
  - but if you are already happy in Less, that’s cool, at least you are doing yourself a favor by preprocessing.
- [Introducing Sass Modules_2019](https://css-tricks.com/introducing-sass-modules/)
  - [css @import](https://developer.mozilla.org/en-US/docs/Web/CSS/@import)
  - Sass just launched a major new feature: a module system. This is a big step forward for @import
  - While the current @import rule allows you to pull in third-party packages, and split your Sass into manageable “partials, ” it has a few limitations:
    - @import is also a CSS feature, and the differences can be confusing
    - If you @import the same file multiple times, it can slow down compilation, cause override conflicts, and generate duplicate output.
    - Everything is in the global namespace, including third-party packages – so my color() function might override your existing color() function, or vice versa.
    - When you use a function like color(). it’s impossible to know exactly where it was defined. Which @import does it come from?
  - Sass package authors have tried to work around the namespace issues by manually prefixing our variables and functions — but Sass modules are a much more powerful solution. 
  - In brief `@import` is being replaced with more explicit `@use` and `@forward` rules.
  - Over the next few years Sass @import will be deprecated, and then removed. You can still use CSS imports, but they won’t be compiled by Sass. 
  - ` @use` is similar to `@import` . but has some notable differences
    - The file is only imported once, no matter how many times you @use it in a project.
    - Variables, mixins, and functions (what Sass calls “members”) that start with an underscore (_) or hyphen (-) are considered private, and not imported.
    - Members from the used file (buttons.scss in this case) are only made available locally, but not passed along to future imports.
    - Similarly, @extends will only apply up the chain; extending selectors in imported files, but not extending files that import this one.
    - All imported members are namespaced by default.
  - We don’t always need to use a file, and access its members. 
    - Sometimes we just want to pass it along to future imports. 
    - Let’s say we have multiple form-related partials, and we want to import all of them together as one namespace. 
    - We can do that with `@forward`
    - Members of the forwarded files are not available in the current document and no namespace is created, 
    - but those variables, functions, and mixins will be available when another file wants to @use or @forward the entire collection.
