---
title: toc-office-presentation-ppt
tags: [office, ppt, presentation, toc]
created: 2020-08-02T08:42:18.196Z
modified: 2021-04-30T20:14:17.669Z
---

# toc-office-presentation-ppt

# guide
- tips
  - 商业化的演示更偏向类似tableau的图形编辑器，而不是文字
  - 侧重信息的ppt上更多的是文字数字，而不是花里胡哨的图形，此时pdf比ppt更合适，很多pdf由ppt转换得到
  - 技术栈基于svg容易实现缩放，基于dom不容易缩放, ppt需要缩放吗

- dev-xp
  - ui组件都可分为state、view2部分，editor框架的核心是通过view更新state
  - ppt可以每页放一个画板或富文本编辑器

- alternatives-ppt
  - 很多ppt的每页是一张图片
  - 只需ppt的viewer，presentation常是各个系统的核心功能
  - ✨ pdf-editor与ppt-editor的相似点: 支持批注、左侧页面缩略图
  - 可参考: svg-editor, pdf-editor, drawio
# popular
- https://github.com/gitbrent/PptxGenJS /3.3kStar/MIT/202305/ts/inactive
  - https://gitbrent.github.io/PptxGenJS/
  - Create PowerPoint presentations with a powerful, concise JavaScript API.
  - This library creates Open Office XML (OOXML) Presentations which are compatible with Microsoft PowerPoint, Apple Keynote, and other applications.
  - Integrates with Node, Angular, React, and Electron
  - All major object types are available (charts, shapes, tables, etc.)
  - SVG images, animated gifs, YouTube videos, RTL text, and Asian fonts
  - PowerPoint shape definitions and some XML code via Officegen Project
  - Includes powerful HTML-to-PowerPoint feature to transform HTML tables into presentations with a single line of code
  - 🚧 [Unimplemented Features](https://github.com/gitbrent/PptxGenJS/wiki/Unimplemented-Features)
    - Animations, Importing Existing ppt, SmartArt, Outlines
  - [Is it possible to read and update a PPTX file using PpptxGenJS? _202206](https://github.com/gitbrent/PptxGenJS/discussions/1120)
    - This library only generates new presentations. Reading existing presentations is an existing item on the Unimplemented Features
  - [Rendering of PPTX on screen _202303](https://github.com/gitbrent/PptxGenJS/issues/1230)
    - You're basically reproducing the functionality of M365 online (turning PPTX and/or code into HTML) while this library produces XML documents.
  - [WYSIWYG Editor or Playground _201706](https://github.com/gitbrent/PptxGenJS/issues/109)
    - Since the PptxGenJS library produces XML, I don't see how to easily translate that to HTML and then keep a canvas or div element populated. That's basically what the PowerPoint Online engine does.
  - https://github.com/wyozi/react-pptx
    - https://wyozi.github.io/react-pptx/
    - React wrapper for PptxGenJS. Works both in browser and node

- reveal.js /66.4kStar/MIT/202503/js/官方editor未开源
  - https://github.com/hakimel/reveal.js
  - https://revealjs.com/
  - 🌓 open source HTML presentation framework. It enables anyone with a web browser to create beautiful presentations for free.
  - broad range of features including nested slides, Markdown support, Auto-Animate, PDF export, speaker notes, LaTeX support and syntax highlighted code.
  - [Question: Is the online editor available in the source?](https://github.com/hakimel/reveal.js/issues/971)
    - the slides.com editor isn't open source
  - [Export reveal.js presentation to .odp or .ppt presentation _201609](https://github.com/hakimel/reveal.js/issues/1702)
    - Currently there isn't such a way, as Reveal.js presentations are just webpages, and they would be difficult to convert to specific proprietary `.ppt/.odp` slides. 
    - PDF printing is currently the easiest way to export presentations.
    - 💡 The best way is to write the presentation in Markdown and then process it with Pandoc into both reveal.js and PowerPoint, as well as other formats.
    - Pandoc can also convert from PowerPoint to Markdown, but the result is normally not usable without a lot of touching up.
- https://github.com/slate-mx/realtime-presentation /202305/js/inactive
  - Minor ui improvements

- https://github.com/piatra/kreator.js /apache2/201604/js/inactive
  - https://piatra.github.io/kreator.js
  - slide tool interface for reveal.js
  - Create web presentations in the browsers
  - 依赖quill

- https://gitlab.com/ruby232/slideme /GPLv3/201611/js
  - open source clone of site slides.com. 
  - The goal of this project is supplied the GUI open source for reveal.js and create one offline editor in the future, using Electron
  - 依赖Rails、wkhtmltoimage

- https://github.com/boardit/boardit /202211/ts/代码少
  - easy to use editor to create stunning presentations using reveal.js

- https://github.com/moonslide-app/moonslide /MIT/202306/ts
  - Moonslide is based on the presentation framework Reveal.js. 
  - write your presentation in Markdown and Moonslide automatically generates a Reveal.js HTML presentation. 
  - Write your presentation directly in the code editor

- https://github.com/marlic7/reveal.js-online /MIT/202103/js
  - simple app that combines Ace Editor and RevealJS. 
  - You can write markdown on the left, and preview your presentation on the right.
- https://github.com/fbedussi/reveal-js-editor /MIT/201805/js
  - A cross platform editor (build upon the electron framework) to author reveal.js presentation in markdown
- https://github.com/patarapolw/reveal-md /201912/ts/vue
  - View markdown files as a presentation in Reveal.js with CLI

- https://github.com/impress/impress.js /37.5kStar/MIT/202404/js/inactive
  - http://impress.js.org/
  - http://impress.github.io/impress.js/examples/classic-slides/
  - 🌓 a presentation framework based on the power of CSS3 transforms and transitions in modern browsers and inspired by the idea behind prezi.com
  - The HTML source code of the official impress.js demo serves as a good example usage and contains comments explaining various features of impress.js
  - [Examples and demos · impress/impress.js Wiki](https://github.com/impress/impress.js/wiki/Examples-and-demos)
  - [Authoring tool discussion](https://github.com/impress/impress.js/issues/5)
  - [Import PPT/PDF to impress.js _201712](https://github.com/impress/impress.js/issues/648)
    - powerpoints nowadays are XML files and the file format is openly documented. So in theory it would be straightforward to write a converter that takes a pptx file and outputs an impress.js HTML presentation. In reality it's bound to be a lot of work.

- https://github.com/henrikingo/impressionist /MIT/202005/js/inactive
  - A Visual 3D editor for creating stunning impress.js presentations
  - a prototype and concept to build a visual (wysiwyg) editor for creating impress.js presentations. 
  - use Electron to make the browser based impress.js presentation into a proper desktop app that can open and save files. TinyMCE is integrated to provide the editing capability.

- https://github.com/abbr/ShowPreper /MIT/201912/js
  - https://abbr.github.io/ShowPreper/
  - WYSIWYG editor for Impress.js and Bespoke.js
  - Strut for inspiration. In many ways ShowPreper can be considered as a re-write of Strut.
  - Impress.js and Bespoke.js for rendering.

- https://github.com/gossip-ink/gossip /MIT/202105/js
  - https://gossip.ink/
  - an online user interface to efficiently author presentations
  - 依赖antd.v3、dva、d3-scale
  - 交互不是ppt的设计，以idea为开始建立一个树形大纲
  - 不能修改背景色
  - 无法拖拽调整布局宽高、大小

- https://github.com/hiroppy/fusuma /MIT/202112/js/inactive
  - https://hiroppy.github.io/fusuma
  - Fusuma makes slides with Markdown easily.
  - Markdown and MDX
  - core依赖mdx、webpack.v5、express
  - client依赖react-modal、prismjs、swiper、screenfull、react-burger-menu、react-event-timeline
  - 支持导出pdf
  - https://github.com/nolimits4web/swiper
    - https://swiperjs.com/
    - Most modern mobile touch slider with hardware accelerated transitions

- https://github.com/netless-io/netless-app /MIT/202312/ts
  - https://netless-io.github.io/netless-app
  - Official Apps for the Agora Interactive Whiteboard.
  - https://github.com/netless-io/flat /MIT/202401/ts
    - https://flat.whiteboard.agora.io/
    - Project flat is the Web, Windows and macOS client of Agora Flat open source classroom.
  - https://github.com/netless-io/flat-server
    - Node.js server for the Agora Flat open source classroom.

- https://github.com/ChurchApps/FreeShow /GPLv3/202402/ts/svelte
  - https://freeshow.app/
  - free software with a user-friendly interface that offers powerful features for creating and editing slideshows. 
  - 依赖pptx2json、slideshow、sqlite、@sveltejs/svelte-virtual-list

- https://github.com/shikijs/shiki-magic-move /MIT/202405/ts
  - https://shiki-magic-move.netlify.app/
  - Smoothly animated code blocks with Shiki.
  - The package provides framework-agnostic core and renderer and framework wrappers for Vue and React.
  - 依赖diff-match-patch-es、ohash
  - [The Magic in Shiki Magic Move _202403](https://antfu.me/posts/shiki-magic-move)
# ppt-editor
- PPTist /6.9kStar/apache2 > AGPLv3/202504/ts/vue/基于DOM
  - https://github.com/pipipi-pikachu/PPTist
  - https://pipipi-pikachu.github.io/PPTist/
  - 基于 Vue3.x + TypeScript 的在线演示文稿（幻灯片）应用，还原了大部分 Office PowerPoint 常用功能，
  - 实现在线PPT的编辑、演示。
  - 支持导入、导出PPT文件。
  - 依赖vue3、vuedraggable、pptxtojson、pptxgenjs、prosemirror、svg-pathdata、tippy.js、dexie4、animate.css、echarts5
  - 基于 DOM 的渲染方案，优点是简单易上手
  - 📝 每个文本块都是一个prosemirror编辑器
  - 每个幻灯片都支持缩放
  - [ ] 待测试，显示视频/动图， excel导出的图表， smartArt图形
  - [feat: 支持移动端/更换开源协议 _202206](https://github.com/pipipi-pikachu/PPTist/commit/704192508247085d327577848691634a925623b8)
    - apache2 > GPLv3

- https://github.com/jotform/dnd-builder /43Star/MIT/202402/js
  - https://www.jotform.com/open-source/dnd-builder/
  - accessible drag and drop page builder with React
  - 依赖use-gesture、fuse.js、react-dnd-cjs、react-quill、react-sortable-hoc、react-zoom-pan-pinch、react-window、recharts
  - 示例丰富，支持preview/ppt/print

- https://github.com/tantaman/strut /AGPLv3/202312/ts
  - https://strut.io/
  - An Impress.js and Bespoke.js Presentation Editor
  - 依赖lexical、vlcn、remark.v10、react-draggable
  - The original project is ancient (2011/2013) and dated. It is now coming back with a facelift, collaborative editing

- react-design-editor /1.4kStar/MIT/202401/ts
  - https://github.com/salgum1114/react-design-editor
  - https://salgum1114.github.io/react-design-editor/
  - a module for React, written in Javascript/Typescript which provides two primary features: image-editor, bpm-workflow
  - 画布区是canvas，其余地方是dom，直接导出图片或json
  - developed direct manipulation of editable design tools like Powerpoint
  - primarily uses the Ant Design, Fabric.js and React, React-Ace

- deckdeckgo /1kStar/AGPLv3+MIT/202301/ts/web-comp/stencil/inactive
  - https://github.com/deckgo/deckdeckgo
  - https://deckdeckgo.com/
  - The web open source editor for presentations
  - 基于stencil和web components
  - Search Unsplash and Tenor GIFs
  - Integrate easily Youtube video
  - The platform and its applications are licensed under the AGPL v3 (or later) licence. 
    - Several separate components are licensed under MIT licence.

- https://github.com/plotly/spectacle-editor /MIT/201906/js
  - Drag and drop Spectacle editor.
  - An Electron based app for creating, editing, saving, and publishing Spectacle presentations. 
  - With integrated Plotly support.
# ppt-viewer 偏向页面展示
- viewer
  - [zettlr slides.md](https://zettlr.com/slides.revealjs.htm)

- slidev /4.8kStar/MIT/202105/ts/vue
  - https://github.com/slidevjs/slidev
  - https://sli.dev/
  - Presentation Slides for Developers
  - Markdown-based
  - Developer Friendly - built-in syntax highlighting, live coding, etc.
  - themeable
  - Integrated editor, or extension for VS Code
- spectacle /8.6kStar/MIT/202006
  - https://github.com/FormidableLabs/spectacle
  - https://formidable.com/open-source/spectacle/docs/tutorial/
  - ReactJS based Presentation Library
  - 依赖history、marksy、prism-react-renderer、react-spring、styled-comp
- https://github.com/cpojer/remdx /ts
  - Create beautiful minimalist presentations with React & MDX.
  - The core of ReMDX is a lean fork of Spectacle. 
  - create-remdx is based on Slidev. 
  - Slidev is modern but only works with Vue instead of React. 
  - I wanted to build a fast MDX-based slide deck tool on top of Vite that uses React and only supports a minimal set of features.
- marpit /MIT/287Star/22009
  - https://github.com/marp-team/marpit
  - https://marpit.marp.app/
  - framework for creating slide deck from Markdown
  - https://github.com/marp-team/marp
    - entrance repository of Markdown presentation ecosystem
    - https://github.com/marp-team/marp-core
- nodeppt /MIT/8.9kStar/202006
  - https://github.com/ksky521/nodeppt
  - https://nodeppt.js.org/
  - probably the best web presentation tool 
  - built with webslides, markdown-it, posthtml

- impress.js 
  - https://github.com/impress/impress.js
  - https://impress.js.org/#/bored
  - a presentation framework based on the power of CSS3 transforms and transitions in modern browsers 
  - inspired by the idea behind prezi.com
- scrollreveal
  - https://github.com/scrollreveal/scrollreveal
  - https://scrollrevealjs.org/
  - Animate elements as they scroll into view.

- https://github.com/Simonwep/presentr
  - https://simonwep.github.io/presentr/
  - Minimalistic javascript presentation-library. 
  - Zero dependencies. 
  - Can be used in combination with frameworks like Bootstrap, Materialize, Vue etc.
# markdown-slide-utils
- https://github.com/googleworkspace/md2googleslides /apache2/202107/ts
  - Generate Google Slides from markdown & HTML
  - This project was developed as an example of how to use the Slides API.

- https://github.com/gnab/remark /MIT/202306/js
  - http://remarkjs.com/
  - A simple, in-browser, markdown-driven slideshow tool 

- https://github.com/decker-edu/decker /GPLv3/202311/js/haskell/inactive
  - A markdown based tool for slide deck creation
  - reveal.js MathJax and Font-Awesome dependencies are tracked via submodules
# examples

# utils

- https://github.com/argyleink/slyd /js/darkTheme/代码少
  - https://slyd.netlify.com/
  - Snappy, responsive, touch optimized, bi-directional presentation framework
  - 支持向右、向下

- https://github.com/davidguttman/power-slides /js
  - Create powerful slideshows for talks and presentations. 
  - Each "slide" is a JS function that can do *anything*.
  - Let you jump to any slide by number in the url hash

- https://github.com/rse/slideshow /MPLv2/202309/appleScript
  - Slideshow is a Node/JavaScript Application Programming Interface (API) and Command Line Interface (CLI) for observing and controlling the slideshow presentation applications Microsoft PowerPoint 2010+ for Windows, Microsoft PowerPoint 2011+ for Mac OS X and Apple KeyNote 5+ for Mac OS X. 
  - It is implemented as a thin Node/JavaScript API layer on top of platform-specific Windows WSH/JScript and Mac OS X Automator AppleScript/JavaScript connectors. No native code is required.
  - 🍴 forks
  - https://github.com/vassbo/slideshow
# ai-slides
- [ChatSlide | Build your Slides and Videos from Documents in one click](https://chatslide.ai/landing)
# more
- https://github.com/nimeshnayaju/tlslides /202204/ts/inactive
  - Create slides using tldraw (Unmaintained)
