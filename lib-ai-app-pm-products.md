---
title: lib-ai-app-pm-products
tags: [ai, pm, product-hunt, products]
created: 2024-12-07T09:50:59.442Z
modified: 2025-03-22T16:10:24.856Z
---

# lib-ai-app-pm-products

# guide

# ai-dev-xp
- selling-points
  - local models support: mlx, lmstudio-alternative
  - citations for search: 外部数据源如字典mdx/书籍epub/wikipedia公开db/统计年鉴
  - large pdf workflows: chunking-strategies, reindex
  - pdf edit

- tips
  - 🤔 不要执着于ai框架，主流模型厂商都会推广包含厂商特性的框架及产品(codex/claude-code/gemini-cli), 可专注于主流开源业务系统实现 或 厂商无关的实现
  - frontend: ai-sdk/chatbot, assistant-ui, librechat
  - backend: langgraph + python/nodejs
  - aisdk + docs/excel/image
  - ai-apps as ref: lasuite

- ai-dev-xp
  - 难复现好的效果，同样的prompt+context，有时输出的效果就是不好
  - agent框架的tool-use实现对最新llm的支持，llm-provider的部署 都会影响llm的效果

- ai相对于搜索引擎的优势 🌹
  - ai能推理和计算, 分析复杂问题，给出更准确的方案
  - ai能拆分复杂任务为多步任务，能通过多轮来执行任务，同时支持one-shot和multi-steps
  - 能通过tool-call使用工具
  - 对多语言支持很好

- why-local-ai? 🌹
  - stable model and stable api
  - privacy: code, data, 还可以跳过广告推广
  - tweak different configs for ai-models
  - 避免模型平台的限制rate limits，如并发请求数(rpm/tpm/需要排队)、context长度、最大输出token数、模型版本、模型大小等
    - no implicit ai degradation/switch: bring your model
  - cost: unlimited tokens, local models支持超大context, 利用本地模型ocr/文生图
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
  - 不同本地api provider实现的逻辑有差异, 有的api只支持ollama而不支持lmstudio
  - 小模型不够智能
  - 移动端计算能力差, 速度慢, ipad的M系芯片非gpu方案也不快
  - 耗电量大, 对手机端不友好

- 需要针对local本地优化
  - 自动unload占用内存的image/llm模型, comfyui-lmstudio-node已实现了相关逻辑, 类似llama-swap 但同时支持文本/图片模型

- roadmap-ai
  - 针对国内免费api定制的chat/ppt/mermaid: 魔搭, 快手万擎
    - 可以~~fork janai,然后扩展provider~~, janai默认支持openai-like api，已经支持了国内models
  - 利用chrome最新的侧边栏，实现类似cline/roocode的页面ai助理/office编辑
    - 基于cline-cli的client/server架构，支持多种工具如 wps/飞书/腾讯文档/notion
    - 甚至结合文生图

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

- coding-based ai products
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
  - ai在前端或后端的架构都和workflow工作流紧密相关
  - 在不同流程或阶段采用不同LLM的方案可参考 docling
  - 🏘️ 架构参考: gemini-cli/qwen-cli(依赖fs) + ui/copilot-chat + framework/langfuse
  - 基于dnd的方案偏前端，后端一般很难定制和scale，会受限于平台提供的组件和工具
  - ✏️ ai修改文档的方案 fast-apply
  - 偏展示型的项目考虑采用ai-coding的思路来更新ui，如sandpack/react-live+ai，更灵活
- 📡 roadmap
  - coding不适合同时编辑多个文件，但同时执行多个project的任务存在需求，特别是在本地硬件资源有限的条件下

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
  - 类似 词典软件+词典mdx 的形式, 搜索软件+书籍pdf/epub

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

- 
- 
- 
- 

# draft
- rewrite open-canvas with langgraph
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
# ai-designing/image
- cursor for design: logo creator
  - 形态是否要基于vscode，产物是否要直接在vscode打开

- 使用ai实现高仿设计，是否可以绕过版权限制

- 版权过期书籍绘画的二创
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
# ai-dev-xp 🚧
- 当一个复杂问题让ai折腾了1h还没解决，不要继续纠结，赶紧换更强的模型
  - 让ai动手前自己先拆分任务，不要让ai分析复杂的任务，ai分析不清会乱改增加工作量，自己可以主动mock状态和对象
  - 有时使用搜索引擎默认的ai结果又快又好，可以尝试解决类似stackoverflow类型的问题

- 让ai将从日志平台复制来的残缺字符串补全为合法字符串并格式化缩进，速度很快很好用
# ai/llm-api 💰
- api-choices
  - 支持的优质大模型、热门模型、vlm
  - api稳定: 稳定时用的api稳定性必须要高，否则产品体验差
  - 速率限制
  - 工具集成支持: cline, roo, librechat

