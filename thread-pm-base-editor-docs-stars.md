---
title: thread-pm-base-editor-docs-stars
tags: [documentation, editor, pm, thread]
created: 2021-08-22T07:28:43.964Z
modified: 2021-08-22T07:29:34.045Z
---

# thread-pm-base-editor-docs-stars

# guide

# discuss-docs-ai 👾
- ## 

- ## 

- ## 

- ## @LandingAI 指出 GPT-5.4、Gemini 和 Opus 等主流 LLM 在文档处理时的问题：视觉定位/可追溯定位能力弱。
- https://x.com/shao__meng/status/2037097008087839005
  - 它们能提取文档中的数值或信息，却无法指出该数值在原始页面上的确切位置（bounding box、页码、坐标等）。一旦要求“把你提取的这个值在原文档里标出来”，模型就搞不定了。
  - 视觉 grounding 的定义与价值： 指将提取结果与源文档的空间位置严格绑定，提供“证据链”。 这是合规、审计、受监管行业（金融、法律、医疗、财报等）的硬性要求。合规团队需核验数据来源，财务团队需审计每笔数字出处，任何文档自动化流程都依赖可追溯性。
  - LLM 的根本局限： 它们把文档“压扁”成 token 序列，只保留文本语义，丢失了页面布局、空间关系和视觉结构。因此提取结果本质上是“黑箱”，无法提供位置证明。
  - ADE 的差异化优势： 采用 Agentic Document Extraction 技术，每一条提取结果都原生携带精确空间坐标（bounding boxes、页码、位置信息）。表格、文本块、表单字段全部实现视觉 grounding，使整个提取过程可审计、可验证、可追溯。
  - [Agentic Document Extraction: API-first Agentic Document Intelligence platform built for accuracy, reliability, and governance at scale. - LandingAI](https://landing.ai/)
  - https://landing.ai/ade

- ## llamaindex: We built LobsterX, an @openclaw specialized for document work on your computer.
- https://x.com/jerryjliu0/status/2021021110721265979
  - It uses high-accuracy document parsing, extraction, classification through LlamaCloud, meaning it can comb through complicated PDFs (with scans, tables, diagrams) and extract out 100% accurate context!
  - It can run as a Telegram bot and is built on top of agentfs ( @tursodatabase ) as a file system.
- https://github.com/AstraBert/workflows-acp/tree/main/packages/lobsterx
  - agent inspired by OpenClaw (formerly known as MoltBot or ClawdBot), which focuses on document-related tasks.

- General-purpose agents are impressive demos. Specialized agents with domain-tuned tools are production systems.
  - When you constrain the problem space, you can optimize for accuracy instead of flexibility.
  - This is the pattern.

- Doc agents win when extraction comes with provenance. If every field links back to the exact page/bbox plus a tight exception queue, “100% accurate” stops being marketing and becomes something reviewers can clear fast.

- Document parsing is the unsexy unlock. Most enterprise data lives in PDFs nobody wants to read. Whoever structures it first wins.

- ## 原来做文档的 Craft 团队出的 Craft Agent 也太牛逼了！
- https://x.com/op7418/status/2018892524937695533
  - 界面非常漂亮，整个交互细节也做得非常到位，完爆昨天的 Codex App
  - 他们这套 Agent 的状态流转系统非常巧妙。
  - 系统会下意识地引导你去开启多个 Agent，然后你可以通过左边的状态和标签筛选，清晰地看到每一个任务的进展和大概状态。
  - 聊天窗口中的文档浏览很舒服
  - 可视化的 Skills 列表和详情页，很清晰

- 好看是好看，但是对于 Claude 功能的支持是不全面的。 比如说： 1. 回退代码和手动压缩会话的功能是不支持的 2. 对于模型切换也比较受限 
  - 总之感觉是一个美丽的花瓶，功能性不是很强，可能在某些特定场合好用吧

- ## [昨天做的Office插件（Claude in Word！）今天打磨得差不多了，还是不选择闭源了吧 _202601](https://linux.do/t/topic/1544743)
  - 因为发现可在商店里下载的 Add-on 不是要付费服务就是太卡太重，于是决定自己写个轻便好用的，直接使用 Office API 来获取用户操作和格式信息，快捷地使用右键菜单和侧边栏操作。
  - 强兼 OpenAI / Anthropic / Gemini 格式 API，推荐使用 OpenAI 格式
  - 自动捕获用户使用鼠标选择的文字内容
  - 辅助排版，伴随着分块处理和全局撤销功能

- ## Kimi can now edit Word docs just like a lawyer. 
- https://x.com/KimiProduct/status/2016720053639811272
  - track-changes 的交互效果

- https://x.com/Kimi_Moonshot/status/2016710842654609648
  - Kimi can now create and edit files! From expert-level spreadsheets to professional slides and PDFs, all it takes is a chat. Quick update: "OK Computer" has officially leveled up and is now "Kimi Agent".

- ## [I built an AI that redesigns your Notion pages into real websites : r/Notion _202510](https://www.reddit.com/r/Notion/comments/1o0bco2/i_built_an_ai_that_redesigns_your_notion_pages/)
  - I’ve been building Bullet.so for a while, growing slowly and steadily. 
  - But recently I hit a point where I started wondering: why do we still have to tweak every block, color, and spacing by hand when Notion already gives us great content structure?

- ## Notion AI can now actually use Notion. _202508
- https://x.com/NotionHQ/status/1953127672848236721
  - It handles multi-step tasks like editing multiple pages or updating entire database—like a power user, built in.

- Amazing. Just need an API endpoint to send a prompt to a page for automation now, would be extremely useful

- the shift from "ai helps with tasks" to "ai performs tasks" is everything
  - this is what we mean by agentic - not just generating text but actually manipulating systems
  - curious about the safety boundaries - what stops it from accidentally deleting important pages?
- It'll ask for confirmation before deleting pages 

- This is how agents should work, not just "ai writes text" but "ai actually does the work": updating databases, cross-referencing pages, maintaining consistency across workspaces

- https://x.com/ivanhzhao/status/1953180931260596387
  - Looks familiar on the surface, but we completely rebuilt Notion AI.

- ## Gemini 的 Stroybook 太酷了, 只要上传一段文字或者提示词或者文档，就可以生成一本图文并茂的故事书，效果相当相当的好
- https://x.com/dotey/status/1952954741777945071
  - 只需简单描述你脑海里的故事，Gemini 就能为你自动创作一本独特的、10 页的个性化插画故事书，还带有温暖的有声朗读哦
  - PS：默认是10张绘本并没有在系统提示词约束，而是可能是在工具中有限制，不过可以试试连载的效果。

- 播放就伴随页面转换，很流畅，配图也很好

- 哈基米是最大生产力的AI

- ## Rspress 2.0.0-beta.25 supports UI display in plugin-llms, which is inspired from fumadocs and other docsites in the community.
- https://x.com/Soon_Iter/status/1953026619536208379

- ## 为啥 Copilot Edit 在 LLM 输出回答后，Applying Edits 那一步会那么慢。
- https://x.com/oasisfeng/status/1903354770288488636
- 看来 Dev AI 团队也做不到让 LLM 直接生成 patch 文件那样规范的代码变化。
  - LLM 会像人类一样笼统地描述「在哪哪之后添加这段」、「保留…直到…」，Copilot 估计又让 LLM 来最终 merge。

- ## 使用 Cursor 之类的代码编辑器写博客的Markdown非常尬，每打一个字都有自动补全，严重影响思路和观感，
- https://x.com/vikingmute/status/1896110973280559112
  - 自动补全的内容行文和小学生作文一样，那么问一下各位推友，有没有类似 Cursor 的编辑器但是是针对写文章的工具？
- 可以配置规则不对某种类型文件 tab 或者暂时 disable tab

- cursor tab rules 的应用场景来了

- ## I need Cursor but for writing. 
- https://x.com/dannypostmaa/status/1894539881499824495
  - Cursor works for document editing too apparently.  

- https://x.com/ycombinator/status/1895202244414574725
  - TamLabs is building Cursor for Microsoft Word.

- ## Grok3 这套 思维链 展示的 UX 也太酷了: 实时推理, 让用户对进度产生信心
- https://x.com/tuturetom/status/1892922300451754105
- Grok前端设计师估计是结合了DeepSeek R1与OpenAI的UI特点，设计了这套介于两者之间的新UI。

- ## Nice blur transition to expose the CoT without overwhelming the conversation scroll view.
- https://x.com/Gavmn/status/1887919024589226082
- what’s your thoughts on the vertical carousel between different thoughts? Some of them are a bit fast that I can’t read it
  - It's definitely a bit fast in this example. Most of the time I see it it's slow enough that I can read a bit before it changes

- I like how Deepseek has it, I want to see what it's thinking

- ## Did you see my @vercel AI text editor integration? You can select text and ask AI to simplify, add detail, translate, and more.
- https://x.com/ctnicholasdev/status/1882829374585786732
  - Soon we'll be enabling this with first-party components at @liveblocks .
  - [Building an AI toolbar for text editors | Chris Nicholas | Developer experience at Liveblocks _202407](https://chrisnicholas.dev/blog/building-an-ai-toolbar-for-text-editors)

# discuss-builder
- ## 

- ## 

- ## 公众号文章排版，你们都有什么工具。 
- https://x.com/mrpanda88888888/status/1889844178303283478
- 当我思考最重要的事是什么之后，得出结论，轻排版重内容。分享给你

- vscode + markdown preview ext
# discuss
- ## 

- ## 

- ## 

- ## 花了四个月终于快完工啦，超顺滑的无限白板和编辑器。
- https://x.com/kk_shinkai/status/1903959640595103966
  - 白板部分更是完全从零编写，交互和配色都雕琢了很久，还支持复杂的对齐和挤压算法。
- Obsidian's Canvas is already capable of doing this.

- https://x.com/kk_shinkai/status/1901791856528363817
  - 给我的白板软件开发的富文本编辑器。目前还有不少 bug，离 “超高质量” 还有一段距离

- ## I am so happy to introduce you to Not Real - a design-driven creative studio focused on art direction, CGI, and animation
- https://x.com/alex_barashkov/status/1902745611125842058
  - The studio is a well known for their work on many Microsoft promo videos

- ## Attempting to replace folders with tags is a rite of passage for info-structure designers.
- https://x.com/msimoni/status/1893260097976975587
- I think there is a generalization of this chore: migrating a 1-n relation to an n-n relation.

- you can go from tags->folders without losing information but you cannot go folders->tags without losing information because one file can only be at one folder

- ## ✨ Did you know you can add section headers to the minimap of @code ? 
- https://x.com/CSSWeekly/status/1806625178878619984
  - Use `MARK:` in the comment, and the designation will be clearly visible in the minimap, which will help you quickly scan and navigate your files.

- ## 🎨 Microsoft Word, redesigned
- https://x.com/upintheozone/status/1791715466479903077
  - 类似lowcode编辑器
- Like the Word for Mac 2003  with properties on a side bar
- This is basically Apple Pages. it already exists
- Looks ok, but more form over function and looks like pages, and the design of pages is the reason I don't use pages, it's too watered down and frustrating to find things.
- I think we have entered the Arc browsing design era
- That looks so figma

- ## 🌰🌐️ pinyin-pro速度嘎嘎快。写了一个使用 ruby 标签排版拼音的 playground
- https://twitter.com/yisibl/status/1767492218670194896 
  - https://codepen.io/yisi/pen/WNWxvJr
- 我搞了几个内部工具的搜索功能都用了 pinyin-pro，确实挺好用的

- https://twitter.com/yisibl/status/1768283436547293440
  - pinyin-pro 目前还不支持变调，我单独处理了一下，现在可以适配绝大多数诗词中的变调。
  - 还增加了儿化音的处理，完全适配了人教版一年级语文《秋天一文》

- ## 🌰📝 今日HackerNews 上的最热贴： 《9 years of Apple text editor solo dev - 独立开发 Apple 文本编辑器的九年》
- https://twitter.com/vikingmute/status/1743447079257858454
  - [9 years of Apple text editor solo dev | Hacker News_202401](https://news.ycombinator.com/item?id=38866170)
  - 作者在九年前受 iA writer 的启发，开始开发一款更极简的文本编辑器  Paper，开发过程中这漫长的九年中的点点滴滴，非常详尽
  * 技术选型
  * 应用架构以及调试
  * 付费特性以及收费策略
  * 文本编辑器的难点

- 这个产品付费用过，编辑体验很好，后来因为没有文件夹体系，就放弃了。

- ## 使用@dotey分享的两步翻译法给这次重写编辑器作为一个结尾吧
- https://twitter.com/beihuo/status/1736172903312613411
  - 这次重构主要对使用流程进行了优化，将触发按钮从侧栏移至顶部工具栏，以提升用户体验。
  - 侧边栏有了更大的空间，之后会放入一些新功能。同时，对侧边栏的后端逻辑进行了重新抽象，有效减少了代码量。
  - 为了更好地满足书写格式的需求，从纯文本编辑器升级为富文本编辑器，并增加了对 Markdown 的导入和导出功能（目前仅给 GPT 用）。

- ## Just build a small demo in Loro. It can record the entire edit history in a DAG, just like git, making playback and diff viewing easy.
- https://twitter.com/zxch3n/status/1721898524403798457
  - 文档历史的滑块交互动画

- ## 使用飞书的时候查看图片不是用mac自带的“预览”，而是在飞书自己的窗口中打开，
- https://twitter.com/TooooooBug/status/1630761293924945920
  - 导致一些常用的图片操作都不能很顺利地进行，甚至OCR识别也不行（尽管飞书也加了这个能力，但不是很灵光）。一开始非常非常不理解，但这两天突然想明白为什么要这么做了
- 主要是为了实现撤回对方哪怕打开查看了也不可见的目的吧，如果用本机的程序预览，就很难做到这个技术实现了。
- 可以审计图片的查看、传播链
- 协同涂鸦
- to B的软件不可以随意加审核删除的，这是企业的权利。另外像企业微信，用预览看图，如果撤回了图片，正在预览的图片也会消失的。

- ## Notion 优化了走直线选不中子级菜的问题，想起之前 @height_app 的一篇关于 context menus 细节的文章。
- https://twitter.com/leadream4/status/1629307997175549952
  - 一般的解决方案是加一个延迟，但是更好的方式是增加三角安全区域，亚马逊和苹果都是这样处理的。
  - [Breaking down Amazon's mega dropdown](https://bjk5.com/post/44698559168/breaking-down-amazons-mega-dropdown)
  - [A comprehensive guide to creating intuitive context menus - Height](https://height.app/blog/guide-to-build-context-menus)
  - [Invisible details - Building contextual menus - Linear Blog_202009](https://linear.app/blog/invisible-details).
  - `clip-path` is a cool css property that lets you define a region of the component that should be drawn to the screen. In this case we use a polygon to draw a triangle.
  - [MouseSafeArea.ts](https://gist.github.com/eldh/51e3825b7aa55694f2a5ffa5f7de8a6a)

- ## Personally, if I had a choice, I would always, always, always start designing with a click-menu instead of a hover menu
- https://twitter.com/vitalyf/status/1630481527497687040
  - Hover menus delays will be too fast for some users, too slow for others; the UI can feel confusing and frustrating, and unresponsive.

- ## GitHub is experimenting with interactive README components, called "blocks."
- https://twitter.com/FredKSchott/status/1590438076677238784
  - https://blocks.githubnext.com/
  - https://www.youtube.com/watch?v=wKZg0DScucw&t=23782s
- “I’m a README developer”
- Interesting! My hopes: implemented via directives (hopefully) or fenced code lang flags (like their new task lists, also okay).
- That's cool but i did it first, built with Astro
  - https://github.com/nikolaxhristov/nikolaxhristov

- ## 想从零实现一个富文本编辑器是不是天坑……
- https://twitter.com/waylybaye/status/1531463471371800576
- https://github.com/Icemic/huozi.js
  - A simple typography engine for CJK languages, especially designed for game rich-text. 用于游戏富文本的中日韩文字排印引擎。
- 活字 JS 应该能满足基础的 Web 排版自绘需求，或者 Skia 提供的 CanvasKit WASM 也能实现。自己从头做的话可利用 HarfBuzz 的 shaping 结果查找字形 glyph，自行将它们分多 run 在平面上放置并折行。
- 我之前为了兼容性尝试做过一个canvas渲染纯文本显示的，坑太多了弃了，老老实实嵌入webview

- ## 💡 Heptabase 面向未来的知识操作系统
- https://sspai.com/post/71842
- Hepta 的组织架构包括 Timeline、Tags、Map、Card Library。
  - Hepta 便是由这些 App 构成的 Productivity App Store。
  - 这四个 App 实质上是为用户提供了一个 收集 → 初步整理 → 深度思考 → 资料库 的完整工作流。
  - Timeline 模式借鉴了 Roam Research 等产品倡导的 Daily Notes 设计，以及 Twitter 等产品的思绪流理念。每一天，你打开 Timeline，便可以快速收集你的各种灵感和想法。
  - 当你在 Timeline 模式中进行快速记录时，顺手打上标签，你的卡片便会自动进入 Tags 模式的卡片分类之中
  - Map 是 Hepta 的核心功能和特色功能。Map = WhiteBoards（相互关联的 Cards）。你可以在 Map 中自由创建白板 WhiteBoard，而在每个白板之中，你又可以自由创建无数相关关联的卡片。深度思考或者创造的核心，在于将抽象的思想具体化，并且使得想法相互碰撞中进行升华。传统的深度思考工具便是写作。然而单纯的文档写作无法以高效地方式呈现思维过程，因此，人们会使用思维导图、概念图、白板等思维工具。
  - Card Library 负责对于信息和知识的聚合管理，属于你的知识库。在这个知识库中，你将可以使用多种方式对内容进行管理和呈现。
- Hepta 的 Map 模式，本质上便是由若干个 Card 组成的 Whiteboard，即 Map Mode= Whiteboards (Card & Card)。
  - 如何理解 Hepta 中的 Whiteboard & Card？目前，存在两种理解方式：
  - Hepta : Whiteboard & Card = Roam : Page & Block；
  - 第一种方法，适合进行卡片笔记写作
  - Hepta : Whiteboard & Card = EverNote : Folders & Page；
  - 第二种方法，适合进行项目管理
  - 上面只是两种理想状态，具体取决于不同用户的使用习惯。最好的方法便是基于卡片的自由组合：短的内容视为 Block, 长的内容视为 Page。
- 目前，Hepta 开发团队只有三人。除了维持几乎一天一版的高开发速度，开发者每天还需要响应处理 20-50 名用户的客户服务需求，以及大量的 1 - 1 视频教学。

- 他们后端用的firebase，底层数据结构应该还是基于文档的
  - 协同应该也是基于firebase的文档同步做的，已经输了
  - 编辑器本身不够牛逼，我觉得方法论级别的大多数革命性特性都是空中楼阁
  - 我们要做更好的tag、更好的search、更好的block扩展

- 我们block-editor的数据结构已经有前人实践过了，缺的只是一个更好的展现方式
  - 这种block式结构，我已知最早的实现是fossil
  - 由sqlite的作者开发的scm，实际上blockdb的前身文档数据库就参考了部分设计，只是针对当时的整体架构做了调整
  - 当我们再次将颗粒度细化到block层级后，实际上就变成了一个better fossil了
  - fossil基于block结构实现了crdt的版本管理工具，我们则实现了crdt的编辑器
  - fossil同样使用block存issue、pr、wiki等等数据，殊途同归
  - 以后 blockdb powered by rust 说不定可以联系下作者
  - yjs目前还没成为瓶颈，等啥时候成了瓶颈，就可以考虑wasm版blockdb了
- 先盈利比较重要
  - 也可能转型做技术开源的公司，商业混不下去
  - 目前我们还在构建服务阶段，大多数时候创业创新产品，速度快比技术快更重要
  - 大多数项目都没有性能优化的门票
  - 过早优化适合兴趣项目，没有盈利要求，自己投资自己

- 以后大可以用flomo整理block-editor的card，双向同步

- ## storybook Component Encyclopedia is in beta
- https://twitter.com/storybookjs/status/1491806826739941377
- We’re on a mission catalog the world’s UI components for you to learn from—3, 490 components & 44 projects so far.
  - Reference components from top teams
  - Play with live implementation 
  - view source

- ## Notion、WordPress 等有基于Block概念的编辑器。人们喜欢 Block。
- https://twitter.com/EryouHao/status/1486954447943057409
  - 我们似乎标准化了一件事：插入新 Block 的 / 键。但是其他所有的内容都是完全专有且非标准的
  - 如果在网络上的 Block 是可互换和可重复使用的，不是很酷吗？
  - 于是一个开放的、免费的、非专有的协议诞生了
- https://blockprotocol.org/
  - https://github.com/blockprotocol/blockprotocol
  - An open standard for building and using data-driven blocks. Make your applications both human and machine-readable.
  - Any valid HTML is already a block.

- ## I’m working on a spike(尖刺) for TLDraw’s renderer, replacing the current “one big SVG” approach with lots of divs for each shape instead.
- https://twitter.com/steveruizok/status/1436638874432851968
  - The goal is to support “shapes” that render regular HTML, not just SVG elements like `<rect>` or `<path>` , which is the current limitation.
  - Instead, the renderer should be able to put any React component on the page. Most of the current shapes will return SVG elements, but shapes like Text wouldn’t have to.
  - The biggest trade off here is auto-sizing `<g>` elements, which are awesome. Since SVG elements are basically `overflow:hidden` , we’ll need to pad the shapes more based on the zoom level.
- My one concern would be files will tend to stop being SVG compatible as the files gets laden with non SVG components. So no clean export. I want non-SVG components though too. Perhaps being able to have constrained parent objects that only allow SVG children so people can intent.
  - **SVG export is more of a “app level” feature vs a “renderer level” feature** , so it’s really up to what you do with it. No reason we can’t still have good SVG export in the tldraw app.
  - For example, if I had a post-it component that I rendered in HTML, in order to make it easier to edit on the page, I could still write my export code to create an SVG shape from its data.
- Is `foreignObject` not an option? I was hoping that we can start using it in projects that don’t need to support IE (which I’m assume TLDraw doesn’t).
- I'm basically doing something similar to this for the visual editor. It's still one big SVG, but also a `foreignElement` that positions HTML elements (single one for perf reasons)

- ## So, dumb question: you're building a (small) Postgres/Node/Vue web application that has a feature where user can upload file, and retrieve it later. Where do you store the file?
- https://twitter.com/stevage1/status/1433215485051613187
  - 结论是避免过早优化
  1. In the DB
  2. On disk on the Node server
  3. In S3
  4. Some other third party?
- If it's a small number of files and there are no big files, I'd definitely go with 1. That way you cut out the AWS dependency and you have all the data in a single place.
- No.1 is also good because of the concurrency guarantees - can use as a rudimentary message queue
- Must be some library out there to make 3 easy? In Python/Django, there's a package that just shims it in so it looks like reading/writing to local disk, and generates signed URLs as needed.
- Depending on how hard you anticipate making the switch later if it starts to cause issues... I'd probably give 1 a crack. Avoid premature optimisation, a bit easier in the short term etc
  - The aws-sdk for node is not that complicated, but you wanna be mindful of security then

- ## I'm super impressed by the approach @craftdocsapp is taking to data ownership. 
- https://twitter.com/geoffreylitt/status/1374144532976168967
  - 提出了制定markdown在线多人共同编辑协议的建议
  - At the same time, I think they're hitting the limits of modern data storage platforms, and hinting at precisely why we need a new kind of "collaborative filesystem".
- As context, Craft is an iOS/Mac notetaking app w/ a "blocks" model that feels inspired by Notion.
  - Unlike Notion it's offline-first (= very fast!). 
  - The interesting thing is they offer two different ways to store your data
- Option 1 is to sync your notes to Craft's servers.
  - The benefit of this is you get realtime collaboration, and you can share a web link with anyone to get comments. 
  - Feels similar to GDocs/Notion, just with much better offline mode.
- Option 2 is to store data on your filesystem. 
  - The benefit here is data ownership: more privacy, and you can open the files in other apps without issue.
- Now, if you want sync with Option 2, you can bring your own w/ iCloud Drive etc. But if two devices edit concurrently, you'll hit conflicts.
  - They currently store data in a JSON format but are trying to move to Markdown as a canonical storage format. Would make the "data ownership" even more meaningful since you could just edit their files w/ any Markdown editor!
- So, to review -- user gets to choose either Option 1 or 2 for any note. Which is already amazing and beyond most other apps!
  - But... it's also annoying that I have to choose. Could we have an Option 3 where we get the best of both worlds?
  - Concretely, what I want is something like a "filesystem", where I own the data and can open it in whatever app I choose.
  - But I don't want manual conflict merging every time two people simultaneously edit a doc. The "filesystem" needs to know how to merge changes.
- In other words: why does Craft (and Figma and GDocs and Notion and Pitch...) have to implement their own custom realtime sync protocol?
  - Could we just have a user-owned "filesystem" that deals w/ that part? So I can open a file in multiple apps, and have them sync in realtime?
- **The world I'm imagining** is one where I have Craft open, and you have Notion open, and another collaborator has VSCode open and we're all editing the same document live, perhaps from slightly different perspectives.
  - Curious if people think this "new collaborative filesystem" would be valuable and what the biggest challenges are.
  - To me, feels like the biggest tension is standardizing vs. diverging "file formats", and seeing how much common ground can be found between apps.
- Some intriguing projects which are taking on aspects of this challenge:
  - Braid (braid.org), a generic protocol for state sync
  - Fission (fission.codes), platform for building apps where users own the data
- The original local-first article from I&S is always worth a re-read for thinking about this tradeoff space.
  - But I think the extra tricky part is going beyond "individual devs should do local-first" to "we should have a cross-app local-first FS"
- I believe that future is possible with event sourcing. @todoist somewhat done this with their sync API.
- As long as we have:
  - websocket/web etc
  - ordered list of events 
  - SDK that convert events to data
