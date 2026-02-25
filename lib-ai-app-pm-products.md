---
title: lib-ai-app-pm-products
tags: [ai, pm, product-hunt, products]
created: 2024-12-07T09:50:59.442Z
modified: 2025-03-22T16:10:24.856Z
---

# lib-ai-app-pm-products

# guide

# ai-dev-xp
- tips
  - 🤔 旧的产品交互逻辑在新的时代都需要调整, 用户大多不想手动搜索, 直接在聊天框里输入指令，将搜索+后续工作一起执行
  - 🤔 不要执着于ai框架，主流模型厂商都会推广包含厂商特性的框架及产品(sdk + codex/claude-code/gemini-cli), 可专注于 主流 开源业务系统实现 或 厂商无关的实现
  - frontend: ai-sdk/chatbot, assistant-ui, librechat
  - backend: langgraph + python/nodejs
  - aisdk + docs/excel/image
  - ai-apps as ref: lasuite
  - ai时代的人工编辑, 可设计为特殊的human-in-the-loop
  - 一切通知/消息，都可以设计为 ai的chat+自动化工具
  - 之前的软件设计是面向用户、开发者，现在不得不重新设计，以大模型为使用者。 WebMCP的推进会让产品api快速发展

- ai-dev-xp
  - 难复现好的效果，同样的prompt+context，有时输出的效果就是不好
  - agent框架的tool-use实现对最新llm的支持，llm-provider的部署 都会影响llm的效果
  - ai适合快速生成草稿文本或原型, 但修改难

- ai相对于搜索引擎的优势 🌹
  - ai能推理和计算, 分析复杂问题，给出更准确的方案
  - ai能拆分复杂任务为多步任务，能通过多轮来执行任务，同时支持one-shot和multi-steps
  - 能通过tool-call使用工具
  - 对多语言支持很好

- why-local-ai? 🌹
  - stable model and stable api
  - privacy: code, data, 还可以跳过广告推广
  - tweak different configs for ai-models
    - 参考cline, 提供针对local场景的精简prompt
  - 避免模型平台的限制rate limits，如并发请求数(rpm/tpm/需要排队)、context长度、最大输出token数、模型版本、模型大小等
  - no implicit ai degradation/switch: bring your model
  - cost: unlimited tokens, local models支持超大context, 利用本地模型ocr/文生图
    - 文本模型有很多api提供商可选择，ocr模型的api可选择的不多，定制模型只能本地运行
    - 简单的 tool call 使用本地模型更高效, 可考虑将tool call小模型内置在软件中
  - 多模态的场景，本地可以对图片预处理，如压缩、裁剪、base64编码
  - 🤔 能充分利用本地文件系统和命令行的资源，进行数据分析/文件修改/...
  - network agnostic
  - 发挥端侧计算的能力，如总结/查询，而不侧重端侧聊天
  - 本地容易实现多种模型的切换和协作，如plan/act/ocr
    - mlx的并发端侧计算能力非常强, 多个mlx并行计算
  - 📕 local vlm ocr + pdf
- 🌹 pros-local-ai-mobile
  - 容易通过摄像头获取图像数据
- 🐛 cons-local-ai
  - 对计算资源的要求高，否则速度慢或效果差
    - mac的token-gen速度还行，但pp处理速度太慢，不适合coding, 勉强用来chat
  - 不同本地api provider实现的逻辑有差异, 有的api只支持ollama而不支持lmstudio
  - mac设备的prompt-processing速度特别慢, mac studio ultra能加快token生成速度，但context很长prompt很多时，本地的速度太慢了，甚至不能接受
    - 可通过支持外部大模型api来解决
  - 小模型不够智能
  - 不同任务需要不同模型，对于图片问答场景，需要根据硬件切换模型，需要专门优化
  - 移动端计算能力差, 速度慢, ipad的M系芯片非gpu方案也不快
  - 耗电量大, 对手机端不友好

- 需要针对local本地优化
  - 自动unload占用内存的image/llm模型, comfyui-lmstudio-node已实现了相关逻辑, 类似llama-swap 但同时支持文本/图片模型

- roadmap-ai
  - 针对国内免费api定制的chat/ppt/mermaid: 魔搭, 快手万擎
    - 可以~~fork janai,然后扩展provider~~, janai默认支持openai-like api，已经支持了国内models
  - 利用chrome最新的侧边栏，实现类似cline/roocode的页面ai助理/office编辑
    - 基于cline-cli/opencode的client/server架构，支持多种工具如 wps/飞书/腾讯文档/notion
    - 甚至结合文生图
  - distributed ai: 限制显卡生图、计算

- local-ai-challenges 🐛
  - 运行大模型需要较多硬件资源，如GPU/CPU/RAM
  - 本地模型的api很多通过gui如ollama/LMStudio提供，需要适配，同时不同GPU在默认token数、RAG处理方式上有差异

- agent-ipc

- markdown-stream
  - table-typewriter

- 基于ai coding实现产品
  - 优点: 功能强大，依赖模型的coding能力
    - 甚至可以考虑基于opfs的能力, 让ai实现类似文件转换的功能、python可视化导出, 甚至充分发挥compiler/interpreter的能力
  - 缺点: 输出的code缺乏类似markdown/xml的标准, 难debug/测试

- coding/claudecode-based ai products
  - 数据分析类，ai写代码、可视化，由代码驱动
  - 🐛 由代码驱动方案的缺点
    - 本地文件数据过大，无法读取完整数据
    - 数据字段如sales/Sales拼写错误

- 🔡 可是尝试用code generation的思路来实现ai产物如ppt
  - web sandbox + ai-coding > lovable ❓
  - sandpack ai? react-live ai?

- 🏠 ai-architecture: 
  - 架构及功能偏向 RAG(ragflow/quivr), 还是偏向 automation/workflow(dify/flowise/coze/sim)
  - 与ai的通信和计算是在前端实现，还是在后端实现
  - 🤔 一种思路: tool-call时使用擅长tool-call的模型，分析时使用公益站的聊天优质但无法tool-call的模型
  - 支持类似 roocode 的 model profile 切换
  - 🐛 前端和大模型直接对接的缺点: 关闭页面会丢失数据、流程中断、并发控制复杂
  - 🤔 why backend server
    - 消息持久化时，使用服务端id才方便消息保存与恢复、多人聊天一致性
    - 方便实现并发控制，特别是多任务
    - background-task
    - 方便在后端处理，避免cors跨域问题
  - ai在前端或后端的架构都和workflow工作流紧密相关
  - 在不同流程或阶段采用不同LLM的方案可参考 docling
  - 🏘️ 架构参考: gemini-cli/qwen-cli(依赖fs) + ui/copilot-chat + framework/langfuse
  - 基于dnd的方案偏前端，后端一般很难定制和scale，会受限于平台提供的组件和工具
  - ✏️ ai修改文档的方案 fast-apply
  - 偏展示型的项目考虑采用ai-coding的思路来更新ui，如sandpack/react-live+ai，更灵活
  - 使用AI gateway 来验证客户端的有效性, 避免被2api滥用
- 📡 roadmap
  - coding不适合同时编辑多个文件，但同时执行多个project的任务存在需求，特别是在本地硬件资源有限的条件下

- agentfs: 隔离性, 轻计算/自动化, 存储安全
  - 💡 ai操作数据库的新方案，agentfs，以bash的形式操作数据库, 对数据库友好
    - agentfs + worktree
    - lix-vcs + agentfs

- 🏘️ ai-backend/platform
  - providers-wrapper: models, communication+state, structured in/output
  - tool-call, MCP
  - streaming
  - caching
  - persistence/storage
  - memory: short, long
  - RAG
  - embedding: chunking, indexing, vector store/db
  - planning
  - ⛓️ workflow
  - 👥 multi-agent, sub-agent
  - parallel
  - manual orchestration: retry, routing
  - self-evaluation
  - human-in-the-loop
  - Observability: connection mgmt
  - prompt management
  - deep-research
  - rate-limiter
  - multi-modal: image, video
  - checkpoint/time travel
  - playground
  - dataset

- rag as a service
  - retrieval
  - code retrieval
  - text-matching
  - 类似 词典软件+词典mdx 的形式, 搜索软件+书籍pdf/epub, 产品价值参考context7

- office
  - excel/database generator
  - mindmap/drawio generator
  - ai-friendly format: 图片/图形中带有元数据
  - 用 ai ppt 的思路来编辑长文档，实现类似deep-research的文档

- image-gen-by-code
  - 文生图难度高，但基于文本的流程图难度低很多，如集成 mermaid
  - 基于代码的文生图方案，如sandpack, 可用于小红书卡片场景，可参考 https://langgptai.feishu.cn/wiki/JQVEwKJQkilWztkMLRGcA8zqngb

- 🖼️ image-generator/editor
  - 风格: 古风, Q版, 手绘(灵感/创意/草稿), 自然植物
  - 拆分图片和文字，提供更灵活的修改和编辑体验
  - prompts: bg, person/object, text
  - 模型选择要考虑: 硬件限制、速度、质量， 只有成熟的model才会提供lite/turbo/精简版
  - 一次生成多幅图
  - stream图片从模糊到高清的效果
  - 在线图片生成或编辑的架构, 涉及到模型下载与扩展下载，目前没有类似ollama的统一方案, 还涉及到GPU/CPU硬件支持，只有成熟方案才处理过相关问题，特别是文生图结合本地llm优化和推理的场景
  - 💡 针对AIGC优化的 image-editor 还存在市场生态位机会
  - 类似 pexels/unsplash/站酷 的图片资源站, 手动下载免费， api调用付费
  - 版权过期书籍: 绘画二创, rag搜索

- data-analysis
  - 基于cli的数据分析方案, 不与jupyter绑定

- workflow
  - Zapier and n8n help to an extent, but they’re not designed for multi-tenant SaaS. They’re great for internal workflows—not product infrastructure.

- ai-ui
  - 可交互，如过滤表格
  - 可编辑
  - 可对比
  - 流式render

- ideas
  - parallel chats
  - speed testing app for models
  - 相同参数下大模型的output结果不确定性很高， 若修改参数或更换embedding也会导致结果变化， 需要记录每次结果环境参数并提供复现方案

- 本地模型 + 数据下载/提供 的方案参考
  - 用户自己上传的pdf，就类似词典软件的词库
  - kiwix提供了wikipedia的各种子主题文章精选集合下载，如历史/地理/计算机/医学
  - linux文档

- model-tuning
  - 针对 中文表格/image 优化的模型

- dictionary
  - 针对可能拼错的词，推荐正确的词, 而不是显示不存在
  - 语料库: exams, wikipedia

- 
- 
- 
- 
- 

# draft
- rewrite open-canvas with langgraph
# 💎🚀 aichorage - local llm with joy, 提供模型API、rag可靠性、pdf文本操作
- selling-points
  - non-goals: local image gen
  - 易用性: 模型推荐 + 场景优化的提示词 + 多模型/多版本对比
    - 对同一场景, 如翻译/ocr, 针对不同模型内置合理的参数且支持配置
    - roadmap: 
      - agentic场景优化: ocr-vlm/pipeline, translation
      - citation, backlinks: 提升rag的准确度, 优化搜索结果中的code/text/image
      - pdf-editing: typst, formula, chart
      - 优化 windows版 coding-agent、模型推理、 rag依赖库
      - acp/WebMCP for pdf/rich-editing
      - translation
      - extraction
      - tts/stt/asr
      - editing-database, coding/table/image
      - chat2db
      - agent-browser
    - 长期难以被AI取代: 
      - 用户数据或模板资源
      - 计算集群
      - 硬件相关
      - 快速，高精度，稳定可靠
      - privacy
  - ✈️ local models support: mlx, lmstudio-alternative
    - 模型库: text模型, ocr模型, 翻译模型, t2i生图模型, tts, stt,  lmstudio在模型分类上做的不够好
    - 较少免费api的模型: ocr, stt
    - 参考janai/pipeshub, 既支持选择本地/api模型，也支持选择图片/文档
    - ocr/vlm comparison-matrix/playground: 识别对比, 翻译对比
      - ocr模型的输出统一为openai格式、统一标签(暂无标准)
    - AI异常后，human-in-the-loop的核心功能，还能用，还好用
    - 允许分享文档/插画中的模型配置/运行日志, 将prompt放入git-commit，还是直接放入图片?
    - ❓ 如何一键切换到cloud版
    - https://github.com/tc-mb/llama.cpp-omni is the first Omni multimodal inference engine built on llama.cpp.
    - modes config for ocr/rag/translation like cline-plan/act/ask
  - local agent
    - 支持同一个任务选择不同agent如claude-code/codex-cli来实现多个版本
    - 支持不同的cli来交叉验证
    - local/cloud agentfs-sandbox: agentfs impl for worktree
  - 🔗 citations for search: 外部数据源如字典mdx/书籍epub/wikipedia公开db/统计年鉴, 产品价值参考context7
    - 目前cli的搜索体验太差, 可针对 context/search-engine 结合 coding-agent 开发类似notebooklm的搜索体验
    - 查看原文pdf-parts时支持仅查看前后几页, 保护原文内容
    - 类似词典库/kiwix的预置模块, 可下载、可分享, 不必每次都全量索引
    - wikipedia zim 自动翻译为中文
    - vector-marketplace, 支持用户选择任意数量的pdf文档创建embeddings, 并发布, 可作为一种变通方案解决数据隐私问题
    - 行业应用: law, medical
    - sources: docs, emails
  - large pdf rag workflows: chunking-strategies, reindex, pdf-parts
  - 🌐 pdf edit
    - pdf ocr one-click eval like FlowDown
      - ui for popular ocr benchmark
      - personal bench suite like FlowDown
    - acp for pdf/rich-editing
    - diff without git
    - WebMCP for pdf/rich-editing
    - obsidian for pdf
    - proofreading: 一键检查, 版本历史
      - chunking viz
    - 还原图文混排
    - 提取 figure、表格
    - 👾 pdf-edit agent
    - ✨ 翻译场景的多种布局一键切换: 双栏对比布局, 仅译文布局, 富文本页面布局
    - 🌰 内置类似mineru/paddleocr的示例和提示词
    - multi-docs
    - 甚至可以通过多栏布局的交互，来展示pdf聊天或补充信息，优点是能展示在原文位置
    - 考虑同一文档的使用场景, 类似代码编辑器的 split view 也可以方便查看和核对
    - 方便原文和译文的跳转交互
    - toc autogen
    - pdf to word: ~~显示summary-per-page~~, 适合教育场景
    - pdf体验尽量与docs一致，包括view/edit
    - 统一 文本pdf 和 图片pdf 的体验，代码实现可以不同
    - ocr bench by claude-code
  - extraction
    - https://x.com/jerryjliu0/status/2026032764131451334
      - llamaindex: We built an AI agent that lets you vibe-code document 
  - office
    - multi-docs: work across documents
    - diff without git
  - history with localsandbox/agentfs
    - worktree
    - lix-vcs + agentfs
  - ai
    - split-view: 显示summary-per-page, 适合教育场景
      - summary的交互采用双栏布局交互还是类似comment面板交互需要考虑
    - progressive doc processing: 边处理/翻译，边查看，能展示文件被处理如翻译的进度和内容交互
  - translation+proofreading: 包括pdf文件, 普通文档、网页
    - 输出不同模型的翻译版本，供用户比对, 参考promptfoo
  - audio
    - 远端分析youtube/b站视频
  - 插画复刻: Qwen-Image-i2L, image-to-prompt-to-image, 同时支持浏览comfyui生成图片的元数据、提示词
    - 根据前文的图片生成风格类似的图片
  - local-optimized
    - 减少并发
    - 减少system-prompt
    - error-retry-for-small-model, more robust
    - 优化并行对话, 外部api并行，本地模型串行
  - token is cheap, 算力越来越不是问题, 现在需要做生态和产品
  - 💰 productivity
    - parallel tasks
  - gui
    - better revert/checkpoint