- resources
  - https://github.com/cheahjs/free-llm-api-resources

- tips: 公益站不稳定(3个月就倒闭一批), 来源不明可能导致效果差, 需要经常确认和维护, 不要浪费过多时间
  - 🤔 一种思路: tool-call时使用擅长tool-call的模型，分析时使用公益站的聊天优质但无法tool-call的模型
  - coding方案还可使用 ccr 转换 qwen-code-cli
  - 有的api不能显示thinking内容
  - 模型不断更新，落后的公益站会逐渐淘汰
  - 公益站主页模型广场展示的可用模型不准确，可以在控制台的playground直接测试，异常会直接抛出
- 免费api的技巧: 在知乎/小红书直接搜索 免费 claude (公益站), 就会有最新的api推广信息, 可以用小号邀请自己
  - 公益站 [Search results for '公益站' - LINUX DO](https://linux.do/search?q=%E5%85%AC%E7%9B%8A%E7%AB%99%20order%3Alatest)
  - [L站免费AI汇总 ](https://linux.do/t/topic/638821)
  - [最新福利羊毛/福利羊毛, Lv2话题 - LINUX DO](https://linux.do/c/welfare/welfare-lv2/61)
  - 📌 [Agent Router](https://agentrouter.org/console), 每日签到获取$25
    - 模型支持 Claude Code、Codex、RooCode、Qwen Code、Gemini Cli 等多款工具
    - 仅支持coding工具，不支持使用api聊天
    - 模型支持不稳定, 似乎不支持claude
    - > 签到功能在哪里呀？ 退出登录重新登陆就好了. 
    - https://github.com/aceHubert/newapi-ai-check-in
    - https://github.com/millylee/anyrouter-check-in
    - [AgentRouter 问题汇总 · Issue · millylee/anyrouter-check-in](https://github.com/millylee/anyrouter-check-in/issues/48)
      - agent 是在登录的时候签到的，并没有额外的 sign_in 接口，是在登录的那个接口是返回了一个check_in 的字段判断的，所以才把cookie 时间给调短了，就是让重新登录签到才有效
  - 📌 [Any Router](https://anyrouter.top/), 每日签到获取$25
    - 仅支持coding工具，不支持使用api聊天
    - 本站直接接入官方 Claude Code 转发，无法转发非 Claude Code 的 API 流量
    - 无充值，邀请注册来获得更多额度
    - tg群讨论的内容看，作者似乎精力不在anyrouter而在开发商用产品
    - 用户较多，有提供vscode插件无法使用的解决方案
  - [Code Router](https://api.codemirror.codes/), 无法签到和更多额度
    - 支持 Claude Code & CodeX
  - 📌 [b4u API](https://b4u.qzz.io/), 每日转盘
    - 会不会增加其他模型: 不会，本站专注于Claude
    - 支持工具调用、上下文 128K+、支持 RooCode，不推荐接入 ClaudeCode
    - 普通用户：每次 1 刀、RPM=10
    - 渠道技术： Claude-SessionKey号池→claude2api→FC使能
    - [转盘抽奖 / 投喂 Claude Session Key](https://tw.b4u.qzz.io/)
    - 仅每周六晚21:00至21:30限时开放注册
    - [【B4U公益站】是克劳德，我们有救了！（每周六限时开放注册） ](https://linux.do/t/topic/801848)
  - 📌 [薄荷 API](http://x666.me/console), 每日签到
    - 仅支持gemini模型
    - 改了下速率限制。现在变成5分钟25次，对自动化和roocode这些用户变好了很多
    - [薄荷公益站签到](https://qd.x666.me/)
  - [23公益站](https://sdwfger.edu.kg/console), 不用签到
    - 平台将于每周五、周六统一发放额度兑换码。 额度申请：如您的额度提前用尽，可联系管理员进行补充申请
    - 模型丰富: claude, gpt, gemini
  - 📌 [KFC API](https://kfc-api.sxxe.net/)
    - [KYX-API](https://api.kkyyxx.xyz/), 每日转盘
    - Claude和gpt 暂时不支持工具调用, gemini模型没有pro
    - API 调用频率限制为 12RPM，公益站永久免费，采用公平限流策略以保障服务稳定
    - [KYX API Refueling Station 公益站额度加油站](https://quota.kyx03.de/)
      - 别玩至尊场，1000积分一次警告扣16x，风险太高; 高级场的高积分也可以获得高收益
  - [包子公益](https://api.codeqaq.com/)
    - [包子铺](https://api.5202030.xyz/)
    - 只开放linuxdo lv2以上注册
    - 支持gpt,claude,gemini, 但没有gpt5(有mini)
    - [包子公益 - Baozi DoneHub](https://lucky.5202030.xyz/)
    - 每日普通用户可自行划转 200$ 到 newapi 站点
    - [【包子公益站】更新一个总的汇总贴。现在上线了newapi的分站 ](https://linux.do/t/topic/1124776)
  - [随时跑路公益](https://runanytime.hxi.me/), 每天签到 10-25 刀
    - 完全支持 cc，主要是 sonnet 4.5，haiku 4.5 会自动重定向到 sonnet 4.5
    - RPM 暂时定为 5，之后看情况调整
    - [【随时跑路公益站】就是那个稳了一个月的AmazonQ2API公益，开放注册 ](https://linux.do/t/topic/1154353)
  - [KFC API](https://kfc-api.sxxe.net/console)
    - [KFC API公益站 - 正式上线  ](https://linux.do/t/topic/1233747)
    - [逆水寒](https://api.sxxe.net/), 即将关闭
    - [逆水寒公益API——扬帆起航 ](https://linux.do/t/topic/1173036)
  - [一个小站的 API 商店](https://one-api.ygxz.in/), 每日签到1刀内随机
    - 提供半公益的高质量 API 中转服务，始于202406
    - 无调用频率限制
    - 支持gpt5,claude,gemini
    - 部分模型倍率很高，可选按次计算版本, 如claude
  - [WONG公益站](https://newapi.netlib.re/), 每日签到
    - rpm为30
    - 高效连接 Claude Code CLI
  - [我爱996公益](https://529961.com/)
    - 仅限 L 站 2 级以上用户注册
    - [【公益站我爱996一次】测试上线已接入LinuxDo ](https://linux.do/t/topic/1147448)
  - [FovtAPI](https://api.voct.top/console), 论坛发码
    - [NewAPI签到系统](https://gift.voct.top/), 已失效
  - [mmkg API](https://api.mmkg.cloud/)
    - 仅在每周五下午 18:00 至 21:00 开放，每周限量 100 人
    - 支持claude,gemini, 不支持gpt
    - Gemini系列模型永久免费， 与Gemini对话不会消耗帐号余额（可忽视帐号余额）
  - [黑与白chatAPI](https://ai.hybgzs.com/), 每日转盘
    - 模型丰富: claude/gemini, 但没有gpt5(有mini)
    - 很多openrouter渠道的模型
    - 本站完全免费！暂无任何充值通道
    - 绝大部分模型倍率换算后与官方价格相同，为缓解服务器资源压力，所有免费模型实际扣除配额均按付费标准计算
    - [黑与白chatAPI福利站](https://cdk.hybgzs.com/)
  - [tbai API](https://tbai.xin/), 即将关闭
    - 模型支持gemini/gpt, 不支持claude
    - API调用频率限制为 10 RPM
    - gpt-load 作者
    - [【T佬公益】TBAI公益站主贴-爽用Gemini|OpenAI|DeepSeek模型 ](https://linux.do/t/topic/683726)
  - [VoAPI公益站](https://demo.voapi.top/), 每日签到
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
  - [Privnode](https://privnode.com/)
    - free分组不支持claude，但支持gpt-5-nano
    - https://pro.privnode.com/
    - [【Cone 公益站】找个佬共同维护  ](https://linux.do/t/topic/1035525)
    - [Cone 公益站更新 ](https://linux.do/t/topic/1002152)
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
  - [翰林文苑公益API站点](https://aiapi.hlwy2025.me/)
    - 价格太高了 我决定攒到1000再用
  - [ThatAPI](https://gyapi.zxiaoruan.cn/pricing)
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
  - [YesCode](https://co.yes.vg/)
    - [YesCode test](https://cotest.yes.vg/)
    - [【YesCode公益测试站】Claude Code/Codex 长期免费测试 ](https://linux.do/t/topic/964164)
  - [Becode 公益站](https://becode.be-a.dev/)
  - [88code - 企业级Claude Code/Codex中转](https://www.88code.org/)
    - 添加客服领取 10 美元免费额度, 每个用户仅限领取一次
  - [AICodeMirror官方共享平台 - 中国用户专属AI编程助手](https://www.aicodemirror.com/)
    - 每月 2000积分
    - 因成本大幅上升，免费用户暂不开放体验。后续开放时间另行通知
  - [packycode：全部服务指南，包含 claude code codex 公益、付费全部站点 ](https://linux.do/t/topic/933715)
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

- image-gen 🖼️
  - [小白生图 - AI Image Generator](https://catsapi.com/)
  - [RyanVan Z-Image | AI 图像生成](https://ryanai.org/)
    - 每天5张免费
    - 排队时间可能较长
  - [Z-Image-Turbo | AI 绘图工作站](https://zzz.supxh.xin/)
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

- llm-ui
  - [SmallAI](https://free.smallai.asia/chat)
    - 基于lobechat实现
    - [【网站自荐】SmallAI公益站——免费使用GPT4o mini，支持多模态 ](https://github.com/ruanyf/weekly/issues/4969)
  - [AI对话 - db的AIGC站](https://ai.feles.town/chat)
  - 💰 [GoAmzAI - 个人、团队、企业私有化、运营的AIGC平台解决方案](https://d.goamzai.com/)
    - https://github.com/Licoy/GoAmzAI /非开源
    - https://github.com/VoAPI/VoAPI /仅提供docker-compose.yml
    - [AI对话 - GoAmzAI Plus](https://demo6.goamzai.com/chat)
    - [对话 - GoAmzAI Pro](https://prodemo6.goamzai.com/chat)
    - [【公益AIGC】最适合日常使用的公益站，高级AI工具一网打尽 ](https://linux.do/t/topic/1175890/37)
      - volo api 吧，基于 new api 改的，但是 v1 开始好像就完全重写了
      - VoAPI 一直是闭源的，甚至好像只放出 Docker 的部署方式，连编译后的可执行文件都不发布的，截止到我最后一次看时是这样的，不知道后续有没有改变和有没有收费计划

## llm-api-official-router

- 📌 [OpenRouter API Rate Limits ](https://openrouter.ai/docs/api-reference/limits)
  - tldr: rpd-1000 
  - Free usage limits: If you’re using a free model variant (with an ID ending in `:free`), you can make up to 20 requests per minute. 
  - If you have purchased less than 10 credits, you’re limited to 50 :free model requests per day.
  - If you purchase at least 10 credits, your daily limit is increased to 1000 :free model requests per day.
  - If your account has a negative credit balance, you may see `402` errors, including for free models.

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

- [Cloudflare Workers AI Pricing](https://developers.cloudflare.com/workers-ai/platform/pricing/)
  - Our free allocation allows anyone to use a total of 10, 000 Neurons per day at no charge. 
  - Workers AI is included in both the Free and Paid Workers plans and is priced at $0.011 per 1, 000 Neurons.

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
  - [模型实时调用专属权益 及 标准单价 (很多免费)](https://bigmodel.cn/usercenter/equity-mgmt/user-rights)
  - [智谱AI - pricing](https://bigmodel.cn/pricing)
  - 免费模型: [福利专区](https://bigmodel.cn/dev/activities/free/glm-4-flash)
  - [Z.ai - Rate Limits](https://z.ai/manage-apikey/rate-limits)
    - GLM-4.5-Flash	2
  - [智谱AI开放平台 - 速率限制 - 用户等级](https://bigmodel.cn/usercenter/proj-mgmt/rate-limits)
  - [智谱AI开放平台 - 速率限制](https://www.bigmodel.cn/dev/howuse/rate-limits)
    - 当前我们限制的维度是请求并发数量（在途请求任务数量）

- [KAT-Coder开发工具接入指南-快手万擎-StreamLake](https://www.streamlake.com/document/WANQING/me6ymdjrqv8lp4iq0o9)
  - tldr: rphour-20~30
  - ✅ [KAT-Coder-Air V1 模型免费使用规则 ](https://www.streamlake.com/document/WANQING/mh1g9y6knewv5sft54k)
  - 非高峰时段: 02:00-08:00 每6小时内您将可以发起200次对话请求，超过此请求数后，您可能会经历更长的排队等待时间或更严格的速率限制
  - 高峰时段: 08:00-02:00（次日） 每6小时内您将可以发起120次对话请求。在此时段，KAT-Coder-Air V1 的请求优先级可能会降低。您可能会经历更长的排队等待时间或更严格的速率限制。

- [LongCat API开放平台快速开始 | API 文档](https://longcat.chat/platform/docs/zh/)
  - tldr: tpd-500K
  - 每个账号每天自动获得 500, 000 Tokens 免费额度
  - 免费额度将于每日凌晨（北京时间）自动刷新
  - 输入和输出Tokens均计入消耗, 流式接口和段式接口消耗相同
  - 单次请求限制 输出文本：最大8K Tokens

- [Moonshot AI 开放平台 - 充值与限速](https://platform.moonshot.cn/docs/pricing/limits)
  - 赠送用完后需要充值

- [七牛 AI 大模型推理服务 - 七牛云](https://www.qiniu.com/ai/chat)
  - 采用按量计费的模式，根据实际使用的 token 数量收费，每月初出账。新用户享有免费额度

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
# ai-products-hunt

# more

# discuss-ai-pm
- ## 

- ## 

- ## "We now want to edit our *tools* as we have previously edited our documents"
- https://x.com/geoffreylitt/status/1646688665479831559
- "As we shape our tools, our tools shape us." 
- This is what makes tools like Notion and Airtable so powerful— they’re lightweight ways to build increasingly customizable interfaces with (albeit small) knowledge databases. As they get more flexible and can handle more data, I feel they’ll become essential parts of UI/UX design
