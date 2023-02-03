---
title: toc-lib-editor-text-popular
tags: [editor, text-editor, toc]
created: 2022-11-08T19:03:42.961Z
modified: 2022-11-08T19:04:00.289Z
---

# toc-lib-editor-text-popular

# guide

- 开源编辑器
  - 国内: wangEditor, vditor, textbus, am-editor/editablejs, ueditor
  - 国外: prosemirror, slate, quill, lexical, tinymce, etherpad, ckeditor

- ref
  - https://github.com/JefMari/awesome-wysiwyg
  - https://github.com/xjh22222228/awesome-web-editor
# known-text-editor
- prosemirror /6kStar/MIT/202208/ts
  - https://github.com/ProseMirror/prosemirror
  - http://prosemirror.net/
  - rich semantic content editor based on contentEditable, with support for collaborative editing and custom document schemas.
  - ProseMirror library consists of a number of separate modules.

- lexical /12.1kStar/MIT/202211/ts
  - https://github.com/facebook/lexical
  - https://lexical.dev/
  - editor framework with an emphasis on reliability, accessibility, and performance.

- slate /25.8kStar/MIT/202211/ts
  - https://github.com/ianstormtaylor/slate
  - https://docs.slatejs.org/general/changelog
  - a completely customizable framework for building rich text editors.
  - since v0.50.0(201911), slate codebase has had a complete overhaul(彻底检修)
    - The data model is now comprised of simple JSON objects.(old: Immutable.js data structures)
    - Plugins are now plain functions that augment the Editor object they receive and return it again.
    - The codebase now uses TypeScript.

- etherpad-lite /13.5kStar/Apache2/202211/js
  - https://github.com/ether/etherpad-lite
  - https://etherpad.org/
  - Etherpad is a real-time collaborative editor scalable to thousands of simultaneous real time users. 
  - It provides full data export capabilities, and runs on your server, under your control.

- textbus /648Star/GPL.v3/202208/ts
  - https://github.com/tbhuabi/textbus
  - https://textbus.io/collab
  - 依赖prismjs、~~rxjs~~、reflect-metadata、@tanbo/di、@tanbo/stream、@tanbo/color、katex
  - 依赖自研 @tanbo/stream，最基础的数据流类，每一次订阅产生一个新的数据流。
  - 基于数据驱动的富文本编辑器
  - 为什么我还要另起炉灶呢？
    - 目前大多数富文本内容都太脏了，比如，加粗一段文字，可能是一个 strong 标签，也有可能是多个，如果这段文字同时还有其它格式，那么就更热闹了
    - 较新的编辑器，基本都有自己的一套抽象数据结构来描述富文本，这同时又引起了另一个问题，即这一数据结构对有的富文本内容描述不了，导致要扩展特定的格式不能实现。
    - 部分富文本编辑器依赖特定的框架或库，造成使用上的限制
    - 实时的代码高亮，这个对程序员写文档来说，比较重要
    - 对于粘贴进来的内容，要么粗爆的只是提取文本内容，导致格式丢失。要么就直接扔进页面，产生非常多的脏数据（如粘贴 word 的内容）
  - TextBus 解决如下
    - 输出非常干净，没有冗余的标签及样式。
    - 没有定义一个标准的数据结构，只抽象出了 Formatter（格式） 和 Component（组件）两个维度的数据来格式化富文本的 Content（内容）
    - 不依赖特定的库
    - 实时代码高亮
    - 由于TextBus的架构设计天然的支持过滤脏内容，所以，当粘贴进 TextBus 不认识的数据时，会自动忽略掉
    - 粘贴进来的资源上传，目前正在开发中
  - Textbus 2.0 已经到来
    - 重新设计了数据模型，可根据用户的操作生成特定的底层原子命令，这让细粒度的历史记录和文档协同成为可能
    - 重写了渲染层，现在 Textbus 2.0 大多数情况下更新视图仅需要 0.2ms 时间，比 1.0 性能更好
    - 核心架构脱离了具体平台，让 Textbus 的能力不仅限于在 PC 端，通过编写特定的中间层，可以方便的在移动端，甚至小程序上实现丰富的富文本能力
    - 重新设计了组件系统，去掉了大家难以理解的装饰器，改为用类似 vue 的 setup 形式开发组件

