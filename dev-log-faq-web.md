---
title: dev-log-faq-web
tags: [faq, web]
created: '2020-11-07T12:26:28.591Z'
modified: '2021-03-29T19:17:38.650Z'
---

# dev-log-faq-web

# faq-not-yet

- autoSave或formatOnSave 经常会导致编辑器卡顿

- 要不要用css-in-js？
  - 优点是方便实现 局部样式、动态样式、theming、type check
  - 缺点是styled组件会带来runtime cost，做性能优化时早晚会干掉
  - 技术选型时，参考知名项目或大公司项目的选择，结论是大公司大多用scss

- css主题方案：加载和重渲染 vs 切换类名和重渲染, 哪个对性能影响更大

- Why it is important to cache DOM
  - http://jsperf.com/dom-caching-excercise

- [微前端的公共依赖是如何解决的?](https://www.zhihu.com/question/419239113)
  - 现在不管什么框架, 都存在一个问题，就是build后摇树, aot等优化操作, 这么一来, 一些公共依赖就不好抽出来了
  - 如果先打出来dll, 然后再搞微前端, 确实也行, 但是没有优化
  - Currently, I mark the module as usedInUnknownWays to prevent tree shaking the exports on exposed moduled/files
    - 这里是折中方案，只摇树去掉无关exports

- bootstrap component vs react component

- 哪些业务计算相关的代码适合放在前端，哪些适合放在服务端
  - 读写文件：文本、图片、文档doc、表格
  - 图表绘

- 将对象的引用保存到dom对象，如pm-editorView保存到dom，是否影响性能

## css更新的方式比较，切换class类名，通过修改style属性来更新css vars的值

- 修改style属性本身可看做修改内联样式
  - inline style不支持伪类、媒体查询，难复用
  - 因为会加大dom体积，增加解析时间和存储空间，所以渲染会慢一点点

- @see: inline style vs className
# inline style vs className
- inline style
  - 使用inline style动态修改样式更方便
  - inline styling does not support pseudos, media queries, keyframes, auto-prefix
- className
  - className is better for debugging
  - 易复用，减少重复
  - 易组织和拆分成多个文件，都放在外部文件方便搜索
- comparison
  - The obvious conclusion must be that changing the className of an element is faster than changing its style (except in Safari)
  - with inline styles, the browser spends more time both scripting and rendering. It spends more time in scripting because it has to map all the styles rules passed in to the component to actual css rules (remember, you have to camelCase all your css rules when using inline css in react). It ends up spending more time rendering because it has to calculate the styles for 10, 000 divs each second.
  - ref
    - https://quirksmode.org/dom/classchange.html
    - https://webkit.org/blog/13/classname-vs-style/
    - https://medium.com/@swazza85/use-css-modules-instead-of-inlining-styles-in-react-fea247b97431

- [External CSS vs inline style performance difference?](https://stackoverflow.com/questions/8284365)
- Using the style attribute, the browser only paints the rule for that particular element, which in this case is the `<div>` element. 
  - This reduces the amount of look up time for the CSS engine to find which elements match the CSS selector (e.g. a.hover or #someContainer li).
- However, putting styling at element level would mean that you cannot cache the CSS style rules separately. 
  - Usually putting styles in CSS files would allow the caching to be done, thus reducing the amount of load from the server each time you load a page.
- Putting style rules at the element level will also make you lose track of what elements are styled what way. 
  - It might also backfire the performance boost of painting a particular element where you can repaint multiple elements together. 
  - Using CSS files separates the CSS from HTML, and thus allows you to make sure that your styles are correct and it's easier to modify later on.

- ### [ReactJS inline styles VS CSS : benchmark _2015](https://www.sderosiaux.com/articles/2015/08/17/react-inline-styles-vs-css-stupid-benchmark/)
- When use one against the other?
  - CSS stylesheets can be better for the layout: such as the bootstrap layout classes: row-fluid, span*. They are fixed and form the static part of the website.
  - The inline styles can be better for the state-styles: the style that can change according to a state. They form the dynamic part of the website.
- I decided to try something stupid and not truly relevant to a real business case:
  - Generate two big `<table>`s: one with inline styles, one with CSS stylesheets. Same content.
  - Check the performance/smoothness/size/time of rendering for both.
  - It’s not relevant because we would not generate a big table in our DOM
  - test at Chrome 45b, React 0.13.3
- Waterfall timeline
  - no difference because small dom
- Size of the DOM
  - DOM size is huge with the inline styles and is linearly proportional to the number of rows.
  - with SSR, the inline styles will be downloaded each and every time (part of the HTML), whereas a CSS stylesheet will be downloaded once. (thanks to the browser’s cache)
- Time to mount the DOM
  - React has done its job converting the virtual DOM into DOM and has injected it into our mounted node
  - It takes twice the time to convert our virtual DOM with inline styles to DOM and mount it.
- Rendering time
  - We assume it will take longer to render the inline styles, because it has more to parse and store every `style` attribute of every `td`.
- Conclusion
  - Inline styles take way more size in the DOM, are converted more slowly from VDOM (have probably a bigger impact on memory), and take more time to be handled by the browser.
  - But they have no impact on performance once it’s rendered.

## 如何将多个传统网站页面集成合并，组成一个portal门户目录，且冲突尽可能少

- 暂时没找到直接的方法，因为原本各网站的文字链接、资源url地址都会变化
- 可考虑重写原网站
- 可参考阿里qiankun微前端解决方案
# 是否要用前端模版引擎
- 根据团队的技术方案
# how to split large html
- 单页拆多页
  - 最简单的方式是通过`<a>`标签跳转
- 使用传统(后端)html模板在编译期合并
  - 如handlebars、ejs、pug
- 使用jsx-like的模板在运行期执行
  - lit-html
- 基于web components的template slot
  - 注意template slot并没有提供插入变量占位符、控制流等方法，需自己实现
- 直接使用js读取和插入html元素
  - `querySelector('s').innerHTML=元素`
  - `$("#includedContent").load("list.html"); `

- ref
  - [Splitting large html file in several files](https://stackoverflow.com/questions/43153049/splitting-large-html-file-in-several-files)
    - HTML Imports 已废弃
  - [How to separate web components to individual files and load them?](https://stackoverflow.com/questions/55080103/how-to-separate-web-components-to-individual-files-and-load-them)
  - [写组件的时候是写好html结构还是在js里拼接好？](https://www.zhihu.com/question/40993912/answers/updated)
  - [Chrome 为何 deprecated HTML Imports？](https://www.zhihu.com/question/310628534)
    - 因为推出了更新的web components标准
# hide dom elements: visibility vs display
- `visibility: hidden` does not cause a reflow on the document, while `display: none` does.
- `display:none` will remove the element from the document's normal flow and set the values for position/height/width to 0 on the element and its children. 
  - When the elements display property is changed to other value than `none` , it triggers a complete document re-flow, which can be a problem for big documents - and sometimes not-so-big documents being rendered on hardware with limited capabilities.
- If you are adding a lot of elements to a DOM, and you add them to the container with `visibility: hidden` , then you'll provoke a reflow for each one. 
  - On the other hand, you can add as many elements as you want with `display:none` and show them all at once provoking a single reflow. 
  - The performance taxing action is the the reflow.
  - 这里描述的是特殊场景，动态添加隐藏的div。
- `visibility: hidden` acts like `opacity: 0` + `pointer-events: none` . 
- `display: none` acts like `Element.remove()` .
- ref
  - [Performance differences between visibility:hidden and display:none](https://stackoverflow.com/questions/11757016/performance-differences-between-visibilityhidden-and-displaynone)
# firefox与chrome滚动条样式不一致，应该如何处理
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