# 💎🚀 modelpedia - 模型参数对比, 历史评测结果, 能免费对比最新参数及上一个版本
- pm-eval/bench
  - 模型文档及参数都是on-paper, 可直接运行的测试集加上量化版本更适合实际效果, 是否存在产品空间

- 基本参数(card)
  - 模型列表
- 评测模型类别: text, ocr, image, embedding
- ✨ 官方评测结果, 历史版本
  - 模型厂商或知名评测机构(第三方)发布的结果
  - 标记被质疑的评测
- ✨ 开源评测(第三方)结果, 多个org的不同bench
  - llamabench
  - aider
  - 标记被质疑的评测, 标记有冲突的结果
  - 🤔 rerun benckmark, 自动将benchmark模型映射到ai-provider
- ✨ 速度与设备评测结果
  - 硬件厂商发布的模型评测数据
  - 同一硬件使用不同backend如vulkan/rocm/cuda的结果不同, 很难统一比较, 但可提供参考价值
  - 设备列表, 关联huggingface的模型id
  - mac专区, 多个型号, 多个模型
  - github工具收集的速度
  - 移动设备
  - 安装使用教程
  - [LocalScore - Local AI Benchmark](https://www.localscore.ai/)
- ✨ 场景测评
  - coding-前端: 天气卡片、贪吃蛇、三维地球
  - coding-后端
  - coding-代码迁移
  - translation: 翻译
- ❓ productivity 需要提供更多的生产力价值, 一键对比prompt、对比结果
  - 🤔 给出迭代优化prompt的建议
  - 推荐相关prompt参考
- 🆚 custom-comparison(功能花哨, 但不提供实际生产力)
  - 自动高亮最高值
  - 一键截图
  - 是否开放: 一键copy表格数据
  - 在线图片编辑
  - ai点评
- 🔗 citations/sources/papers
  - 提供数据来源, ai对内容相关性打分
  - 标记被质疑的评测
- ugc用户上传评测结果(共同维护/其他)
  - 论坛评测结果搜集, 可靠度confidence
  - github工具收集的评价
  - aichorage工具上传
- 其他讨论(场景效果/使用教程/精选)
  - tutorials/discussion: 仅提供链接，暂不提供数据库保存的原文, 但可使用ai-summary总结数据库的原文
  - 主动提供 playground + prompt 来复现
- ❓ playground-chat/ocr
  - 支持接入 openrouter/siliconflow 批量测试, 结果类似 promptfoo 表格, 支持分享测试结果, 一键rerun
- bench-source-code: reproducible
- futuristic/new-model-notification
- premium: ad-free, history, multi-comparison, ai-summary-online, auto-update-custom-compare-table
  - rewards: local-speed-uploads, 参数补充
  - ? api-usage? remote-control?

- 测试各项功能的参考
  - https://x.com/Lakr233/status/2014354022573178985

- windsurf arena mode 竞技场
  - [Wave 14: Arena Mode - May the Best Model Win _202601](https://windsurf.com/blog/windsurf-wave-14)
  - One prompt. Two models. Your vote.
  - 不告诉你模型，好像是为了让人工根据实际生成的效果来判断哪个模型写出来的效果更好。
  - 一般最新的(可能多个)模型作为挑战目标, 然后选择结果
  - [windsurf现在可以免费在竞技场用前沿模型了，持续一周 ](https://linux.do/t/topic/1548962)
    - 可以一次性得到两个结果选择你认为更好的，目前我选的基本都是 gpt 和 claude 更好..kimi 暂时没赢过，因为我没问前端问题

- bench-naming
  - modelpedia
  - modelbench
  - modeleval
  - modelxp
  - modelRated
  - modelReviews

- bench/reviews-like
    - G2/grid
    - Gartner, Capterra
    - Product Hunt
    - AlternativeTo
    - Slant
    - StackShare
    - Clutch
    - Google Reviews, 
    - TripAdvisor, TheFork, pitchfork
    - Rotten Tomatoes, Zomato
    - Trustpilot, TrustRadius
    - OpenTable
    - Letterboxd
    - Metacritic
    - La Liste
# 💎 llm-playground - 使用公益api的效率工具+api统计分析
- 公益版

- 企业版
# pm-mcp
- writing

- image-generation
  - 现在的ai产品很少将图片生成和编辑设计和实现的体验很好

- browser-use
  - computer-use
  - container-use
  - vscode-use, vscode-mcp

- ai-sandbox
  - 不仅用于代码，还可扩展到更多场景，类似manus
  - 在一台vm的前提下，能将ai执行任务的过程更具体的展示给用户，甚至邀请用户协作，甚至执行完将产物以用户熟悉的文件夹或预置软件打开给用户查看操作
# ai-editor
- drawio-use

- 不适合流式的数据
  - markdown-table
  - mermaid-graph
# ai-designing/image/ppt
- cursor for design: logo creator
  - 形态是否要基于vscode，产物是否要直接在vscode打开

- 使用ai实现高仿设计，是否可以绕过版权限制

- 版权过期书籍绘画的二创

- 🌰 nano-banana的体验

- 🌰 notebooklm-gen
  - 点击生成app时能手动编辑prompt
  - audio
  - video
    - 包含图片播放和语音讲解
  - slide
  - mindmap
    - 默认只展开一级节点，此时下载图片也只有一二级，需要手动点击才显示后续节点
  - infographic
  - report
    - 支持查看prompt
    - 不可编辑
  - flash-card
    - 卡片显示问题，点击显示答案
  - quiz
    - 多是选择题，可点击显示hint/explain
  - note: rich text notes
  - data-table
    - 支持 export to google sheets
- 🌰 notebooklm-slide-deck的体验
  - 默认生成的ppt包含14页
  - 生成slide deck的速度慢，缺少进度反馈
  - slides的每页内容都是图片，难以编辑，并且导出的体积大
  - 导出的格式是pdf，而不是ppt，难编辑
  - [Best Prompt for generating Slide Deck : r/notebooklm](https://www.reddit.com/r/notebooklm/comments/1psect8/best_prompt_for_generating_slide_deck/)
    - Here’s my trick. In NBLM, ask for an outline. Create the slides in NBLM. Download. Upload to slides and copy the outline to Canvas and ask to “create a presentation from this outline with a minimum of 30 slides -one thought per slide. I have attached a deck for inspiration. Use engaging visuals in my color scheme. Here’s the style: (font, font sizes, color hex codes).
  - [Need Help Converting Slide Deck/Infographic PDF to PowerPoint : r/notebooklm](https://www.reddit.com/r/notebooklm/comments/1pm2ucp/need_help_converting_slide_deckinfographic_pdf_to/)
    - I used Adobe Acrobat. Edit PDF andit recognizes the text and separates graphics. Its not perfect but gets you to 70%
  - [finally found a way to edit notebooklm slides lol : r/notebooklm](https://www.reddit.com/r/notebooklm/comments/1pbeq8d/finally_found_a_way_to_edit_notebooklm_slides_lol/)
    - Put the slides into Gemini. Activate the Canvas. Ask it to generate slides. Open in slides. It should be editable.
    - [Slide deck - possible to export as powerpoint? : r/notebooklm](https://www.reddit.com/r/notebooklm/comments/1p41at4/slide_deck_possible_to_export_as_powerpoint/)
      - Not NLM, but Gemini can now make slide decks in the canvas and export to slides. So you might chain something like: NLM export to PDF—>Upload PDF to Gemini to make slides in canvas—>Export canvas slides to gSlides —> export to ppt
# ai-lowcode
- tips
  - 基于dnd的方案偏前端，后端一般很难定制和scale
  - Zapier and n8n help to an extent, but they’re not designed for multi-tenant SaaS. They’re great for internal workflows—not product infrastructure.
# ai-workflow
- tips
  - 基于dnd的方案偏前端，后端一般很难定制和scale

- n8n open alternative
- langgraph-studio open alternative

- logicflow + ai
# ai-coding
- 玩具代码可用时，立即保存快照, 如果后面写乱了方便恢复

- 
- 
- 
- 

- [Compare Top AI IDEs & Coding Assistants | 2025 Reviews & Alternatives](https://www.aiidecompare.com/)

```markdown
- apps,       tabs,  chats, pricing
- cursor,     2k,    50,    $20
- windsurf,   any,   100,   $15
- trae,       5k,    1000,  $10
- gh-copilot, 2k,    50,    $10
- gemini-cli, 180k,  240x30,$10/1M-tokens
- amazon-kiro,any,   50,    $19   

```

- pm-coding
  - 将ai-prompt保存在git commit，方便查看历史, 也方便区分human-edits/commits

- [智能编码助手通义灵码 产品文档](https://help.aliyun.com/zh/lingma/)
  - [价格-通义灵码](https://lingma.aliyun.com/pricing)
  - 个人专业版为限免阶段，所有用户均可享受个人专业版服务，限免期结束后，也会对所有开发者免费提供个人基础版服务，限免周期暂未确定

- roadmap
  - 1. human-in-the-loop
  - 2. self-correction, auto-debug
  - 3. async-workflow
  - 4. idea-to-launch, 类似manusAi, 基于类似个人云桌面底层实现的助理
  - 5. value as a service

- 可以使用ai协助将代码库从一种语言转换到另一种语言
  - 甚至用ai将GPL协议的代码重写成自己的代码

- ai写与第三方sdk集成的代码时，先写注释example，再写代码

- [腾讯云代码助手 CodeBuddy](https://copilot.tencent.com/ide/)

- [CodeFlicker ](https://www.codeflicker.ai/)

- [通义灵码 ](https://lingma.aliyun.com/)

## ai-coding-draft

- lib-port
  - pdf: PyMuPDF(AGPL), python-docx(AGPL)
  - image: poppler

## ai-coding-xp

- 实测用 claude-opus-4.5 和 glm-4.7 将同一个项目从vue迁移到react，
  - opus只存在很小的vite配置错误，修复后可以运行
  - glm-4.7存在很低级的jsx未闭合、css属性值的引号未闭合这类低级问题，但自己也可以修复
    - glm-4.7在处理monorepo的import路径、vite方面明显不如claude-opus
# ai-office
- 产品方向: ask、生成、集成
  - core-features: improve, shorter, longer, fix/checker, translate

- ai-ppt 🌗
  - 🔡 尝试用code generation的思路来实现ai ppt
  - 🎞️ 基于演讲视频生成视频中的ppt, 还原ppt内容

- 
- 
- 

- google-docs-ai
  - [How to Use AI in Google Docs - Numerous.ai](https://numerous.ai/blog/how-to-use-ai-in-google-docs)

- notion-ai
  - [Everything you can do with Notion AI](https://www.notion.com/help/guides/everything-you-can-do-with-notion-ai)
    - Notion AI helps you find information, create content, understand data, and chat - without ever leaving Notion.
    - Analyze files and images
    - Access information across your integrated apps like Slack & Google Drive
    - Limit your search to trusted knowledge sources

- [Project Idea: Using an AI face search to find data leakage in RAG source repositories. : r/ChatGPTCoding](https://www.reddit.com/r/ChatGPTCoding/comments/1oq4p2s/project_idea_using_an_ai_face_search_to_find_data/)
# ai-hardware/硬件
- 智能家居
  - 各家设备

- 国产显卡
  - 华为昇腾, 摩尔线程, 砺算科技

- 
- 
- 

# ai-dev-xp
- 当一个复杂问题让ai折腾了1h还没解决，不要继续纠结，赶紧换更强的模型
  - 让ai动手前自己先拆分任务，不要让ai分析复杂的任务，ai分析不清会乱改增加工作量，自己可以主动mock状态和对象
  - 有时使用搜索引擎默认的ai结果又快又好，可以尝试解决类似stackoverflow类型的问题

- 让ai将从日志平台复制来的残缺字符串补全为合法字符串并格式化缩进，速度很快很好用
# ai/llm-api 👾
- api-choices
  - 支持的优质大模型、热门模型、vlm
  - api稳定: production用的api稳定性必须要高，否则产品体验差
  - 速率限制
  - 工具集成支持: cline, roo, librechat
  - 另一种思路， 新开的商业站一般会限免最新的模型和热门模型，也可以用来测试

- resources
  - https://github.com/cheahjs/free-llm-api-resources

- news
  - [OAI-FREE](https://newapi.zhx47.xyz/pricing)
    - [LinuxDo 社区福利活动](https://campaign.zhx47.xyz/)
    - [OAI-FREE 签到发送订阅 ](https://linux.do/t/topic/1632349)
    - 都是临时渠道，不开签到了，直接每天送 100 刀余额
  - [讯飞的GLM-4.7免费用 _202602](https://linux.do/t/topic/1573384)
    - 限免至0305, 20qps
    - [讯飞星辰MaaS平台](https://maas.xfyun.cn/modelSquare)
  - [华为云 CodeArts 试用期间开放GLM4.7与DeepSeek V3.2模型无限畅用，大善人还是小白鼠？ _202601](https://linux.do/t/topic/1536794/5)
  - [寻找L站开源作者，UUcode送商业级API额度—— 优质开源项目扶持计划 1228](https://linux.do/t/topic/1370667)

- claude-news
  - [Ollama v0.14.0 and later are now compatible with the Anthropic Messages API _202601](https://ollama.com/blog/claude)
  - [魔搭免费api接口支持Anthropic API可直接用于claude code附教程 _202508](https://linux.do/t/topic/876488)
    - 模型库里面有的模型可能不支持，k2好像也不行，试了glm4.5和qwen3都可以

- tips: 公益站不稳定(3个月就倒闭一批), 来源不明可能导致效果差, 需要经常确认和维护, 不要浪费过多时间
  - 🤔 一种思路: tool-call时使用擅长tool-call的模型，分析时使用公益站的聊天优质但无法tool-call的模型
  - 🤔 与其花时间签到游戏，不如研究2api和反代; 比较 公益站的配置折腾 / 反代的配置及更新
  - coding方案还可使用 ccr 转换 qwen-code-cli
  - 是否需要统一管理公益站，不同站点的安全盾绕过方式不同，模型名不同，api分组名不同，key的有效期不同
  - 有的api不能显示thinking内容
  - 模型不断更新，落后的公益站会逐渐淘汰
  - 公益站主页模型广场展示的可用模型不准确，可以在控制台的playground直接测试，异常会直接抛出
- 免费api的技巧: 在知乎/小红书直接搜索 免费 claude (公益站), 就会有最新的api推广信息, 可以用小号邀请自己
  - 公益站 [Search results for '公益站' - LINUX DO](https://linux.do/search?q=%E5%85%AC%E7%9B%8A%E7%AB%99%20order%3Alatest)
  - [L站免费AI汇总 ](https://linux.do/t/topic/638821)
    - [LD OPEN HUB — 公益站导航](https://ldoh.105117.xyz/)
    - [站内公益站汇总 ](https://linux.do/t/topic/1398351)
      - 公益站的域名被集中泄露遭到集中的打击
      - 跑路，黑与白，薄荷，wong，elysiver，都是可以kilo的。cline和roocline不懂
      - 👀 不要花费过多时间，有站点会不定期清理不活跃账号，如 windhub/Fovt
    - [模型中转状态检测](https://check.linux.do/)
    - [L站的佬友们应该早已经 token 自由了吧 ](https://linux.do/t/topic/1397594)
    - [最新福利羊毛话题](https://linux.do/c/welfare/36)
    - [All-API-Hub：开源AI中转站集中管理和自己的New API增强管理，基于 one-api-hub 大幅重构增强 _202511](https://linux.do/t/topic/1001042)
    - [关于部分公益站支持CC的测试，欢迎更多反馈 ](https://linux.do/t/topic/1162888)
  - 📌 [duckcoding 公益站](https://free.duckcoding.com/console/personal), 签到
    - [DuckCoding](https://duckcoding.com/console/personal)
    - [DuckCoding Az-CC，单独开启公益站，只允许L站注册 ](https://linux.do/t/topic/1308120)
    - [status](https://status.duckcoding.com/status/duckcoding)
  - [claudex-反重力号池](https://code.claudex.us.ci/panel)
    - [claudex-反重力号池](https://claudex.us.ci/console/personal), 签到
    - [【福利】公益福利，反重力Opus4.6踩油门（只要没爆会继续延长) ](https://linux.do/t/topic/1542040)
    - 纯公益反重力池子，无套路 L 站 2 级直登，加了 CF
  - 📌 [Any Router](https://anyrouter.top/), 每日签到获取$25
    - 仅支持coding工具，不支持使用api聊天
    - 本站直接接入官方 Claude Code 转发，无法转发非 Claude Code 的 API 流量
    - 无充值，邀请注册来获得更多额度
    - tg群讨论的内容看，作者似乎精力不在anyrouter而在开发商用产品
    - 用户较多，有提供vscode插件无法使用的解决方案
  - [Agent Router](https://agentrouter.org/console), 每日签到
    - 转向商业
    - 模型支持 Claude Code、Codex、RooCode、Qwen Code、Gemini Cli 等多款工具
    - 仅支持coding工具，不支持使用api聊天
    - > 签到功能在哪里呀？ 退出登录重新登陆就好了. 
    - [AgentRouter 问题汇总 · Issue · millylee/anyrouter-check-in](https://github.com/millylee/anyrouter-check-in/issues/48)
      - agent 是在登录的时候签到的，并没有额外的 sign_in 接口，是在登录的那个接口是返回了一个check_in 的字段判断的，所以才把cookie 时间给调短了，就是让重新登录签到才有效
  - [Code Router](https://api.code-relay.com) , 无法签到和更多额度
    - [Code Router](https://api.codemirror.codes/)
    - 支持 Claude Code & CodeX
  - [SWT-API](https://api.lhyb.dpdns.org/), 无限额度, 无需签到
    - [备用站](https://new-api.koyeb.app/)
    - [免费众多模型公益api站  ](https://linux.do/t/topic/1106811)
    - 公益站干一两年了，都是白嫖的api
    - 现在Gemini的模型都用不了了，我也进不去主站了，副站也进不了，备用站无法登陆
    - [200刀用完关停](http://152.136.137.130/pricing)
  - [123nhh](https://new.123nhh.xyz/pricing), 余额多
    - 模型来源谷歌反重力，rpm限制10/3min，不可用于NSFW，酒馆等
    - 模型不稳定，经常异常再恢复再异常
    - [【nhh公益站】介绍贴及主贴  ](https://linux.do/t/topic/1370326)
    - [模型中转状态检测](https://status.123nhh.xyz/)
  - [Wind Hub](https://windhub.cc/panel/model_price), 农场
    - https://api.224442.xyz/panel  /legacy
    - [福利站](https://wcdk.224442.xyz/)
    - 提供了free分组，包含deepseek-v3.2, gpt-4.1-mini
    - cc分组倍率0.6
    - 活跃任务检测：窗口=600s，活跃任务槽位=8（阈值>5），疑似异常并发/自动化（辅助指标）
    - [[Wind Hub]新的公益API 主帖 ](https://linux.do/t/topic/1344450)
  - 📌 [薄荷 API](http://x666.me/console), 每日签到
    - 改了下速率限制。现在变成5分钟25次，对自动化和roocode这些用户变好了很多
    - [薄荷公益站签到](https://up.x666.me/), 模型一次调用 0.002
    - 模型丰富: claude, gpt, gemini
    - [薄荷公益站主贴 ](https://linux.do/t/topic/1170760)
    - 支持cline/roo/cc
    - Gemini 的模型是支持三种格式的： Gemini 格式（带原生和搜索）, OpenAI 格式, Claude 格式（能 CC？）
    - 反重力和veterx逆向的锅，claude对open ai格式调用问题，用cline系的产品吧，比如roo或者kilo
    - [请问薄荷怎么才能用Claude Code ](https://linux.do/t/topic/1304580)
  - [WONG公益站](https://wzw.pp.ua/console/topup), 每日签到
    - [WONG公益站](https://wzw.de5.net/console)
    - [WONG公益站](https://newapi.netlib.re/)
    - rpm为30
    - 高效连接 Claude Code CLI
    - [【WONG公益站】弄个主贴 ](https://linux.do/t/topic/1179964)
    - 不要对模型进行测试，测试失败不是因为服务不可用，是我禁掉了测试
  - [随时跑路公益](https://runanytime.hxi.me/console/personal), 每天签到
    - [随时跑路福利站](https://fuli.hxi.me/wheel)
    - 完全支持 cc，主要是 sonnet 4.5，haiku 4.5 会自动重定向到 sonnet 4.5
    - RPM 暂时定为 5，之后看情况调整
  - [Elysiver](https://elysiver.h-e.top/console/personal), 站内签到
    - 支持embedding model
    - [模型健康度监控](https://elysiver.h-e.top/model-health)
    - [Elysiver 添加 Nanobanana Pro 啦 _202601](https://linux.do/t/topic/1506018/16)
      - 是 business 2api
    - [『Elysiver公益站主贴』 ](https://linux.do/t/topic/1175087)
    - 2cx 指接入 Codex 使用
    - docs 指的是这是 claude 的文档 ai，不破限只会回答文档相关的内容
  - [ThatAPI](https://gyapi.zxiaoruan.cn/console/personal), 签到
    - 有多个cc分组，IP限制严格(无需gfw)
    - 免费提供 glm flash
  - [太子公益 API](https://api.codeme.me/console/personal), 签到
    - cc支持
  - [Old API](https://sakuradori.dpdns.org/console/personal), 签到
    - [Old API](https://oldai.zeabur.app/console/personal)
    - [【old API公益站】公益站上线（已恢复？） ](https://linux.do/t/topic/1541085)
    - rpm 为 25，还是老样子小容器部署，服务稳定性未知，随时可能因为账号短缺、高并发而死掉
    - 仅支持 sonnet 和 haiku，等 kiro 恢复 free 用户的 opus 使用权后会上 opus
  - [小呆API](https://api.daiju.live/console/personal), 签到，api不稳定
    - [小呆API](https://new.184772.xyz/)
    - cc支持
    - [农场](https://game.daiju.live/)
    - [小呆公益站 要不要claude模型这件事 ](https://linux.do/t/topic/1424755)
  - [Hotaru API](https://hotaruapi.com/console/personal)，签到, 不定期清理
    - https://api.hotaruapi.top/console/personal
    - codex
    - [〔Hotaru公益站〕新的公益站启动 ](https://linux.do/t/topic/1398297)
  - [KFC API](https://kfc-api.sxxe.net/console/personal), 签到
    - Claude和gpt 暂时不支持工具调用, gemini模型没有pro
    - API 调用频率限制为 12RPM，公益站永久免费，采用公平限流策略以保障服务稳定
    - 别玩至尊场，1000积分一次警告扣16x，风险太高; 高级场的高积分也可以获得高收益
  - [Huan API](https://ai.huan666.de/console/personal), 签到, 生图模型
    - cc支持
  - [API分享站](https://new-api-bxhm.onrender.com/console/personal)
    - [【API分享站】公益站主帖 ](https://linux.do/t/topic/1355814)
    - 反代 kiro
  - [小辣椒 公益站～(～￣▽￣)～](https://yyds.215.im/console/topup)
    - cc
  - [真好记公益站](https://newapi.zhenhaoji.qzz.io/console/personal)
    - 随便刷吧，可能刷崩了，我就关站了
    - cc
  - [黑与白chatAPI](https://ai.hybgzs.com/), 每日转盘
    - 模型丰富: claude/gemini/codex
    - 很多openrouter渠道的模型
    - cc不支持tool, **cc渠道经常上架下架**
    - [黑与白chatAPI福利站](https://cdk.hybgzs.com/)
  - [ibsgss公益站](https://codex.ibsgss.uk/console/personal), 签到
    - [【ibsgss公益站】支持codex cli / cherry  ](https://linux.do/t/topic/1434464)
    - 维护期限：到 codex-team 渠道耗尽为止
  - [随缘API](https://newapi.tanmw.top/console/personal)
    - [【随缘API公益站】开放注册！余额已调整 ](https://linux.do/t/topic/1634879)
    - RPM:20
    - 目前只有 GPT 和 Grok 
    - 不保证稳定性！随时跑路
  - [Einzieg API](https://api.einzieg.site/console/personal), 签到
    - 仅提供codex模型
    - [【Einzieg公益站】再次启动 ](https://linux.do/t/topic/1569418)
  - [api-test](https://openai.api-test.us.ci/console/personal)
    - [开个小公益站测试一下 ](https://linux.do/t/topic/1414593)
    - [LDC Virtual Goods Shop](https://shop.api-test.us.ci/)
    - 包括 deepseek，硅基流动全模型，阿里云千问全模型，glm，gemini，codex
    - 有claude, 无opus
    - 默认 RPM30，1 级可注册，不允许批量测活
  - [GGBOOM公益站](https://ai.qaq.al/dashboard)
    - [签到控制台](https://sign.qaq.al/app)
    - [【GGBOOM公益站】签到站上线啦 ](https://linux.do/t/topic/1517772)
    - 本站点为codex中转站，不包含其他模型
    - sub2api的openai api仅支持 openai-responses API协议。不要选老版本的哦
    - [【GGBOOM公益站】 全面支持gpt-5.3-codex ](https://linux.do/t/topic/1581803)
  - [NPC API](https://npcodex.kiroxubei.tech/console/personal)
    - [[NPC-API]codex公益站开业 ](https://linux.do/t/topic/1564054)
  - [520 API](https://520.wcgio.com/console/personal)
    - gpt-5.3-codex 
  - [爱你公益站](https://x.ainiaini.xyz/console/personal)
    - [[爱你公益站]开站 ](https://linux.do/t/topic/1638562)
    - 暂时只有 gpt 系列，
  - [Codex - New API](https://codex.makeup/console/personal)
    - [又一个codex公益站，人手一个蹬  ](https://linux.do/t/topic/1645651)
  - [纳米哈基米](https://free.nanohajimi.mom/console/personal), 签到
    - Gemini Imagen
    - [【纳米哈基米 · 公益站】 支持香蕉Pro画图，Veo视频，Gemini全系模型 ](https://linux.do/t/topic/1512770)
  - [OAI-FREE](https://newapi.zhx47.xyz/pricing)
    - [LinuxDo 社区福利活动](https://campaign.zhx47.xyz/)
    - [OAI-FREE 签到发送订阅 ](https://linux.do/t/topic/1632349)
    - 都是临时渠道，不开签到了，直接每天送 100 刀余额
  - [玩票 API](https://api.361888.xyz/console/personal)
    - opus4.6 和 codex 虽迟但到
  - [sorai API](https://newapi.sorai.me/console/personal)
    - [codex公益站启动 _202601](https://linux.do/t/topic/1524003)
    - 只有 codex 模型
  - [lucky codex](https://codex-lucky.zeabur.app/console/personal), 签到 1-4 刀
    - [【lucky公益站】codex公益站  ](https://linux.do/t/topic/1616313)
    - 目前只有 10 个 team 号，所以可能随时跑路
  - [云端API](https://cloudapi.wdyu.eu.cc/console/personal), 签到, 生图
    - grok-imagine-1.0
  - [Neb 公益站](https://ai.zzhdsgsss.xyz/console/personal), 签到
    - 采用按量计费，每次0.01，注册送2000次，因为该阶段的初衷就是最大化利用这些将要过期的key。
    - 当前额度用完或2026.1.31之后进入第二阶段，采用按量计费，倍率会很低
    - 会不会有签到站不会，因为我太懒了
    - 之前想过接入CC，但是对于我这种新手来说调教整个流程还是太难了
    - [【Neb 公益站】这是主贴 ](https://linux.do/t/topic/1354122)
  - [北极AI大模型](https://bapi.outaucer.me/console/personal)， 签到
  - [Ciprohtna](https://anthorpic.us.ci/console/personal), 签到
    - [【Ciprohtna 公益站】上新 10 LDC = $100 一天订阅畅享包 ](https://linux.do/t/topic/1606615)
    - 注意！没有 opus，opus 在后台都会被重定向到 sonnet
  - [Jarvis API](https://ai.ctacy.cc/console/personal), 签到
    - 备用, [Jarvis API](https://jarvis.ccwu.cc/)
  - [八岁公益站](https://ai.xoooox.xyz/console/personal)
    - cc
  - [摸鱼公益](https://clove.cc.cd/console/personal), 可签到, 额度少
    - [【摸鱼公益】 自己的反重力和codex有一些不怎么用，开个摸鱼站给需要的用用 ](https://linux.do/t/topic/1513131)
    - 后续只能使用积分充值。随用随冲。
  - [WOW公益站](https://linuxdoapi.223384.xyz/console/personal)
    - [【已接入LinuxDO OAuth】老破小公益站复活 ](https://linux.do/t/topic/1516043/1)
    - 因站内目前不支持 Claude-Sonnet，所以接入 Claude Code 时需指定模型 ID 为站内可用的模型
  - [SNOW AI CLI](https://snowcli.com/dashboard/overview), 签到但余额仅当天有效
    - Kiro政策似乎有变化，Opus不稳定，但不是不能用，Sonnet和Haiku正常
    - 特别注意，Kiro逆向因为Token返回数据不精确，所以Snow CLI 无法准确判断自动压缩，根据经验，上下文到达25k~30K左右差不多就满了（这不是真的只有这么短）而是Kiro逆向没有返回缓存信息实际上下文可能非常接近200k了
    - [【Snow CLI】Console 开放部分注册人数，以及近期更新汇总 ](https://linux.do/t/topic/1568653/1)
    - 依旧免费提供稳定的 Kiro 逆向、Codex、KIMI 以及适用于 Codebase 的嵌入模型
  - [GLM 仪表板](https://pureai.shop/dashboard.html)
    - glm + qwen
  - [FovtAPI](https://api.voct.top/console)
    - 模型旧，模型少
    - [NewAPI签到系统](https://gift.voct.top/dashboard/checkin), ~~已失效~~
  - [FKAI](https://orchids.fuckai.me/dashboard), 无需签到
    - [【FKAI公益站】 ](https://linux.do/t/topic/1476184)
    - 额度每天刷新 
    - 根据论坛等级确定额度 等级 1 20000, 等级 2 50000, 等级 3 100000
    - 可用模型：claude, gpt
    - 在CC中效果不佳，更推荐作为日常对话
    - 这个网站最开始是给kiro写的，但生不逢时
  - [Mu. API 2026](https://demo.awa1.fun/console/personal)
    - cc支持
    - [「公益站」最终还是换成了 New-API _202509](https://linux.do/t/topic/927953)
  - [轻 API](https://lightllm.online/console/personal), 签到
    - cc支持
  - [DEV88公益](https://api.dev88.tech/console/personal), 签到-0.01
    - cc支持
  - [曼波API](https://ai.dik3.cn/console/personal), 签到
  - [ICAT公益站](https://icat.pp.ua/console/personal), 签到
    - [【公益站】ICAT公益站上线了 _202601](https://linux.do/t/topic/1461073)
    - 目前仅支持Claude Code相关模型，其他模型视情况再接入
    - 目前服务器是甲骨文的免费服务器，所以性能上有点一言难尽
    - [ICAT公益站可用状态](https://status.icat.pp.ua/status/icat-server-status)
  - [扣腚API](https://api.jonwinters.pw/console/personal), 
    - 每天15刀，0点重置
    - cluade 配置, 有多余的反重力小号 可以捐到号池里面
    - [CLI Proxy API Management Center](https://cpamc2.jonwinters.pw/management.html#/quota-public)
  - [Luckin 公益API](https://api.oaiapi.online/console/personal)
    - 所有模型均支持 沉浸式翻译
  - [a__i__d__r__o__u ](https://linux.do/t/topic/1513815), 无余额, 购买积分, 待删除, qzz, io
    - 到2.14可用，不可以使用opus和all,应该可以用于cc了（不会有莫名其妙报错）
  - [香草API](https://ai.xiangcao.de/pricing), 文生图
  - [六哥公益站](https://api.crisxie.top/), 文生图
  - [佬友API](https://lyclaude.site/console/personal)
  - [APIKEY_公益站](https://welfare.apikey.cc/console)
  - [XiaoYo](https://www.xiaoyo.cn/personal), 签到, deepseek多
  - [唔系唔系](https://claude.chiddns.com/console)
  - [foxhank - Claude Relay Service](https://cc.foxhank.cn ), 无法注册
    - [【CC公益站】尝试维护一个智谱的CC公益站  ](https://linux.do/t/topic/1108974)
  - [Fengye API](https://fengyeai.chat/console)
    - cc
  - [一个小站的 API 商店](https://one-api.ygxz.in/app/dashboard), 每日签到1刀内随机
    - 提供半公益的高质量 API 中转服务，始于202406
    - 无调用频率限制
    - 支持gpt5,claude,gemini
    - 部分模型倍率很高，可选按次计算版本, 如claude
  - [mmkg API](https://api.mmkg.cloud/)
    - 仅在每周五下午 18:00 至 21:00 开放，每周限量 100 人
    - 支持claude,gemini, 不支持gpt
  - [【公测开启】Kiro账号托管平台  ](https://linux.do/t/topic/1227895)
  - [莹のAPI](https://api.wpgzs.top/pricing)，模型贵
    - rpm15
    - [莹のapi 加油站](https://quota.wpgzs.top/), 鸡你太美，每天可转100刀到公益站
    - [公益站支持claude ](https://linux.do/t/topic/1351151)
  - [莹のapi & 随时升天](https://supersb.me/console)，模型贵
    - [随时升天的公益站](https://any.97819781.xyz/)
  - [KFC API](https://kfc-api.sxxe.net/console/personal)
    - [KFC API公益站 - 正式上线  ](https://linux.do/t/topic/1233747)
    - [逆水寒](https://api.sxxe.net/), 即将关闭
    - [逆水寒公益API——扬帆起航 ](https://linux.do/t/topic/1173036)
  - [包子铺](https://api.5202030.xyz/)
    - [包子公益](https://api.codeqaq.com/)
    - 只开放linuxdo lv2以上注册
    - 支持gpt,claude,gemini, 但没有gpt5(有mini)
    - [包子公益 - Baozi DoneHub](https://lucky.5202030.xyz/)
    - 每日普通用户可自行划转 200$ 到 newapi 站点
    - [【包子公益站】更新一个总的汇总贴。现在上线了newapi的分站 ](https://linux.do/t/topic/1124776)
  - [我爱996公益](https://529961.com/console)
    - [我爱996公益附属站 - 每日签到领取奖励](https://hub.529961.com/)
    - [【公益站我爱996一次】测试上线已接入LinuxDo ](https://linux.do/t/topic/1147448)
  - [GoGoGo公益站](https://api.chengtx.vip/console/personal), 签到可得20~50刀，0.2刀/次
    - [GoGoGo公益站启航：目标是刷爆gemini小破号池 ](https://linux.do/t/topic/1494070)
    - rpm-15, 不限用途，可酒馆
    - 模型: gemini-2.5/3-flash/pro
    - 渠道是自部署gemini business2api，自己域名邮箱注册的，放了100多个号
  - 🗑️ [b4u API](https://b4u.qzz.io/console), 每日转盘, 关站20260222
    - 会不会增加其他模型: 不会，本站专注于Claude
    - 不支持opus
    - 支持工具调用、上下文 128K+、支持 RooCode，不推荐接入 ClaudeCode
    - 普通用户：每次 1 刀、RPM=10
    - 渠道技术： Claude-SessionKey号池→claude2api→FC使能
    - [转盘抽奖](https://tw.b4u.qzz.io/)
    - 仅每周六晚21:00至21:30限时开放注册
    - [【B4U公益站】是克劳德，我们有救了！（每周六限时开放注册） ](https://linux.do/t/topic/801848)
    - [[B4U]如何 配置 claude code ](https://linux.do/t/topic/1068671)
    - 需要ccr，而且工具调用不稳定。  反正我b4u聊天经常被断，所以只能简单的写个代码修改个东西
    - [B4U2CC：让B4U支持Claude Code＋思考 ](https://linux.do/t/topic/1285981)
    - B4U2CC 是一个Anthorpic Message 格式到 Openai Chat 的桥接器，无需上游支持FC, 就能实现接入Claude code并支持启用thinking
    - 不止支持b4u，任意支持openai chat格式的模型都可通过b4u2cc接入claude code，如果模型是claude的话还能启用思考
  - 🗑️ [Privnode](https://privnode.com/)
    - free分组支持claude-code，也支持gpt-5-nano
    - https://pro.privnode.com/
    - [【Cone 公益站】找个佬共同维护  ](https://linux.do/t/topic/1035525)
    - [Cone 公益站更新 ](https://linux.do/t/topic/1002152)
  - 🗑️ [无言AI](https://aiai.li/panel), 每日签到, 已关闭
    - 支持cc
  - 🗑️ [23公益站](https://sdwfger.edu.kg/console), 已关闭
    - 平台将于每周五、周六统一发放额度兑换码 
  - 🗑️ [tbai API](https://tbai.xin/), 已关闭
    - 模型支持gemini/gpt, 不支持claude
    - API调用频率限制为 10 RPM
    - gpt-load 作者
    - [【T佬公益】TBAI公益站主贴-爽用Gemini|OpenAI|DeepSeek模型 ](https://linux.do/t/topic/683726)
  - [VoAPI公益站](https://demo.voapi.top/), 每日签到, 
    - [【首发更新】全新API分发和管理系统-VoAPI ](https://linux.do/t/topic/218662)
    - 曾经的帐号已注销，需要重新注册
  - [~~Cats API~~](https://catsapi.com/), 已关闭
    - API调用频率限制为 15 RPM
    - [【猫猫公益】API使用说明 ](https://linux.do/t/topic/851028)
  - [RawChat公益站点](https://chatgptplus.cn/)
    - 免费的共享ChatGPT账号
    - [RawChat公益站点](https://sharedchat.fun/)
    - [HammerAI公益站](https://hammerai.vip/)
  - [Claude免费镜像号池](https://share.claude.best/)
    - 若无法对话了，说明对话额度被其他朋友用完了（需要你更换其他账号或者等待额度刷新）
    - [RawChat公益站点 kelaode](https://kelaode.ai/)
  - [cupsfunny API](https://free-llm.cupsfunny.com/)
    - 支持cluade, gpt5, 其中gpt5全免费(但经常429响应异常)
    - 每位用户RPM为2
    - 借助Toolify项目实现了函数调用，可以用于Claude Code
    - 如果增加额度和申请Claude的留言我没有及时回复，可能只是我不在而已，可以再等等 
    - Sonnet模型每次调用消耗两次使用次数，Opus每次调用消耗四次使用次数
    - [公益大模型API接口 - 小欢博客 - Fly your dreams](https://www.cups.moe/archives/free-llm-api.html)
  - [yx](https://api.dx001.ggff.net/pricing)
  - [方舟API](https://www.yxaiapp.com/)
  - [YesCode](https://co.yes.vg/)
    - [YesCode test](https://cotest.yes.vg/)
    - [【YesCode公益测试站】Claude Code/Codex 长期免费测试 ](https://linux.do/t/topic/964164)
  - [银河AI](https://mmaqq.top/console)
    - 需支付宝付费
  - [cone Veloera Zone](https://zone.veloera.org/)
    - 此服务完全免费提供，并仅在 LINUX DO 社区宣传
    - 不定期删除 0 额度，0 消耗，且注册超过一周的用户。
  - [SLA API](https://www.sla-api.zone.id/)
  - [ZenscaleAi](https://gy.zenscaleai.com/)
    - 仅提供gemini模型
  - [小丑Ai公益站](https://gy.jiubanai.com/)
    - 仅提供gemini模型
  - [小松公益站 New API](http://api.lanapi.top/pricing)
    - 仅提供gemini模型， 满血版
    - 默认分组只有5分钟3次的请求速率，至尊分组无上限分组
  - [素墨API —— AI公益站](https://apifree.rensumo.top/)
  - 🗑️ [翰林文苑公益API站点](https://aiapi.hlwy2025.me/)
    - 价格太高了 我决定攒到1000再用
  - [SillyDream 公益站](http://ff.sillydream.top/pricing)
  - [linjinpeng Veloera](https://linjinpeng-veloera.hf.space/)
    - 现在rpm是6，模型全部免费，1级即可注册
    - 一次一美元的调用，但是这个1美元是无限刷新的，你用了就知道了
    - 聊天记录均留样检测，违规直接封禁，请不要对话任何隐私信息
    - [能否成为全站用量最大的claude 4.1 opus公益站 _202509](https://linux.do/t/topic/956435)
  - [learn-ai 公益站点](http://free.learn-ai.top/), 需要签到且额度很少
    - 支持的模型质量较低: 很少一部份claude模型, gpt-mini/nano
    - 可以加入付费站点：https://learn-ai.top/
  - [LLM API 公益站](https://llm.indrin.cn/)
    - 本站永久运营，服务免费提供个人使用,禁止高并发,禁止高输入, 高并发会封号
    - 额度不限量,注册送$30，邀请送$5,正常用户额度快用完时会给后台增加
    - 不支持claude，支持openai, xai
  - [归一](https://ai.luuu71.dpdns.org/pricing)
    - gpt5
  - [TudouAPI](https://www.tudou.chat/), 签到复杂
    - 如果账户连续3天以上都是只有5-10条， 会判定为屯额度账号签到失败
    - 支持claude, gpt
  - [Becode 公益站](https://becode.be-a.dev/)
  - [88code - 企业级Claude Code/Codex中转](https://www.88code.org/)
    - 添加客服领取 10 美元免费额度, 每个用户仅限领取一次
  - [AICodeMirror官方共享平台 - 中国用户专属AI编程助手](https://www.aicodemirror.com/)
    - 每月 2000积分
    - 因成本大幅上升，免费用户暂不开放体验。后续开放时间另行通知
  - [一叶知秋API](https://88996.cloud/)
    - 本站已勉强运行 1020 天
  - [cto.new ](https://cto.new/)
  - [Claude 4.5 国内免费使用指南 | 最全访问方式汇总 2025 - 知乎](https://zhuanlan.zhihu.com/p/1956204058139431066)
    - 镜像、中转、合租、代充
  - [2025年10月 Claude 国内使用指南（支持 Claude Sonnet 4.5） - 知乎](https://zhuanlan.zhihu.com/p/1940070586635223559)
  - [白嫖最强AI编程模型Claude 4.5，暨一哥Claude Code的免费下位替代（10月22亲测可用） - 知乎](https://zhuanlan.zhihu.com/p/81947374736)
  - [求推荐免费模型api，公益站付费的太慢了，只是用于ai中文翻译成英文，速度有要求 ](https://linux.do/t/topic/1061766)
  - [长期收录靠谱稳定长期免费AI （API）Claudecode等 实现 AI 自由](https://www.nodeseek.com/post-450243-1)
    - https://github.com/CyYxl2024/freeai
    - 只收录商业平台。
  - [【项目自荐】一个免费使用Claude AI纯公益号池镜像站 ](https://github.com/ruanyf/weekly/issues/8047)
  - https://x.com/search?q=claude%20%E5%85%AC%E7%9B%8A%E7%AB%99&src=typed_query&f=live     /搜索最新公益站
  - https://github.com/chatanywhere/GPT_API_free
    - 免费ChatGPT&DeepSeek API
    - 免费API Key限制200请求/天/IP
  - [【Check-CX】监控站正式上线啦！现已加入LinuxDo元宇宙豪华套餐 ](https://linux.do/t/topic/1286480)
    - https://check.linux.do/
    - 之前 @Dean 佬做了一个富可敌国商家评价平台，我心血来潮：能不能做一个富可敌国商家模型渠道监控站呢？
    - 前后端代码全部开放，检测逻辑一目了然
    - https://github.com/BingZi-233/check-cx /MIT/ts

- api-bookmarks
  - [agentify API](https://api.agentify.top/pricing)
    - [H800 公益站回归！200tps 的 gpt-oss-120b 继续不限量免费用 ](https://linux.do/t/topic/1356689)
      - 模型部署在两张 H800 上面，人少的时候可以 200tps
      - 还加了一些 openrouter 的免费模型也几乎不限量
  - [做点长期公益，nvidia nim 大部分开源模型 + OpenAI免费模型的gptload ](https://linux.do/t/topic/1427060)
    - 搭建了一个gpt-load负载站：
    - NVIDIA NIM
    - OAI-Free: gpt-5-nano, GPT-4.1-mini
    - https://independent-adrea-mtg-154afb72.koyeb.app/proxy/nvidia
    - https://independent-adrea-mtg-154afb72.koyeb.app/proxy/openai
    - GALAXYPUBLICAI1984282

- embedding
  - [embedding New API](https://router.tumuer.me/)
    - [[Embedding 公益站] 专门提供 Embedding API 的迷你站 ](https://linux.do/t/topic/1385442)
    - 服务器在国外，所以需要使用魔法
    - [Embedding API 使用指南](https://embedding-docs.tumuer.me/)
    - 来自 gemini, vertex 渠道的后来几天陆续添加。
  - [【求助】寻找一个嵌入模型的公益站 ](https://linux.do/t/topic/1637724)

- llm-ui/apps
  - [SmallAI](https://free.smallai.asia/chat)
    - 基于lobechat实现
    - [【网站自荐】SmallAI公益站——免费使用GPT4o mini，支持多模态 ](https://github.com/ruanyf/weekly/issues/4969)
  - [AI对话 - db的AIGC站](https://ai.feles.town/chat)
  - 💰 [GoAmzAI - 个人、团队、企业私有化、运营的AIGC平台解决方案](https://d.goamzai.com/)
    - https://github.com/Licoy/GoAmzAI /非开源
    - https://github.com/VoAPI/VoAPI /仅提供docker-compose.yml
    - [AI对话 - GoAmzAI Plus](https://demo6.goamzai.com/chat)
    - [对话 - GoAmzAI Pro](https://prodemo6.goamzai.com/chat)
    - [goamzai已集成LinuxDO Connect，演示站开放给L佬们使用 _202406](https://linux.do/t/topic/122462)
    - [【公益AIGC】最适合日常使用的公益站，高级AI工具一网打尽 ](https://linux.do/t/topic/1175890/37)
      - volo api 吧，基于 new api 改的，但是 v1 开始好像就完全重写了
      - VoAPI 一直是闭源的，甚至好像只放出 Docker 的部署方式，连编译后的可执行文件都不发布的，截止到我最后一次看时是这样的，不知道后续有没有改变和有没有收费计划
  - [WorldOF](https://worldof.onrender.com/)
    - [GPT5、gemini2.5 Flash 的不限量无需登录的 API 来了，应该刷不死 ](https://linux.do/t/topic/1443674)

## image-gen 🖼️

- modelscope对部分模型提供了免费生图的额度, 如z-image-turbo

- [Cogview-3-Flash - 智谱AI开放文档](https://docs.bigmodel.cn/cn/guide/models/free/cogview-3-flash)
  - 智谱推出的免费图像生成模型，能够根据用户指令生成符合要求且美学评分更高的图像
  - 支持多种分辨率，包括 1024x1024、768x1344、864x1152、1344x768、1152x864、1440x720、720x1440 等

- image-api
  - [云端API](https://cloudapi.wdyu.eu.cc/pricing), 签到
  - [Huan API](https://ai.huan666.de/pricing)
  - [香草API](https://ai.xiangcao.de/pricing)
  - [六哥API站](https://api.crisxie.top/pricing)
  - [pollinations.ai](https://enter.pollinations.ai/)
    - [基于Pollinations的图像生成接口的工作台  _202601](https://linux.do/t/topic/1423187)
    - 1 额度可生成张数: z-image--5k, sdxl--3k, seedream--25
    - 已经被阉割了，现在免费的生图质量极差
  - [啾啾小铺](https://api.usegemini.xyz/pricing)
    - [NanoBananaPro 4K生图公益 ](https://linux.do/t/topic/1486971)
    - 注册送100额度，用完重新注册即可; 不要走 linux.do 渠道注册就好了
    - 逆向的flow接口
    - 模型名如下：gemini-3.0-pro-image-landscape,gemini-3.0-pro-image-portrait,gemini-3.0-pro-image-square
    - 由于目前flow官方流量大，官网都生不了图，佬友们等会再蹬
  - [图片生成](https://pam-carrier-korean-chemicals.trycloudflare.com/)
    - [nanobanana公益站 ](https://linux.do/t/topic/1616133)
  - [TS-AI | 灵感创作工坊](https://linux.tsart.lat/workspace)
    - [【绘画公益站】TS-AI  ](https://linux.do/t/topic/1641029)
    - 每天签到可获得 3000 积分（三天内有效）

- image-saas
  - [小白生图 - AI Image Generator](https://catsapi.com/)
  - [AI 生图平台](https://ztu.ai/)
    - 每天5张免费
    - [【公益站】ztu.ai 视频生成上线 _202601](https://linux.do/t/topic/1507837)
  - [RyanVan Z-Image | AI 图像生成](https://ryanai.org/)
    - 每天5张免费
    - 排队时间可能较长
  - [RyanVan Z-Image | AI 图像生成](https://txt2img.1771177.xyz/)
    - [[Z-Image公益] 跟随R佬脚步，闲置显卡分享zimage ](https://linux.do/t/topic/1643183)
    - 按照教程通过 gpu-worker 的方式接入了 R 佬的节点。目前本地跑的是 fp8 量化版的 z-image-turbo 模型，实测生成一张 1K 图片 15 秒左右。
  - [Z-Image 控制台](http://image.dx001.ggff.net:8080/dashboard)
  - [香蕉皮 AI](https://nanobanana.xiao.mom/)
    - [NanoBananaPro支持4K、免费无限制，轻蹬 ](https://linux.do/t/topic/1401748)
    - 在家逆向了一个NanoBananaPro香蕉皮AI，支持4K，不用登录，不限次数
  - [Nano Banana Pro - Free AI Image Editor & Generator ](https://www.nanaai.app/)
  - [最新公益绘画API ](https://linux.do/t/topic/599258)
    - 百度绘画
    - 豆包绘画
  - [Dreamifly - 免费AI绘画在线生成工具 | 一键生成动漫、插画、艺术图](https://dreamifly.com/zh)
    - 由全国30台家用电脑的闲置4090显卡，免费无限制提供分布式算力支持
  - [FluxEz - 免费的文生图网站](https://flux.comnergy.com/zh)
    - 提供完全免费的生图服务, 无需注册
  - [Seedream AI - 免费在线AI图像生成器](https://seedream.pro/zh)
  - [Cloudflare Workers AI Models](https://developers.cloudflare.com/workers-ai/models/)
    - 提供免费的文生图模型: sdxl, sdv1-5
  - [Free AI Image Generator - AI Free Forever](https://aifreeforever.com/image-generators)
  - [Free Gemini Pro](https://freebanana.pro/)
    - 速度慢
  - [FreeGen 白嫖图片生成器](https://hachimiai.dpdns.org/freegen/)
  - [SoraApi](https://api.67.si/)
    - 不可用
  - [呜哩AI，一站式AIGC创意平台](https://wuli.art/generate)

- image2api
  - [Antigravity的反代的Nano Banana用不了了 ](https://linux.do/t/topic/1419858/2)
    - 下午都很慢。晚上1点后一般都快些
  - [Libre Assistant](https://libreassistant.vercel.app/)
    - [又一款免费无限用的生图及对话LLM站 ](https://linux.do/t/topic/1418376)
  - [youmind2api，可以使用大香蕉 ](https://linux.do/t/topic/1363986)
  - https://github.com/iptag/jimeng-api /GPL/202511/ts
    - Free AI Image and Video Generation API Service - Based on reverse engineering of Jimeng AI (China site) and Dreamina (international site).
    - [【即梦jimeng/dreamina官网2api】10/20更新：双站均支持文生图和图生图  _202509](https://linux.do/t/topic/995691)
    - 即梦 jimeng 和 dreamina 文生图和图生图的官网 api，借鉴了几位大佬的项目，但他们的参数都有些小问题，稍加改进下，稳定性强了不少，目前只测试了文生图和图生图功能
  - [[Flow2api] 无限次数的banana pro！逆向账号池 ](https://linux.do/t/topic/1214169)

- tutorials-image
  - https://github.com/rere43/image-generator-hybrid
    - CliProxyApi 反重力生图 skill, 支持4K, 有两种方法整合, http 和google genai SDK
    - [CliProxyApi 反重力生图 skill, 支持4K, claude code , codex可用 _202512](https://linux.do/t/topic/1378927)
  - [借助 Antigravity-Manager, 终于用上反重力了！可4k banana pro _202512](https://linux.do/t/topic/1374557)

- video-gen
  - [Video Studio](https://doubao.happieapi.top/)
    - rpd: 30
    - 两款模型分别是 doubao-seedance-1-0-pro-fast-251015 和 doubao-seedance-1-5-pro-251215：前者主打高速视频生成，适合大多数文本或单图生成视频的场景，视频时长为 4–12 秒，最多支持 1 张图片输入，支持全部比例，不支持音频，默认无水印（API 可配置水印）；后者主打高质量视频生成，支持多图输入，画面一致性更强，视频时长同样为 4–12 秒，最多支持 2 张图片输入，支持全部比例，支持音频（默认带音频），默认无水印（API 可配置水印）。

- [Lorem Picsum - Images - The Lorem Ipsum for photos](https://picsum.photos/images)

## translation

- 「慕鸢の公益站」 [这是谁的公益站呢？好难猜阿](https://newapi.linuxdo.edu.rs/pricing), 签到获取0.01
  - 专门有一个翻译分组，需要创建对应分组的key，超低倍率，不限制并发
  - [上新沉浸式翻译和codex ](https://linux.do/t/topic/1501277)
- [cerebras fanyi API](https://fanyi.963312.xyz/pricing)
  - cerebras 的，目前有200个号
  - 智普官网的 glm-4.5-flash, glm-z1-flash
- [老魔公益站](https://api.2020111.xyz/pricing)
  - [【老魔公益站】沉浸式翻译站开放注册 ](https://linux.do/t/topic/1514451)
  - translate：沉浸式翻译分组，限速 300次/5min
  - cc-glm4.7和cc-m2.1：支持cc的分组，上游分别路由到glm-4.7和minimax-m2.1，限速 35次/5min
- [6655 API](https://translate-api-cf.6655.pp.ua/)
  - [【2月兑换码】6655公益 沉浸式翻译api ](https://linux.do/t/topic/1564148)

- [Chiban api](https://api.chibanban.de/pricing)
  - [［赤坂公益站］维护通知 ](https://linux.do/t/topic/1630985)

- [New API](https://new-api-latest-1-eu26.onrender.com/pricing)
  - 无法签到, [公益API站~ 可用于翻译  ](https://linux.do/t/topic/1552193)

## llm-api-official/router/gateway/aggregator

- 北龙超级计算云平台 [AI 智算云](https://ai.blsc.cn/#/lms/model)
  - 免费提供: PaddleOCR-VL-0.9B, GLM-4.5-Flash, GLM-4V-Flash, GLM-4-Flash, GLM-CogView3-Flash, GLM-Z1-Flash

- 📌 [OpenRouter API Rate Limits ](https://openrouter.ai/docs/api-reference/limits)
  - tldr: rpd-1000 
  - Free usage limits: If you’re using a free model variant (with an ID ending in `:free`), you can make up to 20 requests per minute. 
  - If you have purchased less than 10 credits, you’re limited to 50 :free model requests per day.
  - If you purchase at least 10 credits, your daily limit is increased to 1000 :free model requests per day.
  - If your account has a negative credit balance, you may see `402` errors, including for free models.
  - [Free Models Router ](https://openrouter.ai/openrouter/free)
    - openrouter/free
  - [openrouter出免费模型路由了 _202602](https://linux.do/t/topic/1559289)
    - 稍微测了下，不是 50rpd，挺好
  - [Introducing Web Search via the API  _202501](https://openrouter.ai/announcements/introducing-web-search-via-the-api)
    - The OpenRouter API now supports a web search feature, available for all models. 

- 📌 [Ollama Cloud models](https://ollama.com/search?c=cloud)
  - Hourly + Weekly limits
  - Unlimited public models
  - [Announcing Cloud models · Ollama Blog _202509](https://ollama.com/blog/cloud-models)

- 📌 [Cerebras Inference Rate Limits](https://inference-docs.cerebras.ai/support/rate-limits)
  - tldr: tpd-1m, rpd-14.4K
  - 注意免费模型的context长度最大为64k
  - Model	TPM	TPH	TPD	
  - gpt-oss-120b	60K	1M	1M
  - llama-3.3-70b	60K	1M	1M
  - qwen-3-32b	60K	1M	1M
  - qwen-3-235b-a22b-instruct-2507	60K	1M	1M
  - qwen-3-235b-a22b-thinking-2507	60K	1M	1M
  - qwen-3-coder-480b	150K	1M	1M, rpd-100

- 📌 [NVIDIA NIM APIs](https://build.nvidia.com/explore/discover)
  - free: Up to 40 rpm
  - models: deepseek-r1, qwen3-coder-480b
  - [NVIDIA NIM FAQ - AI & Data Science / NVIDIA NIM - NVIDIA Developer Forums _202409](https://forums.developer.nvidia.com/t/nvidia-nim-faq/300317)
    - NIM access through the NVIDIA Developer Program is for prototyping, research, development and testing purposes only and does not include enterprise features or support.

- [Groq Rate Limits - Docs](https://console.groq.com/docs/rate-limits)
  - tldr: tpd-100k~500k
  - MODEL ID	RPM	RPD	TPM	TPD
  - groq/compound	30	250	70K	No limit
  - qwen/qwen3-32b	60	1K	6K	500K
  - openai/gpt-oss-120b	30	1K	8K	200K
  - llama-3.3-70b-versatile	30	1K	12K	100K
  - moonshotai/kimi-k2-instruct-0905	60	1K	10K	300K
  - meta-llama/llama-4-scout-17b-16e-instruct	30	1K	30K	500K

- [Gemini Developer API Pricing  ](https://ai.google.dev/gemini-api/docs/pricing)
  - tldr: 国内不可用, rpd-100~250
  - gemini-2.5-pro: Grounding with Google Search	Not available
  - gemini-2.5-flash: Grounding with Google Search, up to 500 RPD (limit shared with Flash-Lite RPD)
  - [Rate limits  |  Gemini API  ](https://ai.google.dev/gemini-api/docs/rate-limits)
    - model,          RPM,   TPM,      RPD
    - Gemini 2.5 Pro	  5	   125,000	  100
    - Gemini 2.5 Flash	10	 250,000	  250
    - Gemini 2.0 Flash	15	 1,000,000	200

- [Mistral Rate Limits & Usage tiers ](https://docs.mistral.ai/deployment/ai-studio/tier)
  - tldr: tpmon-1b(tpd-33m)
  - Maximum requests per second: 1
  - Tokens per Minute: 500, 000
  - Tokens per Month: 1 billion
  - models: codestral-2501, mistral-large-2411
  - [Codestral - AI Studio - Mistral AI](https://console.mistral.ai/codestral)
    - Limits: 30 requests/minute, 2,000 requests/day
    - Use Codestral via your favorite Code completion tool for free.
    - Codestral is available in select code-completion plugins but can also be queried directly. 

- 📌 [魔搭推理API-Inference API推理介绍 · 文档中心](https://modelscope.cn/docs/model-service/API-Inference/intro)
  - tldr: rpd-200~500
  - 免费推理API由阿里云提供算力支持，要求您的ModelScope账号必须绑定阿里云账号后才能正常使用。
  - 每位魔搭注册用户，当前每天允许进行总数为2000次的API-Inference调用，其中每单个模型不超过500次，具体每个模型的限制可能随时动态调整。
  - 在每个模型每天不超过 500 次调用的基础上，平台可能对于部分模型再进行单独的限制，例如，deepseek-ai/DeepSeek-R1-0528，deepseek-ai/DeepSeek-V3.1等规格较大模型，当前限制单模型每天200次调用额度。
  - 在上述调用次数限制的基础上，不同模型允许的调用并发，会根据平台的压力进行动态的速率限制调整，原则上以保障开发者单并发正常使用为目标。
  - 实际单模型可用次数以及允许的并发，以平台实时调整为准。
  - 🖼️ 当前API-Inference为魔搭平台上的部分开源大语言模型（LLM），多模态模型（MLLM），以及AIGC专区文生图模型等，提供了可直接使用的API。

- [硅基流动 SiliconFlow - 大模型 API 价格方案](https://www.siliconflow.cn/pricing)
  - tldr: tpm-50k
  - llm: Qwen/Qwen3-8B, deepseek-ai/DeepSeek-R1-0528-Qwen3-8B, THUDM/GLM-Z1-9B-0414, THUDM/GLM-4-9B-0414, Qwen/Qwen2.5-Coder-7B-Instruct
  - vlm: THUDM/GLM-4.1V-9B-Thinking
  - image: Kwai-Kolors/Kolors
  - asr: TeleAI/TeleSpeechASR
  - [Rate Limits - SiliconFlow](https://docs.siliconflow.cn/cn/userguide/rate-limits/rate-limit-and-upgradation)
    - 语言模型(Chat)	 RPM=1000-10000 TPM=50000-5000000
    - 🖼️ 图像生成模型(Image)	 IPM:2 IPD:400

- 📌 [iflow 心流开放平台 - 限流](https://platform.iflow.cn/docs/limitSpeed)
  - 当前服务免费使用，但请合理使用资源，避免不必要的高并发请求。
  - 每个用户最多只能同时发起一个请求，超出限制的请求会返回429错误码。
  - 流式请求: 主动取消后立即释放令牌，推荐使用流式请求以提高效率。
  - 非流式请求: 主动取消后，模型实际仍在运行，需等待运行完毕后才释放令牌。
  - 最大输出 64K:  qwen3-coder-plus, glm-4.6, deepseek-v3.2, deepseek-v3.1, qwen3-235b-a22b-thinking-2507, qwen3-235b-a22b-instruct, kimi-k2, kimi-k2-0905, 
  - 最大输出 32K:  qwen3-vl-plus, qwen3-max, deepseek-r1

- [302. AI - API超市 cn](https://dash.302ai.cn/product/list?cate=api&tag=LLM)
  - [302. AI - API超市 ww](https://302.ai/product/list?cate=api&tag=%E8%AF%AD%E8%A8%80%E5%A4%A7%E6%A8%A1%E5%9E%8B)
  - 很多免费api, 国内版和国外版免费的api相同
  - 很多api是直接转发的其他平台，如硅基流动/快手万擎平台本身就提供的小模型， 质量不高
  - 有时会有限时免费的大模型

- [无问芯穹 LLM API 计费规则 ](https://docs.infini-ai.com/gen-studio/api/billing.html)
  - 基础服务：RPM=12、RPD=300、TPM=12000；默认情况下，租户均享受基础服务。基础服务不计费。支持在线自助升级为高级服务
  - 高级服务：RPM=120、RPD 不限、TPM=120000；租户可选择升级服务，享受更高限频。高级服务根据实际 Token 用量进行后付费结算。
  - 每个并发槽位代表 1 个正在执行的 LLM API 请求。LLM 包并发服务包并发槽位服务同样受 API 频率限制指标约束

- [火山方舟大模型服务平台-免费推理额度](https://www.volcengine.com/docs/82379/1399514?lang=zh)
  - ⚠️ 规则复杂, 注意每日超额使用token需付费, 部分模型名需要使用自动生成的id别名才能被采集和限免而不能使用预置的名称
  - rpm/tpm各模型不同，一般rpm为1w， tpm为500w
  - 单模型默认免费50w, 协作计划可奖励单模型200w
  - 免费额度仅适用于抵扣模型推理消耗的 token（50w 免费 token），不能抵扣使用各类插件、知识库等产生的费用
  - 免费推理额度，基础模型和精调后模型共享。
  - 模型支持deepseek/kimi/doubao/seedream
  - 协作奖励计划规则（第二期）和数据授权协议
    - 将在每日额度内自动按顺序采集授权模型推理接入点对应的调用数据，次日根据每个模型的前一日采集量返还等量的每日奖励包
    - 奖励包将在发放到您账号后的 30 个自然日内有效，到期后清零

- [DeepSeek API Docs - 模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/)
  - 扣减费用 = token 消耗量 × 模型单价，对应的费用将直接从充值余额或赠送余额中进行扣减。
  - 百万tokens输入（缓存命中）	0.2元
  - 百万tokens输入（缓存未命中）	2元
  - 百万tokens输出	3元

- 📌 [Z. AI DEVELOPER DOCUMENT](https://docs.z.ai/guides/overview/pricing)
  - tldr: 请求并发数量（在途请求任务数量）flash-2
  - GLM-4.5-Flash Free ✅
  - free: glm-4-flash-250414(20), glm-4-flash(200), glm-4.1v-thinking-flash(5), glm-4v-flash(10), cogview-3-flash, cogvideox-flash, glm-experimental-preview(5)
  - 没找到 用量统计/token统计 的界面
  - 非glm-coding-plan的api，仅提供openai格式，不提供 anthropic格式
  - [免费模型 - 智谱AI开放文档](https://docs.bigmodel.cn/cn/guide/models/free/glm-4.7-flash)
  - [智谱AI - pricing](https://bigmodel.cn/pricing)
  - [模型实时调用专属权益 及 标准单价 (很多免费)](https://bigmodel.cn/usercenter/equity-mgmt/user-rights)
  - 免费模型: [福利专区](https://bigmodel.cn/dev/activities/free/glm-4-flash)
  - [智谱AI开放平台 - 速率限制 - 用户等级限制](https://bigmodel.cn/usercenter/proj-mgmt/rate-limits)
  - [智谱AI开放平台 - 速率限制 - 通用默认限制](https://www.bigmodel.cn/dev/howuse/rate-limits)
    - 当前我们限制的维度是请求并发数量（在途请求任务数量）
  - [Z.ai - Rate Limits](https://z.ai/manage-apikey/rate-limits)
    - GLM-4.5-Flash	2

- [KAT-Coder开发工具接入指南-快手万擎-StreamLake](https://www.streamlake.com/document/WANQING/me6ymdjrqv8lp4iq0o9)
  - tldr: rphour-20~30
  - ✅ [KAT-Coder-Air V1 模型免费使用规则 ](https://www.streamlake.com/document/WANQING/mh1g9y6knewv5sft54k)
  - 非高峰时段: 02:00-08:00 每6小时内您将可以发起200次对话请求，超过此请求数后，您可能会经历更长的排队等待时间或更严格的速率限制
  - 高峰时段: 08:00-02:00（次日） 每6小时内您将可以发起120次对话请求。在此时段，KAT-Coder-Air V1 的请求优先级可能会降低。您可能会经历更长的排队等待时间或更严格的速率限制。
  - https://wanqing.streamlakeapi.com/api/gateway/v1/endpoints/kat-coder-air-v1/claude-code-proxy
  - https://wanqing.streamlakeapi.com/api/gateway/v1/endpoints

- [LongCat API开放平台快速开始 | API 文档](https://longcat.chat/platform/docs/zh/)
  - tldr: tpd-500K
  - 每个账号每天自动获得 500, 000 Tokens 免费额度
  - 免费额度将于每日凌晨（北京时间）自动刷新
  - 输入和输出Tokens均计入消耗, 流式接口和段式接口消耗相同
  - 单次请求限制 输出文本：最大8K Tokens

- [腾讯混元大模型 混元生文计费概述 ](https://cloud.tencent.com/document/product/1729/97731)
  - Hunyuan-lite 免费使用
  - 经常拒绝用户的直接请求，而回答其他内容
  - [腾讯混元大模型 混元 OpenAI 兼容接口相关调用示例](https://cloud.tencent.com/document/product/1729/111007)
  - [腾讯混元大模型全面降价！混元-lite 即日起免费 _202405](https://cloud.tencent.com/developer/article/2419914)

- [百度千帆 - 百度智能云控制台](https://console.bce.baidu.com/qianfan/modelcenter/model/buildIn/list)
  - ERNIE-Lite 免费使用， 非开源， 上下文长度: 6K tokens + 2K tokens
  - [百度千帆 - 百度智能云控制台](https://console.bce.baidu.com/qianfan/modelcenter/model/buildIn/detail/am-ju3hi4ts39u9?tab=version)

- [讯飞星火大模型API](https://xinghuo.xfyun.cn/sparkapi)
  - 免费1个模型: Spark Lite 
  - QPS: 2
  - [星火大模型，燃情双十一-讯飞开放平台](https://www.xfyun.cn/activities/discount)
  - [讯飞星辰MaaS平台](https://maas.xfyun.cn/modelSquare)
    - 限免活动
  - 🐛
    - 少部分模型存在无法调用mcp的问题，如kimi-k2.5, 而glm-4.7支持调用mcp-tools; 调用失败的表现是， claude对话突然停止，且history里面没有相关对话日志
      - 排查过程: 中转claude模型能用mcp， 但讯飞的kimi用不了， 进一步测试讯飞的glm-4.7能用
  - 🛝

- [七牛 AI 大模型推理服务 - 七牛云](https://www.qiniu.com/ai/chat)
  - 采用按量计费的模式，根据实际使用的 token 数量收费，每月初出账。新用户享有免费额度
  - [AI 大模型广场](https://www.qiniu.com/ai/models)
    - 部分免费模型为其他厂商的免费模型

- [模力方舟（Gitee AI）](https://ai.gitee.com/serverless-api)
  - 提供了很多免费小模型，如 8b/4b, glm-4.6v-flash, 
  - AI图片检测: 并发数不限制，根据负载动态调整

- gitcode - [AtomGit AI社区 - 模型: 开源大模型 ](https://ai.gitcode.com/models)
  - [AtomGit AI社区 - 模型广场](https://ai.gitcode.com/serverless-api)
  - 注册即可领取 2M 免费 Token
  - 免费容器 1000 核时/月

- [DMXAPI官网：中国多模态大模型API聚合平台](https://www.dmxapi.cn/rmb)

- [Moonshot AI 开放平台 - 充值与限速](https://platform.moonshot.cn/docs/pricing/limits)
  - 赠送用完后需要充值

- [Xiaomi MiMo 开放平台](https://platform.xiaomimimo.com/#/docs/pricing)
  - 平台公测期间，模型推理服务免费

- [Cloudflare Workers AI Pricing](https://developers.cloudflare.com/workers-ai/platform/pricing/)
  - Our free allocation allows anyone to use a total of 10, 000 Neurons per day at no charge. 
  - Workers AI is included in both the Free and Paid Workers plans and is priced at $0.011 per 1, 000 Neurons.
  - gpt-oss-120b, 31818 neurons per M input tokens
  - gpt-oss-20b, 18182 neurons per M input tokens

- [GitHub: Prototyping with AI models ](https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models#rate-limits)
  - 限制很严格
  - Requests per day	50~150
  - Tokens per request	8000 in, 4000 out

- [huggingface Pricing and Billing](https://huggingface.co/docs/inference-providers/pricing)
  - limited to models smaller than 10GB. Some popular models are supported even if they exceed 10GB.
  - [Inference Providers](https://huggingface.co/docs/inference-providers/index)
  - Hugging Face provides a Serverless Inference API as a way for users to quickly test and evaluate thousands of publicly accessible (or your own privately permissioned) machine learning models with simple API calls for free
  - Every Hugging Face user receives monthly credits to experiment with Inference Providers
  - Account Type	Monthly Credits	Extra usage (pay-as-you-go)
  - Free Users	$0.10, subject to change	no
  - [HuggingFace changes to PRO subscription Inference limits, should I switch providers now? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ii4nst/huggingface_changes_to_pro_subscription_inference/)
    - The $2 credit limit is pretty weak for a $9 subscription. RunPod gives you way more bang for your buck - just pay for what you use and test as many models as you want.

- [Cohere API Keys and Rate Limits](https://docs.cohere.com/docs/rate-limits)
  - all endpoints are limited to 1000 calls per month with a trial key

- [AIHubMix - Models](https://aihubmix.com/models)
  - 免费模型不多，大多coding相关
  - free-per-model: 5rpm, 500rpd, 1Mtpd
  - mimo-v2-flash-free
  - coding-glm-4.7-free, coding-glm-4.6-free, coding-minimax-m2-free, kimi-for-coding-free

- [现在做大模型，还有靠谱且免费的 api 接口吗？ - 知乎](https://www.zhihu.com/question/662092970)
  - 纯粹免费的API也是有的，但是多限于轻量级的大模型，比如智谱AI的flash模型，Google的 Gemini 1.5 Flash。
  - 目前主流的 API 接口都是采用相同的套路，即免费注册送固定的额度，然后再收费的策略。我反正是没有看到纯免费一直可用的 API 接口。
  - DeepSeek和MiniMax是国内模型，包括其他厂商的国内模型也都有免费额度。不过Groq几个月来一直都是免费
  - Groq是一家美国AI芯片公司，专注设计高性能的AI处理器，目前借助自研的AI芯片LPU，每秒能够输出近500个token。和GPT-4，Gemini对标，同一个问题所需的时间，Groq完全碾压了其他两者，输出速度比Gemini快10倍，比GPT4快18倍。
  pm- Groq平台提供个人免费的API-KEY接口，不同的模型限制不同

- [Groq is Fast AI Inference](https://groq.com/)
  - Fast AI inference for openly-available models like Llama 3.1
  - Move seamlessly to Groq from other providers like OpenAI by changing three lines of code.
  - [On-demand Pricing for Tokens-as-a-Service](https://groq.com/pricing/)
  - [Groq公司推出的全球最快的大模型推理服务达到每秒输出500个token，如何看待这一技术？ - 知乎](https://www.zhihu.com/question/645010090)
    - 一句话来说，这个芯片就是玩了个用空间换时间的把戏，把模型权重和中间数据都放在了 SRAM 里面，而不是 HBM 或者 DRAM。
    - 这是我 8 年前在微软亚洲研究院（MSRA）就做过的事情，适用于当时的神经网络，但真的不适合现在的大模型。因为基于 Transformer 的大模型需要很多内存用来存储 KV Cache。
    - Groq 芯片虽然输出速度非常快，但由于内存大小有限，batch size 就没法很大，要是算起 $/token 的性价比来，未必有竞争力。

- [江城模境 模型广场](https://www.whaihub.cn/modelplaza/modelsquare/)
  - free: 百度 ernie-tiny/lite/speed
- [鲸智 模型广场](https://aihub.caict.ac.cn/modelplaza/modelsquare/)
  - free: free: 百度 ernie-tiny/lite/speed

- [超算互联网](https://www.scnet.cn/ycjh/index.html)

- [ZenMux](https://zenmux.ai/models?sort=pricingLowToHigh)

- paid-api
  - [OAIPro API](https://api.oaipro.com/)
    - L 站不倒，这个就不倒

- [令牌查询](https://apikey.cifang.xyz/)

## llm-2api

- embedding
  - [Embedding](https://router.tumuer.me/pricing)
    - [[Embedding 公益站] 问题+更新+预告 _202601](https://linux.do/t/topic/1421074)
      - 用 gemini 的 embedding-001 和 text-embedding-004 时容易出现，因为上游接的是 tier1 层的号，所以有限额，可以等段时间或者使用其他模型
    - [[Embedding 公益站] 囤囤鼠集合啦  ](https://linux.do/t/topic/1507741)
      - 上架了模型 gemini-embedding-001(不是 embedding-001)
      - openrouter 的 key 了，专门用于 text-embedding-3-large 

- tutorials
  - [手把手带你用上AI神器 - CLIProxyAPI（零：配置详细解说） _202510](https://linux.do/t/topic/1011966)
  - [手把手带你用上AI神器 - CLIProxyAPI（壹：项目介绍+Qwen实战） _202510](https://linux.do/t/topic/1011983)
  - [在 opencode 中使用CLIProxyAPI 的配置教程，享受模型自由 _202601](https://linux.do/t/topic/1407247)
  - [CLIProxyAPI 的反重力BananaPro 稳定输出 4k 图片 教程 _202601](https://linux.do/t/topic/1396957)
  - [zeabur免费搭建CLIProxyAPI，CLI和Antigravity都能用 _202601](https://linux.do/t/topic/1381902)

- [OpenCode - Zen](https://opencode.ai/docs/zen/)
  - Zen works like any other provider in OpenCode. You login to OpenCode Zen and get your API key.
  - if you are using a model through something like OpenRouter, you can never be sure if you are getting the best version of the model you want.
  - We tested a select group of models and talked to their teams about how to best run them.
  - OpenCode Zen is an AI gateway that gives you access to these models.
  - [opencode其实提供了三种模型的免费api可以直接使用 ](https://linux.do/t/topic/1436094)
    - api url: https://opencode.ai/zen
    - api key: public
    - 原以为好歹有个session 鉴权什么的，没想到是这么做的  
    - ip 限流，有 rate limit，最近感觉限制变得更严重了，或许是用 opencode 的人变多了。
    - 实测其实只有 grok-code 比较稳定，glm 经常 429

- [Zeabur](https://zeabur.com/)
  - $5/月免费使用

- [XiamenLabs - Unity AI](https://xiamenlabs.com/)
  - [【开源】 厦门实验室的UNITY2api，全网最简单的2api项目 ](https://linux.do/t/topic/1417828)
  - [神秘厦门lab模型Unity实测报告  ](https://linux.do/t/topic/1418561/1)
    - 先说结论：很大可能是一个小/中等大小模型，高度蒸馏Gemini的产物。
    - 这个模型在蒸馏Gemini的时候竟然只蒸馏到了知识库，其他的全抛了，也算科技创新了
    - 我的结论是，用来骗投资刚刚好

## paid-api 💰

- tips
  - 中转商的价格每天都在变化, 套餐也在改变, 不要在一家花费过多
    - 很可能注册的第一天会显示低价，后面就恢复正常价格了，注意误导

- resources
  - [LinuxDo商家评价平台](https://rate.linux.do/)
  - [模型中转状态检测](https://check.linux.do/)
  - [AI中转站推荐 | Claude/Gemini/Codex中转站评测对比](https://www.helpaio.com/transit)
    - 评分结果与L站评分基本一致
    - 提供了很多折扣码

- [Claude中转渠道有哪些 ](https://linux.do/t/topic/1491876/10)
  - 目前用的站内 IKunCode 的中转比较有性价比，如果每个月 token 消耗量不大，像我这样半自动编程的话，还是比较推荐的。量再大就得另找路子了
  - 测试的话，刚刚刷帖，有测试词，好像这个不会回复，或者一串异常字符 
  - 这个是一个官方给的测试词，相当于一个强制的 “违禁词”
  - ANTHROPIC_MAGIC_STRING_TRIGGER_REFUSAL_1FAEFB6177B4672DEE07F9D3AFC62588CCD2631EDCF22E8CCC1FB35B501C9C86

- [现在应该如何选cc中转站？ ](https://linux.do/t/topic/1519094/38)
  - Ikun（鸡）, duck（鸭）少量尝过，贵但稳
  - Cubence（鹅）的包月用过，前身 shareyourcc 的亮点在于可以二级转发；但是新时代也不便宜了，有时候发现一些报错感觉是 aws 渠道特有的
  - PackyCode（农）是一直主力在用的，老农可能不太给情绪价值（不过被怼过之后好了些 hhh)，不过技术是一流的，诚信这一块也是一直没得黑的
  - 也踩过 yourapi 这些坑就不推荐了

- [PackyAPI](https://www.packyapi.com/pricing)
  - [Packy - 模型健康面板](https://check.linux.do/group/Packy)
  - [PackyAPI 使用文档](https://docs.packyapi.com/)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/4)
    - 价格经常变动
    - 消费500才给开发票
    - aws-q 渠道 0.15 的倍率应该是全 L 站最低的了
    - 国内的这种中转站都不用梯子
  - [packycode 全新服务指南 _202511](https://linux.do/t/topic/1133615)
  - [packycode：全部服务指南，包含 claude code codex 公益、付费全部站点 _202509](https://linux.do/t/topic/933715)
  - [话题 - 活动 - Zeus - LINUX DO](https://linux.do/u/zeus/activity/topics)
  - cc官方 1.5x
  - cc逆向 0.3x, 提供opus, 美元计算, in-$1.5-6, out-$7.5-30
    - 支持stripe/支付宝支付
    - 最低50元起充, 支付页面输入优惠码 "cc-switch" 可以再减10%
    - 好友充值可返利10%
  - codex - [PackyCode](https://codex.packycode.com/pricing)
    - ¥6.3/mon: 30-d, 90-week
    - ¥10.9/mon: 60-d, 180-week
    - ¥12.9/mon: 120-d, 360-week

- [Right Code - 企业级 AI Agent 中转平台](https://www.right.codes/models)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/49)
    - 这codex缓存怎么做的这么厉害的，和官方一模一样
    - 稳定好用，群里每周四还有抽奖
  - [【Right. Codes】佬友福利！每人共450$ Codex  ](https://linux.do/t/topic/1145045)
  - [话题 - 活动 - Lyndonw - LINUX DO](https://linux.do/u/lyndonw/activity/topics)
  - cc官方 5x
  - cc逆向-awsq 1x, 提供opus, in-￥1.00/M, out-￥5.00/M
    - Kiro逆向，200K上下文、有缓存，与官渠相差不大
    - cc-token大约是官方0.2x
    - 支持支付宝
    - 好友支付完成后，双方同时获得实付金额对应额度的 5%
  - codex套餐量大管饱
    - ¥45/mon: 30-d, 900-mon
    - ¥60/mon: 60-d, 1800-mon
    - ¥75/mon: 90-d, 2700-mon
  - L站用户注册就送小小股东, $5/mon
    - right code 也是站内的一家主要做codex的中转站

- [IKunCode](https://api.ikuncode.cc/pricing)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/15)
    - 太喜欢有求必应的客服了，回复速度快，解决问题快，稳定性也很不错
  - [【IKunCode】全民编码人们大家好，我们是练习时长两周半的cc中转站 ](https://linux.do/t/topic/965944)
  - [话题 - 活动 - zyoung - LINUX DO](https://linux.do/u/zyoung/activity/topics)
  - cc官方 1.5x
  - cc逆向 0.4/0.8, 提供opus, in-¥2-4/M, out-¥10-20/M
    - 200K上下文 + 5min缓存，支持非CC客户端
    - 支持 支付宝/微信

- [CUBENCE - Claude Code & Codex Gateway](https://cubence.com/dashboard/model-plaza)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/17)
    - 目前用过最稳的，别家一天一崩，这家一周一崩
  - [【Cubence】SHAREYOUR正式改名Cubence ](https://linux.do/t/topic/1069292)
  - [话题 - 活动 - Fetters - LINUX DO](https://linux.do/u/fetters/activity/topics)
  - cc官方 1.5x
  - cc逆向 0.3x, 提供opus, in-¥1.5/m, out-¥7.5
    - 支持缓存

- [DuckCoding](https://duckcoding.com/)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/12)
    - 最贵的一家
    - 太贵了，消耗token太快了，即使买官方的包月也没有这么夸张啊
    - L站最贵的倍率了
  - [【富可敌国】InstCopilot API 更名 DuckCoding ](https://linux.do/t/topic/937521)
  - [话题 - 活动 - WCyrus - LINUX DO](https://linux.do/u/wcyrus/activity/topics)
  - cc官方 1.5x , 提供opus, in-¥5-15/M, out-¥25-75

- [米醋API](https://www.openclaudecode.cn/)
  - 提供opus, in-￥1.00/M, out-￥5.00/M
  - [openclaudecode好像是也被卖了，但还是好评 _202601](https://linux.do/t/topic/1520754)
    - 比较负责的，人家全退款了。 花了 2 个月的时间，办理完所有退款，才交割出售。 这点非常好评。

- [AICodeMirror官方共享平台](https://www.aicodemirror.com/dashboard/pricing)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/59)
    - 这家中奖必须给五星好评？那我直接给你0.5星
  - cc官方 0.4x
  - cc逆向 0.2x, 提供opus, in-¥1.4/M, out-¥7/M
    - 缓存创建也要付费

- [foxcode](https://foxcode.rjj.cc/)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/6)
    - aws渠道有点蠢，其余渠道经常卡。。。体验差
  - [【FoxCode稳定超耐用】一款为你量身定制的ClaudeCode镜像+API双合一 O](https://linux.do/t/topic/859649)
  - 消耗量惊人，店铺写的次数严重虚标
  - 暗改了计费的 一个问题能跑10$
  - 开发票要收5%的开票费，88code和鸭子都不用
  - [FoxCode 中转站 Claude 2API 上下文压缩时6倍天价计费 ](https://linux.do/t/topic/1373802)
  - [FoxCode发卡](https://fk.hshwk.org/)
    - ¥35/0.1b, ¥135/0.5b, ¥468/2b
  - [扛过这波了，FoxCode 稳定不涨价通知 + 优惠券发放 + 新增超高质量cc-Super渠道 _202601](https://linux.do/t/topic/1505358)
  - [【富可敌国】小于1毛钱/$的claude-opus-4-6已全面适配, 上线gpt-5.3-codex _202602](https://linux.do/t/topic/1571488)
  - [一文搞清楚foxcode的计费 ](https://linux.do/t/topic/1486166)
    - 在这里以我的实际上付费为例，我充了 135 人民币，在账号上有 500 刀的可用余额。在实际上进行调用后可以发现，这三个渠道有以下的比率。aws 是原价的 0.25 倍，ultra 是 2 倍，max 是 18 倍。
  - 🐛 [foxcode 和 tiger 用一台服务器? _202601](https://linux.do/t/topic/1468155)
    - IP 和 证书都一样，买 MAX 还送服务器啊，还是主站服务器啊
  - [foxcode+opencode计费是否出问题了？ ](https://linux.do/t/topic/1473221)
    - 买东西不能光盯着几分钱的价格，没缓存 / 缓存不生效，相同的场景会贵很多的，命中缓存只有 1/10 价格
  - [Foxcode最近的utral和super是啥渠道？ ](https://linux.do/t/topic/1506436)
    - utral 是反重力
    - 只有几种渠道 1、官转 2、aws 3、kiro/cursor/antigravity

- [Tiger API](https://tiger.bookapi.cc/pricing)
  - opus, in-¥1/M, out-¥5/M
  - [【低倍率&耐用王Tiger】春节炸场福利！Claude 4.6 Opus ，Codex 5.3首发 ](https://linux.do/t/topic/1572928)
    - 充值 6000 以上的佬友请私信群主转账并可开具发票
    - 纯血 CC Max，假一赔十

- [Jiekou AI](https://jiekou.ai/resource-pack)
  - ¥15/20M/mon, ¥75/0.1b/mon, ¥225/0.3b/mon

- [YesCode](https://co.yes.vg/)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/13)
  - [YesCode, Claude Code中转站测试完毕已正式上线 ](https://linux.do/t/topic/801547)
  - 按月付费, 美元计费, $10-20-45-66

- 88code [LinuxDo商家评价平台](https://rate.linux.do/merchant/5)
  - 最近不要再买了，建议观望，极其不稳定，经常没法用

- [DMXAPI官网：中国多模态大模型API聚合平台](https://www.dmxapi.cn/)
  - 提供免费小模型: glm-flash, qwen3-8b
  - 很多国内模型
  - 提供opus， in-¥12/M, out-¥62/M

- [Ai Go Code - AI编程助手 | 接入Claude等先进AI模型](https://www.aigocode.com/)
  - ¥400/4weeks

- [兔小店](https://store.tu-zi.com/)

- [UUcode - API 中转管理平台](https://www.uucode.org/)
  - [【致敬开源】与其打硬广，不如给佬友们的代码“供电”，寻找L站开源作者，UUcode送商业级API额度 ](https://linux.do/t/topic/1370667)

- [AI Ping](https://aiping.cn/modelList)

## video/movie

- [OmniBox - 在线观影](https://omnibox.wangchao.uno/)
  - [MoonTVPlus](https://moontv.wangchao.uno/)

## hosting

- [LD士多 - LDC积分商城](https://ldst0re.qzz.io/)

- [风萧萧公益机场](https://chanel.weyolo.com)
  - [萧草 · 臻选](https://shop.sxxe.net/)

- [Canopy Wave](https://cloud.canopywave.io/)
  - 提供模型API
  - 也提供部署环境

- [Huggingface和Cloudflare羊毛自建代理的方法 ](https://linux.do/t/topic/1411544)
  - 利用cf大善人的网络代理加速，利用hug大善人的免费域名和证书，达到我们的目的
  - huggingface.co免费的容器： Free版本就是2vCPU和16GB RAM，就已经非常强了
    - 新建一个Space，然后点 Embed this Space
    - huggingface 跑了个前置的Nginx或Caddy或traefik代理，自动申请了证书，代理后端容器的7860端口，为什么是7860端口呢？
    - 因为最常见的用途是托管基于 Gradio 构建的机器学习模型演示。Gradio 是一个非常流行的 Python 库，用于快速创建交互式 Web 界面来展示 ML 模型。它的默认启动端口就是7860。
  - 接着我们去薅大善人cloudflare，首先弄好一个域名并托管到CF上面
    - 点开左边的菜单：Build –> Compute & AI –> Workers & Pages > create app
    - 返回这个worker的空间，点击Settings，下面的Domains & Routes ，右边点击 +Add

- [gdgame - 免费单机游戏下载 | 游戏库 - 免登录直接下载单机游戏](https://gdgame.org/)
  - [公益免费单机游戏站 ](https://linux.do/t/topic/1561998)
  - 免登录享受 4000 款单机游戏
  - 支持国内全主流网盘：百度，夸克，迅雷，123，天翼。天翼盘是可以做到免费不限速，真正不花一分钱。
# ai-products-hunt

# more
