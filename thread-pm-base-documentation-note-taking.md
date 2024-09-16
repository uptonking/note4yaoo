---
title: thread-pm-base-documentation-note-taking
tags: [documentation, note-taking, pm, thread]
created: 2021-04-19T14:49:44.712Z
modified: 2021-08-16T06:56:53.061Z
---

# thread-pm-base-documentation-note-taking

# guide

# discuss-stars
- ## 

- ## ✨🤝🏻 Version history as chat: what if you could chat about editing progress with your collaborators right in the history timeline of a document?
- https://twitter.com/geoffreylitt/status/1773423061938708839
  - That's the idea of our latest Patchwork experiment...
  - The goal of this timeline view is to give structure and legibility to the document history.
  - All edits get an AI-generated summary and you can also leave little notes annotating the history in a super informal way

- is chat the right framing here? is it more a timeline? i like this approach.
  - Yeah it’s kinda both depending on how you look at it I think

- ## 🆚️ It seems that there are just three approaches that "knowledge management" apps take:
- https://twitter.com/jessmartin/status/1710261497786413516
  - Document-first (Notion, Obsidian, etc)
  - Spatial-first (Miro, Muse, etc)
  - Table-first (Airtable, Tana?, etc)
  - ...and then they try to add the other two.
- Thought of another one: Notebook-first. Observable, Jupyter Notebooks, etc.
- How you answer the question determines many things:
  - primary/secondary nav metaphors
  - which components you spend the most time on
  - what should be embeddable in what
  - how you visually present an entity/object throughout(各方面)

- Tana, Roam, and Logseq all seem like Outline-first, where the primary unit is actually a point in the outline.
  - Good point! Outline ≠ document. When I’ve tried to treat an outliner as a normal document, I’ve been incredibly frustrated

- Task-first. @clickup Docs function as my primary knowledge base with links to Tasks in Lists that track my long-term and ongoing projects. It’s powerful to have knowledge management and project management in a single tool.