- editablejs-editable /17Star/MIT/202208/ts/只依赖slate不依赖slate-react/自绘光标
  - https://github.com/editablejs/editable
  - https://docs.editablejs.com/playground
  - 一个实验性的富文本编辑器框架，希望通过自绘光标来替代原生 contenteditable 属性，提供更丰富、稳定的编辑能力。
  - 使用slatejs数据模型，借助 react 使用自绘光标的模式渲染，不再依赖 contenteditable 属性
  - 主要对一些 unicode 字符进行索引的计算。因为有些字符占位所占的字节数不确定，造成某些字符拆分后的索引不准确，所以需要这个工具包来解决这个问题。
- am-editor /541Star/MIT/202209/ts/maintenance
  - https://github.com/red-axe/am-editor
  - https://editor.aomao.com/zh-CN
  - 富文本实时协同编辑器框架，可以使用React和Vue自定义插件。
  - 协同编辑基于ShareDB实现。
  - 过去两年中，am-editor 编辑器基于 contenteditable 属性上做了很多功能和扩展，也遇到了很多问题。
    - 所以，现在大胆一些，尝试抛弃contenteditable属性，使用自绘光标的模式开发的下一个版本的富文本编辑器。

- taleweaver(织书) /71Star/MIT/202007/ts
  - https://github.com/yuzhenmi/taleweaver
  - https://yuzhenmi.github.io/taleweaver/
  - Web word processor for 2Tale Writer's Portal.
  - feature
    - 基于dom实现，且支持显示分页
  - core无依赖，react封装很少(只有2个文件)，不依赖prosemirror
  - 大量使用es6 class
  - 自己实现了依赖注入，设计了model/service/component

- tinymce /12kStar/MIT/202209/ts
  - https://github.com/tinymce/tinymce
  - https://www.tiny.cloud/
  - web-based WYSIWYG editor. Available for React, Vue and Angular

- quill /34kStar/BSD/202211/ts
  - https://github.com/quilljs/quill
  - https://quilljs.com/
  - Quill is a modern rich text editor built for compatibility and extensibility.
# open-editors
- canvas-editor /112Star/MIT/202301/ts/几乎无依赖
  - https://github.com/Hufe921/canvas-editor
  - https://hufe.club/canvas-editor/
  - rich text editor by canvas/svg
  - The render layer by svg is under development, see feature/svg
  - The export pdf feature is available now, see feature/pdf

- roosterjs /655Star/MIT/202211/ts/测试覆盖率高
  - https://github.com/microsoft/roosterjs
  - https://microsoft.github.io/roosterjs/index.html
  - Rooster is a framework-independent JavaScript rich-text editor neatly nested inside one HTML `<div>` element.
  - Rooster provides DOM level APIs (in roosterjs-editor-dom), core APIs (in roosterjs-editor-core), and formatting APIs (in roosterjs-editor-api) to perform editing operations.
  - It is used by outlook.com, and some other projects.
  - https://github.com/JiuqingSong/contentModel

- ace-editor /25kStar/BSD/202211/js
  - https://github.com/ajaxorg/ace
  - https://ace.c9.io/
  - Ace is a standalone code editor written in JavaScript. 
  - 支持virtual_renderer
  - Our goal is to create a browser based editor that matches and extends the features, usability and performance of existing native editors such as TextMate, Vim or Eclipse
  - Ace is developed as the primary editor for Cloud9 IDE
    - AWS Cloud9: A cloud IDE for writing, running, and debugging code

