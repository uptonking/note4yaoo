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
  - 可参考: svg-editor, pdf-editor, drawio(可插入丰富元素/集成)
    - mxgraph视图层支持svg/html
  - 基于markdown的编辑器方案可参考mermaid

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
# ai-ppt/slides
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

- https://github.com/sligter/LandPPT /1.5kStar/apache2/202511/python
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
  - 深度研究：集成 Tavily API 和 SearXNG 的多源研究功能
  - 多格式导出：PDF/HTML/PPTX 多种格式导出支持
  - 智能解析：使用 MinerU 和 MarkItDown 进行高质量内容提取
  - 🎨 丰富的模板系统: 统一的HTML模板系统，支持响应式设计
    - 场景化模板：通用、旅游、教育等多种专业场景模板
  - 用户友好的响应式Web界面
  - [ollama本地连接一直显示错误，服务器500 _202507](https://github.com/sligter/LandPPT/issues/5)
    - ollama测试一直失败，尝试修复了很久也没有成功，最后发现其实可以直接运行。
    - 我也是一直测试失败，跨域调了好久，结果发现配置好了可以直接运行。

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
