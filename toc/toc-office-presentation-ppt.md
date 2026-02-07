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
  - 🤔 pdf-editor也需要支持排版与编辑, 优先级比ppt-editor高
  - 技术栈基于svg容易实现缩放，基于dom不容易缩放, ppt需要缩放吗? msoffice和wps均支持zoom

- dev-xp
  - ui组件都可分为state、view2部分，editor框架的核心是通过view更新state
  - ppt可以每页放一个画板或富文本编辑器

- alternatives-ppt
  - 📌 一种思路: 很多ppt的每页是一张图片, 缺点是交互弱、编辑弱、文件大
    - 图片/pdf的优点是跨设备保持排版
    - 改进思路: image > image2html > ppt
    - 改进思路: image > image2html > html-editor
    - ocr方案相对于代码方案的优点，用户能直接拖拽修改文本/图形
    - 🤔 基于代码的编辑如html/markdown的方案，视觉及交互体验都不如图片编辑
  - 📌 一种思路: html > ppt; html > pdf > ppt
    - 💡 新思路: 先隐藏所有文本得到底图，再将文本渲染到底图上，可考虑headless实现
  - 一种思路: html > svg > ppt
  - 一种思路: html > website-editor/builder, 但site编辑器对拖拽不友好
  - 📌 一种思路: markdown/typst > pdf/ppt
  - 一种思路: 预置ppt模版文件 + 自定义内容 > 修改模版而生成ppt
    - 这种纯代码操作的传统方案，创意不够
  - ✨ pdf-editor与ppt-editor的相似点: 支持批注、左侧页面缩略图
    - pdf-editor和ppt-editor都支持缩放，没必要重复开发功能
  - 可参考: svg-editor, pdf-editor, drawio(可插入丰富元素/集成)
    - mxgraph视图层支持svg/html
  - 基于markdown的编辑器方案可参考mermaid
  - 只需ppt的viewer，presentation常是各个系统的核心功能

