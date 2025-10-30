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
  - aisdk + docs/excel/image
  - frontend: ai-sdk/chatbot, assistant-ui, librechat
  - backend: langgraph + python/nodejs
  - ai-apps as ref: lasuite

- ai-dev-xp
  - 难复现好的效果，同样的prompt+context，有时输出的效果就是不好

- ai相对于搜索引擎的优势 🌹
  - ai能推理和计算, 分析复杂问题，给出更准确的方案
  - ai能拆分复杂任务为多步任务，能通过多轮来执行任务，同时支持one-shot和multi-steps
  - 能通过tool-call使用工具
  - 对多语言支持很好

- why-local-ai?
  - stable model and stable api
  - privacy: code, data
  - tweak different configs for ai-models
  - 避免模型平台的限制，如并发请求数(需要排队)、context长度、最大输出token数、模型版本、模型大小等
    - no implicit ai degradation/switch: bring your model
  - cost: unlimited tokens
  - network agnostic
  - 发挥端侧计算的能力，如总结/查询，而不侧重端侧聊天

- roadmap-ai
  - 针对国内免费api定制的chat/ppt: 魔搭, 快手万擎
    - 可以~~fork janai,然后扩展provider~~, janai默认支持openai-like api，已经支持了国内models

- local-ai-challenges 🐛
  - 运行大模型需要较多硬件资源，如GPU/CPU/RAM
  - 本地模型的api很多通过gui如ollama/LMStudio提供，需要适配，同时不同GPU在默认token数、RAG处理方式上有差异

- agent-ipc

- markdown-stream
  - table-typewriter

- 🏠 ai-architecture: 与ai的通信和计算是在前端实现，还是在后端实现
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

- 🔡 可是尝试用code generation的思路来实现ai产物如ppt
  - web sandbox + ai-coding > lovable ❓
  - sandpack ai? react-live ai?

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

- rag
  - retrieval
  - code retrieval
  - text-matching

- office
  - excel/database generator
  - mindmap/drawio generator
  - ai-friendly format: 图片/图形中带有元数据

- image-gen-by-code
  - 文生图难度高，但基于文本的流程图难度低很多，如集成 mermaid
  - 基于代码的文生图方案，如sandpack, 可用于小红书卡片场景，可参考 https://langgptai.feishu.cn/wiki/JQVEwKJQkilWztkMLRGcA8zqngb

- image-generator/editor
  - prompts: bg, person/object, text
  - 模型选择要考虑: 硬件限制、速度、质量， 只有成熟的model才会提供lite/turbo/精简版
  - 一次生成多幅图
  - stream
  - 在线图片生成或编辑的架构, 涉及到模型下载与扩展下载，目前没有类似ollama的统一方案, 还涉及到GPU/CPU硬件支持，只有成熟方案才处理过相关问题

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

- 
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
# ai-designing
- cursor for design: logo creator
  - 形态是否要基于vscode，产物是否要直接在vscode打开