- Also http://getguru.com - they look similar but take a different approach (with verification features) and are very successful with it
  - [Guru | Your company’s all-in-one solution for trusted information | Guru](https://www.getguru.com/)
  - 3 products. 1 platform: AI-powered enterprise search, wiki, and intranet
- On the surface, it looks like document-first (an enterprise wiki)
- What would you say differs about their approach?
  - One differentiator is verification. Each "card" needs checking and verifying within a certain time-period. This ensures that information doesn't grow stale which is a problem in so many company wikis. By default the card creator is the verifier, but they can also be nominated.

- I would consider http://rewind.ai a tool for knowledge management, a very novel one.

- This makes me wonder about Anki’s use for PKM where it is very document-first but the primary interaction is at a sub-document level. The relationship to and navigation of the corpus is also distinct. Then primary-nav: folders, tags, piles, search (inc. keyword or semantic).
- This is helping me think - perhaps representation/medium should be tied to activity:
  - capture/ingest/create new
  - search/recall
  - browse/explore
  - organize/curate/interlink
  - edit/remix

- Maybe this is the mythical graph-first? Curious how this feels in practice. Many people who use tools with knowledge graphs seem to only use as an auxiliary view, kinda like a dynamic plot

- https://get.mem.ai is interesting from this lens... "Snippet first" maybe?
  - but I'd argue that snippets are just short documents.

- I was going to joking reply, "clipboard first" to your original. I'm working on a clipboard manager that takes influence from the tools of thought space, particularly obsidian

- I would describe Fabric as entity-first (like Finder), we don't try to coerce things into a new shape
  - So I thought about that, too. The problem is entity/object is too generic. Items on a spatial canvas are entities.
- How I think about it for my entity-first product: One has to focus on some components/UI first.
  - The difference is how deeply those metaphors are baked into the core. Airtable will always have tables as primary view, while others are more neutral towards how the app should be used
- I’m also working on an entity-first system and pondering the same concerns. Formable looks interesting!

- I've been using Notion since they launched and they definitely started Document-first and have added more Table features over time.
  - Document is the organizing metaphor navigationally (they call them Pages).

- Arguably wikis are supposed to be hyperlink-first.
  - I was cheekily thinking of hypertext as the Platonic(纯友谊的，柏拉图式的) form of the Document.

- Command line first perhaps?
  - maybe this overlaps with cmd-K / cmd-space first (Raycast, Alfred, Quicksilver)?

- @RoamResearch is block-first, even in a way that Notion is not (I think you're right to call Notion "Document-first") 
  - It then *composes* the three approaches you list here by combining together the same underlying items in different forms (slightly different than "adding on")
# discuss-academic
- ## 

- ## 

- ## 

- ## love that apple just ripped off @inkandswitch with the math notes thing. 
- https://x.com/max__drake/status/1800225633286737966
  - the computation and annotation existing on the same layer is Very Cool
  - ["Programmable Ink" by Szymon Kaliski (Strange Loop 2022) - YouTube _202210](https://www.youtube.com/watch?v=ifYuvgXZ108)

# discuss
- ## 

- ## 

- ## 按钮放大为卡片
- https://x.com/vaunblu/status/1833548581342487020
  - Made with React and Tailwind, Framer Motion
  - https://github.com/vaunblu/lab/blob/main/src/app/create-new/page.tsx

- ## 缩略卡片放大成文档的动画交互
- https://x.com/henrikruscon/status/1821475322929324078
  - https://x.com/Gomila_club/status/1832013063446212698

- https://x.com/tonilijic/status/1834344409992765865
  - 卡片切换效果， stacked card interaction

- ## This has got to be one of the coolest product changelogs I've ever seen 
- https://x.com/steventey/status/1809347539176657188
  - https://ronin.co/updates
- What is this kind of expanding bento grids called?
- It should be sequential, this would be a nightmare to track.

- ## ✨🧪 On the Patchwork project at @inkandswitch we've been exploring _202404
- https://x.com/geoffreylitt/status/1784717448207274073
  - [Patchwork lab notebook](https://www.inkandswitch.com/patchwork/notebook/)
  - What are powerful, ergonomic version control UIs that support all kinds of collaboration workflows? And how can that support both human + AI collab?
  - That's why on Patchwork we're interested in universal version control: What if all your creative tools (writing, drawing, spreadsheets, ...) could share one version control system, managed by the OS? And what if AI could hook in at that layer, to collab in any app?
  - Eg, in a world of universal versioning, imagine you ask an AI to update an app design, and it proposes tweaks to the mockups, the code, and the docs... all together in a branch!

- Thankfully a few libraries seem to have won out that are adjacent to version control: Yjs for collaborative editing, TipTap/Prosemirror for text editing, React Flow for structured diagramming, tldraw for unstructured diagramming, etc
  - The Yjs+TipTap+Prosemirror combination that’s currently the easiest way to implement collaborative text editing, has an UndoManager for local undo/redo but no version control or comments system
  - Hopefully Patchwork will become mature enough soon to fill the gap
- yep that's the eventual goal!
  - our starting point was markdown editing in codemirror, but a good automerge + prosemirror integration is finally landing soon so we wanna expand to rich text as well.
  - surprising how big a deal comments is across all these domains

- ## 记笔记是生产力游戏里面最基础的部分。有点像玩 RPG，记笔记只是每天下副本刷材料的日常任务。
- https://twitter.com/mayneyao/status/1776114010859139122
  - 把材料加工做成装备，强化角色，攻克更难的 boss 或者卖掉产生经济效益，则是产出的部分。
  - 每个玩家都能找到自己的乐趣。攻克难关能获得快乐，仓鼠党整理素材背包也能获得快乐。
  - 笔记工具更像是某种攻略 build，攻略会引导玩家走向某种游戏“胜利”，速刷boss 、白金全收集诸如此类，各自的侧重点也不同，PvP 还是 PVE，休闲还是硬核。
  - 多维表数据库适合抽象分类整理数据。大纲式笔记适合递进的逻辑推导。白板类工具适合帮助梳理事物之间复杂逻辑关系。

- ## 💫 combine it with CSS scroll-driven animation
- https://twitter.com/jh3yy/status/1770603402923225175
  - 图片挤压文字的动画效果
- https://twitter.com/jh3yy/status/1772702339389923355
  - https://codepen.io/jh3y/pen/ZEZJYVe

- https://twitter.com/jh3yy/status/1772705093546107377
  - The CSS trick here is using custom properties to drive your CSS animation behavior
  - Doesn't have to be a scroll animation

- https://twitter.com/jh3yy/status/1771294048889786389
  - Custom property powered responsive scroll animations with CSS
  - https://codepen.io/jh3y/pen/JjVRGwR

- ## 一个程序员最卷的项目：Markdown 编辑器。
- https://twitter.com/vikingmute/status/1768090000481288276
- 卷是卷，就是没一个特别好用的，尤其是缺乏原生的。比如一些markdown 扩展支持不好，互相不兼容，例如obsidian 的查询语句。

- 还不够卷，我就没见过哪个 markdown 编辑器的渲染不依靠现成的 web 渲染器的。有本事直接去渲染啊，markdown 需要的文本样式又不多。
  - 自己渲染的话有些直接在 md 里写 html tag 就没法给预览了。另外 mermaid 这些扩展也没法直接用（虽然可以用两套渲染器）。 Mac 平台上确实有几个不走 web 渲染的，都不便宜。
- 我一直觉得 MD 那么简单的样式，不是 native 的都是花拳绣腿，毕竟 MD 一开始就是 HTML 的语法糖。
- https://mweb.im mweb应该是原生不用web渲染的

- typora 在处理大量文本（100k+) 时候会卡, 不知道其他怎么样

- 用过好几个，现在不折腾了，就vscode吧，起码有个多光标

- ## 用了两年的 Logseq 后，神奇的发现我好像不怎么使用双链了。
- https://twitter.com/henices/status/1748365491633049904
  - Journal 的好处是可以随时输入一个较为完整的文字片段，心智负担很小。
  - 但如果要真正对某个主题有较为深刻的理解，需要将零碎片段的完整逻辑和前后关系串连起来。真正可以实现这个目标的是写文章，而不是依靠双向链接。
  - 只要写文章的时候，你需要的所有内容都在同一个地方，具体的是用使用标签，还是文件夹都不是重要。
  - 知识体系的构建是通过不断学习和自我迭代来实现，边界的延伸则可以跟随着自己的好奇心，学习真的是一件很有趣的事情。

- ## I think a spatial alternative to Notion where the blocks are laid out in a customisable Bento pattern would be pretty useful.
- https://twitter.com/JungleSilicon/status/1747707553419821374
  - Gives a degree of spatial flexibility without going full free-form like tldraw.

- I wish...notion extended their view flexibility from databases to page content. 
  - One of the reasons databases are popular is because you can have views. 
  - I wish they had views for page blocks (for example, see different toggles in grid) or switch to linear document.

- Transno had some interesting ideas in this area: https://transno.com 
  - And some interesting ideas here: https://essay.app (reordering and indentation), https://writereason.app (mapping), https://speare.com (stacks)

- ## @_pastelsky built the app of my dreams: https://tsdocs.dev. it's basically docs​.rs for TypeScript.
- https://twitter.com/galstar/status/1734919519921955147
- There are https://paka.dev and https://jsdocs.io too
-  A couple of differences –
   1. TSdocs finds types even when the package may not be written in Typescript e.g. d3
   2. You can also browse types that aren’t directly exported by the package. e.g try @sentry/browser

- Coming from the world of Java, I have learned that JavaDocs tell you nothing by telling you everything. And _because_ JavaDocs are so easy to generate from the type information, devs don't bother to write readmes. I hope these tools won't make it happen in the JS world.
- I wasn't familiar with Rust documentation, so had a look at some packages in http://crates.io. Nice! You've got both readmes _and_ JavaDoc style information. So you may be right in that you can have both!

- ## There's a new breed of note-taking apps in town. These apps help to better visualize your ideas, notes, and thoughts.
- https://twitter.com/FrancescoD_Ales/status/1719731096634687952
- @Heptabase Enhance your research and make detailed connections between notes in a combination of canvas & structured notes.
- @Napkin_Ideas A flow of ideas is amazing, but the capture and connect process can unlock even greater results, Napkin wants to solve this.
- @Scrintal Mind mapping & notes, married. This experience wants to be a blend of traditional note-taking & visual note-taking.

- ## A math teacher at @GVSU used Obsidian to create a course textbook with exhaustive linking
- https://twitter.com/kepano/status/1718008501589639321
  - [START HERE - MTH 225 Fall 2023 - Obsidian Publish](https://publish.obsidian.md/mth225/START+HERE)
  - I like this structure because you can easily dig deeper on any concept you don't understand. Very well done!

- 
- 

- ## In Europe, Estonia has had the digital signature for some time and it works really well:
- https://www.reddit.com/r/InternetIsBeautiful/comments/zxdz3e/i_made_a_free_pdf_editor_that_works_in_your/
  - https://github.com/open-eid – it's all open-source.
  - Using their protocol, any document (PDF or not) can be put in an envelope to be signed.
- Let's hope that more countries adopt it!

-  I would most likely rely on open-source implementations such as this one: https://github.com/open-pdf-sign/open-pdf-sign

- ## 你需要一个faq或者产品知识库，
- https://twitter.com/guageaaa/status/1643405528809480193
  - app里做一个收缩列表，或者三方的客服系统（比如智齿，小芝麻客服，网易七鱼或者腾讯自带的客服机器人之类的），有很多简单集成一下就可以用。用户触达方便，最后留一个转人工给邮箱地址入口。
  - 不是广告哈，之前小创业团队有类似经历，爆发期省下了非常多精力

- ## 如何基于 ChatGPT 创建个人的知识库 AI，经过几周的内测，现在正式发布 Copilot Hub 
- https://twitter.com/Tisoga/status/1640261647267938304
  - Copilot Hub 是一个帮助你基于私有数据创建智能知识库 & 人格化 AI 的平台。你可以基于文档、网站、Notion database 或其他数据源在几分钟内创建一个自定义的 ChatGPT。

- 平台上已经预训练了一些 AI，例如：
  - 基于 Steve Jobs 传记、演讲、书信训练的 Steve Mind AI，可以以 Steve Jobs 的视角来回答你的问题
  - 基于 How to Start a Startup 这门课的语料训练的 Startup Launch 创业导师，可以回答任何关于创业的问题

- 如何创建一个自己的 Copilot
  - 第一步：选择数据源
  - 第二部：定义 Copilot 的配置
  - 第三步：Chat，创建完 Copilot 之后就可以直接和 AI 进行聊天了，使用方式和 ChatGPT 类似。

- Copilot Hub 同时也是一个社区，你可以在 Gallery 中浏览到其他人创建的公开 Copilot 并进行交互。

- Copilot Hub 现在还在快速迭代中，我们基本上会以天级别来 ship 新的功能 & 修复 bugs。
  - 在上个 Sprint 中 close 了 52 个 issue 👇

- 非常感谢 @nishuang 老师体验 & 给出宝贵的建议。
  1. 文本上传大小，为了避免滥用，暂时做了限制，目前支持 100,000 token； 相当于大约50000汉字？
  2. Twitter 数据源的接入会在未来支持，可以做到 connect 到 twitter 账号后，自动创建一个对应的 AI；

- ## 大家平常都是怎么分别用文件夹或标签来组织内容的？
- https://twitter.com/tualatrix/status/1626158103283765248
  - 如果「文件夹 Folder」表示：可以嵌套，但内容对象只能塞进一个文件夹里；
  - 「标签 Tag」表示：不能嵌套，但内容可以同时关联多个标签。
- 以笔记为例，我用folder做大的领域区分，比如「个人」和「工作」，不太可能有一个数据既归个人又归工作。剩下的全交给标签，不过标签我也用嵌套。
  - 稍后阅读，也差不多，文件夹管理大分类。就两个，「内容」和「资源」，因为文件夹的互斥性，会尽量少分，减少整理时的纠结。
- 目录不容易失控，且可以产生管理动作（比如移动、清理等）。Tag太容易失控，更多是把 Tag 当做第二目录来使用，目的是增加第二个甚至更多的分类字段。
- 文件夹——中图分类，标签——关键字
- 标签是网结构，文件夹是树结构
  - 树结构是特殊的网结构
  - 操作系统的文件系统使用树结构，能方便URI前缀定位，iNode能搜索更快

- ## 外国人可能不知道这世界上有一个特殊的赛道，
- https://twitter.com/dingyi/status/1623503301458427904
  - 微信公众号文章因为因为种种限制，中国人发明了用 svg 做各种酷炫的排版和动效，而且专门做这个的团队非常赚钱，全世界大牌为了在国内推广都要做。
  - 现在用 Framer 也有这种感觉，为了实现一些特殊效果用各种奇技淫巧……
- [跟苹果学习微信公众号排版_201912](https://mp.weixin.qq.com/s/BotA3ppdrikVK-r-LmXr8Q)

- ## Notion 发布了三个偏向团队协作的大功能，开始在团队协作上发力。
- https://twitter.com/Linmiv/status/1499186981590671361
  1. Teams：自由创建团队对导航栏内容进行分类组织，春季内推出；
  2. Better Databases：支持跨数据库选择数据，平铺视图展示，升级视图筛选和协作功能，几周内推出；
  3. Synced Databases：与谷歌日历、Github 联动同步，年内推出。

- ## @logseq users in my timeline. How do define when to go block-based vs going page-based in your graphs?
- https://twitter.com/PabloBernardoTW/status/1534193024934326273
- Here's my writing process in @RoamResearch 
  - 1. DNP for 95% of my writing 
  - 2. Write blocks and liberally backlink to existing relevant pages 
  - 3. Create new pages as recurring/important topics arise 
  - 4. Tag important notes so it's easy to filter signal from noise in linked references
- I typically create blocks within the context of a DNP which provides me with a type of "breadcrumbs" for traversing linked references.
  - This encourages me to regularly review past DNP which can re-introduce me to past thoughts/ideas/topics.
- I always create a page for any concept that can’t be expressed in a single block, while a block is never longer than a paragraph in a “traditional” note-taking app would be.

- To me it is something like this:
  - Block - default
  - Page - when there is something specific that I want to keep as a standalone page - like for example the details of a project, the write up of an article, notes on a book, a course I am taking

- blocks are like tweets, pages are like threads. it depends on the scaling and it helps to have both!

- my xp
  - 1. Always in blocks from a daily note
  - 2. An empty page is now generated with linked references
  - 3. If I search for a term and realise the page is empty with a lot of linked references - i use them as an inbox/todo list for organising into a page
  - The outlining in Logseq excels in that it encourages single bullets/blocks to be naturally atomic concepts.
  - Everything is a block, until I give it a title (because I keep referring to it), or I want to export it (because LS cannot export only blocks)

- ## github markdown

- https://github-md.com/
- https://github.com/jacob-ebey/github-md
  - A markdown parser API for GitHub. SWR for 2 days with revalidation every 5 minutes.

- https://collected.press/
- https://github.com/ThatCollected/collected-press
- I made an open source service that loads from GitHub via jsDelivr and then renders the Markdown to HTML. Let me know if the docs aren’t clear or if you have feature suggestions!
  - jsDelivr can do the fetching of content for you, I believe they won’t be rate limited like normal GitHub API users. The hard part is getting the SHA of the repo’s HEAD. I solved this by doing the equivalent of `git ls-remote` to fetch from GitHub

- Fastest way to get GitHub hosted markdown into @remix_run while avoiding rate limiting during dev: GO!
- https://twitter.com/tannerlinsley/status/1527449478269005824

- ## I am looking at my @logseq graph, and I see ... nothing.
- https://twitter.com/preslavrachev/status/1522203242989502465
- Are those block-based? I think this is only how the page connects to other pages. What I really need is having the separate blocks in a given page to form multiple graph clusters.
  - I think that only @rem_note supports something like this yet. @obsdmd has powerful filters and graph options, but they also just include links to other pages (as far as I know).

- ## what if jupyter notebooks looked like this(natto)? 
- https://twitter.com/_paulshen/status/1521169957957955585
  - cells with explicit dependencies
  - 2D canvas
  - interactive outputs
- natto has a related (but not exactly the same) interaction! you can select all upstream or downstream panes

- I love the 1D simplicity of Jupyter-like notebooks. 
  - I think removing one dimension of layout complexity removes so much unnecessary faff and pain, that it's one of the best UI innovations of the last 20 years.
  - Fewer Windows. Less "layout". More 1D scrolling!!!

- In addition to StickyLand this was explored in ipyspaghetti

- It’s already challenging to keep track of variables and maintain good notebook hygiene in the current form lol.. spaghetti graphs is another level
  - possibly! but one difference here is that there are no global variables. dependencies are explicit so you can better see the topology of the notebook.
- as for large ML models, you're right that execution/state is session-based in the browser. but the execution semantics are similar to functional programming - autorun panes rerun whenever an input changes.
- Cool, cool. Yeah, I get that computers "see" or "read" it as functional. Idempotent even in this case, no persistence. But having given 1000s of Jupyter Notebook/PPT presentations, I can say humans would struggle with that visual representation.
  - good to know! my intuition is that 2D space allows more flexible layouts that show relationships between the cells. The trade off is non-linearity, increase in cognitive load.
- My Jupyter notebooks are a mess in 1D already, but it does give me simulink vibes which is a good thing 👍

- ## @logseq URL Protocol handler will be a game changer
- https://twitter.com/HDanzu/status/1515515854112362498

- ## While I love http://heptabse.io's vision of a unified flow, I think in the short term we'll see specialization
- https://twitter.com/jasonlaster11/status/1513130393515565058
  * curation: http://Notion.so
  * exploration: figjam, 
  @tldraw
  * storytelling: http://Tome.app

- ## Introducing Ladle, a drop-in alternative to Storybook for React components. 
- https://twitter.com/vmiksu/status/1503748029354024971
  - Based on @vite_js , instant server start, 4x faster production build, 20x smaller footprint, code-splitting, fast refresh, single dependency & command and no configuration required.

- ## [Write plain text files](https://sive.rs/plaintext)

- PORTABLE
  - Every device, including ones long gone, and ones not invented yet, can read and edit plain text.
- UN-COMMERCIAL
- OFFLINE
- NO DEPENDENCIES
- EASIEST TO CONVERT
  - HTML, Markdown, JSON, LaTeX, and many other standard formats, are just plain text.
- NEED HIERARCHY?
  - Use directories — also known as folders. 
  - These are also good for keeping your text together with other files like images and audio.
- NEED VISUALS OR GRAPHICS?
  - Need visual mind-mapping with circles and lines? Maybe you do. But maybe you don’t.
  - Maybe it’s just another distraction, focusing on the tools instead of your thinking.
  - If you really need graphics, do your drawing using something else. Digital drawing into SVG files. Paper drawing, scanned into JPGs.
  - Keep your graphics files alongside your text files. But keep your text as plain text.

- CONCLUSION
  - Reliable, flexible, portable, independent, and long-lasting. 

- ## 用纯文本作效率软件
- https://geekplux.zhubai.love/posts/2112558255871123456
- 本文虽然标题是说用纯文本做效率软件，但无意于散布效率焦虑，主要目的是让大家尽量重视数据的控制权。
- 各种效率工具的目的无非是时间管理，而各种笔记软件的目的也无非是知识沉淀，做好这两项对于纯文本来说绰绰有余，而我们的人生也大概率就是做这两件事。
- OBTF（One big text file）在 2005 年的时候非常流行，在软件行业发展了十几年之后，越来越多人又回归到了这个概念。

- 纯文本有以下几个好处：
  - 不依赖任何公司，不依赖于任何软件。任何一个操作系统，包括手机，都有办法打开和处理纯文本文件
  - 体积小。方便迁移、同步、备份
  - 排版自由
  - 离线。想想没网的时候打开那些在线写作软件
  - 版本管理。计算机对纯文本的处理相当成熟，尤其是版本管理方面
  - 方便转换。你可以随意根据自己的需求定制，可能要写点代码

- 时间管理
- Jeff Huang 用一个 .txt 文件做时间管理用了 12 年
  - 每天临睡前把明天要做的事列出来，写上大致的时间，第二天晚上做同样的事情，列表里做完的事会自然沉淀到当天，而没做完的则可以复制粘贴到第二天，以此重复 12 年。
  - 作者还有些小 tips，比如在阐述 todo 事项的时候尽量保持同样的风格，如 meet with XXX 就是和 XXX 开会，那么只要打开软件搜索 “meet with” 就可以搜到所有的开会记录

- 自从被 Evernote 恶心到之后，我后来选择任何一个软件，第一件考虑的事情都是看它支不支持数据导出

- 关于效率，文中说了这么多用纯文本做管理的好处与示例，但效率这种东西千人千面，适合自己的才是最好的。

- ## We’re redesigning Notion’s sidebar so you can organize your pages by custom teams! 
- https://twitter.com/NotionHQ/status/1499069682581590020
  - Create teams. Hide some. Show others.
  - All part of the plan for Notion to scale to every size 
- [New sidebar design will help Notion scale to fit even the biggest companies](https://www.notion.so/blog/new-sidebar-design)
  - we’re excited to unveil our Teams feature — a new sidebar design that makes scaling with Notion effortless for even the largest of workspaces.

- Would love a right hand side bar that displays a perpetual calendar. The same way google apps have that right hand side bar for key application or blocks. Makes it easier to see things as a glance.

- ## 总有人来教育我飞书多好用，就好像我没用过飞书一样。
- https://twitter.com/haoel/status/1497197608908976128
  - 工作不是聊天，而是信息交换和共享。首要就是把信息做好，下面这些做不好，别来跟我说好用。
- 1）像邮件一样，让信息归属于一个主题，一个thread，在这个thread下不要打扰到别人。别一发消息就是reply all
- 2）你要把信息沟通工具做成拉群，你就错了。信息就是以频道的方式，不是以拉群的方式。你能明白吗？就像论坛版面一样，我想了解哪个版面， 就去看就好了，而不是拉群。这里的区别有多大，你真的明白吗？频道相当于信息分类 ，拉群不会让你的员工养成把信息归类的好习惯，你团队里的信息全是乱的。
- 3）信息文本支持简单的富文本和Markdown难吗？你知道在很多信息中，加粗、倾斜，下划线，缩进+bullet，对于信息的可读能有多重要吗？  你知道对于我们程序员来说，如果一个工具不能正常高亮显示代码，这工具者有多难用吗？
- 4）这是在中国区的软件中我最废解的一个事，你在聊天中分享一个链接，连个网页的摘要都取不回来，你看看slack, twitter, telegraf分享网页链接是什么样的，这很难学吗？你硬要学微信那个样？不是你是英文的就是国际化了。你连国际化的 Open Graph Protocol 你都不支持，你还好意思说你是国际化？
- 5）你知道一个信息能够被edit有多重要，工作中的信息就应该是准确的，就是可以让人修改的，这样才能够变得更清楚，别说撤回，还可以删除，没有用的信息就是可以删除掉
- 6）你知道为什么聊天可以使用反斜杠来发一些功能性的命令吗？你不是程序员，你不知道这样的方式在体验上有多好，而且也很舒服。/snippet /mute /giphy ... 这些才是国际化的事，而不是要要点过来点过去找不到功能。

- 微信的员工工作都是用企业微信拉群解决问题，新进群的人前面的聊天记录看不了还要手动一个个选再转发，最多还只能选100条，要是问题解决不了还要再拉一个高级点的工程师进群再一个个选择聊天记录转发，连一次性多选都用不了。我还以为他们内部有权限来云聊天记录后进群的人能看到建群以来所有聊天记录
- IM治理公司，尤其是小公司，最后信息没有任何沉淀，全部都是事件驱动的，没有一点计划性。
- 我公司老板就在推崇飞书… 我直接给所有下属说明了涉及正式的工作事项需要进行排期、评审和指派直接负责人的、多部门沟通协作以及特别重要的事项，一律只允许用邮件。群里发些散碎的信息就好，正式的工作沟通不接受群聊或者私聊！
- 飞书有两种群，普通群和话题群。话题群进群后有新话题会收到提示，关注或回复话题后会收到更新推送

- ## What are some apps that use an "infinite canvas" for things other than white-boarding or visual design?
- https://twitter.com/steveruizok/status/1479437094552489991
- Node based programming. Shader graphs. Audio effects editors. 2D side scrolling games if they need zoom and are touchpad/mouse/touch based controls
- Many flow/node based programming environments have an infinite canvas. Starting with max/map and puredata up to UE Blueprint, Unity animation state machines, shader graphs, etc etc
- You surely know about it but if you don’t, I think you’d love @KinopioClub (mind mapping, journaling, note-taking on canvas)
- prezi

- ## How are the best Storybooks organized? We surveyed 60 teams to find out.
- https://twitter.com/storybookjs/status/1488919138001207299
  - Use docs pages for intro, usage guides & design tokens
  - Use folders to group components and make navigation easier
  - Write stories to show what a component does

- ## We now had five opponents in the competition: @RoamResearch , @obsdmd , @logseq , @craftdocsapp , and @rem_note .
- https://twitter.com/rcvd_io/status/1485256388888641541
- [TfT Performance: Interim(期中的；暂时的) Results](https://www.goedel.io/p/tft-performance-interim-results)
  - Obsidian ranked first in almost every category; 
  - RemNote delivered pretty solid results even with larger data sets
  - Logseq showed that it’s pretty fast on small data sets, but the larger the collection gets, the slower it becomes. 
  - The same goes for Roam Research in contrast to Logseq handles even the big data set, but some of the processing times are annoying.
- [TfT Performance: Methodology](https://www.goedel.io/p/tft-performance-methodology)
  - This is the first article in a series looking at the performance of current applications for Personal Knowledge Management - so-called "Tools for Thought."
  - This is how the generated pages look in Roam Research and in Logseq

- ## Yes, Logseq does copy some features and UX from roam, that's why I open sourced logseq. 
- https://twitter.com/tiensonqin/status/1374351298456219654
  - But Logseq is not a clone, we have two-way sync between plain-text and Datascript, almost full org-mode support, GitHub sync on Web, 
  - and last, we don't store user's data

- ## Announcing http://papertohtml.org, an on-demand PDF to HTML converter for scientific papers!
- https://twitter.com/lucyluwang/status/1437837455902658560
  - HTML is easier to make accessible for screen readers or on mobile. 
- We @curvenote have been working at the opposite-problem how to write html-native papers that export to PDF nicely. (+ keep benefits of metadata/interactivity)

- ## Fragment: A Couple of Unofficial and Unofficial Unofficial Jupyter Extensions for VS Code and the Future of Rich Visual Editing of Interactive Generative Texts
- https://blog.ouseful.info/2021/09/13/on-a-couple-of-unofficial-and-unofficial-unofficial-jupyter-extensions-for-vs-code-and-the-future-of-rich-visual-editing-of-interactive-generative-texts/
- on my long list, one thing I’m hoping to see at some point is an executable document editor running purely in the browser on top of something like a JupyterLite kernel. 
- There are a couple of different directions I think this could come from: 
  - one would be getting something like the Curvenote editor or a Stencila editor working in the browser on top of a JupyterLite WASM powered backend, 
  - and the other would be some plugins to make a Jupyter Book editable, cf. a wiki, with edits saved to browser local storage. 

- ## HelpKit allows you to easily build your company's Knowledge Base or Help Center with @NotionHQ
- https://twitter.com/sobedominik/status/1436016818079076366
  - With HelpKit you can use all the Notion blocks you know and love.
  - No code required
  Ultra fast
  Customizable
  Looks professional
  Embeddable widget like Intercom or Zendesk
  Sophisticated search
  Custom domain

- ## Anyone know of smarter reading time estimation algorithms than words/wordsPerMinute?
- https://twitter.com/wooorm/status/1436262232338444310
  - https://github.com/syntax-tree/hast-util-reading-time
- I thought about text to speech + measuring audio length

- ## no idea if this naming is any less confusing but http://natto.dev now has "browser drafts" and "user canvases". 
- https://twitter.com/_paulshen/status/1433508225651904522
  - browser drafts are local to your browser not tied to any account. 
  - user canvases are synced to natto's server like your favorite SaaS
  - The differentiation may be premature(未成熟的，过早的) but this is setting up for an offline-capable future.
  - I do think it's nice that you're able to persist state in the app without an account unlike most SaaS

- ## Tried copying in my entire thesis into @curvenote . Learned a new HTML status code: 413. (Too large!)
- https://twitter.com/rowancockett/status/1432935094868594688
  - I know that we *can* handle larger documents via import, but not currently in a single copy-paste event of a few hundred pages which relies on our real-time collaboration.

- ## When reading docs, which mode/code highlight theme combo do you prefer
- https://twitter.com/youyuxi/status/1430689446664491012
- Code should always be dark, the doc theme should remain consistent with the system preference.
- According to settings in my OS. Light mode light theme at day, dark mode dark theme at night.

- ## The Text2PixelArt neural network (generates pixel art based on text) already allows you to create a good cover images for articles.
- https://twitter.com/sitnikcode/status/1430213610542964740
  - 生成的图片色彩风格都很浓郁，如深红深紫深蓝

- ## Evernote used to have a feature that let you export all of your notes (1943 for me) in one go... 
- https://twitter.com/simonw/status/1430407513606791170
  - but at some point recently they dropped that down to either 50 individually selected notes at a time or everything in a specific notebook
  - github从设计上就解决了此问题，每个仓库单独下载
- More frustrating though... the notes they export used to be valid XML, but now they are not! 
  - Just hit an XML error running my evernote-to-sqlite tool against the ".enex" export file

- ## Just added Markdown, HTML, and CSS as export options. Markdown includes links to hosted assets.
- https://twitter.com/4lpine/status/1428064775372607488
- We use the Theme UI sx prop as part of our internal data structure since we want direct theme mapping and the nesting of CSS-in-JS (Emotion).
  - We're statically extracting the styles to pure CSS using some tricks I hope to write a post on (soon).
  - Also, the declarative and composable nature of a props object that handles styling is so choice for this kind of tooling.

- ## I've been diving into @replicache and I'm convinced its model is what you want for majority of SaaS apps (eg todo apps, figma)
- https://twitter.com/_paulshen/status/1415365748675907584
  - client update lifecycle with authoritative server 
  - all these things have tradeoffs and I think it chooses the right ones for most use cases
- It works a lot like git where each client keeps a list of mutations 
  - although instead of the exact "diff" itself, the log contains mutation name and args (you define mutations). pure intention preservation!
  - key here is how client rebases because server is truth
- I've also been diving into https://yjs.dev, an excellent(!) CRDT library. 
  - however, replicache's model is simpler and doesn't impact your backend as much. It's really just an excellent client library with a protocol specification (big points here)
- some tradeoffs
  - you define mutations twice (once on client, once on server)
  - flat KV data structure (hi fractional indexing)
  - authoritative server (no p2p)
  - realtime updates require roundtrip
  - again I think they're reasonable
- natto does some funky iframe sandboxing that makes replicache hard to use right now but I'd use it otherwise!
  - replicache does not handle collaborative text editing rn. yjs/automerge does a good job here. on natto, I'm okay with treating each block's code as atomic unit
- I would say more that @replicache is at a lower level of abstraction than text editing. 
  - We need some good libraries for unstructured text editing on top of Replicache. 
  - You can do it right now with fractional indexing and it will mostly work, but there are likely even better ways
  - Fractional indexing has some known deficiencies when cursors are editing concurrently at exact same position.  
- I suspect that the other CRDT approaches for text editing Martin discusses can equally be applied to Replicache but I haven't had time to dig into it.

- ## Try the omakase layout on http://natto.dev! 
- https://twitter.com/_paulshen/status/1388211716001910786
  - Panes rearrange as you move your focus. 
  - Connected panes are shown to the side (inputs on left, outputs on right)
- if there's too much motion, turn on "reduce motion" in your accessibility settings
- I am pretty excited about dynamically showing related content in tools. eg showing incoming/outgoing calls when you're focused on a function in your editor
  - seems like a natural feature
