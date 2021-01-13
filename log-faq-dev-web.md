---
title: log-faq-dev-web
tags: [faq, web]
created: '2020-11-07T12:26:28.591Z'
modified: '2020-12-23T09:54:10.963Z'
---

# log-faq-dev-web

# faq-not-yet

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

- 前后端一体化方案

- bootstrap component vs react component

- 哪些业务计算相关的代码适合放在前端，哪些适合放在服务端
  - 读写文件：文本、图片、文档doc、表格
  - 图表绘

## 如何将多个传统网站页面集成合并，组成一个portal门户目录，且冲突尽可能少

- 暂时没找到直接的方法，因为原本各网站的文字链接、资源url地址都会变化
- 可考虑重新开发

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
  - `$("#includedContent").load("list.html");`

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