- 使用ai实现高仿设计，是否可以绕过版权限制
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
- 免费api的技巧: 在知乎/小红书直接搜索 免费 claude (公益站), 就会有最新的api推广信息, 可以用小号邀请自己
  - 公益站 [Search results for '公益站' - LINUX DO](https://linux.do/search?q=%E5%85%AC%E7%9B%8A%E7%AB%99%20order%3Alatest)
  - 📌 [Agent Router](https://agentrouter.org/), 每日签到获取$25
    - 支持 Claude Code、Codex、RooCode、Qwen Code、Gemini Cli 等多款工具
    - 模型支持不稳定, 似乎不支持claude
    - > 签到功能在哪里呀？ 退出登录重新登陆就好了. 
    - https://github.com/aceHubert/newapi-ai-check-in
    - https://github.com/millylee/anyrouter-check-in
    - [AgentRouter 问题汇总 · Issue · millylee/anyrouter-check-in](https://github.com/millylee/anyrouter-check-in/issues/48)
      - agent 是在登录的时候签到的，并没有额外的 sign_in 接口，是在登录的那个接口是返回了一个check_in 的字段判断的，所以才把cookie 时间给调短了，就是让重新登录签到才有效
  - 📌 [Any Router](https://anyrouter.top/), 每日签到获取$25
    - 无充值，邀请注册来获得更多额度
    - 本站直接接入官方 Claude Code 转发，无法转发非 Claude Code 的 API 流量
    - tg群讨论的内容看，作者似乎精力不在anyrouter而在开发商用产品
    - 用户较多，有提供vscode插件无法使用的解决方案
  - [Code Router](https://api.codemirror.codes/), 无法签到和更多额度
    - 支持 Claude Code & CodeX
  - [b4u API](https://b4u.qzz.io/)
    - 仅每周六晚21:00至21:30限时开放注册
    - 会不会增加其他模型：不会，本站专注于Claude
    - 渠道技术： Claude-SessionKey号池→claude2api→FC使能
    - [【B4U公益站】是克劳德，我们有救了！（每周六限时开放注册） ](https://linux.do/t/topic/801848)
  - [tbai API](https://tbai.xin/)
    - API 调用频率限制为 10 RPM
    - gpt-load 作者
    - 使用兑换码兑换余额后的账号视为激活用户, 激活用户可长期使用，额度用完后可无条件联系我增加额度
    - [【T佬公益】TBAI公益站主贴-爽用Gemini|OpenAI|DeepSeek模型 ](https://linux.do/t/topic/683726)
  - 📌 [23公益站](https://sdwfger.edu.kg/console), 不用签到
    - 平台将于每周五、周六统一发放额度兑换码。 额度申请：如您的额度提前用尽，可联系管理员进行补充申请
    - 模型丰富: claude, gpt
  - [KYX-API](https://api.kkyyxx.xyz/), 不用签到
    - Claude和gpt 暂时不支持工具调用
    - API 调用频率限制为 12RPM，公益站永久免费，采用公平限流策略以保障服务稳定
    - [KYX API Refueling Station 公益站额度加油站](https://quota.kyx03.de/)
  - [learn-ai 公益站点](http://free.learn-ai.top/), 需要签到且额度很少
    - 支持的模型质量较低: 很少一部份claude模型, gpt-mini/nano
    - 可以加入付费站点：https://learn-ai.top/
  - [RawChat公益站点](https://chatgptplus.cn/)
    - 免费的共享ChatGPT账号
    - [RawChat公益站点](https://sharedchat.fun/)
    - [HammerAI公益站](https://hammerai.vip/)
  - [Claude免费镜像号池](https://share.claude.best/)
    - 若无法对话了，说明对话额度被其他朋友用完了（需要你更换其他账号或者等待额度刷新）
    - [RawChat公益站点 kelaode](https://kelaode.ai/)
  - [Privnode](https://privnode.com/)
    - free分组不支持claude，但支持gpt-5-nano
    - https://pro.privnode.com/
    - [【Cone 公益站】找个佬共同维护  ](https://linux.do/t/topic/1035525)
    - [Cone 公益站更新 ](https://linux.do/t/topic/1002152)
  - [cone Veloera Zone](https://zone.veloera.org/)
    - 此服务完全免费提供，并仅在 LINUX DO 社区宣传
    - 不定期删除 0 额度，0 消耗，且注册超过一周的用户。
  - [薄荷 API](http://x666.me/)
    - 仅提供gemini模型
  - [ZenscaleAi](https://gy.zenscaleai.com/)
    - 仅提供gemini模型
  - [小丑Ai公益站](https://gy.jiubanai.com/)
    - 仅提供gemini模型
  - [小松公益站 New API](http://api.lanapi.top/pricing)
    - 仅提供gemini模型， 满血版
    - 默认分组只有5分钟3次的请求速率，至尊分组无上限分组
  - [翰林文苑公益API站点](https://aiapi.hlwy2025.me/)
    - 价格太高了 我决定攒到1000再用
  - [ThatAPI](https://gyapi.zxiaoruan.cn/pricing)
  - [linjinpeng Veloera](https://linjinpeng-veloera.hf.space/)
    - 现在rpm是6，模型全部免费，1级即可注册
    - 一次一美元的调用，但是这个1美元是无限刷新的，你用了就知道了
    - 聊天记录均留样检测，违规直接封禁，请不要对话任何隐私信息
    - [能否成为全站用量最大的claude 4.1 opus公益站 _202509](https://linux.do/t/topic/956435)
  - [LLM API 公益站](https://llm.indrin.cn/)
    - 本站永久运营，服务免费提供个人使用,禁止高并发,禁止高输入, 高并发会封号
    - 额度不限量,注册送$30，邀请送$5,正常用户额度快用完时会给后台增加
    - 不支持claude，支持openai, xai
  - [归一](https://ai.luuu71.dpdns.org/pricing)
    - gpt5
  - [TudouAPI](https://www.tudou.chat/), 签到复杂
    - 如果账户连续3天以上都是只有5-10条，会判定为屯额度账号签到失败
    - 支持claude, gpt
  - [YesCode](https://co.yes.vg/)
    - [YesCode test](https://cotest.yes.vg/)
  - [Becode 公益站](https://becode.be-a.dev/)
  - [88code - 企业级Claude Code/Codex中转](https://www.88code.org/)
    - 添加客服领取 10 美元免费额度, 每个用户仅限领取一次
  - [AICodeMirror官方共享平台 - 中国用户专属AI编程助手](https://www.aicodemirror.com/)
    - 每月 2000积分
  - [packycode：全部服务指南，包含 claude code codex 公益、付费全部站点～ - 福利羊毛 - LINUX DO](https://linux.do/t/topic/933715)
  - [cto.new ](https://cto.new/)
  - [Claude 4.5 国内免费使用指南 | 最全访问方式汇总 2025 - 知乎](https://zhuanlan.zhihu.com/p/1956204058139431066)
    - 镜像、中转、合租、代充
  - [2025年10月 Claude 国内使用指南（支持 Claude Sonnet 4.5） - 知乎](https://zhuanlan.zhihu.com/p/1940070586635223559)
  - [白嫖最强AI编程模型Claude 4.5，暨一哥Claude Code的免费下位替代（10月22亲测可用） - 知乎](https://zhuanlan.zhihu.com/p/81947374736)
  - [求推荐免费模型api，公益站付费的太慢了，只是用于ai中文翻译成英文，速度有要求 - 搞七捻三 - LINUX DO](https://linux.do/t/topic/1061766)

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
