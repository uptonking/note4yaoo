---
title: note-fwk-web-lib
tags: [framework, web]
created: 2021-01-13T07:57:30.313Z
modified: 2021-01-13T07:57:54.308Z
---

# note-fwk-web-lib

# guide

- frontend-framework
  - view: snabbdom, ultradom
  - state: eventemitter, elm, flux, redux, mobx
  - effect/fetch: swr
  - router: express-router, nanostore-router
  - ssr: nanojsx

- tips
  - 产品开发前进行技术选型时要多分析使用场景，ssr和csr的技术栈本身就是不同的，jsx只是view层，服务端要考虑routing/cache/streaming/i18n
  - 一般ssr方案都会提供自己的router, nextjs将file-based-routing作为卖点
  - 没必要寻找前后端通用的router，前端、后端框架都有自己的，routing常和prefetch耦合
  - 有的方案支持首屏ssr，之后spa，基于不同的render mode

- features
  - code-split, dynamic-import
  - react的替代框架，考虑 nanostore+logux
# fwk

## [Qwik, a new framework from the authors of angular.js and Ionic](https://vived.io/qwik-a-new-framework-from-the-authors-of-angular-js-and-ionic-frontend-weekly-vol-106/)

## [如何看待由react router原班人马打造并获得三百万美元融资的ts全栈开发框架remix框架?](https://www.zhihu.com/question/502743886)

- 如果remix框架仅仅是解决了语言的问题是远远不够的，它需要提供类似springcloud的完整解决方案，否则很可能类似现在的BFF模式，不是很有价值。
  - 未来当然是好的，但是我们也应该看到，后端的技术栈并不仅仅是语言，它包含了许多的知识体系，比如SQL优化、微服务架构、RPC、限流、熔断降级、负载、读写分离、高并发等等。

- 看过router源码的都知道其实现没什么难度。。。用的还是react提供的api.
  - 这就像写了一个github很多人用的组件，比如通用switch按钮，tab之类的，说拿到融资然后要实现一个js框架。。。。你只会觉得unbelievable，至于期待什么的，我倒是挺好奇他们的技术水平能实现到什么程度
# stimulus
- stimulus /10kStar/MIT/202101/ts
  - https://github.com/hotwired/stimulus
  - https://stimulus.hotwire.dev/
  - A modest JavaScript framework for the HTML you already have
  - it's designed to augment your HTML with just enough behavior to make it shine.

- ## [前端框架Stimulus的使用体验如何？](https://www.zhihu.com/question/266673543/answers/updated)
- 它是为了配合HTML页面，为传统（大量HTML，SEO，重写代价极大）项目提供动态交互支持。
- Stimulus是完全依靠HTML5的MutationObserver和实体DOM，而非Vue/React经过编译的DOM。
  - 同时Stimulus中并不存在vdom，并不会进行UI渲染。
- 这是Ruby社区给多页面应用设计的框架。
  - 别再拿单页面框架跟 Stimulus 做对比了，适用的场景是不同滴。
# discuss-web-fwk
- ## 

- ## 

- ## 

- ## 🎯⌛️ [Four Eras of JavaScript Frameworks | Hacker News _202204](https://news.ycombinator.com/item?id=31176910)
- Four eras of practice:
  1. DHTML scripts: individual scripts that provided functionality e.g. a date picker. You grabbed the scripts, and wired them together on your pages to enhance your page. Includes the first generation of Ajax scripts (in page communication with the server, often using raw HTML, text, or XML). Hidden iframes and other techniques also used for server communications.
  2. jQuery: the popular library that everyone used because it provided a fabulous API to access and modify the DOM, plus helper methods to abstract out browser differences and bug workarounds. Bringing Ajax to all web developers, allowing them to enhance the pages delivered by their backend web server of choice (PHP, RoR, etcetera).
  3. component framework (Cambrian explosion): mostly enhance pages delivered by the server, each framework with a unique approach to its API. Pages use components designed for each framework. YUI, Dojo, jQuery UI, Mootools, ExtJS. Starting to see more Single Page Apps, but no widespread usage of any framework on large numbers of sites.
  4. React (and other 2nd gen frameworks, mostly virtual DOM): fully component based, can easily deliver an SPA (Single Page Application) and often the server only really delivers JSON (no HTML pages except a blank container). Widespread usage of React in industry.

- the author is too young to have accurate memories of what web development was like pre-2010.
  - The primary difference between GWT/Closure and what we've got now is that JavaScript was treated as a compilation target, not a developer platform.
  - The tooling was all in Java or C++, there was no concept of writing a transpiler or bundler in JavaScript and no culture of standalone JS interpreters. 
  - IIRC the only option at the time for running JS on the server was Rhino (based on Netscape/Mozilla), which for whatever reason never saw the broad adoption of Node.

- ExtJS, Ember, Angular, and Next are all "full-stack" frameworks and the all were released at very different times.
  - Direct manipilation with custom architecture and models (JQuery) -> MVC/P (Ember/ExtJS/Angular) -> Components (React/Vue).

- the next generation: "compiler-frameworks"(or "UI compilers").
  - The real revolution is in what these next-generation frameworks like Svelte or SolidJS offer: small bundles combined with high performance achieved through eschewing virtual DOM in favour of precise changes in the DOM.

- Yep. SSR has been around for ages. The very first "web frameworks" were pure SSR. And by that I'm referring to PHP and the old CGI!
  - The big leap forward from Solidjs and Svelte is that they do complex source-to-source compilation to avoid virtual dom diffing. That approach lets them get the best of both worlds - the programmer can pretend their components are pure & reactive. (Solidjs looks almost identical to react.) Thats great because it means there's no bugs due to fiddly or forgotten DOM updating.

- The one lesson of the past 2 decades that I’ve taken: do not adopt a JS framework for your production env. until it reaches industry-wide acceptance.
