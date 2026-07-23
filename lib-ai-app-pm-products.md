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
  - llm ux: natural language as interface
  - 🤔 旧的产品交互逻辑在新的时代都需要调整, 用户大多不想手动搜索, 直接在聊天框里输入指令，将搜索+后续工作一起执行
  - 🤔 不要执着于ai框架，主流模型厂商都会推广包含厂商特性的框架及产品(sdk + codex/claude-code/gemini-cli), 可专注于 主流 开源业务系统实现 或 厂商无关的实现
  - frontend: ai-sdk/chatbot, assistant-ui, librechat
  - backend: langgraph + python/nodejs
  - aisdk + docs/excel/image
  - ai-apps as ref: lasuite
  - ai时代的人工编辑, 可设计为特殊的human-in-the-loop
  - 一切通知/消息，都可以设计为 ai的chat+自动化工具
  - 之前的软件设计是面向用户、开发者，现在不得不重新设计，以大模型为使用者。 WebMCP的推进会让产品api快速发展
  - 大模型可能的成本变化: 推广期token廉价, 等到工程师coding能力下降, token再涨价, 因为本地运行大模型成本太高
  - 需要清理ai工作的中间物缓存、代码缓存、npm/uv缓存
  - 足够好用的工具能够改编用户习惯，如 claude-code 替换 cursor
  - skill免费， 预览免费，编辑付费， ~~是否可行~~ 
    - 似乎不可行，因为是ai编辑

- ai-dev-xp
  - 🦞 openclaw带来的产品变化, 用户更能接受在本地电脑安装常驻app/进程, 然后通过im-app交流
  - 难复现好的效果，同样的prompt+context，有时输出的效果就是不好
  - agent框架的tool-use实现对最新llm的支持，llm-provider的部署 都会影响llm的效果
  - ai适合快速生成草稿文本或原型, 但修改难

- ai-harness
  - claude-code(ts)
  - codex-cli(rust), openai-agent-sdk
  - ~~gemini-cli/qwen-code~~ (ts) , deprecated
  - opencode(ts), nanocoder(ts)
  - mistral-vibe(python), openhands(python), aider
  - cursor-cli/sdk
  - vscode copilot-cli/sdk
  - ✨ kilo-vscode的易用性很强, 不同模式如ask/code可设置默认model, chat可直接在editor区域打开, 还采用了client/server架构
    - 隐藏左右侧边栏 加上 chat在editor区域打开后， 使用自定义模型api, 就可作为一个通用AI前端
    - 甚至可用 codex-app-server 替换kilo的后端
    - 甚至可用 opencode-desktop 替换codex-cli的前端
  - cline(ts)
  - openclaw(ts)
  - hermes(python)
  - fwk-ts: pi/pi-coding-agent(ts), vercel-ai-sdk, tanstack-ai
  - fwk-python: langchain, smolagents, pydantic-ai

- app vs browser
  - 不是每个用户都能免费使用word的审阅模式, 自定义webapp/app提供了可选方式
  - 自定义webapp/app能提供独特的体验, 如artifacts/diff/image/code-running/table/ocr
  - agent擅长浏览器操作, agent能读取其他文件或程序

- ai-ux/visiual
  - 在浏览器cdp成熟后, 通过cdp直接打开浏览器操作web ui似乎比electron app更强大
  - 输入或输出包含visual内容的产品需要human-in-the-loop, 如ocr/image
  - 很多产品以chat作为入口, 有用户觉得不够直观, 可采用类似浏览器经典的搜索/聊天框+快捷方式
  - app-store 向 skills-hub 迁移, 可参考 aionui的assistant, 可以在app中设置默认或推荐的model、提示词

- ai相对于搜索引擎的优势 🌹
  - ai能推理和计算, 分析复杂问题，给出更准确的方案
  - ai能拆分复杂任务为多步任务，能通过多轮来执行任务，同时支持one-shot和multi-steps
  - 能通过tool-call使用工具
  - 对多语言支持很好

- why-local-ai? 🌹
  - popular local apps: claude-code, obsidian, openclaw
  - stable model and stable api
  - privacy: code, data, 还可以跳过广告推广
  - tweak different configs for ai-models
    - 参考cline, 提供针对local场景的精简prompt
  - 避免模型平台的限制rate limits，如并发请求数(rpm/tpm/需要排队)、context长度、最大输出token数、模型版本、模型大小等
  - no implicit ai degradation/switch: bring your model
  - cost: unlimited tokens, local models支持超大context, 利用本地模型ocr/文生图
    - 文本模型有很多api提供商可选择，ocr模型的api可选择的不多，定制模型只能本地运行
    - 简单的 tool call 使用本地模型更高效, 可考虑将tool call小模型内置在软件中
    - 将本地token与移动/联通/电信的套餐做对比
    - 本地ai实现 draft初稿 并优化prompt, 再由更强的模型优化效果
  - openclaw比manus更火的原因，是支持在本地自动化执行任务，而不是云端
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