- resources
  - [List of markdown presentation tools](https://gist.github.com/johnloy/27dd124ad40e210e91c70dd1c24ac8c8)
# popular
- https://github.com/gitbrent/PptxGenJS /4.2kStar/MIT/202506/ts/inactive
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

- reveal.js /69.9kStar/MIT/202510/js/官方editor未开源
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

- https://github.com/mklilley/slidee /MIT/202210/js/inactive
  - Slidee turns a folder of markdown files into Reveal.js presentations.
  - [Slidee: A presentation tool powered by Reveal.js _202209](https://mattlilley.com/posts/slidee/)

- https://github.com/impress/impress.js /38.5kStar/MIT/202509/js/提交少/inactive
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

- https://github.com/netless-io/netless-app /MIT/202312/ts/inactive
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

- https://github.com/shower/shower /4.8kStar/MIT/202411/html/inactive
  - https://shwr.me/
  - Shower HTML presentation engine
  - Built on HTML, CSS and vanilla JavaScript.

- https://github.com/webslides/WebSlides /MIT/201801/js/inactive
  - https://webslides.tv/
  - everything you need to make HTML presentations, landings, and longforms in a beautiful way.
# ppt-editor
- PPTist /6.9kStar/apache2 > AGPLv3/202504/ts/vue/基于DOM
  - https://github.com/pipipi-pikachu/PPTist
  - https://pipipi-pikachu.github.io/PPTist/
  - 一个基于 Web 的在线演示文稿（幻灯片）应用，还原了大部分 Office PowerPoint 常用功能，支持 文字、图片、形状、线条、图表、表格、视频、音频、公式 几种最常用的元素类型
  - 可以在 Web 浏览器中编辑/演示幻灯片
  - 支持导入、导出PPT文件。
  - 依赖vue3、vuedraggable、pptxtojson、pptxgenjs、prosemirror、svg-pathdata、tippy.js、dexie4、animate.css、echarts5
  - 基于 DOM 的渲染方案，优点是简单易上手
  - 📝 每个文本块都是一个prosemirror编辑器
  - 每个幻灯片都支持缩放
  - [ ] 待测试，显示视频/动图， excel导出的图表， smartArt图形
  - 基于 Vue3.x + TypeScript 构建，不依赖UI组件库，尽量避免第三方组件，样式定制更轻松
  - 👾 支持AI生成PPT, AI改写/扩写/缩写
  - [AIPPT的基本原理](https://github.com/pipipi-pikachu/PPTist/blob/master/doc/AIPPT.md)
    - 定义PPT结构（一套PPT中都有什么类型的页面，每种页面都有些什么内容）
    - 示例数据：public/mocks/AIPPT.json
    - 制作模板，模板中标记好结构类型；
    - AI生成符合第1步定义的PPT结构的数据；
    - 利用AI或其他方案，生成相关的配图（常见途径有：AI文生图、图库搜索匹配）；
    - 将AI生成的数据、配图与模板进行匹配结合，生成最终的PPT。
    - 注意：实际上并不存在专门提供给AIPPT的模板。所谓的AIPPT模板只是把在PPTist中制作的普通页面标注上类型标记而已。这些数据不仅仅用于AI生成PPT，也可以作为普通的页面模板使用。
    - 页面标记和节点标记: 封面页、目录页、过渡页、内容页、结束页
  - [feat: 支持移动端/更换开源协议 _202206](https://github.com/pipipi-pikachu/PPTist/commit/704192508247085d327577848691634a925623b8)
    - apache2 > GPLv3
  - [[Feature request] iframe 自适应及点击问题 _202503](https://github.com/pipipi-pikachu/PPTist/issues/334)
    - 本身不支持iframe，那个文档只是用iframe简单举个例子来说明下怎么自定义元素，而不是真的去实现了一个iframe元素，这个元素的具体样式/行为都需要由开发者自己实现。PPTist本身没法预先对未知的自定义元素进行提前适应。
  - [基于fabric + canvas的在线设计 _202305](https://github.com/pipipi-pikachu/PPTist/issues/199)
    - 代码结构，UI设计参考本项目，集合多背景样式，印刷设计元素

- https://github.com/MrXujiang/pptx /201Star/apache2/202503/ts/dom/inactive
  - https://mindlink.turntip.cn/
  - 一款基于web端的ppt在线编辑器
  - Nextjs, @radix-ui, tailwindcss, html2canvas, recharts
  - 自研PPT结构转换算法
  - 多组件支持（图文，形状，表格，可视化图表等）
  - 组件可视化拖拽
  - PPT导出功能(html2canvas)

- react-design-editor /1.7kStar/MIT/202507/ts/canvas
  - https://github.com/salgum1114/react-design-editor
  - https://salgum1114.github.io/react-design-editor/
  - a module for React, written in Javascript/Typescript which provides two primary features: image-editor, bpm-workflow
  - 画布区是canvas，其余地方是dom，直接导出图片或json
  - developed direct manipulation of editable design tools like Powerpoint
  - primarily uses the Ant Design, Fabric.js and React, React-Ace
  - 提供了 image-canvas-editor 和 workflow-editor

- https://github.com/jotform/dnd-builder /57Star/MIT/202511/js
  - https://www.jotform.com/open-source/dnd-builder/
  - accessible drag and drop page builder with React
  - 依赖use-gesture、fuse.js、react-dnd-cjs、react-quill、react-sortable-hoc、react-zoom-pan-pinch、react-window、recharts
  - 🌰 示例丰富，支持preview/print, 典型的ppt布局和交互

- https://github.com/tantaman/strut /1.9kStar/AGPLv3/202312/ts/inactive
  - https://strut.io/
  - An Impress.js and Bespoke.js Presentation Editor
  - 依赖lexical、vlcn、remark.v10、react-draggable
  - The original project is ancient (2011/2013) and dated. It is now coming back with a facelift, collaborative editing

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
# ai-ppt/slides 👾 
- https://github.com/presenton/presenton /1.8kStar/apache2/202508/python/ts
  - Open-Source AI Presentation Generator and API (Gamma, Beautiful AI, Decktopus Alternative)
  - generating presentations with AI — all running locally on your device.
  - using models like OpenAI and Gemini, or use your own hosted models through Ollama.
    - 只支持ollama，不支持lmstudio
  - 基本流程是: text-extract > gen-outlines > template-styling > gen-slides
  - 处理pdf的体验非常慢
  - 🌹 可以并行生成幻灯片, 生成顺序不是按从头到尾
    - 支持拖拽调整幻灯片顺序
    - 支持导出pptx/pdf
  - 🐛 编辑能力特别弱
    - 幻灯片内容不能自由移动文本/图片的位置，也不能改变大小尺寸，只能使用预设排版, 甚至不能删除图片/色块
    - 不支持缩放后显示自适应的分栏布局
    - 不支持编辑现有ppt
  - 端口 nextjs 3000
    - fastapi 8000
    - mcp 8001
  - 👾 
  - i'm running this project locally without nginx, instead of using docker and nginx. 
    - frontend is started by `cd servers/nextjs && npm run dev`.
    - backend is started by `cd servers/fastapi && uv run --env-file .env -- python server.py --port 8000`.
    - i'm using local ollama for llm api
  - custom layouts with HTML and Tailwind, support any presentation design
  - Support for accessing custom templates over API
  - Support external SQL database
  - API Presentation Generation — Host as API to generate presentations over requests
  - Ollama Support — Run open-source models locally with Ollama integration
  - Use any OpenAI-compatible API endpoint with your own models
  - Image Generation — Choose from DALL-E 3, Gemini Flash, Pexels, or Pixabay for your visuals
  - Save as PowerPoint (PPTX) and PDF
  - [We made open source AI presentation generator (Gamma Alternative) : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kn6btt/we_made_open_source_ai_presentation_generator/)
    - We've actually archived electron project for now. We'll only support docker for now. Most wanted in docker format to run on web, and it was hard to maintain both. Hopefully, if we prove useful to many, we will go back to desktop as well.
  - database_url vs container_db_url in servers/fastapi/services/database.py
    - database_url: The main database (which uses your DATABASE_URL from .env): 存储应用的主要业务数据
    - container_db_url: 存储容器内部的临时或特定数据, 硬编码路径 `/app/container.db`

- https://huggingface.co/spaces/barunsaha/slide-deck-ai/tree/main /MIT/202511/python
  - Describe your topic and let SlideDeck AI generate a PowerPoint slide deck for you
  - Given a topic description, it uses a Large Language Model (LLM) to generate the initial content of the slides. The output is generated as structured JSON data based on a pre-defined schema.
    - next, it uses the keywords from the JSON output to search and download a few images with a certain probability.
    - it uses the `python-pptx` library to generate the slides, based on the JSON data from the previous step, from predefined ppt templates
    - may provide additional instructions to refine/modify the content

- https://github.com/allweonedev/presentation-ai /2kStar/MIT/202511/ts/提交少
  - https://presentation.allweone.com/
  - AI Presentation Generator (Gamma Alternative)
  - Editable Outlines: Review and modify AI-generated outlines before finalizing
  - Customizable Slides: Choose the number of slides, language, and page style
  - Choose different AI image generation models for your slides
  - Real-Time Generation: Watch your presentation build live as content is created
  - Full Editability: Modify text, fonts, and design elements as needed
  - Presentation Mode: Present directly from the application
  - Auto-Save: Everything saves automatically as you work
  - Multiple Themes: 9 built-in themes with more coming soon
  - OpenAI API key (for AI generation features)
  - Together AI API key (for Image generation)
  - Google Client ID and Secret for authentication feature

- https://github.com/ComposioHQ/open-gamma /202512/ts
  - A production-ready AI Chat application featuring tool usage (Google Slides, etc.), Vercel AI SDK for chat streaming, and NextAuth v5 for authentication.
  - Tool Integration: Connect with external tools like Google Slides.
  - Database: PostgreSQL with Drizzle ORM.
  - https://x.com/KaranVaidya6/status/2000966735672041772
    - An Open Source Presentation Generator with @composio Tool Router and @aisdk

- https://github.com/sligter/LandPPT /1.7kStar/apache2/202601/python/js
  - https://landppt.pages.dev/
  - 一个基于大语言模型（LLM）的智能演示文稿生成平台，能够自动将文档内容转换为专业的PPT演示文稿
  - 从主题到完整PPT，全程AI自动化处理
  - 🏠 三阶段工作流：需求确认 → 大纲生成 → PPT生成
  - 直观的大纲编辑器和实时预览
  - 侧边栏AI编辑功能，支持实时对话和视觉参考
  - 版本管理：项目历史记录和版本回溯功能
  - 演讲稿生成：支持单页/多页/全部幻灯片的演讲稿生成，导出为DOCX/Markdown格式
  - 智能配图：AI自动匹配最适合的图像，支持多源获取和参考图片生成
    - 多源图像获取：本地图库、网络搜索、AI生成三合一
    - 网络图像搜索：支持 Pixabay、Unsplash 等优质图库
  - AI图像生成： 集成 DALL-E、SiliconFlow、Pollinations 等服务
  - 支持本地部署: OpenAI, Claude, Gemini, Ollama
  - 能处理不同文件：支持 PDF、Word、Markdown 等格式输入
  - 深度研究：集成 Tavily API 和 SearXNG 的多源研究功能
  - 多格式导出：PDF/HTML/PPTX 多种格式导出支持
  - 智能解析：使用 MinerU 和 MarkItDown 进行高质量内容提取
  - 🎨 丰富的模板系统: 统一的HTML模板系统，支持响应式设计
    - 内置简洁的 HTML 模板和布局样式
    - 场景化模板：通用、旅游、教育等多种专业场景模板
  - 用户友好的响应式Web界面
  - [ollama本地连接一直显示错误，服务器500 _202507](https://github.com/sligter/LandPPT/issues/5)
    - ollama测试一直失败，尝试修复了很久也没有成功，最后发现其实可以直接运行。
    - 我也是一直测试失败，跨域调了好久，结果发现配置好了可以直接运行。
  - [【LandPPT】耗时N天开发的开源 AIPPT 生成工具 _202507](https://linux.do/t/topic/767490)

- https://github.com/YOOTeam/OpenPPT /1kStar/GPL/202509/ts/vue/dom/inactive
  - https://www.chatppt.cn/
  - https://open.chatppt.cn/?channel=github-openppt
  - AIPPT在线编辑器，基于ChatPPT，支持整个过程的文档编辑服务，包括导入、导出、布局美化、在线编辑、播放和演示动画。

- https://github.com/icip-cas/PPTAgent /2.3kStar/MIT/202511/python
  - Generating and Evaluating Presentations Beyond Text-to-Slides [EMNLP 2025]
  - We present PPTAgent, an innovative system that automatically generates presentations from documents.
  - PPTAgent follows a two-phase approach: 
    - Analysis Phase: Extracts and learns from patterns in reference presentations
    - Generation Phase: Develops structured outlines and produces visually cohesive slides
  - https://huggingface.co/Forceless/PPTAgent-coder-3B /qwen2/202508

- https://github.com/YOYZHANG/ai-ppt /144Star/MIT/202410/ts/inactive
  - Generated ppt by AI based on RevealJS synax
  - Supabase - User OAuth
  - Gemini API - AI Powered

- https://github.com/veasion/AiPPT /1.4kStar/GPL/202503/js
  - https://veasion.github.io/AiPPT
  - https://www.veasion.cn/AiPPT/
  - AI 智能生成 PPT，通过主题/文件/网址等方式生成PPT，支持原生图表、动画、3D特效等复杂PPT的解析和渲染，支持用户自定义模板，支持智能添加动画
  - PPT 解析成 JSON
  - JSON 反渲染为 PPT
  - 针对上面技术，我们开发了一套可商用 aippt 软件，支持代理 & 私有化部署, 商业合作 & 进群交流

- https://github.com/limaoyi1/Auto-PPT /737Star/MIT/202311/python/提交少/inactive
  - 使用 gpt-3.5-turbo 和 pptx 一站式生成指定主题的PPTX文件
  - 只需输入标题，Auto_PPT将立即为你创造一份全新的PPTX
  - 我们独特地运用 md格式 多步链式地生成PPT文本
  - 在v1.0使用langchain对程序进行优化和重构
  - 与Unsplash合作，提供最精美的插图
  - 支持本地部署，只需添加你的OpenAI API密钥和Unsplash API密钥信息即可
  - https://github.com/otahina/PowerPoint-Generator-Python-Project /202311/inactive

- https://github.com/SlideSpeak/slidespeak-webapp /202308/ts/inactive
  - SlideSpeak allows you to chat with your PowerPoint slides.
  - NextJS, React Chat Stream
  - https://github.com/SlideSpeak/slidespeak-backend /202412/python/flask/inactive
    - Backend for SlideSpeak. Create PowerPoints with AI.
    - 实现简单
    - Llama Index and uses the OpenAI GPT 3.5 Turbo Mobel
    - PineCone as the primary vector storage
    - MongoDB as the Index Store and Document Store
    - AWS S3 as the blob file storage

- https://github.com/hughdazz/PPTCopilot /MIT/202308
  - ppt编辑界面，基于g站上pptist修改而来，该项目ppt的内部表示方式是JSON，这就给我们修改的空间
  - 后端是基于beego框架从0搭建
  - 项目管理界面，基于vue-element-admin修改，不过后期由于我个人的喜好将element换成了腾讯的tdesign库
  - 生成PPT的流程是：
    - 前端接受到一个ppt的主题(topic)，发送到后端
    - 后端请求chatgpt，返回一个xml格式的大纲，这是我们的prompt工程
    - 后端返回大纲到前端，前端进行解析并让用户修改
    - 前端将修改后的PPT发送到后端
    - 后端将xml中的每一页概述发给chatgpt，进行请求，得到有具体内容的xml，这样能突破chatgpt的字数限制，可以生成任意多ppt
    - 数据库中事先存了一些ppt模版，这些ppt模版遵循固定格式，方便进行文本替换，如`{{title}}`之类 进行文本替换，得到完整ppt
    - 代表ppt的JSON返回给前端，直接渲染、展示
  - https://github.com/hughdazz/PPTCopilotBackend /go
  - https://github.com/hughdazz/PPTCopilotEditor /ts/vue

- https://github.com/barun-saha/slide-deck-ai /251Star/MIT/202508/python 
  - https://huggingface.co/spaces/barunsaha/slide-deck-ai
  - Co-create a PowerPoint presentation with Generative AI
  - providers — Azure OpenAI, Google, Cohere, Together AI, and OpenRouter. 
  - Offline LLMs are made available via Ollama. 
  - SlideDeck AI generally recommends the use of Mistral NeMo, Gemini Flash, and GPT-4o to generate the slide decks
  - SlideDeck AI works in the following way:
    - Given a topic description, it uses a  LLM to generate the initial content of the slides. The output is generated as structured JSON data based on a pre-defined schema.
    - Next, it uses the keywords from the JSON output to search and download a few images
    - Subsequently, it uses the `python-pptx` library to generate the slides, based on the JSON data
    - Every time SlideDeck AI generates a PowerPoint presentation, a download button is provided.

- https://github.com/SmartSchoolAI/ai-to-pptx /1.2kStar/GPL/202503/ts
  - https://pptx.dandian.net/
  - 一个使用AI技术(DeepSeek)制作PPTX的助手，支持在线生成、修改和导出PPTX
  - 使用DeepSeek等大语言模型来生成大纲 
  - 生成PPTX的时候可以选择不同的模板 
  - 支持导出PPTX
  - 支持在线修改PPTX的文字内容，样式，图片等(商业版功能)
  - 支持用户设计自己的模板上传到共享平台, 分享给其它人使用(商业版功能)
  - https://github.com/SmartSchoolAI/ai-to-pptx-backend /php

- https://github.com/qrpcode/letsPPT /202309/java/php/inactive
  - AI自动生成PPT文档的Java应用，一个标题生成PPT模板。
  - 生成系统（Java）
  - 生成后人工审核系统（Java）
  - C端前端页面（PHP，原生html，自适应）
  - 登录端小程序（原生微信小程序）
  - 因为POI对2010版本PPT特性支持太差，我直接写了个Java原生生成PPT的jar工具包，开源了
  - https://github.com/qrpcode/pptshow /apache2/202306/java/inactive
    - Java生成PPT文档，支持2010版PPTX新特性
  - https://github.com/qrpcode/wordgo /apache2/202306/java/inactive
    - 传统的Java生成word通常需要先手动创建模板文件，之后导入。如果不希望创建模板，还想少些点代码，选Word GO是个好主意

- https://github.com/lesteroliver911/ai-pdf-ppt-generator-openai /MIT/202410/python/inactive
  - a Flask-based application that generates presentations from documents

- https://github.com/Anionex/banana-slides /8.7kStar/MIT > CC-NC/202512/python/ts
  - http://bananaslides.online/
  - 🌰 [【持续更新】使用案例 | Use Cases _202512](https://github.com/Anionex/banana-slides/issues/2)
  - 基于nano banana pro🍌的原生AI PPT生成应用，支持想法/大纲/页面描述生成完整PPT演示文稿，自动提取附件图表、上传任意素材、口头提出修改，迈向真正的"Vibe PPT"
  - 已支持openai格式的模型调用（文本，生图），可以切换第三方的中转
  - 多格式支持：上传 PDF/Docx/MD/Txt 等文件，后台自动解析内容。
  - 支持上传参考图片或模板，定制 PPT 风格。
  - "Vibe" 式自然语言修改: 对不满意的区域进行口头式修改
  - 一键导出标准 PPTX 或 PDF 文件。
  - ✨ 可自由编辑的pptx导出（Beta迭代中）: 导出图像为高还原度、背景干净的、可自由编辑图像和文字的PPT页面
  - Flask, SQLite + Flask-SQLAlchemy, python-pptx, Pillow, ThreadPoolExecutor
  - React Router v6, Zustand, @dnd-kit
  - https://github.com/Anionex/banana-slides/tree/main/backend
  - 用于抽象不同的inpaint方法，支持接入多种实现：
    - 基于InpaintingService的实现（当前默认）
    - Gemini API实现
    - SD/SDXL等其他模型实现
    - 基于火山引擎的 Inpainting 服务
  - [license - MIT to CC-NC _20251213](https://github.com/Anionex/banana-slides/commit/304848490722f263e66b8884285975f797a7e3c3)
  - [【v0.3.0版本更新】更好的可编辑pptx效果及其他若干改进 _20260105](https://github.com/Anionex/banana-slides/issues/121)
    - 现在，可编辑pptx导出可以分离带样式文字、插画、配图，并得到干净的背景，所有文字和图像都应该是可编辑的pptx元素
    - 在百度智能云平台中获取API KEY，填写在.env文件中的BAIDU_OCR_API_KEY字段（有较多免费额度）, 需要的百度云服务包含1. 高精度文字识别 2. 图像修复
    - hybrid 模式优势： MinerU 负责识别元素类型和整体布局, 百度 OCR 负责精确的文字识别和定位, 文字位置更准确，识别率更高
    - 文字样式提取（颜色、粗体等）依赖 AI 视觉模型（Caption Model）
    - 为什么有些文字的颜色识别不准确？ A: 对于低对比度、渐变色、特殊字体的文字，AI 识别准确率可能下降，这是已知限制。
    - 表格识别依赖百度 OCR，对于合并单元格、嵌套表格、手绘表格等复杂结构，识别效果有限。
    - 可编辑 PPTX 导出需要多步 AI 处理（版面分析→背景修复→样式提取），通常需要 1-5 分钟。可通过减少页数加快速度。
    - 可以只导出部分页面吗？ A: 可以，在导出时选择需要的页面即可。
    - 只配置了 MinerU 为什么不行？ A: MinerU 只负责版面分析（识别元素位置），背景修复和样式提取还需要 AI API Key 和/或百度 API Key。
    - 图片可以在导出的 PPT 中编辑吗？ A: 可以。版面分析会识别出图片元素，并将其作为独立的可编辑图片嵌入 PPTX，用户可以移动、缩放、替换这些图片。
  - 目前还在进行应该是最困难的一步的开发，就是从纯图的图片中分割出可编辑的元素，目前想到的技术方案是用类似SAM（segment anything ） + Inpaint这样的东西来实现，或者佬们有什么好方案也可以分享
    - 能否先:banana:出整页之后丢回视觉LLM（或者SAM之类的）解析文字元素和图片元素，然后让:banana:进一步出一个纯背景再把各个图片和文字扣出来放上去
    - 目前在做的大概就是佬的想法，不过我想的是除了背景，把分割元素也让:banana:做了 :bili_040:（直接让:banana:生成前景），然后用一个连通性判断+cv把元素提出来；文本框的话再用类似mineru的layout yolo模型来定位
  - [【已开源】一个基于banana pro的一站式PPT生成应用, 告别排版美化烦恼 _202512](https://linux.do/t/topic/1285413)
    - 如果是可编辑功能，我也做了一个ocr识别文本位置GitHub - Tansuo2021/OCRPDF-TO-PPT 但是需要干净的背景图，还需要在生成一次，然后我觉得生成干净的背景图可以直接用本地 IOPaint来去除图片中的文字得到干净背景图，目前思路是这样，今天还想到可以直接在原图裁切图案叠加过去
  - [增加本地llm 本地图片生成模型支持 _202512](https://github.com/Anionex/banana-slides/issues/57)
    - 效果很差，还是不要本地了，改了代码用的qwen image实现的效果，如下
  - [大香蕉直出PPT底图和文字 ](https://linux.do/t/topic/1523689)

- https://github.com/JuniverseCoder/MinerU2PPT /202602/python
  - [[开源] 手搓了个小工具，解决 NotebookLM 生成的 PPT 没法编辑的问题 _202602](https://linux.do/t/topic/1576291)
    - 有两个痛点实在忍不了：
    - 格式是 PDF：完全不可编辑，想改个字都不行。
    - 字体问题：生成中文内容时，字体经常很奇怪，看着难受。
    - 解决思路 最近正好发现 MinerU 这个项目，它解析 PDF 的时候不仅能识别元素，还带上了精确的坐标信息。 于是我就参考它的解析结果，写了这个 MinerU2PPT。
      - 可以理解为，是按照 MinerU 画出的图片和框，先填上一层背景，再加上一层图片，最后加上一层文本，个人觉得这块的话，对于后续进行调整，会比较友好一点。
      - 当然这个方案也有问题，就是加粗不好还原，还有就是如果通过颜色进行切字不准的话，有可能出现个别字体颜色不对，还有如果 MinerU 没识别出的文字也无法处理了。
    - 非 OCR 方案：为了保持效率和排版，我没用 OCR。
    - 样式还原：字体颜色和大小是根据背景颜色自动推断的。
    - 效果：实测下来准确率还行，能满足我绝大部分需求（对于背景特别混乱或者复杂混排的场景，可能处理得还不够完美）。
    - 初衷是为了解决 NotebookLM 的痛点，但理论上别的 PDF 也能转

- https://github.com/HisMax/RedInk /4.4kStar/CC-BY-NC/202512/python/ts/vue
  - https://redink.top/
  - 一句话一张图片生成小红书图文
  - 依赖 Flask、Nano banana Pro、pinia
  - 可编辑每页内容
  - 可调整页面顺序（不建议）
  - 自定义每页描述（强烈推荐）
  - 支持并发生成所有页面（默认最多 15 张）, 如 API 不支持高并发，请在设置中关闭
  - 支持单独重新生成不满意的页面
  - [文本模型可以配置国内的，但是文生图模型可以支持国内的吗 _202512](https://github.com/HisMax/RedInk/issues/38)
    - 目前文生图模型暂不支持国内 API，后续会支持豆包 seeddream 4.5。 请关注项目更新。
  - [【开源】红墨 RedInk - 基于 大香蕉 🍌Nano Banana Pro 的一站式小红书图文生成器 _202511](https://linux.do/t/topic/1217947)
  - [生图的api调用使用起来很困难 _202512](https://github.com/HisMax/RedInk/issues/32)
    - 配置了国内外的各种模型的api key无一成功，大佬能不能添加一些更亲民的指南和避坑说明？
    - 👷: 有些中转站可能缩水了。其实我也是想做很多适配的，但是我发现大部分中转站对于新出来的nanobanana的这个格式支持的不是很好，文档也不是很全。主要是文档不全，而且怎么处理的都有。
    - 花了2天时间捣鼓，只有tuziapi的原价模型成功了，其他都失败了，关键是原价贵啊，一次烧掉20刀，有点可怕。用他们默认的分组，怎么都不成功
    - 专门开了GEMINI 付费API才跑通，其他国内API都不行。
    - 实际验证了下：gemini-2.5-flash 和 gemini-3-pro-image-preview 分别作为文本和图片的模型是 ok 的
    - gemini的key只能用于生图。作者用了两个不同的库导致的。
    - 我试了下豆包的没问题啊 这个就是调用个api的事情啊
    - 我调用七牛的api来生图, 只有封面能成功, 后面的图都会报这个错
    - 我也是七牛，绘图阶段只能首页成功，其他都失败。

- https://github.com/MoonWeSif/NextCreator /196Star/AGPL/202512/ts/tauri
  - 基于可视化节点的 AI 内容生成工作流工具，支持 文本/图片/视频/PPT 链式创作。
  - 基于workflow画布定义步骤，再生成ppt页面图片
  - 可编辑模式 - 去除文字仅保留背景，方便后期编辑
  - 如需使用 PPT 可编辑导出功能（去除文字仅保留背景），需要 OCR 和 Inpaint 服务。可以自行 Docker 部署（推荐）
  - [【开源】画布式 AI 工作流创作平台，基于 NanoBananaPro 创作可编辑文字的 PPT _202512](https://linux.do/t/topic/1304016)
    - 基于NanoBanana Pro的PPT制作是其中一股比较热门的方向。 前段时间尝试手动AI生成大纲——PPT图片模板——图片拼接，一系列流程下来。做了一些介绍文献的 PPT 感觉效果着实不错，于是着手将其实现为一个工作流平台，方便大家也是方便自己。
    - 开始着手后，想到不能编辑图片
    - 直接参考OCRPDF-TO-PPT思路，将这一套逻辑内嵌到代码里面，加上这几天完善了一下（全靠Vibe Coding），终于发布了初版
    - 基于 Tauri 构建的应用，支持网页端与桌面端(推荐，因为图片占用存储空间大，本地性能更优)。
    - 但是项目最后针对于可编辑 PPT 的实现还是有所局限的，经过测试，发现如果字体有样式与排版规则的话，那么借助佬友的实现思路实现下来，将文字重新嵌入到 PPT 中会有排版布局样式问题。
    - 因此项目最终实现了将生成的 PPT 中的文字全部移除掉，仅保留背景部分（效果见下方图片），文字部分各位下载 PPT 后，自行文本框添加即可，这部分对人来说应该是比较简单的工作，对照着原 PPT 添加文本框即可，但想要借助程序实现下来的话，目前还没有实现思路。
    - 同时编辑 PPT 时，个人来说大部分情景下也是文字部分有修改的需要，背景和排版部分保留，因此对于我来说目前项目是可用的程度了
    - AI 图片生成 - 支持文生图、图生图，可配置分辨率和比例
    - PPT 工作流 - 自动生成大纲、页面图片，导出 PPTX
- https://github.com/shrimbly/node-banana /481Star/MIT/202601/ts
  - node-based workflow application for generating images with NBP. Build image generation pipelines by connecting nodes on a visual canvas. Built mainly with Opus 4.5.
  - 类似comfyui for nano-banana
  - AI Image Generation - Generate images using Google Gemini models
  - Image Annotation - Full-screen editor with drawing tools (rectangles, circles, arrows, freehand, text)
  - Node Editor: @xyflow/react (React Flow)
  - Canvas: Konva.js / react-konva

- https://github.com/yyy-OPS/slidedeconstruct-ai /113Star/MIT/202512/ts
  - 基于 AI 视觉能力的智能演示文稿反向工程工具。它利用 Google Gemini (或 OpenAI Compatible) 模型，将一张静态的 PPT 截图“拆解”为可编辑的图层（背景、文字、视觉元素），并支持将其转化为矢量形状，最终导出为可编辑的 .pptx 源文件。
  - 图片拆解：自动移除图片中的文字（保留背景），并提取视觉元素。
  - 矢量化重构：尝试将图像中的视觉元素转化为 PPT 原生的矢量形状（如矩形、圆形、箭头等），而非简单的图片贴图。
  - 支持批量上传 PDF、PNG、JPG 格式的幻灯片（PPT/PPTX 建议先导出为 PDF）。
  - 使用 AI 视觉模型精确识别页面中的文本块、视觉元素和背景颜色。
  - 🤔 智能背景修复: 也可用于pdf ocr的场景，能使文档视觉整洁
    - 自动去字：在提取文本后，AI 会自动“擦除”原图上的文字，并根据周围纹理修复背景，生成干净的底图。
    - 手动擦除：提供“橡皮擦”模式，用户可手动框选区域让 AI 移除多余元素。
    - 背景
  - 矢量化转换 (Beta)：尝试将识别到的简单几何图形（矩形、圆形、箭头等）转换为 PPT 原生形状，而非仅仅粘贴图片。
  - 一键导出 PPT：将拆解后的所有元素（文本、背景、图片、形状）按原位置重组，导出为可编辑的 .pptx 文件
  - AI Integration: Google GenAI SDK (@google/genai), OpenAI API Compatible
  - File Handling: pptxgenjs (PPT生成), pdfjs-dist (PDF解析)
  - [开源了一个 PPT“逆向”工具，图片直接转可编辑 PPT _202512](https://linux.do/t/topic/1368469)
    - 代码都是AI写的！我也不咋能看懂，慢慢学习嘛

- https://github.com/JaffryGao/notebooklmfix /202601/ts
  - https://notebooklmfix.vercel.app/
  - 一款专为修复 NotebookLM 生成的 PDF 文档、图片（如信息图等）而设计的智能工具。它利用最新一代 Nano Banana Pro 多模态模型，解决文档中常见的文字模糊、伪影和分辨率过低问题，实现像素级的画质重塑，并支持导出为高清晰度的 PDF 或 PPTX 演示文稿。
  - 基于 Nano Banana Pro 模型，智能识别并重绘文档内容，非单纯滤镜增强
  - 👀 文字精准还原: 修复文字边缘锯齿与模糊，同时保持原有排版布局不变（注：仅修复画质，不篡改内容）。
  - 支持导出高清 PDF 和 PPTX（PPTX 内也是图片）。

- https://github.com/cat3399/ezppt /202511/python/js/inactive
  - 开源的大模型生成PPTX方案, 包含完整前后端, 支持图片搜索, 支持自定义参考内容, 支持自定义模型服务商, 支持自定义场景
  - 页面生成：调用大模型生成HTML代码。
  - 图片能力（可选） 通过 SearXNG 聚合搜索图片。
  - 自定义参考资料：支持自定义参考资料，用于生成内容，减少模型自身知识的幻觉。
  - 在线预览编辑 可在浏览器中实时预览与编辑。
  - 导出 PDF 或 PPTX 导出的 PPTX 文件可保持 HTML 预览 90% 的效果，并且内容可二次编辑。
  - 怎么把HTML转换为 PPTX 格式的？能做到什么程度的还原度呢
    - html–(playwright)–pdf–(apryse_sdk)–pptx
    - 还原程度的话,动态效果肯定还原不了,其余的例如光晕,渐变,阴影等都还原不了
    - 主要瓶颈在pdf2pptx, html2pdf基本上是无损的
    - 可以的，自己读 cdp 然后 openxml 绘制就行。
  - [【开源自荐】EZPPT 一键生成可导出 PDF/PPTX 的AI PPT项目 _202511](https://linux.do/t/topic/1123898)
    - 我觉得效果挺一般的,做不到一键出成品的效果,这也是目前ai ppt项目的通病吧,效果都不大行
    - 我这个项目的优势就是导出的PPT文件和HTML预览效果基本一样(代价是美观度的降低),并且可以自由编辑
  - [目前html转PPT还是一个天大的难题吗？ ](https://linux.do/t/topic/1114556/18)
    - 目前基本上可以用了，转换逻辑在src/html…那里，对于普通的排版还是可以保留90％样式的，复杂的就不行，我在提示词里面限制了很多“高级css效果”，那些都是无法转换的 genspark，质谱应该都是这个方案，因为pdf转pptx有些bug都是通的，例如阴影和超出范围还有转换后的字体

- https://github.com/uniqueww/unique-ppt /202601/js
  - AI 驱动的图文并茂 PPT 生成器 — 输入主题或文本，AI 自动生成大纲，并为每一页智能生成匹配内容的精美配图。
  - [unique-ppt ｜AI一键搞定高质量的图文并貌的PPT _202601](https://linux.do/t/topic/1487758)
    - 做 PPT 最头疼的就是找配图，花一小时写完内容，再花两小时找图、抠图、调版式。
    - AI 自动生成结构化大纲
    - 根据每页内容自动生成匹配的 AI 图片, 不是随机配图，是真正理解内容后生成的匹配图片
      - 每页内容 → 英文提示词 → AI 生成匹配图片
    - 标准 PPTX，兼容 Office 和 Keynote
    - 导出的是真实文本框，并非 SVG 或图片
    - 并发生成	5 张图同时生成，速度提升 3-5 倍

- https://github.com/hugohe3/ppt-master /913Star/MIT/202512/python
  - https://hugohe3.github.io/ppt-master/
  - 基于 AI 的智能视觉内容生成系统，通过多角色协作，将源文档转化为高质量的 SVG 内容，支持演示文稿、社交媒体、营销海报等多种格式。
  - 多格式画布支持（PPT 16:9/4:3、小红书、朋友圈、Story 等 10+ 格式）
  - 使用设计工具（如 Figma、Adobe Illustrator）编辑
  - 网页感太明显
  - 每个页面都是 `<object>` 元素包裹的 svg, 可单独打开，类似 https://hugohe3.github.io/ppt-master/examples/demo_project_intro_ppt169_20251211/svg_final/slide_02_pain_points.svg
  - PPT 不认 rgba、不认组透明、不认图片透明
  - [PPT-master 一个用AI生成真正可编辑的高质量PPT的工具 _202512](https://linux.do/t/topic/1305492)
    - 使用 mineru 对 pdf 进行了提取，然后用 md 文档重新生成一份含有企业预警通图标和封面图的 ppt，因为时间更空余，生成的比视频里面的更精美多了

- https://github.com/vigorX777/ppt-svg-generator /MIT/202601/js
  - https://mp.weixin.qq.com/s/0KhNkuoFkT9zq9I9COVnSg
  - 一个 Skill，帮助你将 Markdown 文稿快速转化PPT 或 PDF，并支持多种预设风格选择，效果美观且可控
  - [【原创】OpenCode + SVG：推荐一套省心可控的 AI PPT 生成方案 _202601](https://linux.do/t/topic/1489177)
  - [小小优化，“ppt-svg-generator” Skill 支持一键导出 PPTX 和 PDF 格式了 ](https://linux.do/t/topic/1522619)

- https://github.com/laihenyi/NBLM2PPTX /MIT/202601/ts
  - Convert NotebookLM PDFs to PPTX with separated background images and editable text layers using Gemini AI
  - AI Text Removal: Uses Gemini 2.5 Flash to automatically remove text from images and reconstruct backgrounds
  - Hybrid Text Extraction: PDF sources use native PDF.js extraction for precise coordinates; image sources use enhanced Gemini OCR
  - Separated Layers: Exported PPTX contains background images and text as independent layers for easy editing
  - Batch Processing: Supports processing multiple PDF pages or images at once
  - Page Selection: Freely select which pages to process, saving time and API quota

- https://github.com/elliottzheng/NotebookLM2PPT /MIT/202601/python
  - https://elliottzheng.github.io/NotebookLM2PPT/
  - 一款强大的自动化工具，旨在将不可编辑的 PDF 文档（特别是 NotebookLM 生成的演示文稿）转换为完全可编辑的 PowerPoint 演示文稿。
  - 全自动化：利用微软电脑管家"智能圈选"，自动完成截图、识别、转换和合并。
  - MinerU 深度优化：(可选) 集成 MinerU 解析能力，智能重排文本、统一字体、替换高清图片
  - 智能去水印：内置针对 NotebookLM 的智能水印去除算法。
  - 批量处理：(v0.7.0) 支持任务队列，可批量添加多个 PDF 及其 MinerU JSON 进行自动化顺序处理。
  - 系统要求: Windows 10/11, Microsoft PowerPoint 或 WPS Office (v0.6.5+ 支持), 微软电脑管家 (版本 ≥ 3.17.50.0，必须开启"智能圈选")

- https://github.com/blacksamuraiiii/pdf2ppt /MIT/202601/python
  - 将 AI 生成的 PDF 文稿（如 Google NotebookLM 导出的内容）或其他标准 PDF 文档，通过智能解析转换为可编辑的 PowerPoint (PPTX) 演示文稿。
  - 提供 基于 CustomTkinter 的现代化界面 (app.py) 和 cli
  - 每个元素都带有精确的边界框坐标 [x1, y1, x2, y2]
  - 支持中英文混排识别
  - Area-based 字号算法: 根据 bbox 面积和字符密度自动计算最佳字号
  - Layout.json 多源解析: 同时利用 layout.json 和 content_list.json，提取 image_caption 的精确 bbox
  - [基于MinerU的pdf转ppt工具（更新v0.3，加入去水印） _202601](https://linux.do/t/topic/1490727)
    - 基于MinerU强大的解析能力，将文字、图片、表格按照位置进行解析重组，字体大小根据Area-based放缩，让Antigravity改了几稿，做了一个简单的GUI页面
    - 加了一个去右下角水印的选项

- https://github.com/YiYoYiYoYiYo-Web3/PDF-Text-Remover /AGPL/202512/python
  - [一个没啥用的PDF去文字工具 ](https://linux.do/t/topic/1257896)
  - 用AI搓了个把PDF文字去除的工具 
  - 主要思路是把PDF分页后用大香蕉:banana: 重新生成一个一样但是无文字的图片，然后再拼成PPT/PDF，后续自己把文字拼上去。
  - 后来想加入文字识别，用了tesseract + AI 合并文字块 + 坐标映射，但是有伪文字不太好识别，基本上搞出来的文字最后都得重新编辑==。实在没办法了，丢上来看哪位大佬有兴趣的话解决一下 
  - [一个没啥用的PDF去文字工具  ](https://linux.do/t/topic/1257896)

- [ChatSlide | Build your Slides and Videos from Documents in one click](https://chatslide.ai/landing)
# ai-canvas
- https://github.com/open-webui/open-webui /104kStar/BSD+LOGO/python/ts/svelte
  - https://openwebui.com/
  - Open WebUI is an extensible, feature-rich, and user-friendly self-hosted AI platform designed to operate entirely offline. 
  - It supports various LLM runners like Ollama and OpenAI-compatible APIs, with built-in inference engine for RAG, making it a powerful AI deployment solution.
  - Install seamlessly using Docker or Kubernetes (kubectl, kustomize or helm) 
  - Ollama/OpenAI API Integration
  - Granular Permissions and User Groups
  - Full Markdown and LaTeX Support
  - Hands-Free Voice/Video Call
  - Local RAG Integration
  - Web Browsing Capability
  - Pipelines, Open WebUI Plugin Support
  - Image Generation Integration: Seamlessly incorporate image generation capabilities using options such as AUTOMATIC1111 API or ComfyUI (local), and OpenAI's DALL-E (external)
  - https://github.com/open-webui/pipelines /2kStar/MIT/202507/python
    - Pipelines: UI-Agnostic OpenAI API Plugin Framework
    - Pipelines bring modular, customizable workflows to any UI client supporting OpenAI API specs 
    - Pipelines comes into play when you're dealing with computationally heavy tasks (e.g., running large models or complex logic) that you want to offload from your main Open WebUI instance for better performance and scalability.
    - Pipelines are a plugin system with arbitrary code execution — don't fetch random pipelines from sources you don't trust.

- https://github.com/langchain-ai/open-canvas /4.8kStar/MIT/202505/ts/inactive
  - https://opencanvas.langchain.com/
  - A better UX for chat, writing content, and coding with LLMs.
  - Open Canvas is an open source web application for collaborating with agents to better write documents. 
  - It is inspired by OpenAI's "Canvas"
  - Open Source: All the code, from the frontend, to the content generation agent, to the reflection agent is open source and MIT licensed.
  - Built in memory: Open Canvas ships out of the box with a reflection agent which stores style rules and user insights in a shared memory store. 
  - allowing you to start the session with your existing content, instead of being forced to start with a chat interaction.
  - ⏳ Artifact versioning: All artifacts have a "version" tied to them, allowing you to travel back in time and see previous versions of your artifact.

- https://github.com/CopilotKit/open-multi-agent-canvas /202504/python/ts/inactive
  - https://open-multi-agent-canvas.vercel.app/
  - The open-source multi-agent chat interface that lets you manage multiple agents in one dynamic conversation and add MCP servers for deep research
  - built with Next.js, LangGraph, and CopilotKit to help with travel planning, research, and general-purpose tasks through MCP servers.
  - Check out these awesome agents (they live in separate repositories). You can run them separately or deploy them on LangSmith
  - [Open Multi-Agent Canvas + MCP Demo : r/mcp _202504](https://www.reddit.com/r/mcp/comments/1k0py22/open_multiagent_canvas_mcp_demo/)
    - Chat with multiple LangGraph agents and any MCP server inside a canvas app.
    - Chat interface - CopilotKit
    - Multi AI Agents - LangGraph
    - MCP Servers - Composio
    - CopilotKit seems to be fairly tightly coupled to LangGraph AFAIK. If I wanted to use Mastra instead, is that fairly easy?
      - Yes we have a tight integration with LangGraph but also CewAI, and soon Mastra + others
# more
- https://github.com/sozi-projects/Sozi /1.7kStar/MPL/202411/js/inactive
  - http://sozi.baierouge.fr/
  - a presentation tool for SVG documents
  - 支持win/linux/mac

- https://github.com/nimeshnayaju/tlslides /202204/ts/inactive
  - Create slides using tldraw (Unmaintained)
