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
  - privacy: code, data
  - tweak different configs for ai-models
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

- ai-architecture: 与ai的通信和计算是在前端实现，还是在后端实现
  - 🐛 前端和大模型直接对接的缺点: 关闭页面会丢失数据、流程中断、并发控制复杂
  - 🤔 why backend server
    - 消息持久化时，使用服务端id才方便消息保存与恢复、多人聊天一致性
    - 方便实现并发控制，特别是多任务
    - background-task
  - ai在前端或后端的架构都和workflow工作流紧密相关
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
- [OpenRouter API Rate Limits ](https://openrouter.ai/docs/api-reference/limits)
  - Free usage limits: If you’re using a free model variant (with an ID ending in `:free`), you can make up to 20 requests per minute. 
  - If you have purchased less than 10 credits, you’re limited to 50 :free model requests per day.
  - If you purchase at least 10 credits, your daily limit is increased to 1000 :free model requests per day.
  - If your account has a negative credit balance, you may see `402` errors, including for free models.

- [Cerebras Inference Rate Limits](https://inference-docs.cerebras.ai/support/rate-limits)
  - Model	TPM	TPH	TPD	
  - gpt-oss-120b	60K	1M	1M
  - llama-3.3-70b	60K	1M	1M
  - qwen-3-32b	60K	1M	1M
  - qwen-3-235b-a22b-instruct-2507	60K	1M	1M
  - qwen-3-235b-a22b-thinking-2507	60K	1M	1M
  - qwen-3-coder-480b	150K	1M	1M

- [Groq Rate Limits - Docs](https://console.groq.com/docs/rate-limits)
  - MODEL ID	RPM	RPD	TPM	TPD
  - groq/compound	30	250	70K	No limit
  - qwen/qwen3-32b	60	1K	6K	500K
  - openai/gpt-oss-120b	30	1K	8K	200K
  - llama-3.3-70b-versatile	30	1K	12K	100K
  - moonshotai/kimi-k2-instruct-0905	60	1K	10K	300K
  - meta-llama/llama-4-scout-17b-16e-instruct	30	1K	30K	500K

- [Gemini Developer API Pricing  ](https://ai.google.dev/gemini-api/docs/pricing)
  - 国内不可用
  - gemini-2.5-pro: Grounding with Google Search	Not available
  - gemini-2.5-flash: Grounding with Google Search, up to 500 RPD (limit shared with Flash-Lite RPD)
  - [Rate limits  |  Gemini API  ](https://ai.google.dev/gemini-api/docs/rate-limits)
    - model,          RPM,   TPM,      RPD
    - Gemini 2.5 Pro	  5	   125,000	  100
    - Gemini 2.5 Flash	10	 250,000	  250
    - Gemini 2.0 Flash	15	 1,000,000	200

- [Mistral Rate Limits & Usage tiers ](https://docs.mistral.ai/deployment/ai-studio/tier)
  - Maximum requests per second: 1
  - Tokens per Minute: 500, 000
  - Tokens per Month: 1 billion

- [魔搭推理API-Inference API推理介绍 · 文档中心](https://modelscope.cn/docs/model-service/API-Inference/intro)
  - 免费推理API由阿里云提供算力支持，要求您的ModelScope账号必须绑定阿里云账号后才能正常使用。
  - 每位魔搭注册用户，当前每天允许进行总数为2000次的API-Inference调用，其中每单个模型不超过500次，具体每个模型的限制可能随时动态调整。
  - 在每个模型每天不超过500次调用的基础上，平台可能对于部分模型再进行单独的限制，例如，deepseek-ai/DeepSeek-R1-0528，deepseek-ai/DeepSeek-V3.1等规格较大模型，当前限制单模型每天200次调用额度。
  - 在上述调用次数限制的基础上，不同模型允许的调用并发，会根据平台的压力进行动态的速率限制调整，原则上以保障开发者单并发正常使用为目标。
  - 实际单模型可用次数以及允许的并发，以平台实时调整为准。
  - 🖼️ 当前API-Inference为魔搭平台上的部分开源大语言模型（LLM），多模态模型（MLLM），以及AIGC专区文生图模型等，提供了可直接使用的API。

- [硅基流动 SiliconFlow - 大模型 API 价格方案](https://www.siliconflow.cn/pricing)
  - llm: Qwen/Qwen3-8B, deepseek-ai/DeepSeek-R1-0528-Qwen3-8B, THUDM/GLM-Z1-9B-0414, THUDM/GLM-4-9B-0414, Qwen/Qwen2.5-Coder-7B-Instruct
  - vlm: THUDM/GLM-4.1V-9B-Thinking
  - image: Kwai-Kolors/Kolors
  - asr: TeleAI/TeleSpeechASR
  - [Rate Limits - SiliconFlow](https://docs.siliconflow.cn/cn/userguide/rate-limits/rate-limit-and-upgradation)
    - 语言模型(Chat)	 RPM=1000-10000 TPM=50000-5000000
    - 🖼️ 图像生成模型(Image)	 IPM:2 IPD:400

- [DeepSeek API Docs - 模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/)
  - 扣减费用 = token 消耗量 × 模型单价，对应的费用将直接从充值余额或赠送余额中进行扣减。
  - 百万tokens输入（缓存命中）	0.2元
  - 百万tokens输入（缓存未命中）	2元
  - 百万tokens输出	3元

- [Z. AI DEVELOPER DOCUMENT](https://docs.z.ai/guides/overview/pricing)
  - GLM-4.5-Flash	Free Fre ✅
  - GLM-4-32B-0414-128K	$0.1  	$0.1
  - GLM-4.5-Air	$0.2  $1.1

- [KAT-Coder开发工具接入指南-快手万擎-StreamLake](https://www.streamlake.com/document/WANQING/me6ymdjrqv8lp4iq0o9)
  - ✅ [KAT-Coder-Air V1 模型免费使用规则 ](https://www.streamlake.com/document/WANQING/mh1g9y6knewv5sft54k)
  - 非高峰时段: 02:00-08:00 每6小时内您将可以发起200次对话请求，超过此请求数后，您可能会经历更长的排队等待时间或更严格的速率限制
  - 高峰时段: 08:00-02:00（次日） 每6小时内您将可以发起120次对话请求。在此时段，KAT-Coder-Air V1 的请求优先级可能会降低。您可能会经历更长的排队等待时间或更严格的速率限制。

- [Moonshot AI 开放平台 - Kimi 大模型 API 服务](https://platform.moonshot.cn/docs/pricing/chat)

- [Cohere API Keys and Rate Limits](https://docs.cohere.com/docs/rate-limits)
  - all endpoints are limited to 1, 000 calls per month with a trial key

- [huggingface Pricing and Billing](https://huggingface.co/docs/inference-providers/pricing)
  - [Inference Providers](https://huggingface.co/docs/inference-providers/index)
  - Hugging Face provides a Serverless Inference API as a way for users to quickly test and evaluate thousands of publicly accessible (or your own privately permissioned) machine learning models with simple API calls for free
  - Every Hugging Face user receives monthly credits to experiment with Inference Providers
  - Account Type	Monthly Credits	Extra usage (pay-as-you-go)
  - Free Users	$0.10, subject to change	no
  - [HuggingFace changes to PRO subscription Inference limits, should I switch providers now? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ii4nst/huggingface_changes_to_pro_subscription_inference/)
    - The $2 credit limit is pretty weak for a $9 subscription. RunPod gives you way more bang for your buck - just pay for what you use and test as many models as you want.

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