- https://github.com/Ashfaqbs/TinyLLM-usecases
  - When Small LLMs Win
    - Tool/function calling - Mapping user intent to a function name + arguments
    - Intent classification - Routing queries to the right service
    - Query parsing - Extracting structured data from natural language
    - Simple Q&A with tools - Answering questions by calling APIs
    - Edge/IoT deployment - Running AI on devices with no internet
    - High-throughput pipelines - Processing thousands of requests per second
    - Privacy-sensitive workloads - Data never leaves your infrastructure
    - Development and testing - Fast iteration on AI pipelines without API costs
  - When You Still Need Large LLMs
    - Complex multi-step reasoning across long documents
    - High-quality creative writing or content generation
    - Tasks requiring deep world knowledge
    - Nuanced understanding of ambiguous instructions
    - Multi-modal tasks (vision + text + audio)

- roadmap-ai
  - 针对国内免费api定制的chat/ppt/mermaid: 魔搭, 快手万擎
    - 可以 ~~fork janai,然后扩展provider~~ , janai默认支持openai-like api，已经支持了国内models
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
  - 🤔 使用code-gen来实现产品对本地模型的能力要求高, 可考虑备用方案
  - web sandbox + ai-coding > lovable ❓
  - sandpack ai? react-live ai?

- 🏠 ai-architecture/patterns
  - OpenAI Agents SDK
  - Claude Agent SDK
  - openclaw pi
  - huggingface smolagents
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
- usecases(有特色不代表有需求)
  - 使用频率: markdown > editor > ocr

- toB-ai
  - 企业需要支持快速集成现有系统、权限、日志审计

- rag
  - pdf-vector bundle 格式, 
    - 优点: 可以隐藏原文但支持搜索
    - 缺点: 体积大，vector/dimension缺乏标准

- pdf
  - gitbook-like viewer, mdBook, sharing without editing
  - LiteParse Grid Projection Algorithm

- image
  - 现在的llm缺少和image结合生成图文混排内容的能力, image不一定是ai生成 的，和已有的百科图片/开放图片/mermaid结合也有机会

- editor-heavy
  - pretext
  - ooxml editing
  - agentfs

- spinedigest: 一次处理完，所有中间结果（Chunk、图谱、Snake、总结）全部打包进一个 .sdpub 文件。以后想重新导出成 Markdown、EPUB、纯文本……完全不需要再跑 LLM，秒级完成。

- translation
  - 基于ai的翻译对比阅读
  - 对比阅读已有pdf的 原文 和 译文

- rewrite 
  - obsidian webclipper to vscode
  - open-canvas with langgraph
  - ~~replace vscode with codemirror, compatible with obsidian~~ (没收益)
  - Gemini file search API

- token-router/gateway
  - 分享本地的GPU、token，类似的项目有分享画图gpu，但如何分享token还未流行

- local-reimpl
  - 比如支持minimax语言的api、mineru-ocr api，直接本地可用

- models
  - reproducible ai/rag/ocr(nice-to-have, not-required)
    - 不同版本的向量模型生成的数据空间维度大小是不一致的会导致后续查询数据处理啥的有问题
    - 另一种思路是通过类似jupyter的重代码工具去实现
    - 可以兼容comfyui的导出json，直接在aichorage打开

- chat-ai
  - 主流ai的web-chat结果能快速对比

- gui(cli is not enough)
  - vision: pdf/image 操作更方便
  - multi process/locations: cli过于混乱，ui操作更清晰
    - 切换files/chat更清晰
    - tasks progress
  - 需要获取页面元素的场景: 如用户选择的文本/浏览器tab
  - browser embedding
  - omni: audio
  - ✨ kilo-vscode的易用性很强, 不同模式如ask/code可设置默认model, chat可直接在editor区域打开, 还采用了client/server架构
    - 隐藏左右侧边栏 加上 chat在editor区域打开后， 使用自定义模型api, 就可作为一个通用AI前端
    - 甚至可用 codex-app-server 替换kilo的后端
    - 甚至可用 opencode-desktop 替换codex-cli的前端

- why-gui-app
  - 用类似 claude-design 的思路来实现 ui/编辑器 类型的产品
  - too many options: 
    - models/quants, cloud api, 处理速度不同
    - model thinking: 需要会话级、模型级的快速开关
    - parallel requests for local models/ocr
    - text/image pdf ocr, 源文件处理方式不同
    - vlm, pipeline, 识别方法不同
    - versions/comparison
    - citation or not