- overleaf /10.5kStar/AGPLv3/202211/js/latex
  - https://github.com/overleaf/overleaf
  - https://github.com/overleaf/overleaf/wiki
  - A web-based collaborative LaTeX editor
  - 编辑器依赖ace
  - https://github.com/overleaf/ace

- trix /17kStar/MIT/202211/js
  - https://github.com/basecamp/trix
  - https://trix-editor.org/
  - Trix is a WYSIWYG editor for writing messages, comments, articles, and lists

- firepad /3.7kStar/MIT/202010/js
  - https://github.com/FirebaseExtended/firepad
  - Collaborative Text Editor Powered by Firebase
  - Firepad requires Firebase in order to sync and store data. 
  - rich text editing with CodeMirror5 and code editing via Ace-c9.

- SunEditor /1kStar/MIT/202210/js/核心代码不多
  - https://github.com/JiHong88/SunEditor
  - http://suneditor.com/sample/index.html
  - Pure javscript based WYSIWYG web editor, with no dependencies

- mobiledoc-kit /1.5kStar/MIT/202209/ts
  - https://github.com/bustle/mobiledoc-kit
  - https://bustle.github.io/mobiledoc-kit/demo/
  - Mobiledoc Kit is a framework-agnostic library for building WYSIWYG editors supporting rich content via cards.
  - Posts are serialized to a JSON format called Mobiledoc instead of to HTML.
  - Mobiledoc is a deliberately simple and terse format, and you are encouraged to write your own renderer if you have other target output formats (e.g., a PDF renderer, an iOS Native Views Renderer, etc.).

- edtr-io /696Star/MIT/202206/ts
  - https://github.com/edtr-io/edtr-io
  - https://edtr.io/
  - a WYSIWYG in-line web editor written in React.
  - 支持拖拽block修改顺序
  - 不支持跨block选择部分文字
  - 示例样式友好
  - 依赖redux、react-dnd

- summernote /10.9kStar/MIT/202209/js
  - https://github.com/summernote/summernote
  - https://summernote.org/
  - core的代码不多
  - 依赖jquery
  - Summernote is a JavaScript library that helps you create WYSIWYG editors online.
  - Saves images directly in the content of the field using base64 encoding, so you don't need to implement image handling at all

- wiz-editor /237Star/MIT/202207/ts/为知笔记/似乎未开源
  - https://github.com/WizTeam/wiz-editor
  - https://github.com/live-editor/live-editor
  - 支持多人实时协同编辑的网页富文本编辑
  - [以 MIT 协议开源，不怕竞品直接拿走吗？](https://github.com/WizTeam/wiz-editor/issues/5)
    - 目前并未完全开源，只是将打包后的代码通过npm发布。开源的部分是编辑器的使用例子。
  - [项目会开源么？](https://github.com/WizTeam/wiz-editor/issues/15)
    - 目前没有计划开源

- https://github.com/margox/braft-editor /archived
  - 美观易用的React富文本编辑器，基于draft-js开发

- lvce-editor /4Star/MIT/202211/js
  - https://github.com/lvce-editor/lvce-editor
  - VS Code inspired text editor that mostly runs in a webworker

- https://github.com/esdmr/rte
  - https://esdmr.github.io/rte/
  - Just a Regular Text Editor… with support for gamepads.
  - 类似代码编辑器

- https://github.com/proj-Aura/AURA
  - Aura is a modern Multi-platform text editor with Full-customization.
  - we used Tauri as a solution. Also, we use Rust for the server, so the server can be more fast and safe.

- jodit /1.3kStar/MIT/202301/ts/NoDeps
  - https://github.com/xdan/jodit
  - https://xdsoft.net/jodit/
  - https://xdsoft.net/jodit/pro/
  - An excellent WYSIWYG editor written in pure TypeScript without the use of additional libraries. 
  - Its file editor and image editor.
  - free版插件很少

- substance /2.7kStar/MIT/202011/js/inactive
  - https://github.com/substance/substance
  - JavaScript library for web-based content editing
