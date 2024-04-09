---
title: toc-saas-ide-js-online
tags: [ide, repos, saas, toc]
created: 2020-08-09T11:22:45.003Z
modified: 2021-05-14T15:03:38.010Z
---

# toc-saas-ide-js-online

# discuss

- ## 请问 StackBlitz 和 CodeSandBox 这类 Web IDE 的技术栈是如何实现的？
- https://www.zhihu.com/question/279268026/answers/updated
- 我想提供一个思路：利用 es module + service worker + browser file system + 浏览器端即时编译实现不依赖服务端能力的 Web IDE.
  - 类似于 CodeSandBox 的方案是在浏览器端实现了一套兼容于 webpack 的打包系统，这主要是为了解决前端构建过程中对模块系统的依赖。
  - 而目前市面上所有主流浏览器（排除掉 IE）都已经很好的支持了 es module，我们其实可以充分的利用这个技术点来替代 webpack（即 bundless 构建）。
  - 在浏览器加载 es module 的过程中会不断的发出 http 请求去获取被依赖的 es module，对于不依赖服务端能力的 Web IDE，我们需要补全这部分本该由静态资源服务器提供的能力。
  - 所以，可以拦截请求并定制响应的 service worker 正好可以提供这个能力。
  - 我们需要将所有的代码资源存储在浏览器端，也就是说需要实现一套 browser file system。
- es module发出的http请求，是以scripts脚本加载的形式。而service worker只能拦截fetch。
  - service worker 中监听 fetch 事件当然是可以拦截脚本的请求的，不信你可以试试
  - 包括esm加载时的请求都可以被拦截
# code-live
- https://github.com/cdr/code-server /MIT/202401/ts
  - https://coder.com/
  - Run VS Code on any machine anywhere and access it in the browser
  - Use cloud servers to speed up tests, compilations, downloads, and more
  - Requirements: Linux machine with WebSockets enabled, 1 GB RAM, and 2 vCPUs
  - https://github.com/coder/coder /AGPLv3
    - Provision remote development environments via Terraform

## CodePen

- https://codepen.io/
- CodePen is a social development environment. 
- It comes fully equipped with all the features you'll need to build, test, share, collaborate and even deploy your websites.

- open source alternatives

- https://github.com/chinchang/web-maker
  - https://webmaker.app/
  - an offline playground for your web experiments. 
  - Something like CodePen or JSFiddle, but much more faster and offline supported because it runs completely on your system.

- https://github.com/konnorrogers/light-pen /MIT/202311/js
  - https://konnorrogers.github.io/light-pen/
  - A lightweight codepen implementation using web components
  - 依赖lit、prismjs、web-component-define

- https://github.com/lostintangent/codeswing
  - an interactive coding playground for VS Code
  - It's like having the magic of a traditional web playground (e.g. CodePen, JSFiddle), but available directly from your highly-personalized editor

- https://github.com/chr15m/slingcode /MIT/202008/clojure/inactive
  - https://slingcode.net/
  - Slingcode is a personal computing platform in a single html file.
  - You don't need a server, hosting, or an SSL certificate to run the web apps.
  - You can share apps peer-to-peer over WebTorrent.

## CodeSandbox

- http://codesandbox.io/
- CodeSandbox is an online editor that allows developers to focus on writing code while it handles all the necessary background processes and configurations. 
- Unlike CodePen, CodeSandbox focuses more on building and sharing code demos that contain back-end components. 
- The editor is optimized to analyze npm dependencies, show custom error messages, and also make projects searchable by npm dependency.
- It is worthy to note that CodeSandbox is one of the few online playgrounds that has support for back-end languages like Node.js. 
  - It has npm support. 
  - As a result of it, you can install any npm package you require in seconds.

- [CodeSandbox - 从入门到实现原理解析](https://www.yuque.com/wangxiangzhong/aob8up)

## StackBlitz

- https://stackblitz.com/
- StackBlitz is a VSCode powered online playground for web developers. 
- Thanks to StackBlitz in-browser development server, you can continue writing code and editing your work even when offline. 
  - This gives you the superpower to build offline while leveraging the power of the online platform

## JSFiddle

- https://jsfiddle.net/
- It is one of the earliest playgrounds that laid the foundation for the creation of other modern-day playgrounds. 
- At the moment, it may seem a bit basic compared to modern playgrounds like CodePen

## JSBin

- https://jsbin.com/
- JSBin is a live playground for Html, CSS and JavaScript and a range of other preprocessors like jade, markdown and much more.
- JSBin is mostly focused on the ability to share code.

## Liveweaver

- https://liveweave.com/
- Like other editors we've come across, Liveweaver gives users the ability to create, test, and share code with colleagues.

## Scrimba

- https://scrimba.com/
- It offers you the ability to pause the video and edit the instructor's code and see the result in the editor.
- In-video interaction
  - Scrimba lets you take up an instructors demo and build it up into whatever use case you desire. 
  - In the playground mode, you can interact with the instructor's code however you please, 
  - and you can edit, copy, paste and basically perform any interactive operation you desire.
# code-live-cn
- [RunJS - 前端开发者在线代码编辑器](https://runjs.work/)
  - 轻松复制任意网站的html/css代码，并在RunJS中预览。
  - RunJS Editor - 在线代码编辑器
  - 在线创建、运行和分享HTML/JS/CSS代码。
  - 支持React/Vue/Angular/Svelte等流行框架。
  - [RunJS帮助文档](https://runjs.work/projects/dcc55687f7dc46bd)

- [MipCode - 快速的在线代码创作工具](http://www.mipcode.com/)

- [笔. COOL - 在线编辑/实时预览你的 HTML/CSS/JS 代码](https://bi.cool/)

- https://play.fe-dev.cn/
# ide-online
- https://github.com/adarshaacharya/CodeTreats /MIT/202110/ts
  - In-browser IDE for running, collaborating, saving and sharing code snippets
# more-online-code-editor
- https://github.com/agneym/playground
  - https://blog.agney.dev/introducing-playground/
  - playground for HTML, CSS and JavaScript supporting module imports.
# ref
- [7 JavaScript Playgrounds to Use in 2019 ― Scotch.io](https://scotch.io/tutorials/7-javascript-playgrounds-to-use-in-2019)