- omni
  - audio
  - video

- cleaner
  - 清理codex-cli/cc的对话历史，展示date/size/suggestion-to-clean
# 💎🚀 aichorage - local llm with joy, 提供模型API、rag可靠性、pdf文本操作

> hybrid local/cloud ai assistant/harness designed to work with documents and mitigate your token anxiety.

- selling-points
  - non-goals: local image gen
  - 易用性: 模型推荐 + 场景优化的提示词 + 多模型/多版本对比
    - llm ux: natural language as interface
    - 对同一场景, 如翻译/ocr, 针对不同模型内置合理的参数且支持配置
    - pdf: ocr(提取table/chart), editing(proof/布局), rag(citation)
    - pm: llamaparse-extract( **mineru/paddleocr**/mistral/本地/远程), cowork(docx-xml/databases/**ilovepdf** ), notebooklm
    - later: GPU硬件+model量化(ai难取代), Image, TableAI, Audio, 翻译, 多维表格, ai-design/lovable, pretext-edit
      - hybrid-ai-with-ssd-caching, eidting-with-brower-use, sandbox-with-just-bash, db-derived-files-sync-dbfs+backlinks
      - doc-ask, doc-mgmt like paperless-ngx
    - roadmap: 
      - agentic场景优化: ocr-vlm/pipeline, translation
      - citation, backlinks: 提升rag的准确度, 优化搜索结果中的code/text/image
      - pdf-editing: typst, formula, chart
      - 优化 windows版 coding-agent、模型推理、 rag依赖库
      - sandbox: mac-container, just-bash
      - lovable/design: easy ux
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
      - ai是基于现有数据和成功训练, 所以现阶段未解决的问题, ai大多未解决, ai更多时候是在加速解决已解决过得问题，而很多业务开发就是在重复解决已解决过的问题
  - ✈️ local models support: mlx, lmstudio-alternative
    - 模型库: text模型, ocr模型, 翻译模型, t2i生图模型, tts, stt,  lmstudio在模型分类上做的不够好
    - affordable, 较少免费api的模型: ocr, stt
    - ocr model choices: benchmarks
    - modes config for coding/ocr/translation/rag like cline-plan/act/ask
      - 内置场景化提示词
      - 内置场景参数, 支持disable thinking(qwen/nemotron)
    - quant量化版本维护, 热门模型经常有社区维护，但非热门模型的量化版本少，维护更新少， 可维护mlx/dflash/turboquant
    - 参考lmstudio支持本地并发请求, 支持展示进度
    - 参考janai/pipeshub, 既支持选择本地/api模型，也支持选择图片/文档
    - ocr/vlm comparison-matrix/playground: 识别对比, 翻译对比
      - ocr模型的输出统一为openai格式、统一标签(暂无标准)
    - AI异常后，human-in-the-loop的核心功能，还能用，还好用
    - 允许分享文档/插画中的模型配置/运行日志, 将prompt放入git-commit，还是直接放入图片?
    - ❓ 如何一键切换到cloud版
    - https://github.com/tc-mb/llama.cpp-omni is the first Omni multimodal inference engine built on llama.cpp.
    - custom model: 针对nvidia/openrouter/mistral的模型做优化, 如qwen3.5-plus
    - cpu-model: 适合cpu的模型是否存在市场需求
  - 👾 local agent
    - skills for local model
    - openclaw比manus更火的原因，是支持在本地自动化执行任务，而不是云端
    - 支持同一个任务选择不同agent如claude-code/codex-cli来实现多个版本
    - 支持不同的cli来交叉验证
    - local/cloud agentfs-sandbox: agentfs impl for worktree
    - 参考 google-workspace-cli 实现 本地版
    - agentfs + history
    - human-in-the-loop: ocr视觉/ui方面的内容验收标准难以确定， 更需要人工反馈
  - 🔗 citations for search: 外部数据源如字典mdx/书籍epub/wikipedia公开db/统计年鉴, 产品价值参考context7
    - 目前cli的搜索体验太差, 可针对 context/search-engine 结合 coding-agent 开发类似notebooklm的搜索体验
    - 查看原文pdf-parts时支持仅查看前后几页, 保护原文内容
    - optimized for long docs/books
    - 类似词典库/kiwix的预置模块, 可下载、可分享, 不必每次都全量索引
    - wikipedia zim 自动翻译为中文
    - web-search
    - vector-marketplace, 支持用户选择任意数量的pdf文档创建embeddings, 并发布, 可作为一种变通方案解决数据隐私问题
    - 行业应用: law, medical
    - sources: docs, emails
    - cited code
  - large pdf rag workflows: chunking-strategies, reindex, pdf-parts
    - 中文rag需要优化
    - rag db支持浏览空间占用、手动删除文件索引
  - 🌐 pdf edit
    - ocr router like openrouter/mineru/paddleocr/new-api/ccswitch
    - obsidian for pdf/ocr: ilovepdf/stirling-pdf/stirling-image
    - acp for pdf/rich-editing: 参考 google-workspace-cli 实现 本地版
    - mineru/paddleocr gui
    - diff without git
    - proofreading: 一键检查, 版本历史
      - chunking viz
      - 基于最新 pertext 还原布局
      - proofreading for word/excel/ppt
    - WebMCP for pdf/rich-editing
    - obsidian for pdf
      - optional pdf uploading
    - 可参考 Edit-Banana/design-to-code 编辑图片ppt的方案，来编辑pdf
    - 还原图文混排: 基于最新 pertext 还原复杂布局
      - 对于还原和提取都很有用
    - 提取 figure、表格
    - 👾 pdf-edit agent
    - ✨ 翻译场景的多种布局一键切换: 双栏对比布局, 仅译文布局, 富文本页面布局
    - 🌰 内置类似mineru/paddleocr的示例和提示词
    - multi-docs
    - 甚至可以通过多栏布局的交互，来展示pdf聊天或补充信息，优点是能展示在原文位置
    - 考虑同一文档的使用场景, 类似代码编辑器的 split view 也可以方便查看和核对
    - 方便原文和译文的跳转交互
    - toc autogen
    - pdf to word: ~~显示summary-per-page~~ , 适合教育场景
    - pdf体验尽量与docs一致，包括view/edit
    - 统一 文本pdf 和 图片pdf 的体验，代码实现可以不同
    - ocr bench by claude-code
    - pdf ocr one-click eval like FlowDown
      - ui for popular ocr benchmark
      - personal bench suite like FlowDown
  - extraction
    - https://x.com/jerryjliu0/status/2026032764131451334
      - llamaindex: We built an AI agent that lets you vibe-code document 
    - 高价值的元素: table, chart
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
    - partial-translate, 仅四六级
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
# 💎 modelbase - 模型参数对比, 历史评测结果, 能免费对比最新参数及上一个版本
- free-model-today
  - 基于 github-action 自动更新各平台的免费模型

- pm-eval/bench
  - 模型文档及参数都是on-paper, 可直接运行的测试集加上量化版本更适合实际效果, 是否存在产品空间
  - prompt-management/evals 是否值得扩展为产品

- free-models
  - nvidia, openrouter
  - modelscope
  - xunfei

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

- llm-playground - 使用公益api的效率工具+api统计分析
  - 公益版
  - 企业版

- news-feed/crawler
  - reddit/hacker-news上的热门讨论
# 💎 ai-pdf/docs
- pdf
  - gitbook-like viewer, mdBook, sharing without editing
  - LiteParse Grid Projection Algorithm

- wikilinks扩展: pdf-bbox, 支持preview, 甚至可以显示为截图内容
  - 引用pdf内容的场景都可以使用类似wikilinks的设计 + preview
  - 还可以优化图片pdf的搜索体验

- translation
  - 基于ai的翻译对比阅读， 支持部分翻译(四六级)
  - 对比阅读已有pdf的 原文 和 译文

- revision history for pdf

- spinedigest: 一次处理完，所有中间结果（Chunk、图谱、Snake、总结）全部打包进一个 .sdpub 文件。以后想重新导出成 Markdown、EPUB、纯文本……完全不需要再跑 LLM，秒级完成。

- 无需打开文档就支持展示image/docs/pdf的元数据

- elements
- table
  - 处理跨页的table

- 
- 
- 
- 
- 

# 💎 syncable/backupable
- 类似last.fm让用户同步本地数据， 类似ai模型

- 
- 
- 
- 
- 
- 

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

- 现有coding agent的优点
  - 功能丰富，比较稳定
  - remote control, cloud task

- 
- 
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

- [LLM Hardware Requirements Calculator — GPU & VRAM Guide | Onyx AI ](https://onyx.app/llm-hardware-requirements)

- 
- 

# ai-dev-xp
- 当一个复杂问题让ai折腾了1h还没解决，不要继续纠结，赶紧换更强的模型
  - 让ai动手前自己先拆分任务，不要让ai分析复杂的任务，ai分析不清会乱改增加工作量，自己可以主动mock状态和对象
  - 有时使用搜索引擎默认的ai结果又快又好，可以尝试解决类似stackoverflow类型的问题

- 让ai将从日志平台复制来的残缺字符串补全为合法字符串并格式化缩进，速度很快很好用
# more
